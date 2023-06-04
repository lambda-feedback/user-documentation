# Base Layer Feedback Implementation

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
1. First `evaluation_function` is called using the response, answer and params
3. If evaluation threw an error, then return the error message
2. If evaluation was successful, check for matching cases
	1. If "params" contains a non-empty list of "cases", determine the correct feedback, add it to the result and return the block (Logic for this is described in the next section) 
	2. If "params" doesn't contain a list of cases, simply return the result

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