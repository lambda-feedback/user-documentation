# Evaluation Function Specification

## Introduction and Philosophy

Functionality for each evaluation function is split up as follows:

!!! note ""
Universal function behaviour applicable to _every_ function, such as the ability to run tests, return documentation and execute the evaluation is handled by the [**Base Layer**](#base-layer). This is the docker image which is extended by every developed evaluation function.

!!! abstract ""
Functionality that may be required in more than one function (but not necessarily all), such as the ability to call already deployed functions and error reporting is handled by the [**evaluation_function_utils**](module.md) python package. This package comes pre-installed in the base layer, and can optionally be imported and called from the _evaluation_function_.

!!! info ""
Finally, specific comparison logic and handling of bespoke evaluation parameters is done in the custom [**evaluation_function**](#the-evaluation_function), unique to each deployed instance. This is the logic that differenciates each function (comparing numbers, matrices, images, equations, graphs, text, tables, etc ...).

!!! note ""
New evaluation functions should use the [**µEd API**](#ed-api). The [**Legacy API**](#legacy-api) is being phased out — only a small number of functions that haven't yet migrated still use it.

## µEd API

Evaluation functions can be registered to serve the [µEd API](https://mued.org/) — a standard, path-based request/response format shared with [Chat Functions](../chat_functions/quickstart.md). Requests are routed and validated by the [base layer](#base-layer) against the [µEd OpenAPI specification](https://github.com/lambda-feedback/shimmy/blob/main/runtime/schema/mued_v0.1.0.yml); only `POST /evaluate` and `GET /evaluate/health` are implemented for evaluation functions. An optional `X-Api-Version: 0.1.0` header selects the schema version.

Importantly, **the µEd routes call the same [`evaluation_function`](#the-evaluation_function) and `preview_function` you write for the Legacy API** — the base layer translates between the two wire formats, so no separate implementation is needed to support both.

### `POST /evaluate`

Runs an evaluation and returns feedback for a submission. If `preSubmissionFeedback.enabled` is `true` in the request, a non-final preview is returned instead (equivalent to the Legacy [`preview`](#preview) command).

!!! example
    ```bash
    curl --request POST \
    --url https://<your-function-url>/evaluate \
    --header 'Content-Type: application/json' \
    --header 'X-Api-Version: 0.1.0' \
    --data '{
        "submission": {
            "type": "OTHER",
            "content": { "value": "x + x" }
        },
        "task": {
            "referenceSolution": { "expression": "2*x" }
        }
    }'
    ```



## Legacy API

The Legacy API is the original command-based interface. It is **frozen** — no longer extended — but [Shimmy](#base-layer) still serves it, so functions do not need to migrate to keep working. It is exposed at `POST /`, with the command given in a request header named `command` (`eval` if the header is absent). The request body is a bare JSON object (`response`, `answer`, `params` — no wrapper); the response is `{"command": ..., "result": {...}}`, or `{"error": {"message": ...}}` if the function raised.

!!! example
    To run the `eval` command against a deployed function:

    ```bash
    curl --request POST \
      --url https://<your-function-url>/ \
      --header 'Content-Type: application/json' \
      --header 'command: eval' \
      --data '{ "response": "2*x", "answer": "x + x", "params": {} }'
    ```

### `eval`

This is the default command, used to compare a student's `response` and correct `answer`, given certain `params`. Outputs for this command depend on the success of the execution of the user-defined [`evaluation_function`](#the-evaluation_function). If an error was thrown during execution, it is caught by the main handler and an error block is returned - otherwise, successful execution outputs are supplied under a `result` field.

!!! success "Output Structure: Successful evaluation"

    ``` { .python .annotate }
    {
        "command": "eval",
        "result": {
            "is_correct": "<bool>",

            # Optional fields added by feedback generation (1)
            "feedback": "<string>",
            "warnings": "<array>"

            # This output can also contain any number of fields given by `evaluation_function`
        }
    }
    ```

    1. See the [Feedback Page](feedback.md) for more information

!!! fail "Output Structure: Error thrown during Execution"

    ``` { .python .annotate }
    {
        "command": "eval",
        "error": {
            "message": "<string>", # Always present

            # This object can contain other number of additional fields
            # passed through by the EvaluationException (1) for debugging e.g.:
            "serialization_errors": [],
            "culprit": "user",
            "detail": "..."
        }
    }
    ```

    1.    This is a custom error class from the [evaluation-function-utils](module.md) package, which developers are encouraged to use in order to output richer errors. See the [Error handling](#error-handling) section for more information.

### `preview`

This command is similar to `eval`, except it doesn't return whether an answer is correct or provide feedback. Instead, `preview` provides a way for students view their response after some pre-processing, e.g. as rendered LaTeX when using Sympy for symbolic algebra.

This should be faster to compute than `eval`, allowing students to get live preview of their response.

### `healthcheck`

Runs the function's own test suite (test discovery over the `*_test.py` files) and returns a summary: `{"tests_passed": <bool>, "successes": [...], "failures": [...], "errors": [...]}`.

## Base Layer

The base layer is [**Shimmy**](https://github.com/lambda-feedback/shimmy), an HTTP server bundled into the [`evaluation-function-base`](https://github.com/lambda-feedback/evaluation-function-base) image that every function extends. It provides the behaviour common to all functions, so the function itself only implements comparison logic. Shimmy:

- serves the [µEd API](#ed-api) (`POST /evaluate`, `GET /evaluate/health`) and the [Legacy API](#legacy-api) (`POST /`, command in a header), plus a `GET /health` liveness probe, all on port `8080`;
- validates each request against the relevant schema before your code runs;
- launches your function as a child process and talks to it over JSON-RPC — Python functions use the [`lf_toolkit`](module.md) package for this — or, for other languages, a file-based interface (see [Other Languages](alternate_languages.md));
- runs the [feedback `cases`](feedback.md) loop, re-invoking your function once per case;
- optionally sandboxes the function with [nsjail](https://github.com/google/nsjail) (`SANDBOX_ENABLED=true`).

!!! note "Older base layer"
    Functions that have not yet migrated extend [`BaseEvalutionFunctionLayer`](https://github.com/lambda-feedback/BaseEvalutionFunctionLayer) instead — an Amazon Linux image built on the AWS Lambda runtime. It serves the Legacy API only (including `docs-user` / `docs-dev`) and is tested locally with the AWS Runtime Interface Emulator; see [Running Functions Locally](local.md#older-aws-lambda-base-layer).

## File Structure

A function created from [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python) has this layout:

```bash
evaluation_function/
    __init__.py
    main.py             # Entry point: create_server() + register eval/preview (rarely edited)
    evaluation.py       # The main evaluation_function
    preview.py          # The preview_function
    evaluation_test.py  # pytest tests for evaluation_function
    preview_test.py     # pytest tests for preview_function
    dev.py              # Local CLI: python -m evaluation_function.dev

docs/                   # Documentation pages for this function (required)
    dev.md              # Developer-oriented documentation
    user.md             # LambdaFeedback content-author documentation

.github/
    workflows/          # Reusable CI/CD from lambda-feedback/evaluation-function-workflows

config.json             # { "EvaluationFunctionName": "<unique lowerCamelCase name>" }
Dockerfile
pyproject.toml          # Dependencies (Poetry); lf_toolkit is pulled in here
poetry.lock
README.md
```

The `Dockerfile` extends the base image and tells Shimmy how to start the worker:

```dockerfile
FROM ghcr.io/lambda-feedback/evaluation-function-base/python:3.12
# ... poetry install ...
COPY evaluation_function ./evaluation_function
ENV FUNCTION_COMMAND="python"
ENV FUNCTION_ARGS="-m,evaluation_function.main"
```

Extra modules you add under `evaluation_function/` are picked up by the existing `COPY evaluation_function ./evaluation_function` line, so splitting logic across files needs no Dockerfile change.

!!! note
	The `staging-deploy.yml` and `production-deploy.yml` workflows call into reusable workflows maintained in [lambda-feedback/evaluation-function-workflows](https://github.com/lambda-feedback/evaluation-function-workflows), which handle the actual build and deploy steps.

!!! note "Older `app/` layout"
    Functions on the older AWS Lambda base layer use an `app/` directory holding `evaluation.py`, `evaluation_tests.py`, `requirements.txt`, a `Dockerfile` and `docs/`, with `config.json` and the workflows at the repository root. There, each additional source file must be added to the `Dockerfile` with its own `COPY` line.

## `evaluation.py`

The entire framework, validation and testing developed around evaluation functions is ultimately used to get to `evaluation_function/evaluation.py`, or the `evaluation_function` within it, to be more precise. `evaluation_function/main.py` registers it with the base layer via [`lf_toolkit`](module.md); you normally only edit `evaluation.py` (and `preview.py`).

### The `evaluation_function`

#### Inputs

All evaluation functions are passed three arguments:

- `response`: Data input by the user
- `answer`: Data to compare user input to (could be from a DB of answers, or pre-generated by other functions)
- `params`: Parameters which affect the comparison process (replacements, tolerances, feedbacks, ...)

For evaluation functions that use Sympy or LaTeX for mathematical expressions, it's not always possible for a student to type the correct symbols. Instead we need to use simpler symbols. For example, $\overline{U_{ij}}$ cannot be written using standard sympy syntax, and therefore has to be substituted for something else, such as `"u"` or `"U"`.

Therefore, evaluation functions using mathematical expressions should be able to handle multiple symbols to represent the same variable. To achieve this, every evaluation function is passed a `symbols` entry in `params`, to allow functions to convert a student's response:

```json
{
    "response": "user input",
    "answer": "model response to compare against",
    "params": {
        "symbols": {...},
        ... # params set by the teacher
    }
}
```

`symbols` is a dictionary, where each key represents the **main** Sympy symbol (known as the `code`), and has two entries:

- `latex`: the string used for rendering the symbol in LaTeX
- `aliases`: a list of alternative Sympy symbols that can be used by the student to represent the `code`.

For the example above with $\overline{U_{ij}}$, `symbols` would have the form:

```json
{
    ...
    "params": {
        "symbols": {
            "u": {
                "latex": "\\overline{U_{ij}}",
                "aliases": ["U"]
            }
        }
    }
}
```

Note that in JSON, special characters need to be escaped, so the latex symbol above will have a double-backslash instead.

Currently, the backend only supports one LaTeX symbol for multiple Sympy symbols. In future, this will be a many-to-many relationship.

#### Context

When a student submits a response to a response area the number of previously submitted responses submitted to the same response area byt the same student will be sent to the evaluation function. The following format is used:
``` { .python .annotate }
    {
        "submission_context": {
            "submissions_per_student_per_response_area": # non-negative integer that represent the nubmer of previously processed responses
        }
    }
```

#### Outputs

Functions using [`lf_toolkit`](module.md) return a `Result` object (`lf_toolkit.evaluation.Result`), which the base layer serialises. Returning a plain JSON-encodable dictionary also works. Although a large amount of freedom is given to what the result contains, when utilising the function alongside the [lambdafeedback](https://lambdafeedback.com/) web app, a few values are expected/able to be consumed:

**`is_correct: <bool>`**: Boolean parameter indicate whether the comparison between `response` and `answer` was deemed correct under the parameters. This field is then used by the web app to provide the most simple feedback to the user (green/red).

!!! info
_More standardised function outputs that the frontend can consume are to come_

### Error Handling

Error reporting should follow a specific approach for all evaluation functions. **If the `evaluation_function` you've written doesn't throw any errors, then it's output is returned under the `result` field - and assumed to have worked properly**. This means that if you catch an error in your code manually, and simply return it - the frontend will assume everything went fine. Instead, errors can be handled in two ways:

**Letting `evaluation_function` fail**: [Shimmy](#base-layer) wraps the call to `evaluation_function` in a try/except which catches any exception. This causes the evaluation to stop completely and return `{"error": {"message": "<repr of the exception>"}}`.

**Custom errors**: If you want to report more detailed errors from your function, use the `EvaluationException` class provided in the [evaluation-function-utils](module.md#class-evaluationexception) package. These are caught before all other standard exceptions, and are dealt with in a different way. These provide a way for your function to throw errors and stop executing safely, while supplying more accurate feedback to the front-end.

!!! note
    `EvaluationException` is part of the legacy `evaluation-function-utils` package. Functions built on Shimmy with `lf_toolkit` have no structured-error equivalent yet — raising **any** exception produces the `{"error": {"message": ...}}` block above.

!!! Example
It is discouraged to do the following in the evaluation code:
`python
    if something.bad.happened():
        return {
            "error": {
                "message": "Some important message",
                "other": "details",
            }
        }
    `

    As this causes the actual function output to be:
    ```json
    {
        "command": "eval",
        "result": {
            "error": {
                "message": "Some important message",
                "other": "details"
            }
        }
    }
    ```

    Instead, use custom exceptions from the [evaluation-function-utils](module.md#class-evaluationexception) package.
    ```python
    if something.bad.happened():
        raise EvaluationException(message="Some important message", other='details')
    ```

    As the actual function output will look like:
    ```json
    {
        "command": "eval",
        "error": {
            "message": "Some important message",
            "other": "details"
        }
    }
    ```

    This immediately indicates to the frontend client that something has gone wrong, allowing for proper feedback to be displayed.

## `evaluation_test.py`

This file contains the tests for `evaluation_function`, run with [`pytest`](https://docs.pytest.org/).
Github Actions runs them on every push and pull request, and the function is not deployed unless
they pass.

!!! Example
    A minimal test:
    ```python
    from .evaluation import evaluation_function

    def test_trivial():
        result = evaluation_function("a + b", "a + b", {})
        assert result.is_correct
    ```
Run them locally from the repository root with:
```bash
poetry run pytest
```

### Autotests

For writing simple tests, it may be easier to write the tests in a config file and have them
run on the evaluation function automatically. This can be achieved using the autotests library,
which can easily be integrated into an existing project by adding a decorator to the test class.
See the autotests [README](https://github.com/lambda-feedback/evaluation-function-auto-tests)
for more information.

Another benefit of this approach is that the tool that collects evaluation function documentation
([EvalDocsLoader](https://github.com/lambda-feedback/EvalDocsLoader)) can read this file and
auto-generate examples of correct and incorrect responses. This can help new users understand
the capabilities of your evaluation function.

For an example of how this looks, see the user docs for [compareBoolean](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/compareBoolean/#examples-from-integration-tests).

## Documentation

Evaluation function documentation is stored in two files, which contain documentation for
developers and users respectively. These files are fetched by 
[EvalDocsLoader](https://github.com/lambda-feedback/EvalDocsLoader), which integrates them
into this documentation site. 

In order for EvalDocsLoader to find your docs, your evaluation function must:

1. be deployed to the production site;
2. belong to the lambda-feedback organisation on Github;
3. have a [topic](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/classifying-your-repository-with-topics) called `evaluation-function`.

Once these requirements are met, the docs you write should appear on the documentation site.

### `docs/dev.md`

This should contain documentation that would be useful for new developers working on your function.

### `docs/user.md`

This should contain information for non-technical users, such as an overview of capabilities,
examples, and a description of parameters.
