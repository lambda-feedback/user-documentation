# Developer Documentation 
Welcome to LambdaFeedback's developer docs.

## Evaluation functions
Evaluation functions are responsible for taking in a user's response, comparing it with a correct answer, and providing feedback to the frontend application. Living as containserized Lambda functions on the cloud, they are infinitely customisable and language-agnostic. Content authors should be able to create their own at will. However, we are aware that in a lot of cases, this grading logic will be similar, which is why a few functions have already been created. 

[Check out our Quickstart Guide](evaluation_functions/quickstart.md){ .md-button .md-button--primary }



## Response area components

# Default Answers

Here is the list of default value answers (this is the case when a student or a teacher opens a question and clicks Check without inputing any value):

| Input Value Type | Default value | Comment                   |
| :---             | :---          | :---                      |
| nuber            | undefined     |                           |
| string           | undefined     |                           |
| MATRIX           | ''            | empty string in all cells |
| TABLE            | ''            | empty string in all cells |
| MULTIPLE CHOICE  | false         | all choices set to false  |



# Guide to create more

TBA

## System Architecture
- Technologies
- Deployment pipelines
- Hierarchy 


## Future Features