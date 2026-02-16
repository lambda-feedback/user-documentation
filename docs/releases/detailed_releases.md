## Release 2026/02/16

- **b901-teacher-role-permissions-to-activities-and-errors** – Aligned Activities and Errors visibility with the resolved user-access policy. Student row visibility and email masking now consistently follow View Student Data rules across both features, including correct handling of mixed Teacher and Tutor roles.
- **b962-restrict-stats-in-module-student-view** – Introduced a separate View Student Stats permission to ensure consistent and explicit control of student-level statistics visibility.
- **b966-closed-modules-not-visible** – Fixed client-side filtering so closed module instances are correctly hidden or shown according to the "Hide finished modules" toggle, with the default behaviour hiding finished modules for new users.
- **b968-add-user-access-documentation-for-student-stats-and-activity-permissions** – Updated User Access technical documentation to reflect the clarified teacher and tutor permissions for Activities, Errors, and student-level statistics.

## Release 2026/02/10

- **b445-pandoc-error-latex-followed-by-a-number** – Improved PDF generation robustness when LaTeX expressions are immediately followed by numbers. 
- **b956-case-insensitive-email-address-on-enrolment** – Normalised email address handling during enrolment.

## Release 2026/01/30

- **b909-stats-displayed-without-permission** - Ensured student progress statistics are displayed only when the user has the View Stats permission. Statistics are now returned only for students the user is authorised to view, including correct handling of tutor-only access.
- **b951-images-response-area** - Added a new Images response area type, allowing students to submit image-based responses and enabling teachers to view and assess image submissions consistently with other response areas.
- **b953-null-responseconfig-api-error** – Prevented GraphQL errors when response configuration is absent by aligning schema nullability.
- **b954-dont-fetch-stats-without-access** – Prevented stats queries from being issued when the teacher role does not grant access to set statistics, avoiding unnecessary backend errors.

## Release 2026/01/16

- **b889-make-the-displayed-numbers-when-importing-students-less-confusing** – Improved student import header mapping by making system column identifiers visually secondary.
- **b909-stats-displayed-without-permission** – Fixed stats being shown without permission by enforcing VIEW STATS access in the Students table.
- **b915-header-for-personal-tutors** – Fixed module header so personal tutors see the correct module title instead of the “TEACHER” label.
- **b930-navigation-to-empty-student-details-page-in-teacher-view** – Fixed navigation to student details so persisted filters do not lead to an empty or incorrect view.
- **b932-api-retrieves-all-students-not-filtered-by-teacher-permissions** – Fixed student filtering so teachers and tutors only see students they are authorised to view.
- **b934-admin-modules-filter-module-name-replaced-by-module-id-after-returning-to-page** – Fixed Admin -> Modules filter to restore module names instead of internal IDs when returning to the page.
- **b940-filter-teacher-modules-students-does-not-remember-sets** – Fixed set-based filters not being restored in the Teacher -> Module -> Students view when navigation away and back.

## Release 2026/01/13

- **b937-meq-likert-scale** – Added Likert scale visualisation for MEQ stats and improved N/A handling.
- **b944-meq-stats-fixes** – Improved MEQ statistics access control, evaluated teacher selection, and various minor changes.

## Release 2026/01/07

- **b943-meq-explore-button-throws-error** – Fixed an issue where the Explore page could throw an error for MEQ submissions with empty responses.

## Release 2026/01/06

- **b808-meq-stats-page** - Improved MEQ statistics visibility, filtering, and access control, ensuring teachers and moderators see only appropriate, recent, and sufficiently populated data.
- **b919-meq-moderation-improvements** - Improved MEQ moderation by excluding empty submissions, consolidating identical responses, showing only the latest submissions, and refining moderation navigation.

## Release 2025/12/19

- **931-chat-cursor-fix** - Keep the chat input focused after sending a message
- **b936-numeric-units-ra-type-cannot-be-cleared** - Fix bug preventing NUMERIC_UNITS response type to clear
- **b933-numeric-and-numericalunits-allow-empty-student-response** - Fix a bug that allowed empty submission on BOOLEAN, ESSAY, NUMBER, NUMERIC_UNITS and  TEXT response types.

## Release 2025/12/16 bis

- **b935-login-fails-when-email-address-changes** - Fix login for Microsoft users after they've changed their email address.

## Release 2025/12/16

- **b547-chat-ui-tweaks** - Improved chat interface behaviour, including correct tab selection when switching questions, immediate display of user messages, updated styling, and a new typing animation.
- **b890-admin-chat-statistics-tweaks** - Simplified the Admin Chat Statistics page by replacing descriptive sentences with concise table headings and labels.

## Release 2025/12/11

- **b923-cannot-assign-moderator-role-to-a-new-teacher-in-admin** - Allow admin to assign moderator roles
- **b926-handle-null-submission-on-teacher-errors** - Show errors with empty submittions
- **927-meq-discard-confirmation** - Ask for confirmation when navigating away from a filled but not submitted MEQ

## Release 2025/12/05

- **b916-meq-tweaks-batch-5** - Minor MEQ UI tweaks: tab and title layout; green ticks on tabs.

## Release 2025/12/01

- **b917-meq-release** - Make MEQs visible on students' home page

## Release 2025/11/27

- **b912-meq-batch-import** - Added modules batch import features for MEQ launch.
- **b914-meq-tweaks-batch-4** - Minor wording and layout changes for MEQ sets.

## Release 2025/11/26

- **b830-remember-search-and-filter-settings-across-the-app** - Added support for remembering search and filter settings across the app during a session.
- **b877-meq-evaluated-teachers-list** - Added the ability to configure which teachers are evaluated in each MEQ set, including a new “repeat statements for each teacher” option and several small usability improvements.
- **b878-meq-likert-updates** - Improved the Likert question type with editable columns, clearer submission behaviour for surveys, and several small usability and layout fixes.
- **b895-set-name-edit-issues** - Fixed issues with editing set names, including unwanted navigation when opening the dialog and repositioning the edit icon next to the title.
- **b898-meq-tweaks-batch-1** - Improved the MEQ sets page with corrected headers, refreshed layouts and styling (including icons, alignment, and backgrounds), and ensured the student module list always reloads correctly.
- **b906-meq-tweaks-batch-2** - Improved the MEQ experience with smoother global submission, clearer messages and titles, support for empty Likert responses, a ‘Next MEQ’ button, and better handling of redacted content.
- **b908-meq-layout-fix** - Fixed a layout issue that caused a double-scroll effect after adding the sets navigation bar.
- **b910-meq-tweaks-batch-3** - Improved the MEQ moderation table and mobile experience, including clearer question numbering, consistent approve/reject buttons, visible essay inputs on mobile, and correct handling of draw mode.

## Release 2025/11/20

- **b845-add-filter-to-global-tags-multi-widget** – Added a search feature to the global tags multi-select widget, making it easier to find tags quickly.
- **b875-meq-student-home-page-links** – Added links to Module Evaluation Questionnaires (MEQs) on the student home page.
- **b876-meq-set-navigation** – Renamed “Surveys” to Module Evaluation Questionnaires (MEQs) and improved navigation so students can easily access MEQs for all their modules.
- **b879-meq-module-stats** – Improved the statistics view so it is clear which sets are MEQ sets.
- **b880-meq-set-dates-defaults** – Added default hide and release dates for MEQs at the tenant level to simplify setup.
- **b886-student-progress-in-teacher-view-is-not-aligned-if-it-contains-stars** – Improved the alignment of progress indicators in the teacher view, including when a star (submitted solution by student) is shown.

## Release 2025/11/17

- **b849-import-tags-with-same-column-name** – Allow columns in the student-upload spreadsheet to have identical titles.
- **b864-admin-chat-statistics** – Added a new page in the admin view to preview chat usage statistics.
- **b868-set-card-items-do-not-align-on-some-cards** – Aligned items inside set cards in the teacher view so they line up.
- **b870-cant-add-links-in-lexdown-except-in-raw-markdown** – Fixed link creation in the Lexdown editor.
- **b874-making-saving-draft-message-to-appear-subtle** – Made the “saving draft” message for question versions less intrusive.
- **b882-expanded-list-of-teacher-roles-overflows-window** – Improved UI to ensure the expanded teacher-roles popup is centered.
- **b886-student-progress-in-teacher-view-is-not-aligned-if-it-contains-stars** – UI fix to ensure student progress bars remain aligned even when they contain stars.

## Release 2025/11/06

- **b871-set-number-in-mobile-view** - Fixed the display of set numbers shown as part of the question title in the mobile view.
- **b847-explore-should-be-grey-when-no-data** - Fixed the clickability of buttons in the response area in the teacher view.

## Release 2025/11/05

- **b851-empty-question-title-prevents-save** - Question title validation and error handling improvements.
- **b765-audio-record-tweaks** - Improved UI for audio recordings.
- **b839-captions-with-latex-adjustments** - Revert **b774-style-in-captions**.
- **b842-button-widths** - Teacher editor UI: response area button widths aligned.

## Release 2025/10/31

- **b853-remove-feedback-when-user-changes-answer** - Feedback disappears when user input is modified.
- **b867-sentry-disable-spans-and-replays** - Adjusted Sentry configuration to prevent a large number of alerts for the same cause.

## Release 2025/10/30

- **b860-reaction-icons-are-flashing-numbers** - Fix: numbers were briefly appearing above all reaction icons.
- **b865-teacher-preview-display-feedback-on-feedback** - Restored reactions in the teacher question preview.

## Release 2025/10/29

- **b221-overall-progress** - Display overall progress of all students to the teacher within a module.

## Release 2025/10/28

- **b854-metadata-when-cloning-questions** – Additional information when cloning from another question.
- **b856-global-tags-owner-validation-error** – Fixed validation logic for global tag ownership.
- **b863-sentry-error-variable-input-got-invalid-value** – Resolved an error reported by the automated alert system that occurred when an empty value was sent to the API.

## Release 2025/10/27

- **b539-chasing-likes** – Improved the UI for reaction icons to prevent them from disappearing before the mouse can reach them.  
- **b843-feedback-feedback** – Added reactions to response areas; students can give feedback on the feedback they receive.  
- **b846-global-tags-editing-group-emails** – Reordered fields on the Global Tag editing page for better clarity and usability.

## Release 2025/10/17

- **b814-retire-expression-ra** - Removed unused Mathpix equation endoint
- **782-branching-strategy** - New deployment workflow

## Release 2025/10/10

- **b638-any-external-chat-function** - Chatbots implemented as external microservices
- **b810-multiple-chatbots-student** - Student UI: choice of chatbot

## Release 2025/10/09

- **b827-unenroll-many-users – part 3** – Added information about the number of students to be unenroled  
- **b802-all-drop-downs-and-tables-in-correct-order** – Checked and corrected default order in drop-down lists and tables across the application  
- **b824-remove-spaces-from-module-instance-dropdown** – Module instance header drop-down UI tweak  


## Release 2025/10/08

- **b827-unenroll-many-users - part 2** – improved button labels  
- **b834-reduce-size-of-description-box-in-settings-modal** – made the description box narrower  
- **b789-admin-global-tag-pages-tweaks** – changed global tag type values to make them more explanatory  
- **b790-students-import-wizard-add-info-on-step-2** – added explanations for each column in Step 2 of the students import wizard  

## Release 2025/10/03

- **b773-export-image-captions-to-json** – included image captions in exported question JSON files  
- **b774-style-in-captions** – enabled LaTeX and Markdown support in image captions  
- **b775-image-caption-character-limit** – removed the 250-character limit on image captions  
- **b827-unenrol-many-users - part 1** – added a new feature to allow unenrolling multiple students at once in the teacher view
- **b828-display-student-stats-even-for-0-user-access** – stats graphs are now displayed even when they show *0 student accesses* (previously no graph was shown)  

## Release 2025/10/02

- **b516-set-layout-ui-upgrades** - new set layout with 2 adjustable panes
- **b740-student-nav-upgrades** - add set navigation within set for students
- **b831-teacher-nav-upgrades** - add set navigation within set for teachers
- **b826-teacher-drag-handles** - add drag handle for re-ordering response areas
- **b821-more-firebase-auth-errors-caught** - ensure usre is fully authenticated before making request to the backend

## Release 2025/10/01

- **b815-filter-tweaks-ii** - improved module filtering in the student view for closed module instances
 
## Release 2025/09/29

- **b567-instance-dropdown-tweak** – improved UI for the module instance dropdown  
- **b813-fix-question-overview-buttons-alignment** – corrected alignment of buttons on the question file tab  
- **b814-remove-expression-ra** – removed code for the legacy EXPRESSION response area  
- **b817-wrong-order-of-module-instances-in-dropdown-in-teacher-mode** – corrected the order of module instances in TEACHER mode  
- **b818-omni-input-tweaks** – tweaks to the multi-line expression response area 
- **b825-teacher-view-of-tutees** - improved ui for the student statistics in TEACHER mode

## Release 2025/09/25

- **b816-likert-response-type-mobile-view** – adjusted Likert grid to fit on mobile screens  
- **b536-optimise-student-module-list-retrieval** – optimised data retrieval for the home screen

## Release 2025/09/23

- **b777-expression-multi-line** - multi-line expression response area tweaks
- **755-rework-expression-ra** - single-line expression response area improvements
- **801-use-mathpix-app-tokens** - use Mathpix directly from the client-side

## Release 2025/09/15

- **b777-expression-multi-line** - multi-line expression response area added

## Release 2025/09/12

- **b708-filter-modules-in-teacher-view-by-teacher-roles** – improved module filtering, adding support for filtering by teacher roles and the *closed modules* flag  
- **b800-likert-response-type** – introduced the new **likert** response type for surveys

## Release 2025/09/08

- **b550-ui-tweaks-iv** – General UI improvements, mainly alignment adjustments.  
- **b783-ugly-mcq-questions-scroll-bars** – Removed unwanted scrollbars in the MCQ response area on Firefox.  
- **b798-expression-type-mode-does-not-display-feedback-correctly** – Fixed an issue where typed input in the Expression area was not parsed correctly. This was caused by earlier fixes, which have now been reverted:  
  - **b796** – Check button not reappearing after changing the answer  
  - **b787** – Discrepancy in teacher and student submission payload  
  - **b335** – Enabled expression live preview in Teacher mode  


## Release 2025/09/05

- **b796-check-button-does-not-appear-again-after-changing-the-answer** - a fix provided so that Check button reappears after the user changes his answer

## Release 2025/09/03 - part 2

- **b787-discrepancy-in-teacher-and-student-submission-payload** - fixed the submission API payload for the TEACHER mode
- **b793-non-interpretable-equation-message** - displaying correct message for typed, non-interpretable equation in TEACHER mode

## Release 2025/09/03

- **b335-enable-expression-live-preview-in-teacher-mode** - enable live preview of expressions in the TEACHER mode
- **b557-the-app-is-hanging-if-the-set-has-no-question** - improved handling of the situation when a set has no question
- **b701-create-tag-on-edit-tags-page-in-admin-mode** - added new admin pages to maintain global tags
- **b729-revisit-roles-redirect** - improved navigation to modules pages when switching from TEACHER view to STUDENT view and vice versa
- **b752-user-filter-tweaks** - UI improvement to the user filter feature
- **b756-zero-stars** - improved stars display in the generated PDF documents
- **b761-bulk-rollover-tweaks** - bulk rollover improvements
- **b762-content-formatting-help-direct-to-milkdown-page** - corrected the navigation from the content formatting help link
- **b772-types-for-global-tags** - introduced global tag types
- **b779-standard-cancel-and-save-buttons-positioned-at-the-end-of-a-page** - fixed positioning of the save and cancel buttons
- **b780-sort-the-evaluation-functions-in-the-drop-down-list-alphabetically** - sorted the evaluation function in the alphabetic order

## Release 2025/07/22

- **b516-ai-bubble-width** - Fix workspace conversation bubbles style
- **b762-content-formatting-help-direct-to-milkdown-page** - Fix content editing documentation links
- **b766-unescape-chars** - Fix characters escaping when switching from Markdown view
- **b768-ra-sandbox** - Introduce response area sandbox
- **hotfix** - Fix TLDraw crashes when using text shape

## Release 2025/07/10

- **b746-bulk-rollover-enhancements** - Converted the bulk module rollover into a backend process and added a dedicated page to monitor its progress.

## Release 2025/07/08

- **b504-canvas-pen-to-be-small-by-default** - Changed the pen to have options s,m,l and made the option s the default one.
- **b611-expression-ra-updates** - Improved the expression response area preview.
- **b727-improve-the-graph-library-dynamic-scale** - Improved the dynamic scale of the graph library.
- **b739-audio-recorder** - Improved the Lexdown to allow to record audios directly.
- **b757-chat-errors-response-time** - Improved the error handling of the chat-function.
- **b745-backup-stopped-in-prod** - Improved the db backup.

## Release 2025/07/03

- **b696-personal-tutor-students-filters-teacher** – Added a new advanced user filter to admin pages (listing admins and teachers) and to teacher pages (listing students).
- **b713-teacher-students-page-add-filter-to-see-closed-modules** – Filtered module instances to display only current ones by default on the Modules page in TEACHER mode, and added an "Include closed module instances" switch.
- **b720-allow-teachers-to-be-linked-to-global-tags-as-students** – Teachers and admins can now be linked to global tags not only as teachers but also as students.
- **b735-students-import-change-to-optional-columns** – When importing students, the *teacher email* field is now optional, and *tag name* is mandatory. The *teacher name* was removed entirely.
- **b742-allow-to-a-module-teacher-or-tutor-access-to-the-the-content-tab-unrestricted** – Removed the "Modify content" restriction from the Content tab in TEACHER mode.

## Release 2025/06/18

- **b720-allow-teachers-to-be-linked-to-global-tags-as-students** – Display both global tags (student and teacher) for **admin** and **teacher** users. Use only student global tags for **student** users.
- **b723-set-edit-icon-buttons** – Display the set visibility icons as **buttons**.

## Release 2025/06/12

- **b706-default-end-date-on-module-instances** - Made the module instance end date a required field.
- **b719-access-denied-redirect** - Improved module instance permission checks to account for both teacher and tutor roles.
- **b726-synchronise-stats-db-queries** - Synchronized the start and end dates used in module, student, and student-module access statistics. Now includes all students, regardless of their user roles.

## Release 2025/06/11

- **b710-navigate-to-explore-student-from-students-module-in-teacher-view** – Enabled navigation to the student explore page from the teacher's students page.  
- **b712-alignment-on-student-home-page** – UI alignment adjustments on the student home page.  
- **b715-admin-teachers-display-which-modules-the-teacher-is-assigned-to** – Added a new admin page showing all modules to which a teacher is assigned, either as a teacher or tutor.  
- **b718-feed-displays-different-content-when-scrolling-through-modules** – Fixed feed pagination on the teacher home page.  
- **b724-personal-tutor-imports-qa-requests** – Improved student import process.

## Release 2025/06/05

- **b588-student-current-active-session-timings** - Improved accuracy of question statistics graphs.

## Release 2025/06/04

- **b714-teacher-students-page-and-panel-ui-adjustments** - UI alignment of the Students and Modules tables on the Teachers home page.

## Release 2025/06/02

- **b668-lexdown-updates** - A set of improvements to the lexical editor implementation.
- **b705-personal-tutor-imports** - Introduction of student import, including personal tutor and global tag assignment.
- **/687-admin-teachers-add-global-tags** - Added global tags to the admin teachers page.
- **b711-overlapping-elements** - Fixed a styling issue in the guidance widget.
- **b716-lexdown-styling-tweaks** - A set of improvements to the styling of the lexical editor.
- **b717-lexdown-raw-markdown-improvements** - Improvements to raw markdown handling.

## Release 2025/05/16

- **b703-personal-tutor-tweaks** - A set of improvements to the personal tutor functionality.

## Release 2025/05/07

- **b684-access-modules-as-personal-tutor** – Added links to the modules listed in the Students panel on the teacher landing page, allowing personal tutors to access the modules.
- **b686-special-teacher-role-for-personal-tutor** – Introduced a special teacher role, "personal tutor", to configure access permissions for personal tutors.
- **b702-filter-by-global-tag-admin** – Created a new filter component to filter users by email and/or cohort. Currently added only to the admin students page for testing.
- **b707-paging-on-admin-modules-page-does-not-work** – Fixed a bug that caused pagination to not work correctly in several tables.


## Release 2025/04/28

- **b683-personal-tutor-introduction** - The teacher home page now includes a Students panel for personal tutors to view their tutor group's students and their their progress.
- **b689-allow-teacher-to-see-user-role-permissions** - Teachers can now view the permissions assigned to each teacher role.
- **b691-admin-dashboard-unique-user-logs** -  Improved metric on the admin dashboard to count unique users.

## Release 2025/04/25

- **b674-breadcrumbs-tweaks** - Updated breadcrumbs to maintain consistency across the application.
- **b682-teacher-role-type** - Admins can now view the teacher role type, and they can change the description for the "owner" role.
- **b688-allow-multiple-teachers-per-global-tag** - Global tags can now have more than one teacher assigned.
- **b695-display-an-error-if-a-content-cannot-be-displayed** - Teachers to see error if a content could not be parsed (by the Lexdown parser).

## Release 2025/04/14

- **b616-teacher-sets-list-redesign** - New look of the student list in the teacher view.

## Release 2025/04/10

- **b699-pdf-generator-inline-images** - Fixed an error that occurred when a question contained no images. This is a temporary fix, which causes non-captioned images to be left-aligned.

## Release 2025/04/04

- **b599-teacher-set-timings-statistics** - set timing statistics introduced
- **b647-fix-tab-numbers** - correct number of activities and errors on the tabs
- **b664-milkup-vertical-spacing** - ui improvements
- **b/681-teacher-landing-page** teacher landing page introduced

## Release 2025/04/02

- **b690-lexdown-legacy-content** - updated Lexdown to ensure all legacy content is correctly displayed
- **b676-user-permissions-tweaks-and-bugs** - added access restrictions to the question Stats tab, specifically limiting access to Explore and Configure functionality

## Release 2025/03/27

- **b647-fix-tab-numbers** - corrected tab to display the correct number of activities
- **b561-comments-buttons** - simplified button arrangement for posting comments
- **b680-lexdown-insert-image-triggers-submit-event** - updated Lexical text editor implementation to prevent incorrect triggering of submit events
- **b650-reactions-scroll-under-tabs-in-teacher-edit-mode** - improved UI so that reaction and flag icons scroll under the top panel instead of over it
- **b599-teacher-set-timings-statistics** - added a graph to show statistics on how students access and work on sets

## Release 2025/03/24

- **b531-teacher-modules-page-table-filtering-and-sorting** - improved sorting of the module list in the teacher view
- **b642-update-manually-hidden-in-sets-page-immediately-after-updating-in-settings** - fixed the issue with the "manually hidden" switch not updating immediately
- **b649-chatbot-message-reactions** - introduced reactions and flagging features to allow students to comment on chatbot responses
- **b657-breadcrumbs-should-show-module-name** - added module name to the breadcrumbs
- **b671-admin-chat-flags-page** - added a new admin page to view student flags on chatbot responses
- **b660-global-tag-attributes** - added teacher email address as an attribute to the global tag to link the global tag with the corresponding teacher

## Release 2025/03/14

- **b655-small-chat-improvements** - Minor chat enhancements, primarily focused on providing suggestions.
- **b663-milkup-editor-improvements-ii** - Text editor tweaks.
- **b659-style-of-chats-to-match-the-lexical-text-editor** - Updated chat styling.

## Release 2025/03/11

- **b658-milkup-editor-improvements-i** - Text editor upgrades, including handling tables, centering images in PDFs, handling modals, and improving step-by-step display in worked solutions and tutorials.

## Release 2025/03/05

- **b652-introducing-milkup-editor** - Implemented a new Milkup editor (a Lexical-based editor with extensions developed by a student group) to replace the existing Milkdown editor.
- **b627-add-a-switch-for-text-editors** - Introduced switch to activate either Mildown editor or Milkup editor.

## Release 2025/02/25

- **b373-show-number-of-unresolved-activities-on-tab-header** - numbers added to tabs in TEACHER mode.
- **b645-fix-question-version-duplicate-statistics** - Fixed statistics to avoid duplicate counting.
- **b634-teacher-modules-progress-bar-tooltip-fix** - Removed module IDs from the progress bar tooltip.
- **b601-stats-switch-to-edit** - New switch in TEACHER mode from response area stats to edit.
- **b635-chat-improvements-more-question-info** - Additional question data provided to chatbots.
- **b630-stats-not-refreshed-after-enrolling-or-deleting-a-student** - stats refreshed immediatley when a student is added/removed to/from the module.

## Release 2025/02/19

- **631-chat-welcome-message-for-new-conversations** - Added a welcome message for students using the chatbot feature for the first time.

## Release 2025/02/13

- **b574-teacher-roles** - Introduced teacher roles to manage permissions and access levels.
- **b583-student-view-should-be-the-same-for-teacher-and-admin** - Admin users now have the same view in student mode as teachers.
- **b624-teacher-modules-stats-performances** - Improved performance when retrieving data for statistics and graphs in teacher modules.
- **b637-chat-functions-upsert-service** - Standardised chatbot function deployment to use the same mechanism as evaluation functions.

## Release 2025/02/07

- **b600-teacher-set-ra-statistics** - Set statistics for teachers
- **b555-firefox-expression-writing-and-scanning-misaligned** - Upgraded canvas library to make sure canvas is working with Firefox
- **b568-header-no-drop-down-if-only-one-instance** - The module instance to be displayed as a text (instead of dropdown) in the header if there is only one module instance

## Release 2025/02/05

- **b559-instances-in-order** - corrected order of module instances in the header for both, teacher and student view, to be in descending chronological order
- **b598-query-for-admin-dashboard-evaluation-functions-needs-optimisation** - optiised query for evaluation function statistics in admin dashboard
- **b604-teacher-modules-stats** - Show set's activity and progress statistics on teacher's modules list page
- **b607-duplicate-notifications** - preventing email notifications to be sent twice

## Release 2025/01/29

- **b602-teacher-sets-overview-stats** - Show set's activity and progress statistics on teacher's module overview page
- **b603-teacher-sets-list-stats** - Show set's activity and progress statistics on teacher's module content page
- **b615-adjust-workspace-size-on-open** - Ensure workspace width always stays in given boundaries
- **b589-teacher-set-statistics-improvements** - various improvements to the question statistics chart


## Release 2025/01/29

- **b591-workspace-split-panes-improvements** - Reworked the workspace split panes

## Release 2025/01/23

- **b543-lost-canvas-snapshot** - improve robustness of canvas saving
- **b522-latex-edit-box-over-displayed-latex** - milkdown UI fixes

## Release 2025/01/21

- **b65-enhanced-stats** - chart added in the question STATS tab
- **b590-chat-canvas-documentation** - chatbot documentation added
- **b598-query-for-admin-dashboard-evaluation-functions-needs-optimisation - part 1** - evaluation function statistics disabled. Query will be optimised.

## Release 2025/01/15

- **b524-modular-chatbot-workspace** - new chatbot functionality
- **b540-chatbot-switches** - chatbot toggles
- **b548-chat-mcqs-information-conversion** - parse MCQ respones into a user-readable format for chatbots
- **b552-pulumi-chat-infra-dev-staging-prod**  - infrastructure for chatbots
- **b578-inconsistent-lambda-function-number-of-errors** - resolved inconsistencies in eval function error statistics


## Release 2025/01/10

- **b584-PDF-tables** - ensure tables compile in PDFs

## Release 2025/01/09

- **b75-add-labels-to-users-to-allow-filtering-in-analytics-examples-of-useful-labels-guest-msc-group2-personaltutor-etc-user-type** - added 'none' option to student filter

## Release 2025/01/08

- **b75-add-labels-to-users-to-allow-filtering-in-analytics-examples-of-useful-labels-guest-msc-group2-personaltutor-etc-user-type** - student admin categories and student module tags  
- **b562-single-multiple-choice-toggle-not-clear** - tidied up multiple choice toggle in the response area configuration panel

## Release 2024/12/12

- **b563-misc-frontend-changes** - client-side setup improvements

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

