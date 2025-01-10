## Release 2025/01/10

- **b584-PDF-tables** - ensure tables compile in PDFs

## Release 2025/01/09

- **b75-add-labels-to-users-to-allow-filtering-in-analytics-examples-of-useful-labels-guest-msc-group2-personaltutor-etc-user-type** - added none option to the student filter

## Release 2025/01/08

- **b75-add-labels-to-users-to-allow-filtering-in-analytics-examples-of-useful-labels-guest-msc-group2-personaltutor-etc-user-type** - implemented student admin categories and student module tags  
- **b562-single-multiple-choice-toggle-not-clear** - tidied up multiple choice toggle in the response area configuration panel

## Release 2024/12/12

- **b563-misc-frontend-changes** - Small client-side setup improvements

## Release 2024/12/06

- **b556-Solutions-PDF---Lambda-step-error** - PDF generator in backend - fix inline LaTeX (only in structured tutorial/final answer/worked solutions)

## Release 2024/12/09

- **b440-notifications-in-ui** - add notifications feed for teachers

## Release 2024/12/06

- **b556-Solutions-PDF---Lambda-step-error** - fix to PDF generator Lambda to handle steps (e.g. in worked solutions)

## Release 2024/12/02

- **b533-teacher-header-eager-auth** - Prevent header/wrapper requests to module without a user
- **fix-week-bounds** - Fix weekly recap bounds including Sunday

## Release 2024/11/29

- **b460-ui-tweaks-iii** - additional tweaks to the user interface
- **b541-module-cloning-should-copy-over-support-material-settings** - module cloning carries over settings for visibility of structured tutorials, final answers, and worked solutions.

## Release 2024/11/25

- **b533-firebase-auth-idtoken-is-required** - no change to UX. Fixed issue "Error: idToken is required" caused by a premature query before the token was available
- **b537-a-gap-between-title-and-list-of-modules** - fix: remove unintended gap between the page title and content when the canvas feature was opened

## Release 2024/11/23
- **b544-eval-function-schema-403** - evaluation functions base layer: schema included to avoid 403 errors when retrieving

## Release 2024/11/20

- **b526-studentgetmodules-query-is-slow** - optimized data retrieval, sorting, and filtering for the student modules page

## Release 2024/11/15

- **b463-save-button-for-all-response-types** - save button to save work before submission. Configurable per response type at ADMIN level, and per response area at TEACHER.
- **b468-email-updates-settings** - introduced an admin feature allowing changes to the recap schedule setting for each teacher
- **b503-the-list-of-errors-and-flags-in-teacher-view-to-contain-info-about-the-part** - enhanced the teacher view by including details about which part each flag and error was created against
- **b527-numericunits-displays-answers-incorrectly-in-the-configure-panel** - resolved an issue with numeric units that previously displayed incorrectly when spaces were present
- **b528-upgrade-next-from-1423-to-1424** - updated Next.js library
- **b529-update-branches-info-in-readmemd** - updated the README.md to provide developers with the latest information about the ticket board and testing processes


## Release 2024/11/13

- **b506-add-authentication-with-google** - replaced MSAL (Microsoft Authentication Library) with Firebase Authentication to allow sign-in using both Microsoft and Google accounts

## Release 2024/10/31

- **b465-do-not-remove-whitespace-from-input-symbols** - fix: remove spaces from input symbols only at the beginning and end, preserving spaces in the middle
- **b477-set-json-generation-returns-403-if-a-media-is-not-accessible** - improvement: PDF generation now returns a clearer error message when media fails to download
- **b507-module-options-edit-does-not-work-correctly** - fix: refresh module options in the teacher view after they are updated
- **b511-publish-whole-set-questions-missing-from-list** - fix: ensure the list of unchanged questions in information messages displays all relevant questions
- **b512-add-eslint-rules-for-imports** - improvement: adjusted import order in code for better readability and logical structure
- **b513-open-link-choices-for-tab-columns-with-links** - enhancement: added “open link” options to table columns containing hyperlinks, improving navigation across tables
- **b514-pdf-generation-pandoc-exited-with-code-43-fontconfig-error-no-writable-cache-directories** - adjustment: modified PDF generation to redirect Fontconfig logs to writable directories within the Lambda function

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

