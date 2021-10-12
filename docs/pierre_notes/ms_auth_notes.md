# Login using Microsoft OAuth 
## Useful docs links
- [Microsoft docs](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow)
- [Microsoft docs for a web app which calls APIs](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-web-app-call-api-overview)
	- [Python code sample](https://github.com/Azure-Samples/ms-identity-python-on-behalf-of)
- [Acquire token to call an API from a SPA](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-spa-acquire-token?tabs=javascript2)
	- [Use token to call API](https://docs.microsoft.com/en-us/azure/active-directory/develop/scenario-spa-call-api?tabs=javascript)
- [Code samples for different languages (ms docs)](https://docs.microsoft.com/en-us/azure/active-directory/develop/sample-v2-code)
- [Tenant param description](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-protocols)
- [Quickstart for a Node.js app](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-v2-nodejs-webapp-msal?WT.mc_id=Portal-Microsoft_AAD_RegisteredApps)
- [Quickstart for React SPA](https://docs.microsoft.com/en-us/azure/active-directory/develop/quickstart-v2-javascript-auth-code-react)
- [React Tutorial](https://docs.microsoft.com/en-us/azure/active-directory/develop/tutorial-v2-react)

## Imperial/App info
- [Find the Imperial College London Microsoft Tenant ID](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Properties)
	- `2b897507-ee8c-4575-830b-4f8267c3d307`
- OAuth Testing app Application ID: `ca92edb1-eb47-44b3-85a7-1011c51fb945`
- msal config 
```javascript
const config = {
  auth: {
    clientId: "ca92edb1-eb47-44b3-85a7-1011c51fb945",
    authority: "https://login.microsoftonline.com/2b897507-ee8c-4575-830b-4f8267c3d307",
    clientSecret: "XXXX",
  },
  system: {
    loggerOptions: {
      loggerCallback(loglevel, message, containsPii) {
        console.log(message);
      },
      piiLoggingEnabled: false,
      logLevel: msal.LogLevel.Verbose,
    },
  },
};
```

## Learnt Things 
- Need to register **BOTH** the SPA and the API on Azure.
- We use two types of tokens ID and Access. 
	- ID: Used to Authenticate the user on the SPA, since we use the library, I don't think we need to touch it 
	- Access: Requested by the SPA, with a specific `scope` and `account`, and sent alongide requests to our API. A new access token should be regenerated every time we make a request. 
		- We can make custom scopes on the API registration
- All of this only works if the registered applications on Azure are set to work with version 2:
	- Set `"accessTokenAcceptedVersion": 2` in the Manifest on Azure.
- Read the README for the *ms-identity-python-on-behalf-of* file carefully
- Use [jwt.ms](jwt.ms) to troubleshoot and decode Access and ID tokens 
- We can add extra 'claims' which get added by Azure when an *Access* or *ID* token is requested
	- One of those is a `group`, which we can setup to assign permissions on the Sheets DB side.
	- Cool ones also include `ipaddr` and `zone`
- When registering an API to Azure, we can add a range of permissions for differnent endpoints, and just flat out rejecting the *Access Token* request directly (before pinging one of our APIs)