# Developing Evaluation Functions: Getting Started 
## What is an Evaluation Function?
It's a cloud function which performs some computation given some user input (the *response*), a problem-specific source of truth (the *answer*), and some optional parameters (*params*). Evaluation functions capture and automate the role of a teacher who has to keep marking the same question countless times. The simplest example for this would be one which checks for exact equivalence - where the function signals a *response* is correct only if it is identical to the *answer*. However, more complex and exotic ones such as symbolic expression equivalence and parsing of physical units can be imagined. 

## Getting Setup for Development

1. Get the code on your local machine (Using github desktop or the `git` cli)
	- For new functions: create and clone a new repository using the [boilerplate template](https://github.com/lambda-feedback/Evaluation-Function-Boilerplate). **Make sure the new repository is set to public (it needs access to organisation secrets)**.
	- For existing functions: please make your changes on a new separate branch 
2. *If you are creating a new function*, you'll need to set it's name (as it will be deployed) in the `config.json` file, available in the root directory.
	- The name must be unique. To view existing grading functions, go to:
		- [Staging API Gateway Integrations](https://eu-west-2.console.aws.amazon.com/apigateway/main/develop/integrations/attach?api=c1o0u8se7b&region=eu-west-2&routes=0xsoy4q)
		- [Production API Gateway Integrations](https://eu-west-2.console.aws.amazon.com/apigateway/main/develop/integrations/attach?api=cttolq2oph&integration=qpbgva8&region=eu-west-2&routes=0xsoy4q)
3. You are now ready to start making changes and implementing features by editing each of the three main function-logic files:
	1. **`app/evaluation.py`**: This file contains the main `evaluation_function` function, which ultimately gets called to compare a *response* to an *answer*. 

		[`evaluation.py` Specification](specification.md#evaluationpy){ .md-button }

	2. **`app/evaluation_tests.py`**: This is where you can test the logic in `evaluation.py`, following the standard `unittest` format. 

		[`evaluation_tests.py` Specification](specification.md#evaluation_testspy){ .md-button }

	3. Documentation files:
		- **`app/docs/dev.md`**: This file should be edited to reflect any changes/features implemented, following a developer perspective. It is baked into the function's image to be pulled by this documentation website under the [deployed functions](index.md) section.
    
		- **`app/docs/user.md`**: This file documents how the function can be used by a teacher user, from the perspective of editing content on the [LambdaFeedback]({{ urls.client }}) platform. This time, files are collated and displayed in the [Teacher](../../teacher/index.md) section.

4. Changes can be tested locally by running the tests you've written using:
```bash
python -m unittest app/evaluation_tests.py
```
[Running and Testing Functions Locally](local.md){ .md-button }

5. Merge commits into the default branch will trigger the `test-and-deploy.yml` workflow, which will build the docker image, push it to a shared ECR repository, then call the backend `grading-function/ensure` route to build the necessary infrastructure to make the function available from the client app.

6. You can now test the deployed evaluation function using your prefered request client (such as [Insomnia](https://insomnia.rest/) or [Postman](https://www.postman.com/) or simply `curl` from a terminal). Functions are made available at:
	```url
	https://c1o0u8se7b.execute-api.eu-west-2.amazonaws.com/default/<function name as defined in config.json>
	```

	!!! example "Example Request to SymbolicEqual"
			``` 
			curl --request GET \
				--url https://c1o0u8se7b.execute-api.eu-west-2.amazonaws.com/default/symbolicEqual \
				--header 'Content-Type: application/json' \
				--header 'command: eval' \
				--data '{"response": "x + x", "answer": "2*x"}'
			```

7. In order to make your new function available on the LambdaFeedback platform, you have to register it via the [Admin Panel]({{ urls.client }}admin/functions). This is done by supplying its name, url (the same as the one above) and supported response types. 

## More Info

- [General Function Specification and Behaviour](specification.md)
    - Function philosophy including deployment strategy
    - Request/Response schemas and communication spec 
    - Base layer logic, properties and behaviour
  
- [EvaluationFunctionUtils](module.md) (python package)
    - Error Reporting 
    - Schema validation
    - Local testing