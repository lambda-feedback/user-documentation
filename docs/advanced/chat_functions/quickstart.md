# Developing Chat Functions: Getting Started

## What is a Chat Function?

A chat function is a function which calls Large Language Models (LLMs) to respond to the messages of students given contextual data:

- question data
- user data such as past responses to the problem

Chat functions host a chatbot. Chatbots capture and automate the process of assisting students during their learning process when outside of classroom.

## The μEd API specification

Chat functions on Lambda Feedback consume the [μEd API](https://mued.org/) request schema. The `messages`, `user`, `context` and `configuration` fields of an incoming request follow the μEd `ChatRequest` format, and the chat function translates them into a tutoring prompt (in the boilerplate this is done by `src/agent/context.py`).

Per the μEd `ChatRequest` schema, **only `messages` is required** — `conversationId`, `user`, `context` and `configuration` are all optional. Refer to [mued.org](https://mued.org/) for the authoritative field definitions.

## Getting Setup for Development

1. Get the code on your local machine (Using github desktop or the `git` cli)

	- For new functions: use the template repo [chat-function-boilerplate](https://github.com/lambda-feedback/chat-function-boilerplate) via *Use this template > Create a new repository*, choosing the `Lambda Feedback` organisation as the owner. **Make sure the new repository is set to public (it needs access to organisation secrets and GitHub deployment protection rules)**.
	- For existing functions: please make your changes on a new separate branch

2. Add your LLM credentials to a `.env` file in the root of the repository. OpenAI, Google AI, OpenRouter, Azure OpenAI and Ollama are supported out of the box:

	```bash
	# If you use OpenAI:
	OPENAI_API_KEY
	OPENAI_MODEL

	# If you use GoogleAI:
	GOOGLE_AI_API_KEY
	GOOGLE_AI_MODEL

	# If you use OpenRouter:
	OPENROUTER_API_KEY
	OPENROUTER_MODEL
	OPENROUTER_BASE_URL

	# If you use Ollama:
	OLLAMA_MODEL
	OLLAMA_BASE_URL
	OLLAMA_API_KEY
	```

	!!! note
		If you use another endpoint than the one set in the template, update the `.github/workflows/{staging-deploy,production-deploy,test-lint}.yml` files so they pass the right secrets and variables during testing and deployment.

3. You are now ready to start making changes and implementing features by editing each of the main function-logic files:

	1. **`src/agent/agent.py`**: This file contains the main LLM pipeline using [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain](https://python.langchain.com/docs/introduction/). If you want a custom agent, copy or update this file and import the new invocation in `src/module.py`.

		The agent uses **two separate LLM instances** — one for chat responses and one for conversation summarisation and style analysis. By default both use the same provider, but you can point them at different models (e.g. a cheaper or faster model for summarisation) by changing the class used in `agent.py`.

	2. **`src/agent/prompts.py`**: This is where you can write the system prompts that describe how your AI Assistant should behave and respond to the user.

	3. **`src/agent/llm_factory.py`**: factory classes for each LLM provider. Add your own provider here if it is not supported out of the box.

	4. **`src/agent/context.py`**: converts the μEd API `context` and `user` dictionaries into the prompt text given to the LLM.

	5. **`index.py`**: the entrypoint of the deployed function. It registers the `chat` and `chat health` handlers from `src/module.py` with `lf_toolkit`'s server.

	6. Update the `config.json` file with the name of the chat function.

	7. Please add a `README.md` file (and update `docs/`) to describe the use and behaviour of your chatbot.

## Request and response schema

Minimal request — only the required [μEd API](https://mued.org/) fields populated:

```JSON
{
	"messages": [{ "role": "USER", "content": "hi" }]
}
```

Full request as Lambda Feedback sends it, with all optional [μEd API](https://mued.org/) fields populated:

```JSON
{
	"conversationId": "<uuid>",
	"messages": [
		{ "role": "USER", "content": "<previous user message>" },
		{ "role": "ASSISTANT", "content": "<previous assistant reply>" },
		{ "role": "USER", "content": "<current message>" }
	],
	"user": {
		"type": "LEARNER",
		"preference": { "conversationalStyle": "<stored style string>" },
		"taskProgress": {
			"timeSpentOnQuestion": "30 minutes",
			"accessStatus": "a good amount of time spent on this question today.",
			"markedDone": "This question is still being worked on.",
			"currentPart": {
				"position": 0,
				"timeSpentOnPart": "10 minutes",
				"markedDone": "This part is not marked done.",
				"responseAreas": [
					{
						"responseType": "EXPRESSION",
						"totalSubmissions": 3,
						"wrongSubmissions": 2,
						"latestSubmission": {
							"submission": "<student's last answer>",
							"feedback": "<feedback text from evaluator>",
							"answer": "<reference answer used for evaluation>"
						}
					}
				]
			}
		}
	},
	"context": {
		"summary": "<compressed chat history>",
		"set": { "title": "Fundamentals", "number": 2, "description": "<set description>" },
		"question": {
			"title": "Understanding Polymorphism",
			"number": 3,
			"guidance": "<teacher guidance>",
			"content": "<master question content>",
			"estimatedTime": "15-25 minutes",
			"parts": [
				{
					"position": 0,
					"content": "<part prompt>",
					"answerContent": "<part answer>",
					"workedSolutionSections": [
						{ "position": 0, "title": "Step 1", "content": "..." }
					],
					"structuredTutorialSections": [
						{ "position": 0, "title": "Hint", "content": "..." }
					],
					"responseAreas": [
						{
							"position": 0,
							"responseType": "EXPRESSION",
							"answer": "<reference answer>",
							"preResponseText": "<label shown before input>"
						}
					]
				}
			]
		}
	}
}
```

Expected response:

```JSON
{
	"output": { "role": "ASSISTANT", "content": "<assistant reply text>" },
	"metadata": {
		"summary": "<updated chat summary>",
		"conversationalStyle": "<updated style string>",
		"processingTimeMs": 1234
	}
}
```

## Testing your changes

Changes can be tested locally by running the pipeline tests from the repository root with `PYTHONPATH=.` set (as CI does):

```bash
PYTHONPATH=. pytest
```

[Running and Testing Chat Functions Locally](local.md){ .md-button }

## Deploying to Lambda Feedback

Deployment is handled by GitHub Actions, as long as the repository is within the [Lambda Feedback organisation](https://github.com/lambda-feedback). Add your API key as a repository **secret** and your LLM model name as a repository **variable** under `Settings > Secrets and variables > Actions`, using the same names as in your `.env` file.

The pipeline has two environments:

- **Staging** — pushing to the `main` branch triggers the `staging-deploy.yml` workflow, which runs the test suite and (on success) deploys the chat function to AWS. After deploying, contact one of the Lambda Feedback admins to make the function accessible on `lambdafeedback.com`.

- **Production** — once you are happy with the staging deployment, create a `Release Request` using the button on the `README.md`, and run the `production-deploy.yml` workflow manually from the GitHub Actions tab. Pick a `version-bump` (`patch`/`minor`/`major`); the workflow redeploys staging, pauses on a manual approval stage (to be reviewed by a Lambda Feedback admin), then creates a `vX.Y.Z` git tag and GitHub Release and deploys to the main [Lambda Feedback platform](https://www.lambdafeedback.com/). Finally, contact one of the Lambda Feedback admins to make the function accessible on `lambdafeedback.com`.

Pull requests trigger the `test-lint.yml` workflow, which runs the test suite only — no deploy.

!!! note
	Once a deployment has been successful, share the necessary environment variables (e.g. API key and LLM model) with one of the Lambda Feedback team members so the function can be enabled on the platform.
