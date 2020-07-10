# Descriptors and Resources
This document will store various knowledge items and articles about the MDE Ed-Fi ODS/API, especially with respect to Minnesota extensions and customizations that differ from the Core Ed-Fi Data Standard and ODS/API.

## Naming Pattern for Extension Descriptors
When MDE extends a pre-existing Ed-Fi descriptor for the MN extension, it may rename the implementation of that descriptor when additional context clarifies the intended use of the descriptor. For example, the [core Ed-Fi descriptor](https://api.ed-fi.org/v3.4.0/docs/index.html?urls.primaryName=Descriptors#/levelOfEducationDescriptors) ```levelOfEducationDescriptors``` is implemented as ```highestCompletedLevelOfEducationDescriptor``` within the "parents" resource (the namespace remains ```uri://education.mn.gov/LevelOfEducationDescriptor```). This can be visualized in the example value for the "parents" resource:

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

## Avoiding Conflicts for Parent Resources
**Parent** records are shared among and between Local Education Authorities (LEAs) like student records. But unlike student records, MDE does not have a system of uniquely identifying parents. That means that duplicate parent records are likely to be created.

Similarly, when a vendor has access to multiple district ```studentParentAssociation``` records (_and_ takes the initiative to first check/validate against those records), there’s the possibility for conflicting information to be overwritten on updates to parent records. In order to reduce the changes of that, MDE recommends that a parent ID be prefixed with a district number to avoid the overwriting and/or conflicts when trying an ID that’s in use elsewhere. We're aware that this will lead to more duplicates, but in our opinion that is preferable to overwrites.

Regardless of the specific implementations, non-unique parent records is a limitation of the system. MDE is not aware of any downstream impacts; for example, ``StudentEarlyEducationProgramAssociation`` is not validated against parent data.

## Managing Multiples for Student-Parent Relationships
When creating a ```Parent``` record, you might notice the ```identificationCodes``` descriptor, which should contain the MARSS ID of a related student. However, if a parent has several students with MARSS IDs, more than one code can be listed - as the Swagger UI reveals, these are identificationCode**s**, and that the descriptor is “An unordered collection of parentIdentificationCodes. Miscellaneous parent Identification Code. E.g., MARSS ID of a related student”. In other words, more than one code can be placed in that data element to handle a 1:M relationship.
