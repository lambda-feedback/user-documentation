# How each service is authenticated:
## SPA Web App (React)
- Uses the `msal-react` library, takes care of all the redirects to the microsoft identity provider, and only renders certain components to logged in users using the wrappers provided in the library.
- As the user logs in, the App acquires an *ID Token* from microsoft, which is used in the *Authentication* part (just checking the validity of a user profile).
- Then, we use the `msal` libraries to acquire *Access Tokens* to each of the resources defined (Problem Set DB, Grading API, Students DB, ...). All of those need to be registered on the Azure console. 

## Problem Sets DB 
- Permissions to access this API will depend on the user that is logged in. So we've already authenticated the user on the SPA side, but now we need to authorize it to access this resource. 
	- To acheive this, we request and attach an *Access Token* to each request made to this API. 
	- These tokens are validated, and its permissions are checked to make sure the request is valid

**Example permissions attached to this resource:**
- `ProblemSet.ViewAll`:  Relevant to Authors and Developpers
- `ProblemSet.ViewReleased`: Relevant to Students
- `ProblemSet.View`: Open a particular problem set, will probably have to attach a `group`, or other identifier to check if the user is allowed to open that particular sheet 

## Grading API
- Similar to the the Problem Set DB, we need to make sure students are allowed to check a certain question's answer. (We don't want students to attempt to grade questions which haven't been released yet).
	- We retrieve and attach an *Access Token* to the request, made for the example `scopes` and `permissions` below.
	- **Note**: We could make these tokens just pass through to requests made to the Sets DB for individual ResArea answers, meaning we don't really need to authenticate requests made to this endpoint.... (or maybe just validating an *ID Token*). This would mean most of the complex permission and authorization code would live on the Problem Sets DB

**Example permissions**:
- `ResArea.Grade`:  Simple scope attached to each grading request....? 