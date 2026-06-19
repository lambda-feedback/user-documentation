## Release 2026/06/19

- **b581-microservice-restrictions-by-module** – Added module-level availability restrictions for Evaluation Functions and Chat Functions.
- **b848-rollover-allow-chat-state** – Added rollover support for the “Allow Chatbot” setting, allowing users to retain or override the existing value when creating a new module instance.
- **b1053-meq-csvs-missing-data** – Corrected MEQ CSV export queries to ensure moderation and dashboard exports include complete response data and generate consistent column layouts.
- **b1070-change-colour-of-message-when-enrolling-student** – Updated enrolment feedback styling to display “already enrolled” messages in yellow warning notifications.


## Release 2026/06/17

- **b728-teacher-question-locking** – Prevented simultaneous editing of the same question by multiple teachers.
- **b1003-add-websocket-pub-sub** – Added WebSocket-based GraphQL subscriptions to support real-time updates across the application, including question locking and live data refreshes.
- **b1072-evaluation-function-headers** – Added secure secret and header management for Evaluation Functions using encrypted secret storage and secret references in request headers, with improved admin guidance for secret management.


## Release 2026/06/12

- **b1055-header-params-chat-functions** – Added secure secret and header management for Chat Functions, enabling authenticated integrations with external services through encrypted secret storage and secret references in request headers. Added new admin pages to manage secrets.

## Release 2026/06/08

- **b763-bulk-module-cloning-cpu-and-memory-problem** – Optimised module instance cloning to resolve CPU/memory pressure and timeout issues, including fixes to Bulk Rollover page timeouts.
- **b1047-module-options-submit** – Module options now save automatically on change; the warning about publishing existing unpublished comments has been moved from the Save button to the “Publish comments instantly” switch.
- **b1048-when-enrolling-already-enrolled-student-return-relevant-message** – Updated enrolment feedback to display counts of newly enrolled and already-enrolled students.

## Release 2026/05/29

- **b1053-meq-csvs-missing-data** – Fixed discrepancies between MEQ moderation CSV exports and in-app data.
- **b1057-analytics-db-grades-import-support-for-variable-csv-formats** – Enhanced the Analytics DB anonymisation grades import to support variable CSV formats.
- **b1058-bulk-enrol-unenrol-improve-step-3-resolved-users-ux** – Reworked Bulk Manage User Step 3 layout with a full-height “Resolved users” panel and added “select all” for global tags.
- **b1059-change-role-assignability-logic** – Updated Teacher Role assignment UI terminology (“Manually assignable” and “Who can assign”).
- **b1060-fix-user-access-to-students-tabs** – Clarified and standardised student visibility rules across Students, Activities, and Errors tabs. 
- **b1063-ra-blank-in-stats-tab** – Fixed an issue where Response Areas were not displayed in the STATS tab (showing blank instead), and standardised the width of the Explore and Configure buttons for consistent layout.
- **b1064-roles-assignability-tweaks** – Defaulted new TEACHER roles to “Manually assignable = true”. Made the disabled state clear and added a tooltip.

## Release 2026/05/11

- **b974-formalise-teacher-role-assignment-rules** – Made teacher role assignment authority explicit in the data model by adding `systemDefined`, `assignableByTeacher`, and `assignableByAdmin` metadata to TeacherRole, replacing hard-coded checks while keeping runtime permission evaluation unchanged.
- **b978-improve-ui-clarity-for-restricted-student-visibility** – Improved UI transparency in restricted access scenarios (e.g. Tutor-only or no VIEW_STUDENT_DATA) by clarifying tab counts vs visible rows, adding permission tooltips for masked emails, and replacing blank progress fields with explicit “Not visible to this user” messaging.
- **b1037-mued-adoption-for-evaluation-functions** – Added support for both Legacy and µEd evaluation functions, with switching managed via the Evaluation Function admin page.
- **b1044-inconsistent-disabled-behaviour-for-user-access-restrictions** – Standardised disabled button and tab behaviour across Module Students, Module Teachers, and module tabs to ensure consistent clickability and tooltip display under access restrictions.
- **b1050-move-bulk-manage-users-to-admin-users-page** – Moved the Bulk Manage Users entry point from Admin → Modules to Admin → Users for improved navigation consistency.
- **b1051-student-stats-visibility-and-popup-behaviour-on-student-details-page** – Resolved StudentView popup flicker when opening and navigating between students, and fixed masked email flicker (masked/unmasked flashing) on the Student Details page.
- **b1052-select-all-in-bulk-enroll-unenroll** – Added a “Select All” option to the Bulk Enrol/Unenrol module instance selection table (with clearer column titles) and improved row display to utilise available modal space.
- **b1056-wkd-solns-not-visible-in-student-mode-for-some-users** – Fixed an issue where users with the Personal Tutor role could not see worked solutions in STUDENT mode, while other teacher roles were unaffected.

---

## Release 2026/04/17

- **b969-when-enrolling-already-enrolled-person-return-relevant-message** – Improved enrolment toast messages to clearly distinguish enrol, role update, already-enrolled, mixed, and no-change outcomes.
- **b979-display-clear-message-when-student-stats-hidden-due-to-permission** – Updated student statistics messaging to clearly distinguish between “no sets available” and “statistics hidden due to permissions”.
- **b981-b472-phase-5-optional-module-instance-with-intelligent-resolution** – Enhanced the Bulk Enrol/Unenrol CSV flow to allow optional module instance values, automatically resolving single-instance modules and prompting for consistent instance selection when multiple instances exist.
- **b1009-mued-api-chat-adoption** – Adopted the muEd API for chat functions with versioned schema fetching and auto-generated backend (TypeScript) and lf_toolkit (Python) types, supporting controlled version upgrades and backwards compatibility with existing APIs.
- **b1039-introduce-permissions-tab-and-fix-tags-ui** – Added a new Permissions tab under Admin → Users (moving Teacher Roles there) and resolved UI inconsistencies in the Tags tab, including spacing, layout shift, page title alignment, and removal of redundant edit buttons.

## Release 2026/03/30

- **b982-refactor-admin-users-section** – Introduced a dedicated Tags tab under Admin -> Users, moved tag creation and import flows there, and simplified and clarified the Users page layout while preserving existing student tag assignment behaviour.
- **b1017-include-response-in-activities-csv** – Extended the Activities CSV export (Teacher → Module → Activities) to include feedback request and response data, aligning the download with the updated table columns.
- **b1024-b472-phase-3-follow-up-improve-fuzzy-matching-validation** – Refined bulk enrol CSV matching, split validation into Modules and Users steps, and improved wizard UX and layout.
- **b1025-moderator-dashboard-tweaks-ii** – Updated Moderator dashboard CSV export to include all rows (not just the current page) and all available columns, including percentage and recently added fields.
- **b1031-render-rewrite-rules-needs-updating** – Ensured Render rewrite rules are regenerated when new dynamic pages are added, preventing 404 errors on reload and incorrect routing (e.g. bulkFill path resolving to a dynamic template route).
- **b1033-remove-useless-set-event-fetch** – Removed redundant SetAccessEvent fetch that was discarding results and causing unnecessary `SetAccessEvent_setId_idx` reads.
- **b1034-broken-teacher-set-access-check** – Fixed a missing `await` in the teacher set access check that could cause the permission validation to be bypassed.
- **b1036-event-tables-date-index** – Added database indexes on createdAt for SetAccessEvent, PartAccessEvent, and ButtonEvent tables to improve performance of admin and date-based queries.

## Release 2026/03/26

- **b996-b472-phase-4-cross-module-bulk-unenrol** – Extended the Bulk Enrol wizard to support cross-module bulk unenrol for students and teachers.
- **b1008-move-bulk-fill-button-to-templates-page** – Moved the Bulk Fill entry point from ADMIN → Modules to ADMIN → Templates and updated routing to align with the templates-based workflow.

# Release 2026/03/20

- **b551-set-user-on-sentry** – Enhanced Sentry integration by attaching authenticated user ID (and backend IP where available) to error reports, improving traceability and troubleshooting across backend and frontend.
- **b749-limit-canvas-snapshot-size** – Introduced safeguards to prevent excessively large canvas snapshots from being stored, addressing rare multi‑MB snapshot payloads and protecting database storage.
- **b836-expression-response-area-bugs** – Fixed UI overlap of Scan and Import (scan/draw) buttons in the EXPRESSION response area configure panel (Test tab) following the MULTI_LINES update.
- **b992-overlap-on-meq-set-settings** – Fixed UI overlap in the MEQ Set settings modal (teacher auto-select covered by white bar) and adjusted modal positioning to ensure module and instance names remain visible.
- **b977-meq-sets-dont-clone-with-instance** – Fixed an error occurring when cloning a module instance containing MEQ sets, ensuring instances clone successfully regardless of associated MEQ data.
- **b995-b472-phase-3-bulk-enrol-by-csv-upload** – Added Phase 3 of the Bulk Enrol wizard, enabling enrolment of students or teachers onto selected module instances via CSV upload.
- **b1001-canvas-assets-store** – Externalised canvas assets (e.g. images) via TLDraw `TLAssetStore`, storing them in S3 instead of embedding data URIs in snapshots, reducing snapshot size and database load.
- **b1010-canvas-blank-auto-saves** – Fixed unintended canvas auto-upsert on open to prevent creation of empty snapshots, reducing redundant canvas records and database noise.
- **b1013-moderator-dashboard-tweaks** – Updated the Moderator dashboard by hiding scores while an MEQ is open, introducing ordering by module name then instance name, and adding percentage completion display.
- **b1015-remove-unintended-search-bar-from-module-students-page** – Removed an unintentionally introduced search bar from the Teacher → Module → Students page, restoring the intended layout (no functional filtering was previously wired).

## Release 2026/03/16

- **b632-chat-functions-admin-page-ui-services** – Introduced full ADMIN management for Chat Functions (create/edit/archive/restore) with soft-delete support (deletedAt), restricted student access to non-archived functions, a new tabbed admin UI (Functions & Statistics), dashboard summary card, and aligned Evaluation Functions admin pages to the same multi-tab structure.
- **b1011-fix-set-access-for-tutors** – Fixed an access-control issue where personal tutors in STUDENT mode could enter a module but were incorrectly denied access to its MEQ sets, aligning behaviour with student and module-owner access expectations.

## Release 2026/03/10

- **b976-moderator-dashboards** – Introduced a tabbed Moderator dashboard (Approvals, Module Stats, Teacher Stats placeholder) and added a comprehensive Module Stats table for moderated MEQ sets with inline editing (dates, visibility, teachers), completion metrics, template-defined reportable Likert averages, and CSV export.

## Release 2026/03/09

- **b994-b472-phase-2-bulk-enrol-by-global-tag** – Added Phase 2 of the Bulk Enrol wizard, enabling administrators to enrol students onto one or more selected module instances based on Global Tags. Supports combining manual email input, CSV import, and tag-based user resolution with deduplication and validation in a single workflow.

## Release 2026/03/05

- **b510-double-dollars-feedback-problem** – Fixed handling of feedback containing double-dollar LaTeX delimiters after reverting a previous incomplete attempt.
- **b811-rich-text-math-improvements** – Improved rendering of evaluation feedback so text, HTML, LaTeX, and Markdown responses are displayed consistently and as intended.
- **b850-improve-show-hide-chat-logic** – Simplified chat visibility defaults by setting `Question - display chatbot` to true and `Set - chatbot visibility` to OPEN, with a migration updating existing records accordingly.
- **b988-meq-spring-import** – Updated MEQ import scripts to support additional teacher roles and evaluated-subject logic, improve CSV handling (whitespace normalisation and optional student assignment), and refine documentation for future imports.
- **b997-bulk-create-meq-sets-tweaks-1** – Improved the Bulk Create MEQ Sets feature by adding instance name to the summary table and correcting release-date time handling to prevent unintended UTC time shifts.

## Release 2026/03/02

- **b472-bulk-enrol-unenroll-enhancements** – Introduced Phase 1 of the Bulk Enrol wizard, allowing administrators and teachers (subject to permissions) to enrol the same selected students or teachers onto one or more selected module instances in a single workflow.

## Release 2026/02/24

- **b975-bulk-create-meq-sets** – Added bulk creation of MEQ sets across multiple modules and instances from a template, with shared settings and background job progress reporting.


## Release 2026/02/20

- **b961-left-handed-canvas** – Improved canvas usability to address left-handed user friction by preventing unintended width resizing, adding support for flipping canvas/content sides, introducing an option to lock canvas width, and enabling a full-screen canvas mode similar to response area canvas behaviour.
- **b967-add-ui-toggle-to-mask-student-emails** – Introduced a TEACHER-mode UI toggle to mask student names and email addresses in the Students table and Student View for presentation purposes.


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
 
