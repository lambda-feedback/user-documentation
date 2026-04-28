# Developing Chat Functions: Getting Started

## What is a Chat Function?

A chat function is a function which calls Large Language Models (LLMs) to respond to the messages of students given contextual data:

- question data
- user data such as past responses to the problem

Chat functions host a chatbot. Chatbots capture and automate the process of assisting students during their learning process when outside of classroom.

## Getting Setup for Development

1. Get the code on your local machine (Using github desktop or the `git` cli)

	- For new functions: clone the template repo for [chat-function-boilerplate](https://github.com/lambda-feedback/chat-function-boilerplate). **Make sure the new repository is set to public (it needs access to organisation secrets)**. 
	- For existing functions: please make your changes on a new separate branch

2. _If you are creating a new chatbot_, you can either edit the `src/agents/base_agent` or copy it and rename it based on the name of your chatbot.
3. You are now ready to start making changes and implementing features by editing each of the main function-logic files:

	1. **`src/agents/{base_agent}/{base}_agent.py`**: This file contains the main LLM pipeline using [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain](https://python.langchain.com/docs/introduction/).

   	- the chat function expects the following arguments when it being called:

   	Body with necessary fields:

   	```JSON
   	{
   		"conversationId": "12345Test",
   		"messages": [{ "role": "USER", "content": "hi" }],
   		"user": { "type": "LEARNER" }
   	}
   	```

   	Body with optional fields:

   	```JSON
   	{
   		"conversationId": "12345Test",
   		"messages": [
   			{ "role": "USER", "content": "<previous user message>" },
   			{ "role": "ASSISTANT", "content": "<previous assistant reply>" },
   			{ "role": "USER", "content": "hi" }
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
   			"summary": "<compressed conversation history>",
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
   			"summary": "<updated conversation summary>",
   			"conversationalStyle": "<updated style string>",
   			"processingTimeMs": 1234
   		}
   	}
   	```

   2. **`src/agents/{base_agent}/{base}_prompts.py`**: This is where you can write the system prompts that describe how your AI Assistant should behave and respond to the user.

   3. _If you edited the chatbot agent file name_, make sure to add your chatbot `invoke()` function to the `module.py` file.

	 4. Update the `config.json` file with the name of the chat function.

   5. Please add a `README.md` file to describe the use and behaviour of your chatbot.

4. Changes can be tested locally by running the pipeline tests using:
	```bash
	pytest
	```
   [Running and Testing Chat Functions Locally](local.md){ .md-button }


5. Merge commits into dev branch will trigger the `dev.yml` workflow, which will build the docker image, push it to a shared `dev` ECR repository and deploy an AWS Lambda function available to any http requests. In order to make your new chatbot available on the `dev` environment of the Lambda Feedback platform, you will have to get in contact with the ADMINS on the platform.

6. You can now test the deployed chat function using your preferred request client (such as [Insomnia](https://insomnia.rest/) or [Postman](https://www.postman.com/) or simply `curl` from a terminal). `DEV` Functions are made available at:
	```url
	https://<***>.execute-api.eu-west-2.amazonaws.com/default/chat/<function name as defined in config.json>
	```

	!!! example "Example Request to chatFunctionBoilerplate-dev"
			curl --location 'https://<***>.execute-api.eu-west-2.amazonaws.com/default/chat/chatFunctionBoilerplate-dev' \
			--header 'Content-Type: application/json' \
			--data '{
					"conversationId": "12345Test",
					"messages": [
							{
									"role": "USER",
									"content": "hi"
							}
					],
					"user": { "type": "LEARNER" }
			}'

7. Once the `dev` chat function is fully tested, you can merge the code to the default branch (`main`). This will trigger the `main.yml` workflow, which will deploy the `staging` and `prod` versions of your chat function. Please contact the ADMIN to provide you the URLS for the `staging` and `prod` versions of your chat function.

8. In order to make your new chat function available on any of the environments of the Lambda Feedback platform, you will have to get in contact with the ADMINS on the platform.
