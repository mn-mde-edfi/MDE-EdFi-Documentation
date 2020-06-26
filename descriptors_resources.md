# Descriptors and Resources
This document will store various knowledge items and articles about the MDE Ed-Fi ODS/API, especially with respect to Minnesota extensions and customizations that differ from the Core Ed-Fi Data Standard and ODS/API.

## Naming Pattern for Extension Descriptors
When MDE extends a pre-existing Ed-Fi descriptor for the MN extension, it renames the implementation of that desriptor within specific resources. For example, the [core Ed-Fi descriptor](https://api.ed-fi.org/v3.4.0/docs/index.html?urls.primaryName=Descriptors#/levelOfEducationDescriptors) ```levelOfEducationDescriptors``` is implemented as ```highestCompletedLevelOfEducationDescriptor``` within the "parents" resource (the namespace remains ```uri://education.mn.gov/LevelOfEducationDescriptor```). This can be visualized in the example value for the "parents" resource:

```javascript
{
  "id": "string",
  "parentUniqueId": "string",
  "firstName": "string",
  "generationCodeSuffix": "string",
  "lastSurname": "string",
  "middleName": "string",
  "sexDescriptor": "string",
  "_etag": "string",
  "_ext": {
    "MN": {
      "classroomVolunteerDescriptor": "string",
      "highestCompletedLevelOfEducationDescriptor": "string",
      "birthDate": "1985-10-26",
      "householdIncome": 0,
      "householdSize": 0,
      "receivingInterpreterAssistance": true,
      "identificationCodes": [
        {
          "identificationCode": "string"
        }
      ]
    }
  }
}
```