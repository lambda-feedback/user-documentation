# Response Area Components

These are what the user interacts with on the front-end. As React components, they admit a certain number of parameters which are described in this section.

## Response Area creation

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

- Select an input style for the student by scrolling or filtering. Most needs are met by 'MCQ', 'NUMERIC' and 'EXPRESSION'.
- INPUT: configure the _Student facing_ options for the input:
  - Enable live preview. Default TRUE for the EXPRESSION input type, to validate student input before submitting for feedback.
  - Display input symbols. Default FALSE. Enable it to give students guidance on how to express themselves. Teachers configure the input symbols in the 'Evaluate' tab
  - Include in PDF. Default FALSE except for MCQ. Only affects the PDF version. Includes pre/post response text in the PDF, with a blank space between.
  - Pre/post response text (optional). To clarify to students what to input in the response area. Accepts plain text, including single-dollar-delimited latex. E.g. `Estimate $f(x)=$` is acceptable.
  - Answer. Enter a reference answer. Configure the answer where relevant (e.g. number of rows and columns).
  - Response Area Preview: for teachers to verify the configuration
- EVALUATE: configure how student expressions are evaluated. This is a 'no code' parametric configuration. Settings will be upgraded as the system improves.

  - [Evaluation Function](https://lambda-feedback.github.io/user-documentation/teacher/reference/evaluation_functions/) - select from the list.
  - Parameters - configure as provided, and add new parameters as required. Details depend on the Evaluation Function.
  - Input symbols - define a dictionary of symbols and their equialevnt in code form. These symbols are used even if they are not displayed to students. All inputs are plain text. For example, the symbol `$f(x)$` may have code `fx` and alternatives `f_x`, `f(x)`, `f`. This dictionary will be provided to the evaluation function, even if the teacher has not displayed it to the student. Input Symbols allows teachers to pickup on multiple acceptable ways to express concepts, including less-rigorous methods that are not encouraged but will still be dealt with as well as possible. The configuration of input symbols is a very important part of providing high quality feedback. Note that the 'visibility' Boolean applies if input symbols are displayed to students, otherwise it is irrelevant. It allows Teachers to communicate some symbols to students, while keeping others hidden but still effective.

- FEEDBACK: add 'cases'. Each case is an alternative reference answer, with customised parameters, so that multiple cases can be dealt with independently. Cases can be used to capture multiple correct approaches that are not equivalent. Cases can also be used to identify common incorrect approaches and to provide customised feedback. The FEEDBACK tab is typically populated after students start using the system, and when data is available to point to common expressions. Configuring a case works similarly to setting up the default answer in the INPUT tab, with added options for changing the colour of the given feedback, give costum feedback and toggling whether the case answer should be considered correct or not. Adding costum feedback will overwrite the feedback produced by the evaluation function. The exceptiong When a response is submitted it is evaluated for all cases and feedback for the first case that matches will be displayed. When determining which matched case is first, the default answer described in the INPUT tab will take precedence over all other cases, otherwise the feedback for the matched case with the lowest number will be displayed (i.e. the answer given in the INPUT tab can be considered to be Case 0).

- TESTS: tests provide a systematic way to log what behaviour the teacher expects. It provides a useful record and an efficient way to retest the bevhaiour of a response area over time (e.g. as evaluation functions evolve, or as the subject matter itself changes).

## Restrictions on changes: the input type

It is possible to change the input type (e.g. from _Text_ to _Number_) without any restrictions until the first version of the question is saved or published to students.

After the response area is saved or published to students, it is still possible to change the input type, but it will result into replacing the response area by a new one. The previous response area will still exist, but only on the previous version of the question. When replacing the response area, all response area content data (those entered by teachers including tutorials, final answer and worked solutions) are copied, but any existing response area event data (student answers, click events and statistics) will remain linked only to the previous response area.

The reason for this restriction is to preserve high quality data analytics as explained in the example below.

### An Example of an input type change on published response area

- A question with input type _Number_ is created and it is saved without publishing to students.
- A student submits an answer in the format of a single number.
- The input type is changed (if the restriction were not in place) by the teacher to _Table_ and is saved and published to students. The format of an answer is now an array of numbers or strings.
- Students submit their answer (in _Table_ format)
- The teacher reverts the question to the previous version with response area Number

=> If the same response area would be used, then different student submissions would be in different formats (number, or Table) at different times. The data would be incompatible.

=> For this reason, if the response area has been saved or published to students, if the input type is changed, then a new response area is created and the original response area is deleted from the current version (as described above).

