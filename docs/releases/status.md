Lambda Feedback is a cloud-native application that is available with full service 24/7.

This page contains information about any known incidents where service was interrupted. The page begain in November 2024 following a significant incident. The purpose is to be informative, transparent, and ensure lessons are always learned so that service improves over time.

## 4-8th November 2024 Incident related to new logins

Deployment of a new authentication process caused service interruptions. Login was not possible at certain times, affecting all users. Effects were between Monday 4th and Friday 8th November, all related to release b506.

### Timeline

Monday 4th November:

7:30am deployed new login system. Initially appeared OK but concerns over server loading.

8:15am began reverting to the old system to avoid any unnecessary risks. Revert took longer than rehearsed.

8:55am system live and operational in its reverted form. No issues hereafter.

The issue was identified and fixed ready to push with the new login system early the next day.

Tuesday 5th November

6:30am deployed new login system with update to avoid errors found on previous push. Systems fine.

9:27am first report of login issues with ipads.

9:37am issue with Safari and iOS identified. Message update on the app.

10:45am revert complete after efforts to implement a fix failed.

The issue was related to blocked thrid-party cookies being on some browsers. A fix was developed to push the next day.

Wednesday 6th November

7:08am deployed new login system with updated auth URLs. Testing on all device types OK.

12:00pm Two users reported issues via email. Investigations continued including emails with users.

Thursday 7th November

Throughout the day the problem was analysed and we found that 12 users had logged in during a brief configuration error, and as a result were not stored correctly in the new auth DB, and this caused problems. All users access was restored and they were contacted with information and an apology.

Friday 8th November

10:31am The app became intermittent. This was traced to an updated in the logging. Resource was increased which partially solved the problem. A deployment was pushed to solve the problem.

11:00am (approx) the issues were fully solved.

### Lessons learned:

- When practicing a revert before a deployment, make sure the exact same revert process is used in production (e.g. don't go via CircleCI if rehearsals were via GitHub). Lesson from Monday morning following a delayed revert process.
- Test changes on all device types. Lesson from Tuesday following issues with Apple devices.
  If systems are used temporarily in production, check for adverse affects on any users who used both systems. Lesson from Wednesday/Thursday following issues for a small number of users.
- Ensure errors due to trivial issues, like changes to logs or failed schema in the DB, do not cause the whole app to go down. Lesson from Monday and Friday.
- Ensure adequate logging systems are in place (these have been improved already), and that a clear process is in place for users to contact the team (use lambdafeedback@imperial.ac.uk, or support@lambdafeedback.com which will redirect there)
- Ensure important messages to users can be seen, e.g. even if they can't log in.
  Keep teachers informed promptly and with transparent info. Generally this protocol was followed during this incident.

Conclusion:

- The new login system offers significant benefits, including allowing logins with a range of systems such as Google or personally created accounts. The app is now available to essentially any users.
- The deployment involved errors which caused access issues for over an hour on more than one occasion in the same week.
- Most of the outages were preventable with improved testing
- The mitigation attempts were successful in reducing the severity of the incident
- Mitigation could have been better. New logs, lower risk tolerance, and better reversion are needed in future
- Overall the level of outage is not considered acceptable and in future should be avoided
