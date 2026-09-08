# Evaluation Functions in Other Languages

[Shimmy](https://github.com/lambda-feedback/shimmy) — the [base layer](specification.md#base-layer)
in front of every evaluation function — is language-agnostic. It handles the HTTP API, request
validation and the feedback `cases` loop, then runs *your* function as a child process over one
of two interfaces. Writing a function in another language means providing that child process.

## Base images

All base images bundle Shimmy and are published under
[`ghcr.io/lambda-feedback/evaluation-function-base`](https://github.com/lambda-feedback/evaluation-function-base):

| Image | For |
| --- | --- |
| `evaluation-function-base/python` | Python functions (uses [`lf_toolkit`](module.md)) |
| `evaluation-function-base/wolfram` | Wolfram Language / `wolframscript` functions |
| `evaluation-function-base/lean` | Lean functions (compiled binary) |
| `evaluation-function-base/scratch` | Any other language — a minimal Debian image with just Shimmy |

Your `Dockerfile` does `FROM` one of these, installs your toolchain and code, and sets the
environment variables below.

## Worker interfaces

Shimmy chooses the interface from the `FUNCTION_INTERFACE` environment variable.

### RPC (default)

The worker is a long-lived process that speaks [JSON-RPC 2.0](https://www.jsonrpc.org/specification),
one method per command (`eval`, `preview`, `healthcheck`). Transport is set by
`FUNCTION_RPC_TRANSPORT`:

- `stdio` (default) — messages over the process's stdin/stdout, framed with `Content-Length` headers;
- `ipc` — a Unix domain socket.

Python's [`lf_toolkit`](module.md) implements this interface, so Python functions just call
`create_server()` / `run()` in `evaluation_function/main.py` and never deal with the wire format.

### File

Shimmy starts a **fresh process per request**, appending two paths as the final arguments — an
input file and an output file. The worker reads the request JSON, writes the response JSON and
exits. This suits languages without a convenient long-running-server story, and large payloads
(e.g. base64 images).

The request file is *wrapped*:

```json
{
  "command": "eval",
  "params": { "response": "...", "answer": "...", "params": {} }
}
```

The worker writes the same `{"command": ..., "result": {...}}` / `{"error": {...}}` shape the
[Legacy API](specification.md#legacy-api) returns.

## Setting the worker command

The base layer reads these from the `Dockerfile`:

```dockerfile
ENV FUNCTION_COMMAND="wolframscript"
ENV FUNCTION_ARGS="-f,evaluation_function.wl"   # comma-separated
ENV FUNCTION_INTERFACE="file"
```

## Boilerplates

- [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python) — RPC interface via `lf_toolkit`
- [`evaluation-function-boilerplate-wolfram`](https://github.com/lambda-feedback/evaluation-function-boilerplate-wolfram) — file interface, `wolframscript -f evaluation_function.wl request.json response.json`
- [`evaluation-function-boilerplate-lean`](https://github.com/lambda-feedback/evaluation-function-boilerplate-lean) — file interface, compiled `.lake/build/bin/evaluation request.json response.json`

Each boilerplate's `README.md` has the full build, run and local-test instructions for that
language.
