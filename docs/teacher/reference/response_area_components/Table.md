# Table

Table response area. Will populate the component with a grid of text input fields, in order to facilitate inputing elements of a table. The number of rows and columns can be specified, along with their corresponding names.


## Evaluation Function Options

### [ArrayEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/arrayEqual/)

### [ArraySymbolicEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/arraySymbolicEqual/)

## Component Parameters 

### `rows` 
The number of rows required for the table can be entered into this input field, either through typing directly, or using thr up and down arrows located inside the box.

### `cols` 
The number of columns required for the table can be entered into this input field, either through typing directly, or using thr up and down arrows located inside the box.

![Screenshot](screenshots/TableRowsCols.JPG)

### `post_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)
Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

## Setting The Answer

Once the required number of rows and cols has been inputted, The names of each row and column should be changed depending on their corresponding variables. The value of each grid element can then be entered into individual input fields. 

If the row or column names are not changed, these will appear blank in the student response area.

![Screenshot](screenshots/TableResponseAreaAnswer.JPG)


## Example Student Response

Correct response:
![Screenshot](screenshots/TableCorrect.JPG)

Incorrect response:
![Screenshot](screenshots/TableIncorrect.JPG)
