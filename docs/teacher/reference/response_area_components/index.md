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

The user can edit any response area attributes without any restrictions except switching the Response Area (see below).

### Switching Response Area

It is possible to switch the response area (e.g. from Text to Number), but only until the question is saved (with or without publishing to students).

#### Restriction

The reason for this restriction is compatibility with student submissions (as explained in the following example). 

#### An Example of a Prohibited Scenario

- A question with response area Number is created and it is saved without publishing to students
- The response area is changed to Table (if the restriction would not be in place) and it is saved with publishing to students
- Students submit their answer (in table format)
- The teacher reverts the question to the previous version with response area Number

 => The submissions are in format Table, while the response area is Number, therefore they are incompatible.

#### Workaround

Instead of changing the response area, it is possible to duplicate it and then delete the orignal one.

However, the existing submissions and statistic will not be linked to the newly created response area, they will remain linked to the "deleted" response area (the response area still exists on the previous version of the question).

