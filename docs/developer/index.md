# Developer Documentation 
---

- Evaluation functions
  - Quickstart Guide
  - General Function Specification and Behaviour
    - *index*: Function philosophy including deployment strategy
    - Request/Response schemas and communication spec 
    - Base layer logic, properties and behaviour
  - EvaluationFunctionUtils (python package)
    - Error Reporting 
    - Schema validation
    - Local testing
  
- Response area components
  - Guide to create more

## Boolean Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is an integer equal to `1` if the `true` option was selected, and `0` if the `false` option was selected.

!!! example 

    ```json 
    "response": 1
    ```

- System Architecture
  - Technologies
  - Deployment pipelines
  - Hierarchy 

- Future Features