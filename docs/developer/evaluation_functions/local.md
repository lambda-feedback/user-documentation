# Running and Testing Functions Locally

## Simple


## Using Docker [:material-docker:](https://www.docker.com/)
This method builds and runs evaluation functions in the same way they are deployed on AWS as Lambda functions. Extending a pre-built and AWS-maintained [base python image](https://docs.aws.amazon.com/lambda/latest/dg/python-image.html#python-image-base), the container contains a HTTP client which can be used to locally simulate Lambda execution events. 

Note that this is different from the [simple](#simple) method proposed, in that it gives access to all the functionality provided by the base layer. This means that commands such as `docs` and `healthcheck` can be tested.

1. Install [Docker](https://docs.docker.com/get-docker/) on your machine

2. Navigate to the root directory of your function

3. Build the image. This will pull our base image from Dockerhub, extend it with files specific to your evaluation function and name it `eval-tmp`.
    ```bash
    docker image build -t eval-tmp app
    ```

4. Spin up a container using the image built in the previous step.
    ```bash 
    docker run --rm -d --name eval-function -p 9000:8080 eval-tmp 
    ```

5. You can now simulate requests to the function using any request client (like [Insomnia](https://insomnia.rest/) or [Postman](https://www.postman.com/)). By default, the url you can hit is:
    ```url 
    http://localhost:9000/2015-03-31/functions/function/invocations
    ```

    ???+ warning
        *When deployed, our Lambda functions are triggered by calls made through an AWS [API Gateway](https://aws.amazon.com/api-gateway/). This means that when testing locally, events sent should follow the structure of events triggered by that resource. That is, if you want to simulate what it would be like to make web requests to the deployed function.*

        Specifically, this means structuring requests in the following way:
        ```json 
        {
          "headers": {
            "command": "eval"
          },
          "body": {
            "response": "a",
            "answer": "a",
            "params": {
              "garlic": "moreish"
            }
          }
        }
        ```

        The main difference is that `headers` and `body` are sent as keys in the main body of the local request. When hitting the deployed function through the API Gateway, the `command` field would instead be passed in the actual HTTP headers of the request - and the actual request body would only contain the `response`, `answer` and `params` fields.

6. *(Optional)* The `run` command specifies the **-d** flag, which spins up the container in detached mode. If you want to inspect the logs of the function, you can run:
    ```bash 
    docker container logs -f eval-function 
    ```

??? note "Tip"
    You will very rarely need this, but you can peek into the running container by opening a shell within it using:

    ```bash 
    docker exec -it eval-function bash
    ```

## Useful Links 

- 
