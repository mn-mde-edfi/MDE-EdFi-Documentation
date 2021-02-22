# Common Ed-Fi Errors
This file will store common Ed-Fi errors and potential troubleshooting steps to resolve them

## "More than one Profile" 400 Errors
This error frequently appears similar to the following in the JSON return message:
``` javascript
{
    "code": 400,
    "type": "Bad Request",
    "message": "More than one Profile is associated with this ApiClient/Application for the Resource (Resourcename). You must pass the Profile as part ofthe Request." 
}
```
This usually occurs when a district has more than one profile associated with the key and secret set up for the current ODS. They should remove the older profile(s) and save the Application in the Enterprise Security Configuration Tool (ESCT) to resolve this.

Districts can resolve this on their own if necessary, but MDE staff are also available to assist in a pinch.
