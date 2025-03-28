Lambda Feedback is a cloud-native application that is available with full service 24/7.

This page contains information about any known incidents where service was interrupted. The page begain in November 2024 following a significant incident. The purpose is to be informative, transparent, and ensure lessons are always learned so that service improves over time.

## 2025 March 28th: access blocked within a particular organisation's WiFi

The URL lambdafeedback.com is served by a content delivery network (CDN), that was blocked by a particular organisation's WiFi. During this period, users on that WiFi couldn't access the site.  

### Timeline

2025/03/27 09:17 GMT We received a report that some users can't load the website at all. We announced this on the home page.

2025/03/27 10:37 GMT The issues were identified as isolated to Imperial WiFi. Update on home page including advice to use a different WiFi (e.g. hotspot, or other location), or a [different DNS](https://developers.cloudflare.com/1.1.1.1/setup/windows/). Ticket with ICT and number shared with users. There was a response within minutes requesting more information, but no further response until the next morning.

2025/03/28 09:22 GMT Imperial ICT acknowledged that their security software had blocked the whole CDN. Lambda Feedback was specifically unblocked and full service was resumed. We have asked for a broader unblocking.

2025/03/28 09:32 GMT Authentication services were down (no logins) but resumed within a few minutes and service remained good. We'll investigate and report.

2025/03/28 13:47 GMT Imperial ICT confirmed a wider unblocking.

2025/03/28 14:45 GMT Incident closed. 

### Lessons learned:

Networks that provide internet access can block or incorrectly redirect users when trying to access Lambda Feedback. The block can be specific to one site or, as in this case, it can block a whole content delivery network (CDN) that serves many sites. 

Affected users will never reach the site, and we will have no way to know that they are failing to access. 

### Recommended Actions

- Alert the ICT departments of key user groups to this problem, and ensure in advance that the relevent CDNs are not blocked.

- Create a backup plan for if the URL or the CDN are not correctly routed

- Monitor traffic to identify drops in usage that may indicate an issue (we already do this, but the drop was not significant enough in this case to be evident)

- Monitor the Lambda Feedback email address (this was effective in this case and we were in touch with users)

- Create a live chat with 'power users' for better communication during these incidents. A chat was started during this incident and will continue to be used

- Consider local WiFi/networks as a possible cause for blocking site access, and test for this cause when troubleshooting access issues

- Investigate the cause of the short unavailability of logins at 09:33 GMT on 28th March 2025.

## 2025 February 13th: Incident related to new teacher roles feature

During this period teachers were not able to access teacher pages.

### Timeline

7:20am deployed a set of new features, including teacher roles

9:47am issue reported - users with the TEACHER role were unable to access teacher pages.

10:27am Issue reproduced on staging

10:39am Issue fixed on staging; release to production initiated

10:49am Confirmation that the fix worked in production

### Lessons learned:

- Features that behave differently for users with the TEACHER role (compared to users with the ADMIN role) must be tested by a user with the TEACHER role who is not a super-admin. This is because super-admins automatically revert from TEACHER back to ADMIN. The same applies to features that behave differently for users with the STUDENT role.

## 2024 mid-December to 2025 January 2nd: Imperial College security measures affected logins

During this period the application was 100% available and operational. We were alerted on 2nd January that some users were not given permission by Imperial College London Microsoft 365 to login to third party applications. This was a a severe incident as it affected access to the application for some users.

### Timeline

11:19 GMT We discovered the issue, escalated to Imperial College ICT and put a notice on our home page.

16:51 GMT The application was approved by Imperial College ICT, which resolved the problem.

Monitoring immediately after and the following morning showed that two known users who had issues no longer have issues. Other users continued to login before, during, and after the incident. No further reports of issues received. Case closed.

### Analysis

- Lambda Feedback has been using Imperial College Microsoft 365 logins (Entra / Azure Active directory) since July 2021 without issues until this incident.

- ICT reported on 2nd January: "due to heightened security arrangements put in place in mid December, ICT prevented unauthorised App registrations as these can pose security threats through unwarranted access to user information and the access to other systems. We have now granted access for the Lambda feedback app."

- Although the app was 'registered' on Entra/AAD in July 2021 within the Imperial College tenant, the permissions required for authentication (read the profile of the user) were granted by the user the first time they logged on. The changes imposed by ICT withdrew the privilege from users to grant such permissions, hence the inability to login. Permissions can be bulk granted by admins in the tenant, but this had not been done. On 2nd January, those permissions were given by admin and the problem was resolved.

- Due to the holiday season, this problem only surfaced on 2nd January, despite the cause being in 'mid-December'.

### Lessons learned:
 
- When an organisation uses single sign-on (SSO), ensure that the Lambda Feedback application permissions are granted by the organisation admin, even if the service initially works without those permissions being granted by admins. This action will protect against possible future issues, especially like the incident reported here.

## 2024 November 4-8th: Incident related to new logins

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
