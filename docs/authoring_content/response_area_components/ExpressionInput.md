# ExpressionInput 

This response area is very similar to [TextInput](TextInput.md), differing in that it can display how the user's response was interpreted back to them. This is done by the grading function providing a `feedback.response_latex` field, which gets rendered.

## Component Parameters 
### `post_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is simply sent as a string, exactly how the user input it in the input field. 

!!! example 

    ```json 
    "response": "4*x + 1"
    ```


## Example Screenshot 
![Screenshot](screenshots/ExpressionInput.jpg)