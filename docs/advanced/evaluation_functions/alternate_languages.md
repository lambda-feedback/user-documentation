# Alternate Evaluation Function Languages
---

## Lambda-Compatible Images
### Extending a pre-built Lambda image
- Available for: Node.js, Python, Java, .NET, Go, Ruby
- [Docs](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-images.html#runtimes-images-lp)
- [Repo](https://github.com/aws/aws-lambda-base-images)
- These base images are regularly updated, and the most widely used (more docs)
- They also come with pre-packaged runtime interface clients - a HTTP interface for runtimes to receive invocation events and respond
	- Good for local development

### Creating custom base images
- Using the [lambda/provided](https://gallery.ecr.aws/lambda/provided) image
	- This "contains all the required components to run functions packaged as container images on Lambda"
- Building a custom runtime from scratch 
	- [Custom AWS Lambda runtimes](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-custom.html#runtimes-custom-build)
	- [Runtimes walkthrough tutorial](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-walkthrough.html)
- Emulate execution locally?
> Lambda provides a runtime interface emulator (RIE) for you to test your function locally. The AWS base images for Lambda and base images for custom runtimes include the RIE. For other base images, you can download the [Runtime interface emulator](https://github.com/aws/aws-lambda-runtime-interface-emulator) from the AWS GitHub repository.

### Misc Notes/Sources
- [The Lambda Execution Environment](https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtime-environment.html)
- [Create Images from Alternative base images](https://docs.aws.amazon.com/lambda/latest/dg/images-create.html#images-create-from-alt)

## Development Philosophy
Ultimately we want to call a function made by a user in any language. Two ways to do this:

- We write and provide runtime in all the different languages. This means that all the logic happens in that language. We write the code that actually receives the requests from lambda function events. In this case, the user function can be imported from those handlers.
	- Writing handlers in each of those languages requires time and extensive knowledge (in order to write robust code)
	- Handler code needs to:
		- Have clean and reliable error catching
  
- We write a global runtime, which makes a call to their function via a sub-process. We call their script, which must recieve the payload as a commandline argument.
	- User has to write more code 
		- For allowing cmdline arguments, and parsing of inputs
	- Might be slower than in other languages. Since another script has to be executed.