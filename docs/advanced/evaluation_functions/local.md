# Running and Testing Functions Locally

Evaluation functions are developed and tested locally **without** the base-image server: you call
your function directly and run its test suite. The full container — your function behind the
[Shimmy](https://github.com/lambda-feedback/shimmy) base layer — is normally exercised by CI and
in deployment, but you can also [build and run it locally](#testing-against-the-container) to
check the real HTTP API before pushing.

!!! info "This page is about Python functions"
    It covers functions built from the current
    [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python),
    which uses [Poetry](https://python-poetry.org/) and an `evaluation_function/` package — the
    commands below (`poetry`, `pytest`, `python -m evaluation_function.dev`) are all
    Python-specific. For Wolfram, Lean or other languages the local loop differs; see
    [Other Languages](alternate_languages.md) and the relevant boilerplate's `README.md`.
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

## Testing against the container

Building the image and sending it real HTTP requests runs the **same container CI builds and
deployment ships**: your function behind [Shimmy](https://github.com/lambda-feedback/shimmy),
serving the API on port `8080`. Use it for the end-to-end checks that calling the function
directly and `pytest` don't cover — schema validation, the µEd and Legacy wire formats, and the
[feedback `cases`](feedback.md) loop.

!!! info "Applies to any base image"
    The steps below use the Python `evaluation_function/` layout for their examples, but the
    build and run commands are the same for Wolfram, Lean and `scratch` functions — only the
    `Dockerfile` contents differ. See [Other Languages](alternate_languages.md).

### Build the image

From the repository root (where the `Dockerfile` is):

```bash
docker build -t my-eval-function .
```

!!! tip "Podman works too"
    [Podman](https://podman.io/) is a drop-in replacement — swap `docker` for `podman` in every
    command on this page and the arguments are identical.

### Run the container

Expose Shimmy's port `8080`:

```bash
docker run --rm -p 8080:8080 my-eval-function
```

Add `--name my-eval-function` if you want to `docker exec` / `docker cp` into the running
container, and `-e SANDBOX_ENABLED=true` to also exercise the optional
[nsjail](https://github.com/google/nsjail) sandbox that Shimmy applies in production.

### Health checks

```bash
curl http://localhost:8080/health
curl --header 'X-Api-Version: 0.1.0' http://localhost:8080/evaluate/health
```

`GET /health` is a plain liveness probe; `GET /evaluate/health` is the µEd health route.

### Send a µEd request

`POST /evaluate` with an `X-Api-Version: 0.1.0` header — the request the platform sends for
newly registered functions:

```bash
curl --request POST \
  --url http://localhost:8080/evaluate \
  --header 'Content-Type: application/json' \
  --header 'X-Api-Version: 0.1.0' \
  --data '{
    "submission": { "type": "OTHER", "content": { "value": "x + x" } },
    "task": { "referenceSolution": { "expression": "2*x" } }
  }'
```

See the [µEd API](specification.md#ed-api) section of the specification for the full
request/response contract.

### Send a Legacy request

`POST /` with the command in a `command` header and a bare `response` / `answer` / `params`
body:

```bash
curl --request POST \
  --url http://localhost:8080/ \
  --header 'Content-Type: application/json' \
  --header 'command: eval' \
  --data '{ "response": "2*x", "answer": "x + x", "params": {} }'
```

The response is `{"command": "eval", "result": {...}}`, or `{"error": {"message": ...}}` if the
function raised — see [Legacy API](specification.md#legacy-api). Swapping the header for
`command: healthcheck` runs the function's own test suite inside the container and returns a
pass/fail summary.

### Postman and other clients

Any HTTP client works — `curl`, [Insomnia](https://insomnia.rest/),
[Postman](https://www.postman.com/). Point it at the running container:

- **µEd** — `POST http://localhost:8080/evaluate`, headers `Content-Type: application/json` and
  `X-Api-Version: 0.1.0`, body as the µEd JSON above.
- **Legacy** — `POST http://localhost:8080/`, header `Content-Type: application/json` plus a
  `command` header (`eval`, `preview` or `healthcheck`), body `{ "response": ..., "answer": ...,
  "params": {} }`.

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
