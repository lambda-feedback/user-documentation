# Matrix

Matrix response area. Will populate the component with a grid of text input fields, in order to facilitate inputing matrices.

## Evaluation Function Options

### [ArrayEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/arrayEqual/)

### [ArraySymbolicEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/arraySymbolicEqual/)

## Component Parameters 
### `rows and cols` (required)
Required paramter, describes the shape of the Matrix to be displayed. 

In the 'Response area answer' section, the number of rows and columns can either be typed directly into the corresponding boxes, or adjusted using the up and down arrows, which appear once the mouse hovers over the input box.

![Screenshot](screenshots/MatrixSize.JPG)


### `post_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Setting The Answer
Once the required number of rows and cols has been selected, Each element of the matrix can be entered by clicking the individual input boxes and typing in the correct numbers.

![Screenshot](screenshots/MatrixResponseAreaAnswer.JPG)

## Example Student Response
Correct response given
![Screenshot](screenshots/ArrayCorrect.JPG)
Incorrect response given
![Screenshot](screenshots/ArrayIncorrect.JPG)