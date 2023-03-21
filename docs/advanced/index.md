# Advanced users

Advanced users can develop their own evaluation functions.

## Evaluation functions

Evaluation functions are responsible for taking in a user's response, comparing it with a correct answer, and providing feedback to the frontend application. Living as containserized Lambda functions on the cloud, they are infinitely customisable and language-agnostic. Content authors should be able to create their own at will. However, we are aware that in a lot of cases, this grading logic will be similar, which is why a few functions have already been created.

[Evaluation functions - Quickstart Guide](evaluation_functions/quickstart.md){ .md-button .md-button--primary }

## Response areas

Response areas are components in the frontend where student users can enter a response. The response is sent to the evaluation function, which returns feedback to the response area. In the alpha version response areas are built into the software (rather than being modular) so are not straightforward to redevelop. This website catalogues the basic behaviour of response areas, to inform developers of evaluation functions.

[Response areas - overview](response_areas/overview.md){ .md-button .md-button--primary}

## System Architecture

- Technologies
- Deployment pipelines
- Hierarchy

## Future Features
