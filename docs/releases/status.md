Lambda Feedback is a cloud-native application that is available with full service 24/7.

This page contains information about any known incidents where service was interrupted. The page begain in November 2024 following a significant incident. The purpose is to be informative, transparent, and ensure lessons are always learned so that service improves over time.

The Severity of incidents is the product of: 

- number of users affected (for 100 users, N = 1), 
- magnitude of the effect (scale 1-5 from workable to no service), 
- duration (in hours). 

Severity:

- x < 1       is LOW
- 1 < x < 100 is SIGNIFICANT
- x >     100 is HIGH. 

The severity is used to decide how much we invest in preventative measures, detection, mitigation plans, and rehearsals.

## 2025 November 18th: Some evaluation functions failing (Severity: LOW):

Some evaluation functions returned errors.

### Timeline (UK / GMT)

2025/11/18 21:18 GMT: some but not all feedback functions failed. Investigation initiated and message on home page
2025/11/18 21:39 GMT: updated to users that the cause was identified.
2025/11/18 21:45 GMT: issue resolved. Home page updated.

### Analysis

The root cause of the issue was the outage of Cloudflare, which cause wide issues on the internet including for example X, ChatGPT, and other services being unavailable.

Our system does not use Cloudflare so was unaffected. However, any of our evaluation functions using an old version of our baselayer rely on calling GitHub to retrieve a schema. GitHub git services were down (presumably due to the Cloudflare outage), which meant that our functions could not validate their schemas and therefore failed.

We tried to implement a solution but were unable to because implementation relied on GitHub workflows, which failed for the same reason. GitHub had announced they were resolving the issue, and when it was resolved our services returned to normal.

The solution in this case is to upgrade all of our evaluation functions to a newer version of the baselayer, which has schemas bundled and does not rely on external services. 

### Recommended action

Update all evaluation function baselayers.

N=1, effect = 2, duration = 0.5. Severity = 1 (LOW)

## 2025 November 10th: Service unresponsive (Severity: SIGNIFICANT):

The application was unresponsive.

### Timeline (UK / GMT)

2025/11/10 14:21 Service became unresponseive, e.g. pages not loading. Reports from users through various channels. Developers began investigating, message sent to Teachers.

2025/11/10 14:28 Service returned to normal. Home page message displayed to inform users.

### Analysis

During the period of unresponsiveness, the key symptoms within the system were overloading the CPU of the servers. Error logging and alerts did successfully detect downtime and alert the developer team, who responded. Although developers were looking into the problem, and tried to increase resource to resolve the problem, in fact the autoscaling solved the problem itself. 

The underlying cause was a combination of high usage, leading to CPU overload. This type of scenario is normal and correctly triggered autoscaling. The issue in this case was that autoscaling should happen seamlessly, without service interruptions in the intervening period. 

### Action taken:

- Decrease the CPU and memory usage level at which scaling is triggered. This increases overall costs but decreases the chance of service interruptions.
- Enhance system logs so that more information is available if a similar event occurs
- Investigate CPU and memory usage to identify opportunities for improvements (outcome: useage is typical for NODE.js applications, no further action)

N=3, effect = 5, duration = 0.15. Severity = 2.25 (SIGNIFICANT)


## 2025 October 17th: Handwriting input temporarily unavailable (Severity: SIGNIFICANT)

Handwriting in response areas (but not in the canvas) did not return a preview and could not be submitted. Users received an error in a toast saying that the service would not work. All other services remained operational.

### Timeline (UK / BST)

2025/10/17 08:24 Handwriting inputs ceased to return previews to the user due to a deployed code change that removed redudant code, but also code that it transpired was required. 

2025/10/17 12:20 We became aware of a problem from using the system and alerted the dev team. A response began at 12:52.

2025/10/17 12:58 Message on home page: "We are aware that handwriting input is not functioning. We will update this message when we have more info."

2025/10/17 12:59 Code revert began. 

2025/10/17 13:07 Problem resolved. Message on home page: "The system is now fully operational. From 08:24-13:07 UK time handwriting inputs were not working. This has been fixed and we will follow up with an investigation."

### Analysis

Technically, the issue was caused by removing code that was necessary. 

Operationally, the process was as follows:
- Removal of 'unused' code submitted by one dev and reviewed by another and approved. 
- The code was not subject to user testing ('QA') due to no anticipated effect to test.
- The code was pushed in the morning to minimise impact on users
- Alerts were not monitored closely

Post-hoc analysis shows that approximately 20 users were affected.

### Lessons learned

- Basic QA of all changes going to PROD is necessary (on STAGING). It won't always catch problems but it will sometimes (and in this case it would have).
- Monitoring immediately after pushes, and approximately an hour after pushes, should be standard procedure.
- Integration tests would help, although they are considered outside the scope of this project at the current stage due to the resource required to continually maintain those tests

N=0.2, effect = 2, duration = 5. Severity = 2 (SIGNIFICANT.)

## 2025 August  27th: Evaluation functions temporarily unavailable (Severity: LOW)

The app was available and fully functional during this time and successfully called external evaluation functions. The evaluation functions managed by the Lambda Feedback team (which is most of them at the current time) became unavailable due to the API gateway of those functions being modified incorrectly. During this time, users submitting an answer on the app were given an error message.

### Timeline

2025/08/26 17:54 Evaluation functions became unavailable due to a deployment error.

2025/08/26 18:21 Message added to the home page. Fix began development and testing.

2025/08/26 21:51 Fix is complete and home page eupdated.

Estimated number of users affected: one. This low number was due to a quiet period in the academic year, and the rapid response to the problem.

### Analysis

- Due to evaluation functions having only one environment ('staging') that was used by both the STAGING and PROD versions of the app, changes to the staging gateway affected the production application.
- The error itself happened because an update to infrastructure included changes by a different developer that weren't noticed by the one pushing the changes

### Lessons learned

- Implement independent staging and prod environments for evaluation functions (DONE as part of the fix)
- When pushing infrastructure changes, always run Pulumi preview before starting, to see if changes are already awaiting push
- Don't push infrastructure changes when no other developers are available to support any issues
- Create a feature on the app for admins to optionally declare a base URL for evaluation functions, allowing groups of evaluation functions to be rapidly redirected

N = 0.01, effect = 3, duration = 4. Severity = 0.12 (LOW)

## 2025 March 28th: access blocked within a particular organisation's WiFi (Severity: SIGNIFICANT)

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

## 2025 February 13th: Incident related to new teacher roles feature (Severity: LOW)

During this period teachers were not able to access teacher pages.

### Timeline

7:20am deployed a set of new features, including teacher roles

9:47am issue reported - users with the TEACHER role were unable to access teacher pages.

10:27am Issue reproduced on staging

10:39am Issue fixed on staging; release to production initiated

10:49am Confirmation that the fix worked in production

### Lessons learned:

- Features that behave differently for users with the TEACHER role (compared to users with the ADMIN role) must be tested by a user with the TEACHER role who is not a super-admin. This is because super-admins automatically revert from TEACHER back to ADMIN. The same applies to features that behave differently for users with the STUDENT role.

## 2024 mid-December to 2025 January 2nd: Imperial College security measures affected logins (severity: HIGH)

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

## 2024 November 4-8th: Incident related to new logins (Severity: SIGNIFICANT)

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
