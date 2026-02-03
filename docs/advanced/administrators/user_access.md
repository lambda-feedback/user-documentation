# Purpose

This section is intended for administrators configuring access and advanced users supporting access-related workflows.

It explains:
- the different types of user roles
- how roles are created and configured
- how those roles affect access to modules and functionality

This documentation focuses on access semantics and configuration rather than providing a full UI walkthrough.

# Base User Roles

There are currently 3 base user roles:

## STUDENT

Users with the STUDENT role have access only to student pages.

## ADMIN

Users with the ADMIN role have access to all admin pages. They also have contextual access to teacher and student pages, subject to the same module-level access rules that apply to users with the TEACHER base role.

## TEACHER

Users with the TEACHER role have access to teacher pages, but only for modules to which they are linked as a teacher, tutor, or moderator. They can also access student pages for those modules.

User access to teacher-facing functionality is controlled by a set of permissions.

These permissions currently apply only to TEACHER pages, tabs, menus, and features (such as activities or viewing statistics).

## Mental model

Access to teacher-facing functionality is determined by:

1. The user’s **base role** (ADMIN or TEACHER)
2. How the user is linked to a module:
    - as a **teacher** (via a teacher role)
    - as a **tutor** (via global tags)
    - as a **moderator** (via a role containing moderation permission)
3. The **permissions** associated with that access

These access mechanisms are evaluated independently and may overlap in effect, but they are not interchangeable.

# Teacher Roles

Teacher Roles are permission groupings used to control direct module-level teacher access for users with ADMIN or TEACHER base roles. They do not apply to users with the STUDENT base role.

The UI currently labels these permission sets as "Teacher Roles," though this terminology may evolve.

## Teacher access

There are currently the following types of Teacher Roles:

### OWNER

This is a system-defined **role type**. Exactly one role exists with this type.

The administrator can modify the role’s description, but cannot delete the role or change its permissions.

This role is assigned automatically to the user who creates a new module instance, but it may also be reassigned to other users with ADMIN or TEACHER base roles.

The role of this type provides **Teacher** access to the module.

### CUSTOM

Roles of this **role type** can be added, updated, or deleted by administrators.

Administrators (or teachers with relevant permissions) can assign this role to users to grant them access to a module instance as teachers.

All roles of this type provide **Teacher** access to the module.

## Tutor access

Tutor access is not a teacher role. It is a separate access mechanism derived from student–tutor relationships.

There is currently the following type of Tutor Roles:

### PERSONAL TUTOR

This is a system-defined **role type**. The system provides a single role of this type.

The administrator cannot delete this role but can modify its description and permissions, except for the **View student data** permission.

This role is assigned indirectly using Global Tags, which group students into student groups and assign teachers or administrators as tutors to those groups.

A teacher or administrator gains access to a module if there is at least one student in that module who shares a Global Tag with the teacher or administrator. Access to the module is then restricted by the permissions assigned to the PERSONAL TUTOR role.

Although the tutor role includes the **View student data** permission, that permission applies **only** to students within the same tutor group (i.e. those sharing the same Global Tag), unless the same user would have a TEACHER ROLE to the same module with **View student data** permission. This differs from teacher access, where permissions apply to all students within the module.

**Tutor access** therefore represents indirect, student-scoped access to a module, rather than full module-level teacher access.

Role of this type provides **Tutor access** to the module.

## Moderator access

Moderator access is currently defined by the presence of the **Moderate student submissions** permission. In the current implementation, moderator access is modelled as a variant of teacher role assignment rather than as a separate access mechanism.

As a result, a user may be assigned **either a “true” teacher role or a moderation-enabled teacher role** for a module, but cannot hold **both role assignments simultaneously**. A moderation-enabled role still grants teacher-level access to the module; however, it replaces any other teacher role assignment rather than layering on top of it.

This choice affects how roles are currently assigned in the UI. It does not imply that moderation represents an additional teaching responsibility, nor that multiple teacher-role assignments are conceptually required.

Any role (typically a CUSTOM role) with this permission enabled grants moderator access to a module.

This reflects the current system behaviour and should not be interpreted as a conceptual requirement of the access model.

## How to assign access to the module

The ADMIN module instance teachers page allows administrators to grant module access to users with ADMIN or TEACHER base roles by selecting the relevant teacher role. Because the system currently allows assigning only one teacher role per user per module, moderation access is mutually exclusive with other teacher-role-based access.

In practice, a user must be assigned either:
	•	a “true” teacher role (with Moderate student submissions disabled), or
	•	a "moderator" role that includes the Moderate student submissions permission.

This reflects a limitation of the current role-assignment model rather than an inherent requirement of the access semantics.

The TEACHER module teachers page allows teachers with the appropriate permissions to grant module access to other users with ADMIN or TEACHER base roles by selecting the relevant teacher role, though they can only assign “true” teacher roles (i.e. roles with Moderate student submissions permission disabled).

>Note: A detailed description of individual permissions and their effects is maintained in the technical documentation for developers. This page focuses on access concepts and configuration rather than permission-by-permission behaviour.

>Note: The administration UI presents teacher roles, tutor access, and moderator access in a single table for configuration convenience. This does not imply that they are equivalent access mechanisms.
