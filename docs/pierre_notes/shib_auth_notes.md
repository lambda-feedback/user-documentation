# Authentication Notes 
## Learning Resources
- [Harvard Guide](https://iam.harvard.edu/resources/saml-shibboleth-integration)
- [SAML GUIDE](https://auth0.com/blog/how-saml-authentication-works/)
- [Shibboleth Wikipedia](https://en.wikipedia.org/wiki/Shibboleth_Single_Sign-on_architecture)


## Imperial Shibboleth Links 
- [Some kind of endpoint description?](https://shibboleth.imperial.ac.uk/idp/shibboleth)

## Blackboard Analysis (Chrome)
This first analysis was done on Chrome, and each request seemed to pass the same cookies, I'd been logged in to BB on this browser before. 

Cookies to `bb.imperial.ac.uk`:
```properties
COOKIE_CONSENT_ACCEPTED=true;
__utma=168090937.117265871.1537450221.1602504962.1605022417.11; 
_ga=GA1.1.117265871.1537450221;
_ga_LME5ZDDFS0=GS1.1.1610645056.2.1.1610645629.0;
NSC_309628_wjq_46.183.240.113*443=ffffffff090b1fce45525d5f4f58455e445a4a4229a1; 
s_session_id=DD61E358DE8D02E26C54AE9A82AD2FE9;

JSESSIONID=BBD25B3D03544577797031A821FBF6CA;
```

Cookies to `shibboleth.imperial.ac.uk`:
```properties
JSESSIONID=node014ekry64k01ycbu9ko0g9eh5z5018.node0;
__utma=168090937.117265871.1537450221.1602504962.1605022417.11;
_ga=GA1.1.117265871.1537450221;
_ga_LME5ZDDFS0=GS1.1.1610645056.2.1.1610645629.0
```

1. Initial fetch returns code 302
2. We get redirected to `login/` which also returns 302, before fetching `login/apid=XXX&redirectUrl=XXX` which returns 200
3. We **POST** to `shibboleth.imperial.ac.uk/idp/profile/SAML2/POST/SSO`
	- It's a post request, returns 302 not found, but in the response there's a location header `Location: https://shibboleth.imperial.ac.uk/idp/profile/SAML2/POST/SSO?execution=e2s1`
	- Passes Form Data, `SAMLRequest`, which is b64 encoded XML (**Content-Type**: application/x-www-form-urlencoded):

```xml
<?xml version="1.0" encoding="UTF-8"?>
<saml2p:AuthnRequest
  xmlns:saml2p="urn:oasis:names:tc:SAML:2.0:protocol"
  AssertionConsumerServiceURL="https://bb.imperial.ac.uk/auth-saml/saml/SSO/alias/_114_1"
  Destination="https://shibboleth.imperial.ac.uk/idp/profile/SAML2/POST/SSO"
  ForceAuthn="false"
  ID="a401d1dghb963e675c16ic74hajddh4"
  IsPassive="false"
  IssueInstant="2021-07-12T11:40:29.222Z"
  ProtocolBinding="urn:oasis:names:tc:SAML:2.0:bindings:HTTP-POST"
  Version="2.0">
  <saml2:Issuer xmlns:saml2="urn:oasis:names:tc:SAML:2.0:assertion">bb.imperial.ac.uk</saml2:Issuer>
  <ds:Signature xmlns:ds="http://www.w3.org/2000/09/xmldsig#">
    <ds:SignedInfo><ds:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/><ds:SignatureMethod Algorithm="http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"/>
      <ds:Reference URI="#a401d1dghb963e675c16ic74hajddh4">
        <ds:Transforms><ds:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/><ds:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/></ds:Transforms><ds:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
        <ds:DigestValue>v0WPinmElHwODk6kvlrgjQkZm58=</ds:DigestValue>
      </ds:Reference>
    </ds:SignedInfo>
    <ds:SignatureValue>C8AiPZBdtet2M6rwOSHggZgKQAGKzJHvt6yVVdwRAWW67392ssygKFyBBs84SWNGUd/tYurrcZqwNlO+ypyC8LjplEJrDzKJ66joY3hRdAJMI4SByeQ1PvUo9hN6h350KnMIZiV+vDiQfL8t9zuHgvd5wr9OLiZZflcCzMLI8igRxbkJglSioNtVWE6SP1UkBqQND8sGORuiE5sz508ngbRo8RnjXwmp2/jpBE6b3kQPeAh/x0VQu7qVhfMdIO01yE5PPTSrgVGfuGisq0QkouFeMOor+L1/F2HA3+tPsdDLgw8Alzf5bLQw9rfAg9ivfc99ex7Ndd1UNWhD4XCu+A==</ds:SignatureValue>
    <ds:KeyInfo>
      <ds:X509Data>
        <ds:X509Certificate>MIICrTCCAZWgAwIBAgIBATANBgkqhkiG9w0BAQsFADAaMRgwFgYDVQQDEw9CbGFja2JvYXJkIFNB TUwwHhcNMTcwODAyMTUwODA5WhcNMjcwODAyMTUwODA5WjAaMRgwFgYDVQQDEw9CbGFja2JvYXJk IFNBTUwwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQC39hmSQPQWZO8MRAwlYKA1FZUh
          57aPaPzeE8lMtdQe3hrovLp6NqFDfx9nhHIIdk9o7salQk8iogo0LwvVjeKEXU8OPkMBJzIubnGj wanXqscvbdptZliSe32xBuWlWNXvA1r7zBOICpcOBnbMhWMGsLsNcbEumroDIt/ppl8/hPima5U4 br3cdHweZiyde4I+M72Mieu42G0tzi6JbP8K2xm3jirGIPxhtZSiyGh0+orY/blVYWzBlGtOUmiY
          RHWX2FpQFcWPFHQTREy/PP9c8Pm4QmJK/a9s46TEt/OmhONcgPX/OHtk4d8TLnX1ps90M1vLby3c rWfrFScKdkOHAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAKSBgITd7uhGevKpMX2tV1sF/+Y2Swbc GNMwram/JQ3KlIEoF/v5mOP+EVBhVymwoXN+/mfw+UcdsUipRKrOyO+47LWGJ4ihefdc+6d7zwR3
          3PGjlDUMomJHM1AiEB8Z/XYAgYVi1iGBuM4/1+E08eQd2xy6tYGF6CVO64VUrHfULo7phH9x9y8k uW4yrUhAjmKGnmQ8g7vWudTUFQf4znLP1MifN6hWlm1os7zEThVRFq1Q/jmDSu3L5Mz6fjonIwQo RGPsmgPBr6J20RIsHXXtWdFfn1LpPXVImMsnhfOu6o9EIlBXTJfZPw081oxvOJXpROKOkFsk1qSi J0RN8J8=</ds:X509Certificate>
      </ds:X509Data>
    </ds:KeyInfo>
  </ds:Signature>
</saml2p:AuthnRequest>
```
4. We get redirected to `https://shibboleth.imperial.ac.uk/idp/profile/SAML2/POST/SSO?execution=e2s1`, This time using the **GET** method. Which returns the HTML for the imperial login page. 

**Entering username and password: AAAAAAAA BBBBBBBB**

5. Post to `https://shibboleth.imperial.ac.uk/idp/profile/SAML2/POST/SSO?execution=e1s1`
	- **Content-Type**: application/x-www-form-urlencoded
 ```properties 
j_username=AAAAAAAA
j_password=BBBBBBBB
donotcache=1
_eventId_proceed=
```
