# Evaluation Function Specification

## Introduction and Philosophy

Functionality for each evaluation function is split up as follows:

!!! note ""
Universal function behaviour applicable to _every_ function, such as the ability to run tests, return documentation and execute the evaluation is handled by the [**Base Layer**](#base-layer). This is the docker image which is extended by every developed evaluation function.

!!! abstract ""
Functionality that may be required in more than one function (but not necessarily all), such as the ability to call already deployed functions and error reporting is handled by the [**evaluation_function_utils**](module.md) python package. This package comes pre-installed in the base layer, and can optionally be imported and called from the _evaluation_function_.

!!! info ""
Finally, specific comparison logic and handling of bespoke evaluation parameters is done in the custom [**evaluation_function**](#the-evaluation_function), unique to each deployed instance. This is the logic that differenciates each function (comparing numbers, matrices, images, equations, graphs, text, tables, etc ...).

## Commands

Commands are handled by the [base layer](#base-layer). They define a unified interface for interacting with all deployed evaluation functions on the web. Practically, these are specified in the "command" request header.

!!! example
To execute the `docs-user` command for a function, the following header would be specified alonside the http request made to the endpoint on which the function is made available:

    ```bash
    curl --request GET \
    --url https://c1o0u8se7b.execute-api.eu-west-2.amazonaws.com/default/isExactEqual \
    --header 'command: docs-user'
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

This command runs and returns a summary three testing suites: requests, responses and evaluation. Request and response tests check that inputs and outputs to the function work correctly, and follow the correct syntax. Evaluation tests are unique to each evaluation function and test the actual comparison logic.

### `docs-user`

Command returns the `docs/user.md` file (base64 encoded)

### `docs-dev`

Command returns the `docs/dev.md` file (base64 encoded)

## Base Layer

## File Structure

A standard evaluation function repository based on the provided [boilerplate](https://github.com/lambda-feedback/Evaluation-Function-Boilerplate) will have the following file structure:

```bash
app/
    __init__.py
    evaluation.py # Script containing the main evaluation_function
    evaluation_tests.py # Unittests for the main evaluation_function
    requirements.txt # list of packages needed for algorithm.py
    Dockerfile # for building whole image to deploy to AWS

    docs/ # Documentation pages for this function (required)
        dev.md # Developer-oriented documentation
        user.md # LambdaFeedback content author documentation

.github/
    workflows/
        test-and-deploy.yml # Testing and deployment pipeline

config.json # Specify the name of the evaluation function in this file
README.md
.gitignore
```

!!! warning

    If you want to split up function logic into different files, these must be added to the `Dockerfile`. This is so they are packaged with the built image when deployed. For example, if `evaluation.py` imports functionality from an `app/utils.py` file, then the following line must be added:

    ```dockerfile linenums="9" hl_lines="7 8"
    RUN pip3 install -r requirements.txt

    # Copy the evaluation and testing scripts
    COPY evaluation.py ./app/
    COPY evaluation_tests.py ./app/

    # Copy additional files
    COPY utils.py ./app/

    # Copy Documentation
    COPY docs/dev.md ./app/docs/dev.md
    ```

## `evaluation.py`

The entire framework, validation and testing developed around evaluation functions is ultimately used to get to this file, or the `evaluation_function` function within it, to be more precise.

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

The function should output a single JSON-encodable dictionary. Although a large amount of freedom is given to what this dict contains, when utilising the function alongside the [lambdafeedback](https://lambdafeedback.com/) web app, a few values are expected/able to be consumed:

**`is_correct: <bool>`**: Boolean parameter indicate whether the comparison between `response` and `answer` was deemed correct under the parameters. This field is then used by the web app to provide the most simple feedback to the user (green/red).

!!! info
_More standardised function outputs that the frontend can consume are to come_

### Error Handling

Error reporting should follow a specific approach for all evaluation functions. **If the `evaluation_function` you've written doesn't throw any errors, then it's output is returned under the `result` field - and assumed to have worked properly**. This means that if you catch an error in your code manually, and simply return it - the frontend will assume everything went fine. Instead, errors can be handled in two ways:

**Letting `evaluation_function` fail**: On the request handler in the [Base Layer](#base-layer), the call to evaluation_function is wrapped in a try/except which catches any exception. This causes the evaluation to stop completely, returning a standard message, and a repr of the exception thrown in the `error.detail` field.

**Custom errors**: If you want to report more detailed errors from your function, use the `EvaluationException` class provided in the [evaluation-function-utils](module.md#errors) package. These are caught before all other standard exceptions, and are dealt with in a different way. These provide a way for your function to throw errors and stop executing safely, while supplying more accurate feedback to the front-end.

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

    As this causes the actual function output (by the AWS lambda function) to be:
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

    Instead, use custom exceptions from the [evaluation-function-utils](module.md#errors) package.
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

## `evaluation_tests.py`

This file is intended to contain unit tests for the `evaluation_function`. Python's built-in
[`unittest`](https://docs.python.org/3/library/unittest.html) framework is used.
These tests are run by Github Actions whenever changes are pushed to the main branch, and
the evaluation function is not deployed unless all the tests pass.

!!! Example
A minimal example of a test:
```python
import unittest
from .evaluation import evaluation_function

# Tests are functions beginning with "test_" in 
# a class that inherits from unittest.TestCase
class TestEvaluationFunction(unittest.TestCase):
    def test_trivial(self):
        result = evaluation_function("a + b", "a + b", {})
        self.assertTrue(result["is_correct"])
```
Tests can be run locally using 
```bash
$ python -m unittest app.evaluation_tests
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
