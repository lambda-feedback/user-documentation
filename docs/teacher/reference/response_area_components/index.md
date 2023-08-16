# Response Area Components

These are what the user interacts with on the front-end. As React components, they admit a certain number of parameters which are described in this section.

## Response Area User Interactions

The user can add, delete, edit or switch response area.

### Add Response Area

The user can add a response area without any restrictions.

### Duplicate

The user can duplicate the response area within the same part using the duplicate icon. When a response area is duplicated, then only data entered in the teacher edit mode are copied (such as input type, evaluation function, input symbols, pre and post text, answer, tests, cases, ...). Data entered in the teacher preview mode (such as comments) and student mode (comments, flags, likes, student solutions, ...) are not copied.

### Reorder

It is possible to reorder response areas within the part using the "drag and drop" feature. It works in the same way a reordering of parts:

Move your mouse cursor over the response are you want to move. Then, press and hold down the left mouse button, move the object to the location you desire, and release the mouse button to set it down.

### Delete Response Area

The user can delete a response area without any restrictions. A popup message appears to confirm the deletion.

However, it is important to remember that there might be submissions against the response area you are trying to delete. If this is the case, the popup message will contain the relevant information.

See more information about analytics against deleted response areas in [Analytics](../../guides/analytics)

### Edit Response Area

The user can edit any response area attributes without any restrictions except changing the input type (see below).

### Changing the input type

It is possible to change the input type (e.g. from Text to Number), but only until the question is saved (with or without publishing to students).

The reason for this restriction is compatibility with student submissions (as explained in the following example).

#### An Example of a Prohibited Scenario

- A question with input type _Number_ is created and it is saved without publishing to students
- The input type is changed to _Table_ (if the restriction were not in place) and is saved and published to students
- Students submit their answer (in _Table_ format)
- The teacher reverts the question to the previous version with response area Number

=> The submissions are in format Table, while the response area is Number, therefore the data are incompatible.

#### Workaround

Instead of changing the input type, it is possible to duplicate the response area and then delete the orignal one. This approach ensures that data associated with the different input types remain separate.

The data for the new response area will be independent of the old one - the old one will only exist in a previously saved version of the question.
