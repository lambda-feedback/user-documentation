# Advanced users


## Microservices

The fundamental idea of Lambda Feedback is that it calls external microservices to provide interaction with users. There are two types of microservice: 

Evaluate a student response and provide feedback: 
[Evaluation functions - Quickstart Guide](evaluation_functions/quickstart.md){ .md-button .md-button--primary style="width: 400px;"}

Dialogic conversations with students:<br>
[Chat functions - Quickstart guide ](chatbot_agents/quickstart.md){ .md-button .md-button--primary style="width: 400px;"}

All microservices are called over http. There is complete freedom in their implementation. Lambda Feedback also provides families of deployed microservices, using open source code available in our public GitHub repositories.

This section of documentation is to help developers of microservices. The documentation is written assuming you have basic developer skills.

In addition to microservices, this 'Advanced' section caters to administrators of Lambda Feedback tenants; and to developers of interactive response areas, that can be published within our web-stack via discussion with the developers. 

## Response areas

Response areas are components in the frontend where student users can enter a response. The response is sent to the evaluation function, which returns feedback to the response area. In the alpha version response areas are built into the software (rather than being modular) so are not straightforward to redevelop. This website catalogues the basic behaviour of response areas, to inform developers of evaluation functions.

[Response areas - overview](response_areas/overview.md){ .md-button .md-button--primary style="width: 400px;"}

## Administrators

Content to be added.
