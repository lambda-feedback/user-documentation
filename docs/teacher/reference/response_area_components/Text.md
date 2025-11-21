# Text

Allows student's to enter any text input, whether that be prose, math, code or any other type of input.

## Evaluation Function Options

As text supports any input, any evaluation function can be used.
However, there are some text specific evaluation functions, such as shortTextAnswer and chatGPT.

### `chatGPT (experimental)`

Passes the student's response and a teacher written prompt to GPT for evaluation. 

### `shortTextAnswer (experimental)`
Uses natural language processing techniques to calculate the similarity between a student's response and a teacher's answer, using semantic similarity.  