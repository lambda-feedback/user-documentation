# NumericUnits

Provides two input fields with `Number` and `Units` placeholder texts. This area will also display its associated grading function (as seen in the screenshot below). 

**Note** this area will display how the user's response was interpred using the `interp_string` field provided in the feedback object returned by that function (if it exists).

## Component Parameters 
### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

In this case, the response is a single string which features the user's response to both fields separated by a space.
!!! example 

    ```json 
    "response": "150 g"
    ```

## Example Screenshot 
![Screenshot](screenshots/NumericUnits.jpg)