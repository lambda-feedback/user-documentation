# Enrolling students

## Correct form of email address

The email address must be the one returned by the authentication process. For Imperial College London this means the *long-form email address*:

#### Valid:

first.nameYY@imperial.ac.uk (student)
<br>
j.doe@imperial.ac.uk (staff)
<br>
first.name@imperial.ac.uk (staff)
<br>

#### Invalid:

abc123@ic.ac.uk
<br>
abc123@imperial.ac.uk
<br>
user@ic.ac.uk
<br>
user@imperial.ac.uk
<br>
first.nameYY@ic.ac.uk
<br>

This is because we use Azure Active Directory (i.e., Microsoft) to **authorise** users.

## Enrollment within a module

In the module, open the **Students** tab and select **+ Enrol Students**.

![Students tab with the Enrol Students button](images/meq-students-tab-enrol.png)

Type the student's long-form email address in the **email** box, press **Enter**, and select **Submit**. Alternatively, upload a CSV with a list of email addresses.

![Enrol Students dialog with email box](images/meq-enrol-students-dialog.png)

A student can be unenrolled by selecting them (LHS) and clicking 'Unenrol selected', or clicking the three dots on the RHS of the student and clicking 'Unenrol'.

![Unenrol option in the student menu](images/meq-unenrol-menu.png)

## Bulk enrol across multiple modules

Click on 'Bulk manage users', which is on the [modules](https://www.lambdafeedback.com/teacher/modules) page.

<img width="171" height="51" alt="bulk_manage_users" src="https://github.com/user-attachments/assets/75d85609-ac2f-4acb-bdc4-3d7cd7f91bde" />

Follow the guidance on the screen to provide the data in a CSV file. A preview is provided before exectuing.

Select **Enrol**, **Students** and **Upload CSV**.

![Enrol, Students and Upload CSV options](images/meq-bulk-enrol-options.png)

Upload the prepared file.

![File upload step](images/meq-bulk-upload-csv.png)

Configure the data. A file that follows the mock example needs little configuration.

![Data configuration step](images/meq-bulk-configure-data.png)

Check that each row maps to the correct module.

![Mapping of rows to modules](images/meq-bulk-map-data.png)

Confirm the enrolments and proceed.

![Enrolment confirmation step](images/meq-bulk-confirm.png)

The enrolments show as processing until all are complete.

![Enrolments in progress](images/meq-bulk-processing.png)