# Developing Chat Agents: Getting Started 
## What is a Chat Agent?
It's a function which calls upon Large Language Models (LLMs) to respond to the student's messages given the known problem-specific information (the *question data*), and the student's own past responses to the problem (the *student submissions and its respective feedback received*). Chatbot Agents capture and automate the process of assisting students during their learning process when outside of classroom.

## Getting Setup for Development

1. Get the code on your local machine (Using github desktop or the `git` cli)
	- For new functions: clone the main repo for [lambda-chat](https://github.com/lambda-feedback/lambda-chat) and create a new branch. Then go under `scr/agents` and copy the `base_agent` folder.
	- For existing functions: please make your changes on a new separate branch 
2. *If you are creating a new chatbot agent*, you'll need to set it's name as the folder name in `scr/agents` and its corresponding files.
3. You are now ready to start making changes and implementing features by editing each of the three main function-logic files:
	1. **`scr/agents/{base_agent}/{base}_agent.py`**: This file contains the main LLM pipeline using [LangGraph](https://langchain-ai.github.io/langgraph/) and [LangChain](https://python.langchain.com/docs/introduction/). 
	
		- the agents expects the following inputs when it being called:

			Body with necessary Params:

			```JSON
			{
					"message":"hi",
					"params":{
							"conversation_id":"12345Test",
							"conversation_history": [{"type":"user","content":"hi"}]
					}
			}
			```

			Body with optional Params:
			```JSON
			{
					"message":"hi",
					"params":{
							"conversation_id":"12345Test",
							"conversation_history":[{"type":"user","content":"hi"}],
							"summary":" ",
							"conversational_style":" ",
							"question_response_details": "",
							"include_test_data": true,
							"agent_type": {agent_name}
					}
			}
			```

	2. **`scr/agents/{base_agent}/{base}_prompts.py`**: This is where you can write the system prompts that describe how your AI Assistant should behave and respond to the user.

	3. Make sure to add your agent `invoke()` function to the `module.py` file.
	
	4. Please add a `README.md` file to describe the use and behaviour of your agent.

4. Changes can be tested locally 
[Running and Testing Agents Locally](local.md){ .md-button } or by running the pipeline tests using:
```bash
pytest src/module_test.py
```

5. Merge commits into any branch (except main) will trigger the `dev.yml` workflow, which will build the docker image, push it to a shared `dev` ECR repository to make the function available from the `dev` and `localhost` client app.

6. In order to make your new chatbot available on the LambdaFeedback platform, you will have to get in contact with the ADMINS on the platform.