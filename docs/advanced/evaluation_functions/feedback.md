# Base Layer Feedback Implementation

Feedback `cases` are handled by [Shimmy](specification.md#base-layer), not by your function —
Shimmy re-invokes `evaluation_function` once per case.

Input structure:

```json
{
	"response": "user input",
	"answer": "original answer",
	"params": {
		"cases": [
			{
				"answer": "same shape as original answer",
				"feedback": "feedback string",
				"params": {...} # Any parameters to set or override
			},
			...
		]
	}
}
```

## Execution Logic for the `eval` command
1. First `evaluation_function` is called using the response, answer and params.
2. If evaluation threw an error, return the error message.
3. If `params` contains a non-empty list of `cases` and the result is `is_correct: false`, run the case-matching procedure below, merge the outcome into the result and return it.
4. Otherwise, return the result unchanged.

When a case matches, Shimmy adds `matched_case` (the case's index) to the result, and if that case defines a `mark` (`0` or `1`) it overrides `is_correct`.

## Determining the correct feedback case
1. Iterate through each case in the list of `cases`:
	1. Validate the case has an 'answer' and 'feedback'
	2. If the case contains 'params', then merge them with the original 'params', overwriting values if they already exist
	3. Call `evaluation_function` with the student "response", case "answer" and merged "params"
		1. If the function returns "is_correct: true", we have a match, store case and feedback returned from the evaluation function
		2. If the function returns an error, catch it and add it to a list of warnings
2. If no matches were found, don't return any feedback 
3. If exactly one match was found, check if `override_eval_feedback` is in parameters
	1. If `override_eval_feedback` is set to true, return the case feedback
	2. If `override_eval_feedback` is not set or set to false, append the evaluation function feedback to the case feedback, separated by a linebreak and the return the result
4. If more than one matches were found, return the first one (using the same procedure as if only one match was found) and add a warning explaining which cases matched, and why only the first was selected.