# Common Ed-Fi Errors
This file will store common Ed-Fi errors and potential troubleshooting steps to resolve them

## "More than one Profile" 400 Errors
This error frequently appears similar to the following in the JSON return message:
``` javascript
{
    "code": 400,
    "type": "Bad Request",
    "message": "More than one Profile is associated with this ApiClient/Application for the Resource (Resourcename). You must pass the Profile as part of the Request." 
}
```
This usually occurs when a district has more than one profile associated with the key and secret set up for the current ODS. The older profile needs to be removed to resolve this; since MDE no longer uses the ECST, MDE staff are available to assist at ed-fi.mde@state.mn.us.

## "Access to the requested SchoolId" Errors
Occasionally the initial access to a school/LEA gets misconfigured in our initial load of keys and secrets, resulting in an error similar to:
``` javascript
{
    "code": 403,
    "type": "Authorization Denied",
    "message": "Access to the requested 'SchoolId' was denied." 
}
```
The solution to this issue is to contact MDE and have staff check the authorization of the LEA in the Admin app. It may be as simple as switching from a "School" authorization to an "LEA" authorization, assuming a single vendor serves the entire LEA.