# Descriptors and Resources
This document will store various knowledge items and articles about the MDE Ed-Fi ODS/API, especially with respect to Minnesota extensions and customizations that differ from the Core Ed-Fi Data Standard and ODS/API.

## Descriptors
Sections below will have additional information about various descriptors.

### Naming Pattern for Extension Descriptors
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

### Multiple Use Descriptors
Since some descriptors are used for multiple data elements, within the ODS API there are often data elements that use a descriptor, but do not match precisely the name of the descriptor that is used. For example:
- Within the Language Academic Honors collection (inside ```studentEducationOrganizationAssociation```), there is an ```assessedGradeLevelDescriptor```. Use the GradeLevelDescriptor values for this element.  
- Within the for Neglected or Delinquent collection, there are elements titled ``elaProgressLevelDescriptor`` and ``mathematicsProgressLevelDescriptor``. Use the ProgressLevelDescriptor values for this element.


Usually the required relationship can be found within the Data Mapping Matrix. Vendors that spot any discrepancies or missing elements are encouraged to contact the [Ed-Fi vendor support team](mailto:EdFiProjectSupportMNIT.MDE@state.mn.us) by email. 

### Duplicate "BR" value within accommodationDescriptors
When viewing SY2021 descriptors, you might note that the code value of "BR" is repeated within ```accommodationDescriptors```, causing problems with database loads that assume that code value is unique across all of those descriptors. However, when incorporating namespace, those values become unique: the value to describe "BR – Accomodation" is within "access" and the value for "Braille" is within "mcamtas", as shown in the descriptor JSON below (available from Swagger). Note that for now this descriptor can be ignored because it's only used by assessment precode which isn't in scope until at least SY22-23 or later.

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

### ClassroomVolunteerDescriptors
In the transition to Ed-Fi, MDE is collecting less detail around classroom volunteers compared to past collections in the [Early Education Student Data System](https://education.mn.gov/MDE/dse/datasub/EarlyLearnServDataReport). The table below provides a translation between EES and EdFi:
|     EES ParticipationCode    |     Description    |     EdFi Code    |     Value    |     Comments    |
|-|-|-|-|-|
|     00    |     Not Specified    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     01    |     Not Volunteering    |     NA    |     NA    |     Do not submit this record to Ed-Fi    |
|     02    |     Class Room Volunteer    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     03    |     Parent Advisory Council    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |
|     99    |     Others    |     **2861**    |     PartTimeVolunteer    |     Code **2860** for FullTimeVolunteer is also available if necessary    |

### LevelOfEducationDescriptors
Another descriptor in Ed-Fi that benefits from a translation from EES is **levelOfEducationDescriptors**. As of 8/6/2020, the ODS endpoints now include the MDE-specific descriptors listed in the LevelOfEducationDescriptor tab of the 2020-21 Data Mapping spreadsheet. With one exception, these values are a direct translation from the _EducationBackground_ codes used in the EE system. For example, code value ```1050``` for Associate's degree. The only exception is that EE code ```0000``` for "Not Specified" should be mapped into Ed-Fi code ```9999``` for "Other". The following table details the translation:
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

### Student Characteristic Descriptors
Note that several changes have been implemented in the Student Characteristic Desciprtors for sy2023. This section will make note of specific issues with this descriptor.

#### Migrant Descriptor value
A vendor asked about the "Migrant" descriptor; while we do not collect the Migrant indicator through Ed-Fi, we do collect that information via other sources, which is populated in the Ed-Fi ODS. As a result, the Migrant indicator was added as a read-only attribute in the Ed-Fi API to allow SIS vendors to be able to read this information and display it to district users in their SIS. This was implemented back in our first year of Ed-Fi for 2018-19. 

## Resources
The following sections contain details about various resources (also called "entities" in some documentation) within the Ed-Fi API and data model.

### Parent Resources
This section contains various details and decisions on **Parent Resources** that have arisen with the EE rollout, particularly in response to vendor questions.

#### Limiting Submissions to Required Records
MDE is aware that vendors have access to parent records for students **not** participating in an Early Education program, i.e. through grade 12 in Ed-Fi. As of July 31, 2020, MDE requests that vendors and districts **withhold** those Parent records.

#### Avoiding Conflicts in Identifiers
Parent records are shared among and between Local Education Authorities (LEAs) like student records. But unlike student records, MDE does not have a system of uniquely identifying parents. That means that duplicate parent records are likely to be created.

Similarly, there’s the possibility for conflicting information to be overwritten on updates to parent records if the same unique ID is used. In order to reduce the changes of that, MDE is requiring that a parent ID be prefixed with a district/organization number and dash (using the [Ed-Fi identifier conventions](sis_test_plan_b_cert_testing.md#minnesota-district-and-school-ids)), such as this:
- "10625000-" for [SPPS](https://public.education.mn.gov/MdeOrgView/organization/show/566)
- "526095000-" for [AALASEC](https://public.education.mn.gov/MdeOrgView/organization/show/14583)

This should help avoid mistakenly overwriting a record when using an ID that is in use elsewhere. We're aware that this will lead to more duplicates, but in our opinion that is preferable to overwrites.

Regardless of the specific implementations, non-unique parent records is a limitation of the system. MDE is not aware of any downstream impacts; for example, ``StudentEarlyEducationProgramAssociation`` is not validated against parent data.

#### Dropping API Requirements for ext-MN-identificationCodes
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
> When creating a ```Parent``` record, you might notice the ```identificationCodes``` descriptor, which should contain the MARSS ID of a related student. However, if a parent has several students with MARSS IDs, more than one code can be listed - as the Swagger UI reveals, these are identificationCode**s**, and that the descriptor is "An unordered collection of parentIdentificationCodes. Miscellaneous parent Identification Code. E.g., MARSS ID of a related student". In other words, more than one code can be placed in that data element to handle a 1:M relationship.

### Supplemental Program Names
ODS-API users will note that the sy21 sandbox contains sample records for ```programs```, described as "any program designed to work in conjunction with, or as a supplement to, the main academic program." These programs are set primarily for Early Education (EE), but 16 types have been set up in the programTypeDescriptors for use. Sample JSON is available in the sandbox to view examples of programs that districts can load into Ed-Fi. As of 8/21/2020, MDE is currently determining guidance on naming these programs via the ```programName``` element.

### Student Early Childhood Screening Program Associations (SECSPA)
When working with MARSS, LEAs previously would enter in State Aid Categories with Early Childhood Screening. With Ed-Fi, EC screening is now recorded with a Student Early Childhood Screening Program Associations record, which does not carry State Aid Categories. Instead, it carries an ```earlyChildhoodScreenerDescriptor``` and a ```earlyChildhoodScreeningExitStatusDescriptor```. This created a question (see [issue #16](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/issues/16)) around the State Aid Category 41 of "Screening by School District". This code is no longer available as a State Aid Category; so for the SECSPA record, an LEA can choose a "PreSchoolScreenerDescriptor" code of 1, "Screening by serving school district".

### Student Special Education Program Associations Resource
#### Placing Local Education Agency Reference
For SY2021-2022, MDE implemented a new element on the StudentSpecialEducationProgramAssociations resource called ```placingLocalEducationAgencyReference ```. Commonly referred to as "Placing District", this optional element is intended for only students with IEPs who are enrolled in a joint powers or intermediate district. It is intended for a subset of students, and should not be automatically associated with any other LEA reference.

The scenario in which a student record would need ```placingLocalEducationAgencyReference ``` is:
- Student is a resident of district A and has an IEP.
- The student open enrolls to district B.
- District B places the student in a joint powers or intermediate district C.

In this scenario:
- A is the resident district
- B is probably the transporting district
- B is the placing district (should be a district type of 1, 2, 3 or 7)
- C is the enrolling/serving district

### Course Records for MCCC
The Minnesota Common Course Catalogue (MCCC) data collection requires districts to create their course offerings (including college courses) and then relate those courses to state-level course definitions. This section contains details on those course record requirements.

#### SEA Defined Courses
Over 1700 State Education Agency (SEA - aka MDE) course definitions are available in the populated sandbox and will be available in Staging and Production.

To get the list of SEA-defined courses, perform a GET operation against the "courses" endpoint, setting the parameter _courseDefinedByDescriptor_ equal to _uri://education.mn.gov/CourseDefinedByDescriptor#SEA_. In an HTTP request this will be escaped as: ```courseDefinedByDescriptor=uri%3A%2F%2Feducation.mn.gov%2FCourseDefinedByDescriptor%23SEA```. An example JSON value for an SEA-defined course is below:

```javascript
{
    "id": "b13d0939aabb450f9e21226dce836364",
    "educationOrganizationReference": {
      "educationOrganizationId": 999999000,
      "link": {
        "rel": "StateEducationAgency",
        "href": "/ed-fi/stateEducationAgencies/ed87f88ff6cc4d088ea42d638e051551"
      }
    },
    "courseCode": "10001",
    "courseDefinedByDescriptor": "uri://education.mn.gov/CourseDefinedByDescriptor#SEA",
    "courseDescription": "Courses introduce computers and peripheral devices, the functions and uses of computers, the language used in the computer industry, and computer applications. They typically explore legal and ethical issues associated with computer use, as well as how computers influence modern society. Students may also be required to perform some computer operations.  Careers related to computer hardware and software are often investigated.",
    "courseTitle": "Introduction to Computers",
    "dateCourseAdopted": "2011-01-01",
    "numberOfParts": 0,
    "_ext": {
      "mn": {
        "assessmentTools": [],
        "curriculumUseds": [],
        "levelTypes": [],
        "programs": []
      }
    },
    "identificationCodes": [],
    "learningStandards": [],
    "levelCharacteristics": [],
    "offeredGradeLevels": [],
    "_etag": "5248797570484187904"
  }

```

Given those course records, districts will be able to relate local course records to SEA-defined courses via course-to-course association records. From there, student attendance, grades, etc can be submitted on the local courses. __Note:__ As of April 12, 2021, MDE and its contractors identified an issue with the levelCharacteristics of courses loaded into the 2021-2022 Sandboxes, which was rectified on April 29,2021. Sandboxes created before that date will have extra characteristics on the SEA courses.

#### Course Data Elements and Validation
This section contains information about the Course resource, including data elements within it and specific validation scenarios we want vendors to be aware of. See the individual sections below. In addition:
 - Note that in the ```dateCourseAdopted``` element (aka "effectiveStartYear" from MCCC), the year must be less than or equal to the reporting year to be a valid code.
 - Vendors may notice the Ed-Fi core element ```offeredGradeLevels``` in the API as an optional API. MDE prefers that vendors specifically do **NOT** include this element when submitting MCCC data to MDE via Ed-Fi.

##### Level Characteristics
LEAs and vendors will need to understand the validation rules around course level characteristics (the "levelCharacteristics" collection on _course_) that are included on some SEA-defined courses. The following characteristics have rules*:
1. **UC - Unclassified Course Indicator**: when an LEA-defined course is associated with an SEA-defined course containing the 'UC' characteristic, a local course description must be entered within the ```courseDescription``` element.
2. **MM - Multiple Marks Indicator**: Validation on this relationship is performed via the grades that are assigned to students enrolled in these courses: When an LEA-defined course is associated with an SEA-defined course containing the 'MM' characteristic, the ```academicSubjectDescriptor``` must be used on the ```grade``` resource (for assigning multiple grades against different subject areas). Conversely, the ```academicSubjectDescriptor``` must **not** be used within a grade given for an LEA-defined course that is **not** associated with an SEA-defined 'MM' course.
3. **IS - Independent Study Indicator**: LEA-defined Independent Study courses must be associated with an SEA-defined course containing the 'IS' characteristic. Validation on this relationship is performed via ```studentSectionAssociations```, where the ```SectionEnrollmentTypeDescriptor``` must be **AI** (ALC_IND_STUDY).
4. **PBL - Project Based Learning Indicator**: LEA-defined Project Based courses must be associated with a PBL SEA-defined course. Validation on this relationship is performed via ``studentSectionAssociations``, where the ```SectionEnrollmentTypeDescriptor``` must be **PB** (PROJECT_BASED).

*It is important to note that UC, MM, IS, and PBL characteristics are **not actually carried** on the LEA-defined (District) course records. Instead, when they are associated the SEA-defined courses via ```courseCourseAssociation``` records, the validations should occur through other data elements, as described above. Getting the SEA-defined course records (see [SEA Defined Courses](#sea-defined-courses)) reveals which of those courses are assigned these level characteristics.

#### sequenceLimit vs. Number of Parts
In April 2021, MDE staff determined that our Ed-Fi implementation contains redundant elements in the "course" entity: numberOfParts (Ed-Fi core) and sequenceLimit (MN extension). In order to increase alignment with core Ed-Fi components, we decided to remove the use of sequenceLimit and rely on numberOfParts for the same information.

#### College Courses
When setting up College Courses (i.e. for Dual Enrollment, Articulation and Direct Pay PSEO), you will need an ```educationOrganizationId``` within the ```educationOrganizationReference```. The IDs to use in this element come from MDE ORG and follow the [district pattern](sis_test_plan_b_cert_testing.md#minnesota-district-and-school-ids). The identifiers can be acquired via the API at the ```/ed-fi/postSecondaryInstitutions``` endpoint, within the ```postSecondaryInstitutionId``` element. Each record in that list will also contain a cross-reference to the USDE OPE IDs inside the ```educationOrganizationIdentificationSystemDescriptor```, labeled as ```uri://ed-fi.org/EducationOrganizationIdentificationSystemDescriptor#USDE - OPE```. 

_Note_: Sandboxes created before May 7, 2021 had only approximately 12 post-secondary institutions loaded in. Sandboxes created on or after May 7 will have at least 100 records for testing. In development, staging, and production servers, records will be updated during regular synch processes.

### Section Enrollment Type Descriptor for MCCC
MCCC uses the Section enrollment Type Descriptor to handle what was previously called _Student Record Type_. The Ed-Fi implementation uses this descriptor on the student section association. The table below "maps" the MCCC student record types to the Ed-Fi descriptor code values.

|     MCCC Code    |     Student Record Type    |     EdFi Code    |     Ed-Fi Description    |     Comments    |
|-|-|-|-|-|
|1|ScheduledStudentRecord  |SC|SCHEDULED|-|
|2|ProjectStudentRecord|PB|PROJECT_BASED|-|
|3|IndependentStudyStudentRecord|AI|ALC_IND_STUDY |Use as needed for independent study|
|4|DirectPayStudentRecord|DP|DIRECT_PAY_PSEO|-|
|NA|NA|OP |OFFSITE_PSEO |Do not use|

### Complex Class Schedules for MCCC
A vendor raised a question about how a complex "modified block" schedule should be set up within Minnesota's Ed-Fi implementation for MCCC. The scenario in question:
>A 5-day cycle has 4 blocks per day Monday thru Thursday; Monday and Wednesday are "A days", Tuesday and Thursday are "B days". Some courses use both types of day, some use only one. On Friday all courses meet for only a "skinny" half block of time.

>A Days: periods 1-4 (block length)
>B Days: periods 5-8 (block length)
>AB Day (Friday): periods 1-8 (skinny length)

As referenced in the [certification scenario for class period](sandbox_cert_e_mccc.md#resource-classperiod), class periods should be named uniquely enough to fit your scheduling needs, and each one should only have one set of meeting times. And as described in the [section scenario](sandbox_cert_e_mccc.md#resource-section), a 1:M relationship between section and class periods is allowed. Therefore, the following partial JSON examples for class periods and a single section detail how a modified block schedule could work for a single class that meets all days of the week. (You may need more or less detail in the names used to identify individual elements uniquely.)

_Please note: MCCC does not **require** data replicating the complex schedules in place at many schools. If a single simplified & representative schedule can be set up and used for reporting to MCCC, that is acceptable - as long as it accurately communicates the **time of day** instruction is provided for the course._

#### Class Periods
Notice the naming of the class periods and their meeting times. 

##### A Day
``` JSON
{
  "classPeriodName": "ADayBlockPeriod4",
  "schoolReference": {
    "schoolId": 10621070,
  },
  "meetingTimes": [
    {
      "startTime": "13:00", 
      "endTime": "14:30"
    }
  ],
...//additional required elements here
}

```

##### B Day
``` JSON
{
  "classPeriodName": "BDayBlockPeriod8",
  "schoolReference": {
    "schoolId": 10621070,
  },
  "meetingTimes": [
    {
      "startTime": "13:00", 
      "endTime": "14:30"
    }
  ],
...//additional required elements here
}
```

##### AB Day
``` JSON
{
  "classPeriodName": "ABDayBlockPeriod16",
  "schoolReference": {
    "schoolId": 10621070,
  },
  "meetingTimes": [
    {
      "startTime": "13:45", 
      "endTime": "14:30"
    }
  ],
...//additional required elements here
}
```
#### Section Record
Notice this section uses three different class periods because it meets every day of the week.
```JSON
{
  "sectionIdentifier": "Section36",
  ...//additional required elements here
  "classPeriods": [
    {
      "classPeriodReference": {
        "classPeriodName": "ADayBlockPeriod4",
        "schoolId": 10621070,
      }
    },
    {
      "classPeriodReference": {
        "classPeriodName": "BDayBlockPeriod8",
        "schoolId": 10621070,
      }
    },
    {
      "classPeriodReference": {
        "classPeriodName": "ABDayBlockPeriod16",
        "schoolId": 10621070,
      }
    }
  ],
  ...//additional required elements here
}
```