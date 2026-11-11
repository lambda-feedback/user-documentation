# Notifications by email

Teachers receive regular emails with notifications. Preferences can be modified in *Settings*, which is accessible via 'My Profile' or the following direct link:
[https://www.lambdafeedback.com/settings/notifications](https://www.lambdafeedback.com/settings/notifications)

- Notifications can be switched on/off per module instance
- Frequency can be switched to:
  - Daily (8am)
  - Weekly (Mondays)
  - Monthly (1st of month)
  - None 
  
The default frequency is set within the tenant (typically the default is Weekly).

Each email summarises activity within relevant module instances, over a period corresponding to the frequency of email, e.g. typically one week of activities.

A single email is sent per period, containing all activities, split within the email by module. Terminology 'recently' and 'upcoming' in the email refers to periods based on the frequency of notifications. E.g. 'recently' means within the last week for those receiving weekly emails.

Emails cover MEQs (Module Evaluation Questionnaires), Problem Sets opening,  student comments and flags on Problem Set content, and errors in automated feedback in Problem Sets.

If there is nothing to report within a period, then no email is sent during that period.

## Conditions for receiving an email

For a teacher to receive an email, at least one Module Instance must meet all of the following:

- Teacher role on the module instance (any teacher role, regardless of permissions)
- Frequency is not 'None'
- Teacher settings include the module instance for notifications (in 'My Profile') 
- The module and the module instance are not deleted ('ended' instances are still *included*)
- There are activities to report

## Contents of an email

In the following order:

- Subject: the first two items of the summary, for example "3 MEQ comments need moderation, 2 MEQ results are available and more".
- Intro: the relevant period. For example: "Here is your weekly recap from Mon 2 Mar to Sun 8 Mar".
- Summary: emails wth 10+ modules include a summary block at the top, showing totals.
- Content relating to each module instance

The content for each module is as follows and in this order:

| Item                        | Example line                                                   | Rule                                                                                                              |
| --------------------------- | -------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| MEQ comments to moderate    | 3 MEQ comments need moderation                                  | See "MEQ moderation" below.                                                                                       |
| MEQ results available       | MEQ 1: Autumn · results are available · 62% completed | The MEQ closed in the period that ended. The close can be the close date, or a manual hide.                      |
| MEQ opened                  | MEQ 2: Spring · opened · Mon 2 Mar · 15% completed   | The MEQ opened in the period that ended.                                                                          |
| MEQ opening                 | MEQ 3: Summer · opens · Thu 5 Mar                  | The MEQ opens in the upcoming period.                                                                          |
| MEQ closing                 | MEQ 4: Another evaluation · closes · Fri 6 Mar · 48% completed   | The close date of the MEQ is in the upcoming period.                         |
| MEQ open                    | MEQ 5: More surveys · open until Mon 30 Mar · 40% completed | The MEQ opened before the previous period, and will remain open after the upcoming period. See below.            |
| Set opening                 | Set 4: Thermodynamics · opens · Tue 3 Mar                       | Same rule as "MEQ opening".                                                                                       |
| Set closing                 | Set 3: Heat transfer · closes · Fri 6 Mar                       | Same rule as "MEQ closing".                                                                                       |
| Set opened                  | Set 3: Heat transfer · opened · Mon 2 Mar                       | Same rule as "MEQ opened".                                                                                        |
| Set closed                  | Set 2: Entropy · closed · Sun 1 Mar                             | Same rule as "MEQ results available".                                                                             |
| Activity                    | 4 comments · 1 flag · 2 errors                                  | See "Activity" below.                                                                                             |

Notes:

- The completion rate shows only for MEQs that have opened (not for unopened MEQs or for any Problem Sets). Completion is the share of enrolled students who completed the MEQ, rounded down.
- The "MEQ open" line reminds the teacher to pursure higher response rates. These reminders persist throughout the period that the MEQ is open - except if listed with the alternative recently "opened" or soon "closing".
- A set or MEQ that has never been visible to students does not show in the notifications. 
- Events "Opened" and "Closed" appear at most once per Set in notifications. 

### MEQ moderation

Moderation means approving or rejecting student comments before teachers can see them (see [MEQ/#moderators](../guides/MEQ/#moderators)). In notifications the moderation line counts the MEQ comments (free-text answers) that are pending moderation. Criteria to be counted:

- The MEQ is closed (by its close date or by a manual hide).
- The module instance end date has not passed.

The number of comments is the total awaiting moderation (including any previously included in notifications).

Comments on an open MEQ are not included in the moderation notification. 


## Synchronicity

The algorithm to produce notification content runs first and stores the results in a database. Subsequently emails are sent based on the results of the algorithm. If any information changes between the algorithm running and the email sending, then the email will contain out of date information. 

In practice, these lags are small i.e. on the order of hours at most, but they can be days if there are continual email failures and retries. If an email has not sent by the end of the relevant period, then it is never sent and the new period begins with a fresh notification.