# Response Area Components

Response Areas are the interactive elements your students will use to submit their answers. They check an input given by the student, and provide feedback. As React components, they admit a certain number of parameters which are described in this section.

![Screenshot](screenshots/Responsearea.png)

## Response Area creation

Response areas are added to the question field, and are configured for each question in the set.

### Add Response Area

You can add any number of response areas to a question part. These may be separated by text fields. If desired, adding a double space in the field will space out response areas.

### Duplicate

You can duplicate the response area within the same part by clicking on the duplicate icon.

*   **What gets copied:** All teacher-configured settings are duplicated. This includes the input type, evaluation function, pre/post text, the correct answer, tests, and any feedback cases you've set up.
*   **What is NOT copied:** Any data generated during use is not carried over. This includes comments, flags, likes, and student submissions.

### Reorder

It is possible to reorder response areas within the part using the "drag and drop" feature. It works in the same way as reordering parts.

### Delete Response Area

You can delete a response area without any restrictions. A pop-up message appears to confirm the deletion.

If students have already submitted answers to the response area you are deleting, the confirmation message will warn you.

See more information about analytics for deleted response areas in [Analytics](../../guides/analytics)

## Response Area configuration

To configure a response area, click the configure button: 

![conifgure button](../images/configure.png)

This opens the **Response Area Panel**, separated into four tabs:

1.  **Input:** Define what the student sees and how they answer.
2.  **Evaluate:** Set up the logic for how the answer is checked.
3.  **Feedback:** Create customised feedback for different correct or incorrect answers.
4.  **Test:** Define correct and incorrect answers to test your configuration to ensure it works as expected.

### 1. Input
![Screenshot](screenshots/Inputfield.png)

- Select an input style for the student by scrolling or filtering. These consist of the following:
    - Matrix
    - Number
    - Boolean (true/false)
    - Text (for short text answers)
    - Table
    - Multiple-choice
    - Expression (gives a preview for the typed symbolic expression)
    - Numeric units (separate fields for a number and its units)
    - Code
    - Essay (for long text answers)
    - Milkdown

Each input type has suitable evaluation functions. Try to choose the most suitable input style for your desired answer. See the subpages for more detailed information about each input type.

- **Configuration Options**

    - **Enable live preview**: Renders the typed expression in realtime. Allows to validate student input before submitting. `Default: TRUE` for the EXPRESSION input type.
    - **Display input symbols**: Displays the symbols and associated shortcut codes that may be required for a problem beneath the input field. These are configured in the 'Evaluate' tab. `Default: FALSE`.
    - **Include in PDF**: Only affects the PDF version. Includes pre/post response text in the PDF, with a blank space between. `Default: FALSE` except for Multiple-choice.
    - **Pre/post response text** (optional): Add text before and after the response area to clarify to students what to input. Accepts plain text, and single-dollar-delimited latex. E.g. `Estimate $f(x)=$` is acceptable. When using fractions in this field, use `$\dfrac{}{}$` as this is more legible.
    - **Response Area Answer**: Enter a reference answer. This will typically be the absolute solution to a problem. When requesting a symbolic answer, you must use the variable names (codes) you define in the 'Evaluate' tab.  Configure the answer where relevant (e.g. number of rows and columns).
    - **Response Area Preview**: Shows you what the configured response area will look like.
  
### 2. EVALUATE

Configure how student expressions are evaluated.

This is a 'no code' parametric configuration. Settings will be upgraded as the system improves.

- **[Evaluation Function](https://lambda-feedback.github.io/user-documentation/teacher/reference/evaluation_functions/)** - Select an evaluation function from the list. For example:
    - `isSimilar`: Best for numerical answers. It performs a basic comparison, allowing for a configurable tolerance (absolute and relative).
    - `compareExpressions`: Best for symbolic answers (e.g., equations).
- **Evaluation Function Parameters** - Configure as provided, and add new parameters as required. Details depend on the selected Evaluation Function.
-   **Input Symbols:** This is a powerful feature for defining a dictionary of accepted symbols. For each symbol, you define:
    *   **Symbol:** The LaTeX-rendered symbol (e.g., `$f(x)$`).
    *   **Code:** The machine-readable variable name (e.g., `fx`). This is what your students will type and what the evaluation function sees.
    *   **Alternatives:** A list of other codes you want to accept for the same symbol (e.g., `f_x`, `f(x)`, `f`). This allows you to anticipate different ways students might type the same thing.
    *   **Visibility:** A `TRUE`/`FALSE` toggle. If "Display input symbols" is enabled in the Input tab, this setting determines whether a specific symbol is shown to the student. This allows you to show students common symbols while still accepting less common or alternative ones in the background.

### 3. FEEDBACK

Here, you can go beyond a simple "correct/incorrect" and provide nuanced feedback by creating **"cases."**

Cases are an alternative answer you want to check for. You can use cases to:

*   Award full marks for a different but equally valid answer.
*   Identify a common mistake and provide specific, tailored feedback to help the student learn.

For each case, you can:

*   Enter an alternative answer to check for.
*   Specify if the case should be marked as "correct" or "incorrect."
*   Write custom feedback text that overrides the default feedback from the evaluation function.
*   Change the color of the feedback (e.g., green for correct, orange for a hint).

Teachers typically add cases after students start submitting answers, and data about common student answers is created.

When a student submits a response, it's evaluated against all cases. The system displays feedback for the **first case that matches**. The main answer you set in the 'Input' tab is treated as "Case 0" and is always checked first.

Feedback fields also support LaTeX equations in both `$f(x)$` and `$$f(x)$$` formats, and Markdown inputs such as line breaks. Make sure to follow good typesetting practice in this field.

![Screenshot](screenshots/Feedback.gif)

### 4. TEST

Tests provide a systematic way to log what behaviour the teacher expects. You can create a list of test inputs and define the expected outcome for each.

It provides a useful record and an efficient way to retest the bevhaiour of a response area over time (e.g. as evaluation functions evolve, or as the subject matter itself changes).

## Restrictions on changing the input type

It is possible to change the input type (e.g. from _Text_ to _Number_) without any restrictions until the response area is saved.

After the response area is saved, it is still possible to change the input type, but it will result into replacing the response area by a new one. The previous response area will still exist, but only on the previous version of the question. When replacing the response area, all content (e.g. answers, feedback cases) is preserved, but any existing student submissions and analytics will remain linked only to the previous response area.

Student answers, click events and statistics are never lost by deleting a response area. Once a question is saved (with or without publishing), then any new changes are saved into a new (draft) version of the question. So, if e.g. a response area is deleted after a question was published, then it is deleted from the draft version only. And if this draft version is later published, then the previously published version is preserved (and with it the "deleted" response area and linked submissions).

The reason why the input type change is restricted is to preserve high quality data analytics as explained in the examples below.

### Example 1 - changing input type on PUBLISHED response area

1.  **Create and Publish:** You create a question with "Response Area 1" and "Response Area 2," both using the *Number* input type. You **Publish** the question. Let's call this `Version 1`.
2.  **Students Submit Answers:** Students begin submitting answers, which are recorded for both response areas.
3.  **Edit the Question:** You decide to edit the question. The system automatically creates a new draft, `Version 2`.
4.  **Make Changes:**
    *   In "Response Area 1," you add a new input symbol. This is a simple change and doesn't affect the input type.
    *   In "Response Area 2," you change the input type from *Number* to *Table*.
5.  **The Result:** Because `Version 1` was published, changing the input type triggers the replacement process. The original "Response Area 2" is archived (with its student data) in `Version 1`. A brand new "Response Area 3" (with the *Table* input type) is created in its place in `Version 2`.
6.  **Publish Again:** You publish `Version 2`.

**The Takeaway:**

*   New student submissions will be recorded for "Response Area 1" (*Number*) and "Response Area 3" (*Table*).
*   The original submissions to "Response Area 2" are safe and preserved with `Version 1`, but you won't see them in the analytics for the currently published `Version 2`.
*   If you later **Revert** to `Version 1`, you will once again see the analytics for "Response Area 1" and the original "Response Area 2".

**Please note:** All statistics and submissions are currently displayed against the published question version only. So, though the submissions against "Response Area 2" are preserved, it is not currently possible to see them. We are working on the improvement to make this possible.

### Example 2 - changing input type on SAVED response area

This scenario works almost identically to the one above. The key is that once a question version is **Saved**, the input types of its response areas are locked to protect potential future analytics. If you edit a saved question and change an input type, it will still trigger the replacement process (archiving the old and creating a new response area).

### Example 3 - adding new response area to a published question

1.  **Start with a Published Question:** You have a published question (`Version 1`) with "Response Area 1" and "Response Area 2."
2.  **Edit the Question:** You start editing, which creates a new draft (`Version 2`).
3.  **Add a New Response Area:** You add "Response Area 3."

**The State of `Version 2` (Draft):**

*   The input types for "Response Area 1" and "Response Area 2" are **locked**. This is because they exist on a previously saved version (`Version 1`). To change their type, you must go through the replacement process described above.
*   The input type for the new "Response Area 3" is **unlocked**. You can change it freely because it doesn't exist on any previously saved version and has no associated student data to protect. It will only become locked after you Save or Publish `Version 2`.

