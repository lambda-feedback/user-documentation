# NumberInput

Very similar to the [TextInput](TextInput.md) response area, except the user response is parsed as a float.

## Component Parameters 
### `post_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is simply sent as a float, parsed from the input field using the JavaScript `parseFloat` function.

!!! example 

    ```json 
    "response": 15.8
    ```

## Example Screenshot 
![Screenshot](screenshots/NumberInput.jpg)