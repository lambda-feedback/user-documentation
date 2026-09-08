# Running and Testing Functions Locally

Evaluation functions are developed and tested locally **without** the base-image server: you call
your function directly and run its test suite. The full container — your function behind the
[Shimmy](https://github.com/lambda-feedback/shimmy) base layer — is exercised by CI and in
deployment, not as part of the local loop.

!!! note
    The commands below assume a function based on the current
    [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python),
    which uses [Poetry](https://python-poetry.org/) and an `evaluation_function/` package.
    Functions still on the older AWS Lambda base layer (those with an `app/` directory) are
    covered [at the bottom of this page](#older-aws-lambda-base-layer).

## Run unit tests

Install dependencies and run the test suite with [`pytest`](https://docs.pytest.org/) from the
repository root:

```bash
poetry install
poetry run pytest
```

This is the same suite the CI pipeline runs on every push and pull request; a function is not
deployed unless it passes.

## Call the function directly

The boilerplate ships an `evaluation_function/dev.py` helper that calls your `evaluation_function`
directly — the quickest loop while iterating on comparison logic:

```bash
python -m evaluation_function.dev "<response>" "<answer>" '<params-json>'
```

For example:

```bash
python -m evaluation_function.dev "2*x" "x + x" '{}'
```

`answer` and the params JSON are optional. See the script's `--help` for its exact arguments,
which vary slightly between functions.

## Older AWS Lambda base layer

??? note "Functions not yet migrated"
    A small number of functions (for example
    [`compareExpressions`](https://github.com/lambda-feedback/compareExpressions)) still extend
    the older `ghcr.io/lambda-feedback/baseevalutionfunctionlayer` image and keep the `app/`
    directory layout. Their tests run with `python -m unittest app.evaluation_tests`, and the
    built image is exercised locally with the AWS
    [Runtime Interface Emulator](https://github.com/aws/aws-lambda-runtime-interface-emulator)
    (`docker run -p 9000:8080 …`, then POST an API-Gateway-style event to
    `http://localhost:9000/2015-03-31/functions/function/invocations`). See the function's own
    `README.md` for the details.

## Useful links

- [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python) — template for new Python functions
- [`toolkit-python`](https://github.com/lambda-feedback/toolkit-python) — the `lf_toolkit` helper package
- [`evaluation-function-base`](https://github.com/lambda-feedback/evaluation-function-base) — the base images (Python, Wolfram, Lean, scratch)
- [µEd API specification](https://mued.org/)
