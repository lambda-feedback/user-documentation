# Overview of response areas

### List of response areas

The list of response areas is maintained in the Teacher section [here](../../../teacher/reference/response_area_components). In the Developer area (here), the behaviour of the response areas is documented.

### Data types when submitting empty responses (default behaviour)

If a user submits a response without inputing a value, the response areas convert the responses as follows before passing them to the evaluation functions:

| Input Value Type | Default Value | Comment                   |
| :---             | :---          | :---                      |
| number            | undefined     | [Behaviour needs updating]                          |
| string           | undefined     |  [Behaviour needs updating]                         |
| MATRIX           | `" "`            | empty string in all cells |
| TABLE            | `" "`            | empty string in all cells |
| MULTIPLE CHOICE  | `False`         | all choices set to false  |