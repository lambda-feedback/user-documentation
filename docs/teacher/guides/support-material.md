# Support material access configuration

Students can use the following types of support materials to help them to answer the question:

- Sructured tutorial
- Final answer
- Worked solutions

## Configuring student access

It is possible to configure the student access to the support material at the set level and also at the question level.

### Configuring student access at the set level

Open the <span style="color: red;">Edit Set Metadata</span> page by clicking on the Edit Set Metadata button in the list of sets:

![Image showing edit set metadata option](./images/edit_set_option.png)

The page contains the <span style="color: red;">Student access to support material</span> section:

![Image showing edit set page](./images/edit_set_page.png)

Access to each support material type can be set to one of the following options:

#### Open

Students can open this support material type without any restrictions. 

This is valid for all questions in the set except those for which the support material access is set to be hidden at the question level (see below).

#### Open with warnings

A warning window appears if the studen opens the content before the recommended time.

The recommended time is the <span style="color: red;">Minimum time estimate (mins)</span> which can be set on the question <span style="color: red;">Guidance</span> page:

![Guidance minimum recommended time](./images/guidance_min_time.png){ width="400" }

However, the option will be changed to **Open**, if any of the following is true:

- The student has downloaded the PDF 
- There is no minimum time estimate set for the question
- The time now minus the time the student first accessed the question is more than the minimum time estimate

This is valid for all questions in the set except those for which the support material access is set to be hidden at the question level (see below).

#### Hidden

Students cannot open any support material for any question in the set.

This is valid for all questions in the set, even those for which the support material access is set to Open at the question level (see below).

### Configuring student access at the question level

The support material access configuration at the question level is located on the  <span style="color: red;">File</span> tab:

![Image showing edit access on question level](./images/edit_question_access.png)

All support material is open by default, it can be changed:

- If the switch is **off**, then the support material is **open**
- If the switch is **on**, then the support material is **hidden**

## Summary overview

| Set level setting  | Question level setting | Result (using <span style="color: red;">Final answer</span> as an example) | Description                      |Comment                          |
| ------------------ | ---------------------- | ----------------------------------------- | -------------------------------- |-------------------------------- |
| Hidden             | N/A                    | ![Guidance minimum recommended time](./images/final_answer_hidden.png){ width="200" } | The <span style="color: red;">Final answer</span> is disabled | The setting at the question level is ignored |
| Open               | Hidden                 | ![Guidance minimum recommended time](./images/final_answer_hidden2.png){ width="200" } | The <span style="color: red;">Final answer</span> is disabled | |
| Open with warnings | Hidden                 | ![Guidance minimum recommended time](./images/final_answer_hidden2.png){ width="200" } | The <span style="color: red;">Final answer</span> is disabled | The same result as above |
| Open with warnings | Open                   | ![Guidance minimum recommended time](./images/final_answer_open.png){ width="200" } | When the <span style="color: red;">Final answer</span> is clicked, a warning message appears | Additional conditions must be met: <BR> <li>PDF not downloaded</li> <li>The minimum time estimate is set for the question</li>  <li>The time now minus the time the student first accessed the question is more than the minimum time estimate</li><BR>If any of them is not met, then the support material will be open with no warnings. |