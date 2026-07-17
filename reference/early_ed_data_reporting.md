# Early Education Data Reporting
This document describes changes to how [Early Learning Services Data Reporting](https://education.mn.gov/MDE/dse/datasub/EarlyLearnServDataReport) is implemented as part of the transition from MDE's Early Education Student (EES) data collection system to Ed-Fi.

### ClassroomVolunteerDescriptor Mapping
 The table below provides a translation between the Early Education Student (EES) data collection and EdFi of how classroom volunteers are reported:
|     EES ParticipationCode    |     Description    |     EdFi Code    |     Value    |     Comments    |
|-|-|-|-|-|
|     00    |     Not Specified    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     01    |     Not Volunteering    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     02    |     Class Room Volunteer    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     03    |     Parent Advisory Council    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     99    |     Others    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |

### LevelOfEducationDescriptor Naming
The core Ed-Fi descriptor ```levelOfEducationDescriptor``` is implemented as ```highestCompletedLevelOfEducationDescriptor``` within the "parents" resource (the namespace remains ```uri://education.mn.gov/LevelOfEducationDescriptor```). This can be visualized in the example value for the "parents" resource:

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
### LevelOfEducationDescriptor Mapping
With one exception, the [LevelOfEducationDescriptor](https://pub.education.mn.gov/edfidocs/LevelOfEducationDescriptor.html) mapping is a direct translation from the _EducationBackground_ codes used in the Early Education Student (EES) data collection. For example, code value ```1050``` for Associate's degree. The only exception is that EE code ```0000``` for "Not Specified" should be mapped into Ed-Fi code ```9999``` for "Other". The following table details the translation:
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


There are also additional code values available in Ed-Fi for additional detail as applications evolve.

### Limiting Parent Data Submissions to Required Records
MDE is aware that vendors have access to parent records for students **not** participating in an Early Education program, i.e. through grade 12 in Ed-Fi. MDE requests that vendors and districts **withhold** those Parent records.

### Avoiding Conflicts in Parent Identifiers
Parent records are shared among and between Local Education Authorities (LEAs) like student records. Unlike student records, MDE does not have a system of uniquely identifying parents. That means that duplicate parent records are likely to be created.

Similarly, there's the possibility for conflicting information to be overwritten on updates to parent records if the same unique ID is used. In order to reduce the changes of that, MDE requires that a parent ID be prefixed with a district/organization number and dash (using the [Ed-Fi identifier conventions](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/sis_test_plan/sis_test_plan_b_cert_testing.md#minnesota-district-and-school-ids)), such as this:
- "10625000-" for [SPPS](https://pub.education.mn.gov/MdeOrgView/organization/show/566)
- "526095000-" for [AALASEC](https://pub.education.mn.gov/MdeOrgView/organization/show/14583)

This should help avoid mistakenly overwriting a record when using an ID that is in use elsewhere. We're aware that this will lead to more duplicates, but in our opinion that is preferable to overwrites.

Regardless of the specific implementations, non-unique parent records is a limitation of the system. MDE is not aware of any downstream impacts; for example, ``StudentEarlyEducationProgramAssociation`` is not validated against parent data.

### MARSS ID Not Collected for Parents
Within the Minnesota extension for the ```parents``` resource, the MDE team decided that the "MARSS ID (Parent)" element (i.e. "parentIdentificationCode") was redundant due to the fact that student-parent relationships are already available via studentParentAssociation records. Therefore, this element was excluded from the Ed-Fi Parents resource.

Historical note on managing multiples for student-parent relationships that applied before this decision:
> When creating a ```Parent``` record, you might notice the ```identificationCodes``` descriptor, which should contain the MARSS ID of a related student. However, if a parent has several students with MARSS IDs, more than one code can be listed - as the Swagger UI reveals, these are identificationCode**s**, and that the descriptor is "An unordered collection of parentIdentificationCodes. Miscellaneous parent Identification Code. E.g., MARSS ID of a related student". In other words, more than one code can be placed in that data element to handle a 1:M relationship.

### Student Early Childhood Screening Program Associations (SECSPA)
When working with MARSS, LEAs previously would enter in State Aid Categories with Early Childhood Screening. With Ed-Fi, EC screening is now recorded with a Student Early Childhood Screening Program Associations record, which does not carry State Aid Categories. Instead, it carries an ```earlyChildhoodScreenerDescriptor``` and a ```earlyChildhoodScreeningExitStatusDescriptor```. This created a question (see [issue #16](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/issues/16)) around the State Aid Category 41 of "Screening by School District". This code is no longer available as a State Aid Category; so for the SECSPA record, an LEA can choose a "PreSchoolScreenerDescriptor" code of 1, "Screening by serving school district".

