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

Similarly, when a vendor takes the initiative to first check/validate against ```studentParentAssociation``` records, there’s the possibility for conflicting information to be overwritten on updates to parent records. In order to reduce the changes of that, MDE recommends that a parent ID be prefixed with a district number to avoid the overwriting and/or conflicts when trying an ID that’s in use elsewhere. We're aware that this will lead to more duplicates, but in our opinion that is preferable to overwrites.

Regardless of the specific implementations, non-unique parent records is a limitation of the system. MDE is not aware of any downstream impacts; for example, ``StudentEarlyEducationProgramAssociation`` is not validated against parent data.

## Managing Multiples for Student-Parent Relationships
When creating a ```Parent``` record, you might notice the ```identificationCodes``` descriptor, which should contain the MARSS ID of a related student. However, if a parent has several students with MARSS IDs, more than one code can be listed - as the Swagger UI reveals, these are identificationCode**s**, and that the descriptor is “An unordered collection of parentIdentificationCodes. Miscellaneous parent Identification Code. E.g., MARSS ID of a related student”. In other words, more than one code can be placed in that data element to handle a 1:M relationship.

## Duplicate "BR" value within accommodationDescriptors
When viewing SY2021 descriptors, you might note that the code value of “BR” is repeated within ```accommodationDescriptors```, causing problems with database loads that assume that code value is unique across all of those descriptors. However, when incorporating namespace, those values become unique: the value to describe "BR – Accomodation" is within “access” and the value for "Braille" is within "mcamtas", as shown in the descriptor JSON below (available from Swagger). Our contractor also notes that for now this descriptor can be ignored because it’s only used by assessment precode which isn’t in scope until at least SY21-22 or later.

```javascript
{
    "id": "9dc5618028ab4caf9bc336a7a0a962f1",
    "accommodationDescriptorId": 2996,
    "codeValue": "BR",
    "description": "BR - Accommodation",
    "namespace": "uri://education.mn.gov/access/AccommodationDescriptor",
    "shortDescription": "BR - Accommodation",
    "_etag": "5248795699641457904"
  },
  {
    "id": "916ef20130b74698ace01f5b559676ca",
    "accommodationDescriptorId": 2997,
    "codeValue": "BR",
    "description": "Braille",
    "namespace": "uri://education.mn.gov/mcamtas/AccommodationDescriptor",
    "shortDescription": "Braille",
    "_etag": "5248795699641457904"
  },
```