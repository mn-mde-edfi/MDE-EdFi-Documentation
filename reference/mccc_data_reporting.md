# Minnesota Common Course Catalog (MCCC) Data Reporting

### Course Records for MCCC
The Minnesota Common Course Catalogue (MCCC) data collection requires districts to create their course offerings (including college courses) and then relate those courses to state-level course definitions. This section contains details on those course record requirements.

#### SEA Defined Courses
Over 1700 State Education Agency (SEA - aka MDE) course definitions are available in all ODS instances, available for LEAs implementing the MCCC pilot.

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
    "careerPathwayDescriptor": "uri://education.mn.gov/CareerPathwayDescriptor#802",  /* for CTE courses */
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

Given those course records, districts will be able to relate local course records to SEA-defined courses via course-to-course association records. From there, student attendance, grades, etc can be submitted on the local courses. 

#### Course Data Elements and Validation
This section contains information about the Course resource, including data elements within it and specific validation scenarios we want vendors to be aware of. See the individual sections below. In addition:
 - Note that in the ```dateCourseAdopted``` element (aka "effectiveStartYear" from MCCC), the year must be less than or equal to the reporting year to be a valid code.
 - Vendors may notice the Ed-Fi core element ```offeredGradeLevels``` in the API as an optional component. MDE prefers that vendors specifically do **NOT** include this element when submitting MCCC data to MDE via Ed-Fi.
 - Vendors may also notice the mn extension element ```careerClusterDescriptor``` in the API as an optional component. This element is **only** used courses for defined by the SEA (MDE). Therefore, vendors have no reason to submit career cluster data for courses their customers are creating, and it can be omitted in submissions.

##### Level Characteristics
LEAs and vendors will need to understand the validation rules around course level characteristics (the "levelCharacteristics" collection on _course_) that are included on some SEA-defined courses. The following characteristics have rules*:
1. **UC - Unclassified Course Indicator**: when an LEA-defined course is associated with an SEA-defined course containing the 'UC' characteristic, a local course description must be entered within the ```courseDescription``` element.
2. **MM - Multiple Marks Indicator**: Validation on this relationship is performed via the grades that are assigned to students enrolled in these courses: When an LEA-defined course is associated with an SEA-defined course containing the 'MM' characteristic, the ```academicSubjectDescriptor``` must be used on the ```grade``` resource (for assigning multiple grades against different subject areas). Conversely, the ```academicSubjectDescriptor``` must **not** be used within a grade given for an LEA-defined course that is **not** associated with an SEA-defined 'MM' course.
3. **IS - Independent Study Indicator**: LEA-defined Independent Study courses must be associated with an SEA-defined course containing the 'IS' characteristic. Validation on this relationship is performed via ```studentSectionAssociations```, where the ```SectionEnrollmentTypeDescriptor``` must be **AI** (ALC_IND_STUDY).
4. **PBL - Project Based Learning Indicator**: LEA-defined Project Based courses must be associated with a PBL SEA-defined course. Validation on this relationship is performed via ``studentSectionAssociations``, where the ```SectionEnrollmentTypeDescriptor``` must be **PB** (PROJECT_BASED).

*It is important to note that UC, MM, IS, and PBL characteristics are **not actually carried** on the LEA-defined (District) course records. Instead, when they are associated the SEA-defined courses via ```courseCourseAssociation``` records, the validations should occur through other data elements, as described above. Getting the SEA-defined course records (see [SEA Defined Courses](#sea-defined-courses)) reveals which of those courses are assigned these level characteristics.

#### College Courses
When setting up College Courses (i.e. for Dual Enrollment, Articulation and Direct Pay PSEO), you will need an ```educationOrganizationId``` within the ```educationOrganizationReference```. The IDs to use in this element come from MDE ORG and follow the [district pattern](../sis_test_plan/sis_test_plan_b_cert_testing.md#minnesota-district-and-school-ids). The identifiers can be acquired via the API at the ```/ed-fi/postSecondaryInstitutions``` endpoint, within the ```postSecondaryInstitutionId``` element. Each record in that list will also contain a cross-reference to the USDE OPE IDs inside the ```educationOrganizationIdentificationSystemDescriptor```, labeled as ```uri://ed-fi.org/EducationOrganizationIdentificationSystemDescriptor#USDE - OPE```. 

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

As referenced in the [certification scenario for class period](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/sandbox_cert/sandbox_cert_e_mccc.md#resource-classperiod), class periods should be named uniquely enough to fit your scheduling needs, and each one should only have one set of meeting times. And as described in the [section scenario](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/sandbox_cert/sandbox_cert_e_mccc.md#resource-section), a 1:M relationship between section and class periods is allowed. Therefore, the following partial JSON examples for class periods and a single section detail how a modified block schedule could work for a single class that meets all days of the week. (You may need more or less detail in the names used to identify individual elements uniquely.)

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