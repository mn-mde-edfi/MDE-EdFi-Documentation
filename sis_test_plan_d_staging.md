# Staging Environment Load and Quality Check

At the completion of Scenario based testing in the Sandbox environment, MNIT will grant vendors a key and secret for the district(s) they are working with in the Staging environment. In the Staging environment, vendors will load actual student data, with student enrollment (studentSchoolAssociation), demographic (studentEducationOrganizationAssociation), program and calendar information. 

The main URL for the Staging Environment is: ```https://stage.edfi.education.mn.gov/edfi.ods.webapi/```

Remember, the new SDK contains everything you need to speak to multiple school years. In Production and Staging there is a single API with multiple school years which are addressed by specifying school year in the path. For example:

- /edfi.ods.webapi/data/v3/**2020**
- /edfi.ods.webapi/data/v3/**2021**
- /edfi.ods.webapi/data/v3/**2022**

For each school year, you will have a unique key and secret. Each key and secret will be associated with a profile that allows data to be submitted based on what was required for the school year. Thus:

- In the 19-20 ODS, your key and secret is constrained to the elements in the **Minnesota_SISVendor_Profile**.
- In the 20-21 ODS, your key and secret will be constrained to the elements in the **Minnesota_Twenty_Twenty_One_SISVendor_Profile**.
- In the 21-22 ODS, your key and secret will be constrained to the elements in the **Minnesota_Twenty_One_Twenty_Two_SISVendor_Profile**. 

[The SDK](https://github.com/mn-mde-edfi/MDE-Ed-Fi-ODS-API-SDK/tree/master/MDE-EdFiClientSDK/EdFi/OdsApiv31_2021/src/EdFi.OdsApi.Sdk
) includes multiple profile definitions.

## Ed-Fi / MARSS Identities API Integration Test 

Vendors have the option of building in support for interfacing with the MN Student Identity System to create new MARSS Student IDs (Ed-Fi Unique Id) through an Ed-Fi Identities API implementation. Vendors will be able to test their State ID creation integrations in the Staging environment. 

Vendors must demonstrate their ability to create new Student IDs when a Student is created in the Student Information System. This would be accomplished by posting to the ```/identities``` endpoint. 

The SY2022 URL for the identities API in the Staging environment is:
```https://stage.edfi.education.mn.gov/edfi.ods.webapi/Identity/v2/2022/identities```

The general process for identity creation is as follows: 

- A Vendor posts a new Student Identity including the following properties to the ODS/API identities end-point:
```javascript
{
 "stateStudentId": "000010000000",
 "educationOrganizationId: "255901",
 "lastSurname": "LastSurname",
 "firstName": "FirstName",
 "middleName": "MiddleName",
 "generationCodeSuffix": "Suffix",
 "birthDate": "2005-12-15T00:00:00",
 "sexType": "Male"
}
```

- The identities API validates the student information against the MN Student Identity System.
- If no match is found in the Student Id System – the student id is created (this is equivalent to code 3002 in the SIS)
- An HTTP response code ```201``` created is returned from the ODS/API.
- If the Student ID System returns an error, the student id will fail to be created, and the ODS/API returns an HTTP status code ```400 Bad Request``` with the corresponding message for the error given (see specific errors below under Test 2).

### Create Student ID Test 1

**Description**: Vendor posts a new Student Identity to the ODS/API identities end-point. Vendor submits Id with additional identifying attributes, and ID is created successfully

Sample JSON:
```javascript
{
 "stateStudentId": "000010000000",
 "educationOrganizationId: "255901",
 "lastSurname": "LastSurname",
 "firstName": "FirstName",
 "middleName": "MiddleName",
 "generationCodeSuffix": "Suffix",
 "birthDate": "2005-12-15T00:00:00",
 "sexType": "Male"
}
```
**Response** 
```201: created```

### Create Student ID Test 2 

**Description**: Vendor posts a new Ed-Fi Student record to the Identities endpoint in order to generate the following error conditions: 
Error|Description|Details
---|---|---
3000|(Input SSID not equal SSID)|Student identifying information given matches a single student, but the State Student Id specified as input does not match the official State Student Id of the matched student.
3001|(Multiple SSIDs found)|Student identifying information given matches multiple existing students.
3003|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Clean Last Name Initial, Clean First Name Initial, Birth Date and gender equal. Review needed.
3004|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Clean Last Name, Clean First Name equal. Exact match. Review needed.
3005|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Soundex of Clean Last Name, Soundex of Clean First Name, Gender, and Birth Date + or - 1 year. Review needed.
3006|(Possible Student Already Exists)|Student identifying information given does not match any students. However, the State Student Id is already in use by a non-matched student. Review needed.

**Response** 
```400: BAD REQUEST { “message”: “<error number> <error description><error details>” }```

Vendors will be expected to demonstrate a mechanism for timely reporting of ID creation errors back to users, either through the SIS user interface, or through a separate interface, or reporting method.

## Ed-Fi / MARSS Student Record Validation Test
When Student Records are created or updated in the Ed-Fi ODS, the API will perform a look up against the MN State Student ID System to determine whether the student is associated to a valid student id.

This validation feature will be enabled in the Staging Environment. Vendors must capture validation errors returned in the API response and surface these errors to district users. 

### Student Validation Process Overview

- SIS posts a new or updated Student record to the Ed-Fi API.
- The Ed-Fi student validator then calls the MDE Student ID System validation process with StateStudentId (StudentUniqueId), LastName, FirstName, BirthDate, and BirthSex.
  - If the MDE Student ID System returns 0 (Exact Match), the student identity matches all the information exactly and only a single student is found. The Ed-Fi API will allow the Student record to be stored in the ODS. The Ed-Fi API returns HTTP response code ```204```.
  - Any other return value from the MDE Student ID system validation process results in HTTP response code ```400 Bad Request```, which also passes back the error code and message from the MDE Student ID System. The SIS should present this error code and message to the district user, informing them of the Student ID issue which must be resolved in the MDE Student ID system.

#### Validate Student ID Test 1

**Description**: Vendor posts a new valid Ed-Fi Student record to the ODS/API Student end-point. Vendor submits Ed-Fi student record to the student’s resource endpoint using a valid student id and associated to the same student.

**Response** 
```201: created```

#### Validate Student ID Test 2

**Description**: Vendor posts a new Ed-Fi Student record to the ODS/API Student end-point for the following error conditions:
Error|Description|Details
---|---|---
3000|(Input SSID not equal SSID)|Student identifying information given matches a single student, but the State Student Id specified as input does not match the official State Student Id of the matched student.
3001|(Multiple SSIDs found)|Student identifying information given matches multiple existing students.
3002|(No match found)|Student identifying information given does not match any students. Also no possible suspect student matches found. (May be safe to add as a new student.)
3003|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Clean Last Name Initial, Clean First Name Initial, Birth Date and gender equal. Review needed.
3004|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Clean Last Name, Clean First Name equal. Exact match. Review needed.
3005|(Possible Student Already Exists)|Student identifying information given does not match any students. However suspect student matches found using Soundex of Clean Last Name, Soundex of Clean First Name, Gender, and Birth Date + or - 1 year. Review needed.
3006|(Possible Student Already Exists)|Student identifying information given does not match any students. However, the State Student Id is already in use by a non-matched student. Review needed.

**Response** 
- The Ed-Fi Student record is unable to post.
- An HTTP status code ```400 Bad Request``` and the corresponding message for the error given is returned from the ODS/API.
- Vendor Captures error and displays for district user

# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)

