# AWS System Architecture 
Description of each part of this software, and how they are deployed on AWS.

## AWS IAM Users, Roles and Policies
### User `lambda-github-pipeline`
Used by lambda function pipelines to upload container images to their respective ECR Repositories, and update their code. Has a single custom `LambdaGithubPipelinePolicy` Policy attached to it.

Access key ID and secret are stored in the Github Organization Secrets as:

- `LAMBDA_CONTAINER_PIPELINE_AWS_ID`
- `LAMBDA_CONTAINER_PIPELINE_AWS_SECRET`

### User `lambda-function-initialisator`
Used by a feedback (grading) function initialization script to instantiate its required AWS Resources: ECR Repository, Lambda function, ... Has a single custom `LambdaInitialisatorPolicy`

**NOTE** This should be replaced by a framework which allows us to define Architecture as Code (AWS CloudFormation, [serverless](https://www.serverless.com/) or [terraform](https://www.terraform.io/)). 

### User `S3 Uploader`
This user has the necessary permissions to upload and edit objects in the S3 Buckets that concerns this system (`problem-set-app`)

Its programmatic access keys are used by the CI/CD Pipeline for the main problem set app, and a locally run [`GeneratePDF.py`](https://github.com/Software-for-Maths-Learning/GeneratePDF) script.

### Role `GradingFunctionExecutionRole`
Execution role assumed by each of the Grading functions. Link [here](https://console.aws.amazon.com/iam/home#/roles/GradingFunctionExecutionRole).


## Main Problem Set App 
React app, uses React Router to navigate between pages. CI/CD done by a github action that runs on every push to master. Pipeline will build then upload files to the `problem-set-app` S3 Bucket. This is served by the main CloudFront Distribution. 

**NOTES**: 

- In order for the distribution to work, the 404 and 403 Error pages on the distribution were set to route to the `app/index.html` for this app.
- The app is built and served from the `app` folder on S3, therefore the `homepage` field in `package.json` was set to `/app/`

**Links**:

- [Repo](https://github.com/Software-for-Maths-Learning/problem-set-app)
- [S3 Bucket](https://s3.console.aws.amazon.com/s3/buckets/problem-set-app?region=eu-west-2&tab=objects)

**Useful Sources**:

 - [Deploying SPA to S3 using Cloudfront Distribution](https://gist.github.com/bradwestfall/b5b0e450015dbc9b4e56e5f398df48ff)


## Problem Set Media 
All the custom images and videos for Problem Sets are stored on the `problem-set-app` S3 Bucket (in the `media` folder). Files are also served from behind the CloudFront Distribution. 

**Links**:

- [S3 Bucket](https://s3.console.aws.amazon.com/s3/buckets/problem-set-app?region=eu-west-2&tab=objects


## Grading (Feedback) Gateway 
Containerized lambda function which handles all response area requests directly from the frontend.


**Associated AWS Resources and details**:

- `GradingGateway` Lambda function
	- Environment variables
		- `ALGORITHM_FUNCTION_BASE_URL`
		- `ENV_MODE`
		- `GRADING_FUNCTION_BASE_URL`
		- `SETS_DB_API_ANSWER_ENDPOINT`
	- Timeout: 40 seconds
- `GradingAPIGateway` API Gateway (set as trigger for lambda function)
- `grading-gateway` ECR Repository (contains lambda function image) 
	-  this is what the Github action pushes to using the **lambda-github-pipeline** user credentials.		

**Links**:

- [Repo](https://github.com/Software-for-Maths-Learning/GradingGateway)
- [Lambda Function](https://eu-west-2.console.aws.amazon.com/lambda/home?region=eu-west-2#/functions/GradingGateway)
- [ECR Repository](https://eu-west-2.console.aws.amazon.com/ecr/repositories/private/172805473475/grading-gateway?region=eu-west-2)
- [Grading API Gateway](https://eu-west-2.console.aws.amazon.com/apigateway/main/api-detail?api=x9j1uaivx1&region=eu-west-2)


## All Grading functions 
Containerized lambda functions handle individual grading requests from the Grading Gateway function. Repositories are all stored in this organisation, with the tag `Grading Function`.

Each function has an identical resource structure as the Grading Gateway:

- Github CI/CD Pipeline (authenticates using the **lambda-github-pipeline** user credentials)
- ECR Repo containing the image built by the pipeline (in kebab-case)
- Lambda function triggered by respective endpoints on the [Grading Functions Gateway](https://eu-west-2.console.aws.amazon.com/apigateway/main/api-detail?api=huwy6j485d&integration=o2mvbao&region=eu-west-2&routes=acde4ib). 

**NOTE:** When adding a new grading function to the gateway, make sure to set the `Payload format version` for the integration to `2.0`!!
