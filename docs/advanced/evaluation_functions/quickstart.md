# Developing Evaluation Functions: Getting Started 
## What is an Evaluation Function?
It's a cloud function which performs some computation given some user input (the *response*), a problem-specific source of truth (the *answer*), and some optional parameters (*params*). Evaluation functions capture and automate the role of a teacher who has to keep marking the same question countless times. The simplest example for this would be one which checks for exact equivalence - where the function signals a *response* is correct only if it is identical to the *answer*. However, more complex and exotic ones such as symbolic expression equivalence and parsing of physical units can be imagined. 

## Getting Setup for Development

1. Get the code on your local machine (Using github desktop or the `git` cli)
	- For new functions: create a new repository from the [`evaluation-function-boilerplate-python`](https://github.com/lambda-feedback/evaluation-function-boilerplate-python) template via *Use this template*, choosing the `Lambda Feedback` organisation as the owner. **Make sure the new repository is set to public (it needs access to organisation secrets)**. Boilerplates for other languages also exist — [`evaluation-function-boilerplate-wolfram`](https://github.com/lambda-feedback/evaluation-function-boilerplate-wolfram) and [`evaluation-function-boilerplate-lean`](https://github.com/lambda-feedback/evaluation-function-boilerplate-lean); see [Other Languages](alternate_languages.md).
	- For existing functions: please make your changes on a new separate branch 
2. *If you are creating a new function*, set its deployed name in the `config.json` file in the root directory:

	```json
	{ "EvaluationFunctionName": "myFunction" }
	```

	The name must be unique across the organisation and is conventionally `lowerCamelCase`.
3. You are now ready to start making changes. The function logic lives in the `evaluation_function/` package:
	1. **`evaluation_function/evaluation.py`**: contains the main `evaluation_function`, which is called to compare a *response* to an *answer*.

		[`evaluation.py` Specification](specification.md#evaluationpy){ .md-button }

	2. **`evaluation_function/preview.py`**: contains `preview_function`, which pre-processes a *response* for live display (e.g. rendered LaTeX) without grading it.

	3. **`evaluation_function/evaluation_test.py`**: where you test the logic in `evaluation.py`, using [`pytest`](https://docs.pytest.org/).

		[`evaluation_test.py` Specification](specification.md#evaluation_testpy){ .md-button }

	4. **`evaluation_function/main.py`**: the entry point. It calls `lf_toolkit.create_server()` and registers your `evaluation_function` and `preview_function` with it. You rarely need to change this file.

	5. Documentation files:
		- **`docs/dev.md`**: edited to reflect any changes/features from a developer perspective. It is baked into the function's image and pulled into this site under the [deployed functions](index.md) section.

		- **`docs/user.md`**: documents how a teacher uses the function when editing content on the [LambdaFeedback]({{ urls.client }}) platform. These files are displayed in the [Teacher](../../teacher/index.md) section.

4. Changes can be tested locally by running your tests from the repository root:
```bash
poetry install
poetry run pytest
```
[Running and Testing Functions Locally](local.md){ .md-button }

5. The pipeline has two environments:

	- **Staging** — pushing to the `main` branch triggers the `staging-deploy.yml` workflow, which runs the test suite and (on success) builds and deploys the docker image to staging.

	- **Production** — once you are happy with the staging deployment, run the `production-deploy.yml` workflow manually from the GitHub Actions tab, picking a `version-bump` (`patch`/`minor`/`major`).

	Pull requests trigger the `test-lint.yml` workflow, which runs the test suite only — no deploy.

	!!! note
		The build and deploy steps are implemented as reusable workflows maintained in [lambda-feedback/evaluation-function-workflows](https://github.com/lambda-feedback/evaluation-function-workflows).

6. Once the deploy workflow has run, the platform hosts your function at a public URL. You can find it in the [Admin Panel]({{ urls.client }}admin/functions) after registering the function (next step), and test it with any request client (`curl`, [Insomnia](https://insomnia.rest/), [Postman](https://www.postman.com/)).

	!!! example "Example µEd request"
		```bash
		curl --request POST \
		  --url https://<your-function-url>/evaluate \
		  --header 'Content-Type: application/json' \
		  --header 'X-Api-Version: 0.1.0' \
		  --data '{
		    "submission": { "type": "MATH", "content": { "expression": "x + x" } },
		    "task": { "referenceSolution": { "expression": "2*x" } }
		  }'
		```

		See the [µEd API](specification.md#ed-api) section of the specification for full request/response details. Functions still running the **Legacy** API instead use the `command` header — see [Legacy API](specification.md#legacy-api).

7. To make your new function available on the LambdaFeedback platform, register it via the [Admin Panel]({{ urls.client }}admin/functions) by supplying its name, URL and supported response types.

	!!! note
		New evaluation functions should be registered as **µEd** (a standard, path-based API — see [Chat Functions](../chat_functions/quickstart.md) for a general introduction to µEd on Lambda Feedback, and [mued.org](https://mued.org/) for the specification). The **Legacy** command-header API — described in the [specification](specification.md#legacy-api) — is frozen and no longer developed, but Shimmy still serves it.

## More Info

- [General Function Specification and Behaviour](specification.md)
    - Function philosophy including deployment strategy
    - Request/Response schemas and communication spec 
    - Base layer (Shimmy) logic, properties and behaviour
  
- [Helper packages](module.md)
    - `lf_toolkit` — server wiring, `Result` / `Params` / `Preview`, image upload
    - `evaluation-function-utils` — the legacy package (error reporting, cross-function client)