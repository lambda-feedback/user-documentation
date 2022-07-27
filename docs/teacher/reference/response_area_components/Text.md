# Text

Most basic response area, displays a single input field, accepting and text from the user. 

## Evaluation Function Options

### `isExactEqual`
A strict comparison in Python using '=='. This function is a basic utility but often not the function you really want to use because it is quite brittle.

### `isSimilar`
Calculates the difference between the teacher answer (ans) and the student response (res); compares this to an allowable difference comprising an absolute tolerance (atol) and a relative tolerance (rtol). 

### `symbolicEqual`
Compares two symbolic expressions for mathematical equivalence, using SymPy. See [SymPy](https://www.sympy.org/en/index.html.md-button) for further information.

## Setting the answer

Type the correct answer into the 'Response Area Answer' section, replacing the work 'Text', which initially occupies the input field.

![Screenshot](screenshots/TextResponseAreaAnswer2.jpg)
![Screenshot](screenshots/TextResponseAreaAnswer.jpg)


## Component Parameters 
### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `grading_parameters` (For isSimilar)
- `atol`: Absolute tolerance parameter
- `rtol`: Relative tolerance parameter

Valid params include atol and rtol, which can be used in combination, or alone. As the comparison made is the following:

!!! note ""

    is_correct = abs(res - ans) <= (atol + rtol*abs(ans))


## Response Structure
*This is how the react component will structure the user's input to the Grading Gateway, when they press the check button.* 

The response is a string containing the user's response, exactly as they typed it in the input field.

!!! example

    ```json 
    "response": "incompressible"
    ```

## Example Student Response
![Screenshot](screenshots/TextStudentResponse.jpg)

Correct response:
![Screenshot](screenshots/TextCorrect.jpg)