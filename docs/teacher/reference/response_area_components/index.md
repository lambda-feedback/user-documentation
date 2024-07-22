# Response Area Components

These are what the user interacts with on the front-end. They check an input given by the student, and provide feedback. As React components, they admit a certain number of parameters which are described in this section.

![Screenshot](screenshots/Responsearea.png)

## Response Area creation

Response areas are added to the question field, and are configured for each question in the set.

### Add Response Area

The user can add any number of response areas to a question part. These may be separated by text fields. If desired, adding a double space in the field will space out response areas.

### Duplicate

The user can duplicate the response area within the same part using the duplicate icon. When a response area is duplicated, data entered in the teacher edit mode is copied (such as input type, evaluation function, input symbols, pre and post text, answer, tests, cases, ...). Data entered in the teacher preview mode (such as comments) and student mode (comments, flags, likes, student solutions, ...) is not copied.

### Reorder

It is possible to reorder response areas within the part using the "drag and drop" feature. It works in the same way a reordering of parts:

Move your mouse cursor over the response are you want to move. Then, press and hold down the left mouse button, move the object to the location you desire, and release the mouse button to set it down.

### Delete Response Area

The user can delete a response area without any restrictions. A popup message appears to confirm the deletion.

However, it is important to remember that there might be submissions against the response area you are trying to delete. If this is the case, the popup message will contain the relevant information.

See more information about analytics against deleted response areas in [Analytics](../../guides/analytics)

## Response Area configuration

The user can configure a response area using the configure button:
![conifgure button](../images/configure.png)
which opens the 'Response Area Panel'. The panel follows a workflow designed around the way a teacher thinks:

- Input
- Evaluation
- Feedback
- Tests

Each stage is in a separate tab. Teachers are recommended to be mindful of this process when creating a response area.

### Input
![Screenshot](screenshots/Inputfield.png)

- Select an input style for the student by scrolling or filtering. These consist of the following:
  - Matrix
  - Number
  - Boolean (True/false)
  - Text (Suitable for short text answers)
  - Table
  - Multiple-choice
  - Expression (Gives a preview for the typed symbolic expression)
  - Numeric units (Two fields, allowing for units to be assessed)
  - Code
  - Essay (Suitable for long text answers)
- Each field has suitable evaluation functions. For example, a simple numerical answer is best suited to number, as this supports isSimilar, while assessing an equation is best suited to the expression foeld, as this supports compareExpressions.
- Each input field may be configured with a series of options:
  - Enable live preview. Default TRUE for the EXPRESSION input type, to validate student input before submitting for feedback.
  - Display input symbols. Default FALSE. When TRUE, the symbols and associated shortcut codes that may be required for a problem are displayed beneath the input field. These are configured in the 'Evaluate' tab. 
  - Include in PDF. Default FALSE except for MCQ. Only affects the PDF version. Includes pre/post response text in the PDF, with a blank space between.
  - Pre/post response text (optional). To clarify to students what to input in the response area. Accepts plain text, including single-dollar-delimited latex. E.g. `Estimate $f(x)=$` is acceptable. When using fractions in this field, use `$\dfrac{}{}$` as this is more legible.
  - Answer. Enter a reference answer. This will typically be the absolute solution to a problem. When requesting a symbolic answer, it must be given in terms of the chosen symbol shortcuts.  Configure the answer where relevant (e.g. number of rows and columns).
  - Response Area Preview: for teachers to verify the configuration
- EVALUATE: configure how student expressions are evaluated. This is a 'no code' parametric configuration. Settings will be upgraded as the system improves.

  - [Evaluation Function](https://lambda-feedback.github.io/user-documentation/teacher/reference/evaluation_functions/) - select an evaluation function from the list. For example:
    - isSimilar will perform a basic numerical comparison between the reference answer and         student input, with a configurable level of absolute and relative uncertainty.
    - compareExpressions is typically used where a symbolic answer is requested.
  - Parameters - configure as provided, and add new parameters as required. Details depend on the Evaluation Function.
  - Input symbols - define a dictionary of symbols and their equivalent in code form. This essentially associates a LaTeX-rendered symbol with a machine-readable variable label, with the LaTeX render returned to the student through the preview. These symbols may also be hiddent to students. All inputs are plain text. For example, the symbol `$f(x)$` may have code `fx` and alternatives `f_x`, `f(x)`, `f`. This dictionary will be provided to the evaluation function, even if the teacher has not displayed it to the student. This allow teachers to accept several alternative symbols, such as those with different cases or conventional expressions. The configuration of input symbols is a very important part of providing high quality feedback. Note that the 'visibility' Boolean applies if input symbols are displayed to students, otherwise it is irrelevant. It allows Teachers to communicate some symbols to students, while keeping others hidden to the student but visible to the evaluation function.

- FEEDBACK: add 'cases'. Each case is an alternative reference answer, with customised parameters, so that multiple cases can be dealt with independently. Cases can be used to capture multiple correct approaches that are not equivalent. Cases can also be used to identify common incorrect approaches and to provide customised feedback. The FEEDBACK tab is typically populated after students start using the system, and when data is available to point to common expressions. Configuring a case works similarly to setting up the default answer in the INPUT tab, with added options for changing the colour of the given feedback, give custom feedback and toggling whether the case answer should be considered correct or not. Adding custom feedback will overwrite the feedback produced by the evaluation function. When a response is submitted, it is evaluated for all cases and feedback for the first case that matches will be displayed. When determining which matched case is first, the default answer described in the INPUT tab will take precedence over all other cases, otherwise the feedback for the matched case with the lowest number will be displayed (i.e. the answer given in the INPUT tab can be considered to be Case 0). <br> Feedback fields also support LaTeX equations in both `$f(x)$` and `$$f(x)$$` formats, and Markdown inputs such as line breaks. Make sure to follow good typesetting practice in this field.

![Screenshot](screenshots/Feedback.gif)

- TESTS: tests provide a systematic way to log what behaviour the teacher expects. It provides a useful record and an efficient way to retest the bevhaiour of a response area over time (e.g. as evaluation functions evolve, or as the subject matter itself changes).

## Restrictions on changes: the input type

It is possible to change the input type (e.g. from _Text_ to _Number_) without any restrictions until the response area is saved (with or without publishing) to students.

After the response area is saved, it is still possible to change the input type, but it will result into replacing the response area by a new one. The previous response area will still exist, but only on the previous version of the question. When replacing the response area, all response area content data (those entered by teachers including tutorials, final answer and worked solutions) are copied, but any existing response area event data (student answers, click events and statistics) will remain linked only to the previous response area.

Student answers, click events and statisticsthose data are never lost by deleting a response area, they are always preserved. Once a question is saved (with or without publishing), then any new changes are saved into a new (draft) version of the question. So, if e.g. a response area is deleted after a question was published, then it is deleted from the draft version only. And if this draft version is later published, then the previously published version is preserved (and with it the "deleted" response area and linked submissions).

The reason why the input type change is restricted is to preserve high quality data analytics as explained in the examples below.

### An Example 1 - changing input type on PUBLISHED response area

#### FIRST Part
- The teacher creates a new question with Response Areas RA1 and RA2. -> The version of the question is QV1 with status DRAFT.
- The teacher is making changes (including the change of the input type if needed). -> The changes are being saved into QV1 with no restrictions
- The teacher performs PUBLISH action (let's assume RA1 and RA2 input types are both _Number_ for this example). -> The QV1 version status is changed to PUBLISHED
- Students are submitting their answers -> submissions are recorder against Response Area RA1 and RA2 (in the single _Number_ format for both response areas)
- The teacher clicks on a question to edit it -> with the first click a new question version QV2 is created with status DRAFT
- The teacher makes following changes (which are being recorded against QV2):
    - In RA1: adds a new Input Symbol -> the change is recorded against RA1
    - In RA2: the teacher unlocks and changes the input type -> RA2 is deleted (from the question version QV2) and a new response area RA3 is created (let's assume input type _Table_ for this example)
- The teacher performs PUBLISH action -> the QV2 is published (with response area RA1 with input type _Number_ and response area RA3 with input type _Table_)
- Students are submitting their answers -> submissions are recorder against Response Area RA1 (in the single _Number_ format) and against Response Area RA3 (in the _Table_ format)

  => No submissions are lost. The original submissions (in the _Number_ format) are linked to the RA2, which is preserved on the question version QV1. New submissions (in the _table_ format) are linked to the RA3 which is recorded on the question version QV2.

**Please note:** All statistics and submissions are currently displayed against the published question version only. So, though the submissions against RA2 are preserved, it is not currently possible to see them. We are working on the improvement to make this possible.

#### SECOND Part - this is an extension of the FIRST Part
- The teacher decides to REVERT (the question created in the FIRST Part) to the question version QV1 -> a new question version QV3 is created and the content of the QV1 is copied to QV3 -> QV3 is DRAFT version which contains RA1 (input type _Number_) and RA2 (input type _Number_)
- The teacher performs PUBLISH action -> the QV3 is published and the teacher can now see submissions against RA1 and RA2, but he cannot see anymore submissions against RA3 (these are preserved against the QV2 version)


### An Example 2 - changing input type on SAVED response area

- The teacher creates a new question with Response Areas RA1 and RA2. -> The version of the question is QV1 with status DRAFT.
- The teacher is making changes (including the change of the input type if needed). -> The changes are being saved into QV1 with no restrictions
- The teacher performs SAVE action (let's assume RA1 and RA2 input types are both _Number_ for this example). -> The QV1 version status is changed to SAVED
- The teacher clicks on a question to edit it -> with the first click a new question version QV2 is created with status DRAFT
- The teacher makes following changes (which are being recorded against QV2):
    - In RA1: adds a new Input Symbol -> the change is recorded against RA1
    - In RA2: the teacher unlocks and changes the input type -> RA2 is deleted (from the question version QV2) and a new response area RA3 is created (let's assume input type _Table_ for this example)
- The teacher performs PUBLISH action -> the QV2 is published (with response area RA1 with input type _Number_ and response area RA3 with input type _Table_)
- Students are submitting their answers -> submissions are recorder against Response Area RA1 (in the single _Number_ format) and against Response Area RA3 (in the _Table_ format)
- The teacher decides to REVERT to the question version QV1 -> a new question version QV3 is created and the content of the QV1 is copied to QV3 -> QV3 is DRAFT version which contains RA1 (input type _Number_) and RA2 (input type _Number_)
- The teacher performs PUBLISH action -> the QV3 is published and the teacher can now see submissions against RA1. There are no submissions against RA2 as it has not been (until now) published. Submissions against RA3 are not visible, but they are preserved against the question version QV2.

### An Example 3 - adding new response area to a published question

- The teacher creates a new question with Response Areas RA1 and RA2. -> The version of the question is QV1 with status DRAFT.
- The teacher is making changes (including the change of the input type if needed). -> The changes are being saved into QV1 with no restrictions
- The teacher performs SAVE (or PUBLISH) action (let's assume RA1 and RA2 input types are both _Number_ for this example). -> The QV1 version status is changed to SAVE (or PUBLISHED)
- The teacher clicks on a question to edit it -> with the first click a new question version QV2 is created with status DRAFT
- The teacher adds a new response area RA3

  => At this point the teacher is making changes in the question version QV2 (DRAFT) in which:

    - The input types of RA1 and RA2 are locked, because they exist on a saved version QV1. It does not matter if QV1 is (only) saved or published or if there are  or there are not existing submissions. The reason why it is locked is that the teacher can revert into this version later after submissions are created. By locking it we are making sure that the "unlock" process will be triggered which will preserve the original response area and it will create a new response area and it will make sure that the submissions are linked to response area with compatible input type.
    - The input type of RA3 is not locked at this point, because RA3 does not (yet) exist on any saved question version.
