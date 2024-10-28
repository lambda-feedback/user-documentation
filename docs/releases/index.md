## Release 2024/10/28

- **473-middle-click-cmdclick-on-links-in-mui-tables** - added “open link” options to table columns with hyperlinks
- **488-links-on-module-home-page** - enhanced cards on the teacher module home page to allow clicks that navigate to relevant tabs
- **499-switching-to-canvas-resets-to-part-a** - prevented reset to part A when opening or closing the canvas

## Release 2024/10/23

- **b498-feedback-does-not-handle-double-dollars** - feedback string display offers basic support for double-dollars. (REVERTED)
- **b505-enable-weekly-recap-by-default-for-new-users** - email notifications tweaks for new users


## Release 2024/10/18

- **b493-one-student-progress-csv-format-change** - adjustment to the CSV format of an individual student’s progress
- **b495-augment-feedback-colour** - updated augment feedback functionality
- **b481-cannot-switch-page-in-the-error-panel-in-the-admin-dashboard** - fix: allowing multiple tables on one page with paging functionality

## Release 2024/10/17

- **b497-milkdown-response-area** - milkdown response area type added

## Release 2024/10/16

- **b482-question-scrolls-up-when-clicking-check-or-mark-as-done-on-mobile-and-tablet** - fix: resolved issue where marking student submissions as done caused the page to scroll to the top on mobiles and tablets.
- **b483-feedback-area-does-not-support-latex-rendering-again** - adjustment to the feedback to support latex
- **b490-dashboard-high-no-of-students** - improved the dashboard’s calculation of the current number of students.
- **b494-augment-feedback-if-the-augment-is-true-and-the-returned-feedback-is-empty** - updated the augment feedback functionality to handle cases where the augment flag is true, but the returned feedback is empty.
- **b496-feedback-to-handle-html-and-latex** - adjustment to the feedback to support html alongside latex

## Release 2024/10/15

- **b461-bulk-rollover-follow-up-ii** - updates to bulk rollover feature
- **b479-scan-in-mobile-tablet-doesnt-activate-camera-or-file-selector** - fix: camera did not activate in mobile or tablet when using scan option


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

