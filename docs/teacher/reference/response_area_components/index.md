# Response Area Components

These are what the user interacts with on the front-end. As React components, they admit a certain number of parameters which are described in this section.

## Response Area User Interactions

The user can add, delete, edit or switch response area.

### Add Response Area

The user can add a response area without any restrictions.

### Delete Response Area

The user can delete a response area without any restrictions. A popup message appears to confirm the deletion.

However, it is important to remember that there might be submissions against the response area you are trying to delete. If this is the case, the popup message will contain the relevant information. 

See more information about analytics against deleted response areas in [Analytics](../../../../guides/analytics)

### Edit Response Area

The user can edit any response area attributes without any restrictions except changing the input type (see below).

### Changing the input type

It is possible to change the input type (e.g. from Text to Number), but only until the question is saved (with or without publishing to students).

The reason for this restriction is compatibility with student submissions (as explained in the following example). 

#### An Example of a Prohibited Scenario

- A question with input type *Number* is created and it is saved without publishing to students
- The input type is changed to *Table* (if the restriction were not in place) and is saved and published to students
- Students submit their answer (in *Table* format)
- The teacher reverts the question to the previous version with response area Number

 => The submissions are in format Table, while the response area is Number, therefore the data are incompatible.

#### Workaround

Instead of changing the input type, it is possible to duplicate the response area and then delete the orignal one. This approach ensures that data associated with the different input types remain separate.

The data for the new response area will be independent of the old one - the old one will only exist in a previously saved version of the question.

