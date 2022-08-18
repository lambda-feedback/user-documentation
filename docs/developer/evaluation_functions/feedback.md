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
				"feeddback": "feedback string",
				"params": {...} # Any parameters to set or override
			},
			...
		]
	}
}
```

## Execution Logic for the `eval` command
1. First `evaluation_function` is called using the response, answer and params
2. If evaluation was successful
	1. If result field contains "feedback", then simply return the result. *This allows functions to return custom feedback without using the "cases" feature.*
	2. If result field doesn't contain "feedback"
		1. If "params" contains a non-empty list of "cases", determine the correct feedback, add it to the result and return the block (Logic for this is described in the next section) 
		2. If "params" doesn't contain a list of cases, simply return the result
3. If evaluation threw an error, before even trying to generate feedback then return the error message

## Determining the correct feedback case
1. Iterate through each case in the list of `cases`:
	1. Validate the case has an 'answer' and 'feedback'
	2. If the case contains 'params', then merge them with the original 'params', overwriting values if they already exist
	3. Call `evaluation_function` with the student "response", case "answer" and merged "params"
		1. If the function returns "is_correct: true", we have a match 
		2. If the function returns an error, catch it and add it to a list of warnings
2. If we had no matches, don't return any feedback 
3. If we had exactly one match, return its corresponding feedback
4. If we had more than one match, return the first one and add a warning explaining which cases matched, and why only the first was selected.