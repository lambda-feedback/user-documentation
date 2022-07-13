# TextInput

Most basic response area, displays a single input field, accepting and text from the user. 

## Component Parameters 
### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is a string containing the user's response, exactly as they typed it in the input field.

!!! example

    ```json 
    "response": "incompressible"
    ```

## Example Screenshot 
![Screenshot](screenshots/TextInput.jpg)