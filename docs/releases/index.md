## Release 2024/10/09

- **b486-cloning-parts-in-wrong-order** - corrected the part order in cloned module instances and updated code to ensure future clones maintain correct part order.

## Release 2024/10/07


- **b220-download-one-student-progress** - download an individual student’s progress in CSV format.
- **b471-admin-teacher-enrolment-should-accept-comma-separated-lists** - admin enrolment of teachers accepts comma-separated lists, allowing multiple teachers to be added at once.
- **b478-question-not-visible-in-tablet-mode-when-canvas-closed** - fix: question was not visible in tablet mode when the canvas was closed.
- **b480-draw-mode-proceed-button-almost-invisible-update-to-match-the-design-on-scan-mode** - EXPRESSION response area: added the “Proceed” button in draw mode to match the design on scan mode.


## Release 2024/10/04

- **b218-teacher-view-modules-students-explore-do-not-limit-next** - teacher view of student progress: “Next” button progresses to all students, not just those listed on the current table page.
- **b448-question-jumps-to-top-on-mark-as-done** - UI fix: resolved issue where marking student submissions as done caused the page to jump to the top.
- **b466-limit-number-of-student-submissions** - eval functions receive the number of student submissions per response area, and can optionally limit submissions e.g. to external services.
- **b467-correct-separatefeedbacks-to-separatefeedback** - schema correction: `separatefeedbacks` to `separatefeedback` (relates to the 'Augment feedback based on correctness' functionality.)
- **b475-set-all-augment-booleans-to-false-in-a-specific-module** - Set all "Augment feedback based on correctness" booleans to `false` for a selected math module.

