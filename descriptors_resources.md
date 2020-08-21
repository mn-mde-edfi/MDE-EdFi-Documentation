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
More information on the levelOfEducationDescriptor [is in this section](#levelofeducationdescriptors).

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

## Parent Resources
This section contains various details and decisions on **Parent Resources** that have arisen with the EE rollout, particularly in response to vendor questions.

### Limiting Submissions to Required Records
MDE is aware that vendors have access to parent records for students **not** participating in an Early Education program, i.e. through grade 12 in Ed-Fi. As of July 31, 2020, MDE requests that vendors and districts **withhold** those Parent records.

### Avoiding Conflicts in Identifiers
Parent records are shared among and between Local Education Authorities (LEAs) like student records. But unlike student records, MDE does not have a system of uniquely identifying parents. That means that duplicate parent records are likely to be created.

Similarly, there’s the possibility for conflicting information to be overwritten on updates to parent records if the same unique ID is used. In order to reduce the changes of that, MDE is strongly recommending that a parent ID be prefixed with a district/organization number and dash, such as this:
- "10625000-" for [SPPS](https://public.education.mn.gov/MdeOrgView/organization/show/566)
- "526095000-" for [AALASEC](https://public.education.mn.gov/MdeOrgView/organization/show/14583)

This should help avoid mistakenly overwriting a record when using an ID that is in use elsewhere. We're aware that this will lead to more duplicates, but in our opinion that is preferable to overwrites.

Regardless of the specific implementations, non-unique parent records is a limitation of the system. MDE is not aware of any downstream impacts; for example, ``StudentEarlyEducationProgramAssociation`` is not validated against parent data.

### Dropping API Requirements for ext-MN-identificationCodes
Within the Minnesota extension for the ```parents``` resource, the MDE team decided on July 24, 2020 that the "MARSS ID (Parent)" element (i.e. "parentIdentificationCode") was redundant due to the fact that student-parent relationships are already available via studentParentAssociation records. Therefore requirements for this element will be dropped from the ODS API as soon as possible. The location of this specific data element within the JSON of a specific Parent resource is below:
```javascript
"_ext": {
    "MN": {
      "classroomVolunteerDescriptor": "string",
      "highestCompletedLevelOfEducationDescriptor": "string",
      "birthDate": "2020-07-24",
      "householdIncome": 0,
      "householdSize": 0,
      "receivingInterpreterAssistance": true,
      "identificationCodes": [ //This section is no longer needed as of 2020.07.24
        {
          "identificationCode": "string"
        }
      ]
    }
  }
```

Historical note on managing multiples for student-parent relationships that applied before this decision:
> When creating a ```Parent``` record, you might notice the ```identificationCodes``` descriptor, which should contain the MARSS ID of a related student. However, if a parent has several students with MARSS IDs, more than one code can be listed - as the Swagger UI reveals, these are identificationCode**s**, and that the descriptor is “An unordered collection of parentIdentificationCodes. Miscellaneous parent Identification Code. E.g., MARSS ID of a related student”. In other words, more than one code can be placed in that data element to handle a 1:M relationship.

## ClassroomVolunteerDescriptors
In the transition to Ed-Fi, MDE is collecting less detail around classroom volunteers compared to past collections in the [Early Education Student Data System](https://education.mn.gov/MDE/dse/datasub/EarlyLearnServDataReport). The table below provides a translation between EES and EdFi:
|     EES ParticipationCode    |     Description    |     EdFi Code    |     Value    |     Comments    |
|-|-|-|-|-|
|     00    |     Not Specified    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     01    |     Not Volunteering    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     02    |     Class Room Volunteer    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     03    |     Parent Advisory Council    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     99    |     Others    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |

## LevelOfEducationDescriptors
Another descriptor in Ed-Fi that benefits from a translation from EES is **levelOfEducationDescriptors**. As of 8/6, the ODS endpoints now include the MDE-specific descriptors listed in the LevelOfEducationDescriptor tab of the 2020-21 Data Mapping spreadsheet. With one exception, these values are a direct translation from the _EducationBackground_ codes used in the EE system. For example, code value ```1050``` for Associate's degree. The only exception is that EE code ```0000``` for "Not Specified" should be mapped into Ed-Fi code ```9999``` for "Other". The following table details the translation:
|EES BackgroundCode|EES BackgroundShortName|Ed-Fi levelOfEducationDescriptorId|Ed-Fi codeValue|Ed-Fi description|
|---|----|-------|------|---|
|0000              |Not Specified          |3403                              |9999           |09999 - Other                                     |
|0798              |8th grade              |3397                              |798            |00798 - Eighth grade                              |
|1044              |HS Diploma             |3381                              |1044           |01044 - High school diploma                       |
|1049              |Some College           |3382                              |1049           |01049 - Some college but no degree                |
|1050              |Associate degree       |3383                              |1050           |01050 - Associate's degree (two years or more)    |
|1051              |Bachelor degree        |3384                              |1051           |01051 - Bachelor's (Baccalaureate) degree         |
|1054              |Master's degree        |3385                              |1054           |01054 - Master's degree (e.g., M.A., M.S.,etc.)   |
|1057              |Doctoral degree        |3386                              |1057           |01057 - Doctoral (Doctor's) degree                |
|1809              |12th grade             |3387                              |1809           |01809 - 12th grade, no diploma                    |
|2409              |GED                    |3388                              |2409           |02409 - High school equivalency (e.g., GED)       |


The following codes are also available in Ed_Fi for additional detail as applications evolve:
|Ed-Fi levelOfEducationDescriptorId|Ed-Fi codeValue|Ed-Fi description|
|----|----|----|
|3380                              |1043           |01043 - No school completed   |
|3389                              |788            |00788 - Preschool             |
|3390                              |790            |00790 - First grade           |
|3391                              |791            |00791 - Second grade          |
|3392                              |792            |00792 - Third grade           |
|3393                              |793            |00793 - Fourth grade          |
|3394                              |794            |00794 - Fifth grade           |
|3395                              |795            |00795 - Sixth grade           |
|3396                              |796            |00796 - Seventh grade         |
|3398                              |799            |00799 - Ninth grade           |
|3399                              |800            |00800 - Tenth grade           |
|3400                              |801            |00801 - Eleventh Grade        |
|3401                              |805            |00805 - Kindergarten          |
|3402                              |819            |00819 - Career and Technical Ed. cert.|

Note that the namespace for the above descriptors is ```uri://education.mn.gov/LevelOfEducationDescriptor```. Prior to **8/6/2020**, MDE Ed-Fi data stores (including Sandboxes created before that date) only included the base ed-fi descriptors in the ```uri://ed-fi.org/LevelOfEducationDescriptor``` namespace, which created confusion among vendors. These should **NOT** be used. Vendors should create new sandboxes to test this functionality and delete any created before 8/6.

## Supplemental Program Names
ODS-API users will note that the sy21 sandbox contains sample records for ```programs```, described as "any program designed to work in conjunction with, or as a supplement to, the main academic program." These programs are set primarily for Early Education (EE), but 16 types have been set up in the programTypeDescriptors for use. Sample JSON is available in the sandbox to view examples of programs that districts can load into Ed-Fi. As of 8/21/2020, MDE is currently determining guidance on naming these programs via the ```programName``` element.