# Expression

> **⚠️ DEPRECATED:** This feature is deprecated and will be removed in a future version. Please use [Math_Single_Line](Math_Single_Line.md) instead.

## Evaluation Function Options

### [isSimilar](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/isSimilar/)

### [symbolicEqual](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/symbolicEqual/)

### [compareExpressions](https://lambda-feedback.github.io/user-documentation/user_eval_function_docs/compareExpressions/)


## Component Parameters

### `post_response_text` (optional)

Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### `pre_response_text` (optional)

Text block to be displayed to the left of the input field. Markdown and LaTeX are allowed following the usual syntax.

### Enable Handwriting Input

Enables a handwriting canvas in the browser, which allows a student to draw their expression, rather than type using Sympy's syntax.

### Enable Photo Upload

Allows a student to upload their expression as an image, as an alternative to handwriting if the student isn't using a phone or tablet.

## Setting The Answer

Type the correct answer into the 'Response Area Answer' using standard syntax. As the student enters the answer, this will be rendered using the 'live preview' feature, to ensure the correct expression has been entered.

Use the 'Response Area Preview' to check the answer has been set correctly.

![Screenshot](screenshots/ExpressionResponseAreaAnswer.JPG)

## Example Student Response area

Correct response given
![Screenshot](screenshots/ExpressionCorrect.JPG)

Incorrect response given
![Screenshot](screenshots/ExpressionIncorrect.JPG)
