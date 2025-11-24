# Number

Very similar to the [Text](Text.md) response area, except the user response is parsed as a float.

## Evaluation Function Options

### [isSimilar](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/isSimilar/)

### [isExactEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/isExactEqual/)

## Setting The Answer

In the 'Response Area Answer' section, enter the required float into the input field. To test this, try typing correct and incorrect answers into the 'Response Area Preview' section.

![Screenshot](screenshots/NumberResponseAreaAnswer.JPG)



## Component Parameters 
### `post_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `grading_parameters` (optional)
- `atol`: Absolute tolerance parameter
- `rtol`: Relative tolerance parameter

Valid params include atol and rtol, which can be used in combination, or alone. As the comparison made is the following:

!!! note ""

    is_correct = abs(res - ans) <= (atol + rtol*abs(ans))



## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is simply sent as a float, parsed from the input field using the JavaScript `parseFloat` function.

!!! example 

    ```json 
    "response": 15.8
    ```

## Example Student Response

Correct response:
![Screenshot](screenshots/NumberCorrect.JPG)

Incorrect response:
![Screenshot](screenshots/NumberIncorrect.JPG)