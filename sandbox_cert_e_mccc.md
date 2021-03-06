# MCCC Certification Scenarios - API Resources
The Minnesota Common Course Catalog (MCCC) is a course classification and data collection system intended to provide uniform information about courses that are taught by Minnesota teachers and completed by Minnesota students. This document contains sandbox certification scenarios for this collection.

## Resource: Students

### Description

This entity represents an individual for whom instruction, services, and/or care are provided in an early childhood, elementary, or secondary educational program under the jurisdiction of a school, education agency, or other institution or program. A student is a person who has been enrolled in a school or other educational institution.

### Prerequisite Data

- None

### Scenarios

1. Create 12 student records including the following elements.
    - studentUniqueID
    - birthdate
    - birthSexDescriptor
    - firstName
    - generationCodeSuffix
    - lastSurname
    - middleName

## Resource: StudentSchoolAssociations

### Description

This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation.

### Prerequisite Data

- Students
- Schools

### Scenarios

1. Enroll the 12 students (spread across elementary, middle and high school)

## Resource: StudentEducationOrganizationAssociation

### Description

This association indicates any relationship between a student and an education organization other than how the state views enrollment. Enrollment relationship semantics are covered by StudentSchoolAssociation.

MDE allows for the capture of student demographic data by school enrollment. Therefore, a StudentEducationOrganizationAssociation record must be submitted for each **school** in which the student is enrolled to provide the student demographic data provided to the enrolling school by the parent(s).

### Prerequisite Data

- Students
- EducationOrganizations (Schools)

### Scenarios

1. Create StudentEducationOrganizationAssociation records for each of the students

## Resource: Calendar

### Description

Ed-Fi Description: A set of dates associated with an organization. **MDE is not using the Calendar entity as collection of dates**, rather MDE captures the following key pieces of Calendar Metadata in the Calendar file: Instructional Days, Length of Day, and Kindergarten Schedule (when applicable). Calendar is captured at the School Level by grade.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create MCCC Calendar for elementary, middle and high schools including:
    - Calendar Code
    - School ID
    - School Year
    - CalendarType = 'MCCC'
    - Days In Session
    - Instructional Days
    - Description

**MARSS**
See also the [Resource:Calendar section of the MARSS Certification Scenarios](sandbox_cert_b_marss.md#resource-calendar).

## Resource: CalendarDate

### Description

Ed-Fi Description: The type of scheduled or unscheduled event for the day. MDE will be collecting the MCCC ScheduleInfo Start and End Dates using Calendar Date.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Calendar

### Scenarios

1. Create 2 Calendar Dates for each of the 3 calendars. Both Dates should reference the MCCC Calendar created above.
    - Date 1 – calendarEventDescriptor = STARTDT
    - Date 2 – calendarEventDescriptor = ENDDT

## Resource: ClassPeriod

### Description

Ed-Fi Description: This entity represents the designation of a regularly scheduled series of class meetings at designated times and days of the week. MDE will be collecting the MCCC PeriodInfo Data in this resource. This data must be submitted for each school.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create a series of Class Periods for elementary, middle and high school. Each Period must include:
    - ClassPeriodName
    - ClassPeriodDescriptor
    - SchoolID
    - ClassPeriodDescription
    - StartTime
    - EndTime

## Resource: GradingPeriod

### Description

Ed-Fi Description: This entity represents the time span for which grades are reported. MCCC collection in Ed-Fi requires the creation of GradingPeriods in order to allow submission of grades. Grading Periods are defined at the School Level.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create a series of GradingPeriods for elementary, middle and high school. Each Period must include:
    - GradingPeriodDescriptor
    - PeriodSequence
    - SchoolId
    - SchoolYear
    - BeginDate
    - EndDate

## Resource: Session

### Description

Ed-Fi Description: A term in the school year, generally a unit of time into which courses are scheduled, instruction occurs and by which credits are awarded. Sessions may be interrupted by vacations or other events. The MCCC collection in Ed-Fi will use Session for collection of TermInfo.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create Sessions for elementary, middle and high school (Fall, Spring, and non-scheduled). Each Period must include:
    - TermDescriptor (S for Semester, NS for non-scheduled)
    - School Year
    - SchoolId
    - DaysInSession
    - TotalInstructionalDays
    - SessionName
    - BeginDate
    - EndDate
    - TermNumber

## Resource: Course

### Description

Ed-Fi Description: This educational entity represents the organization of subject matter and related learning experiences provided for the instruction of students on a regular or systematic basis. The MCCC collection in Ed-Fi will use Course for collection of District, College and State Courses.

**Important Note on College Course Codes:** To ensure uniqueness, the College Course Code must include a district’s LocalEducationAgencyId followed by a hyphen with no spaces, then followed by the College’s Course Identifier for that course. For example, an college course code submitted by Saint Paul Public School District would be submitted as ```10625000-ENG1000```.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- State Courses (published to ODS by MDE)

### Scenarios

1. Create 8 **District** Courses (set up at least 1 course per school type – Elementary, Middle and High School)
    - Course 1 Course Level Type = B
    - Course 2 Course Level Type = G
    - Course 3 Course Level Type = E
    - Course 4 Course Level Type = D
    - Course 5 Course Level Type = A
    - Course 6 Course Level Type = C
    - Course 7 Course Level Type = X
    - Course 8 Course Level Type = N

Including the following elements:
  - CourseDescription (only when associated with an Unclassified State Course)
  - HighSchoolCourseRequirement
  - CourseLevelCharacteristic for End of Course Indicator
  - Course Code (Local)
  - SequenceLimit
  - LocalEducationAgencyId
  - CourseTitle
  - CourseDefinedByDescriptorId = "LEA"
  - CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
  - CourseIdentificationSystemDescriptor = "LEA course code"
  - _LearningStandardid_ (not currently required)

2. Create an EE District Course
 Elements that must have valid values:
    - Course Description (only required when associated with Unclassified State Course)
    - Course Code (local)
    - Course level Type (P)
    - Sequence Limit (1)
    - StandardId (State)
    - High School Course Requirement (False)
    - **Must NOT include CourseLevelCharacteristic for End of Course Indicator**
    - CurriculumUsed
      - CurriculumUsedDescriptor (CRCUE, HWOT)
      - ImplementationStatusDescriptor (FULL, CEXP)
    - AssessmentTool
      - AssessmentToolDescriptor
      - ImplementationStatusDescriptor
    - CourseDefinedByDescriptorId = 'LEA'
      - CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
      - CourseIdentificationSystemDescriptor = 'LEA course code'
    - LearningStandardid (99.E5.1)

3. District Courses to associate with College courses
    - Create additional District courses to be associated with college course levels D and A
4. Create **College** Courses
    - 1 with Course Level Type = D
    - 1 with Course Level Type = A
    - 2 college courses to be used for Direct Pay PSEO, including the following elements:
      - PostSecondaryInstitutionId
      - MaximumAvailableCredits
      - CourseCode (College Course Identifier – generally dept letters & course number)
      - CourseTitle
      - CourseDefinedByDescriptorId = 'College'
      - CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
      - CourseIdentificationSystemDescriptor = 'University course code'

5. Create a District Course for Independent Study

**NOTE:** Independent Study course section enrollments did not previously require the setup of a course section – the Ed-Fi Model enforces the full set of master schedule entities (course, course offering and section) in order to associate a student with a course and record grades for that course.

Separate course, course offering and section records are required for your district to report ALC Independent Study records; however Course Offering and Section will not be used by MDE for reporting. (The Ed-Fi Model requires an entry in Course Offering linked to the non-scheduled term, and a section default.)

Include the following elements:
  - CourseLevelCharacteristic = IS
  - Course Code
  - CourseDescription
  - HighSchoolCourseRequirement
  - SequenceLimit
  - LocalEducationAgencyId
  - CourseTitle
  - CourseDefinedByDescriptorId = 'LEA'
  - CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
  - CourseIdentificationSystemDescriptor = 'LEA course code'
  - LearningStandardid (k-12 Courses)
    
6. **Create a course** for Direct Pay PSEO section enrollments – the Ed-Fi Model requires course, course offering and section. At minimum, a **single Placeholder course, course offering, and section will be required for your district** to report Direct Pay PSEO Student Section Association records. Ed-Fi required elements:
    - Course Code: Direct Pay PSEO
    - Course Title
    - Course Identification Code
    - Number of Parts
    - CourseDefinedByDescriptor = 'LEA'

7. **Not applicable to SIS Vendors - Project Foundry Only -** Create a course for Project Based section enrollments – While these types of enrollments do not include MDE course, course offering or section requirements – the Ed-Fi Model enforces these entities in the Master Schedule. At minimum, a **single Placeholder course, course offering, and section will be required for your district** to report Project Based Student Section Association records. Ed-Fi required elements:
    - Course Code: Project Based
    - CourseLevelCharacteristic = PBL
    - Course Title
    - Course Identification Code
    - Number of Parts
    - CourseDefinedByDescriptor = 'LEA'

8. Create CourseCourseAssociation records between the district Courses and State Level Courses (including IS, and Project Based if applicable)
    - EducationOrganizationId = District ID
    - CourseCode = District Course Code
    - ToCourseEducationOrganizationId = State Course EducationOrganizationId
    - ToCourseCode = State Course Code
      - IS can only use state codes with CourseLevelCharacteristicDescription = IS and Project Based can only use state codes with CourseLevelCharacteristicDescription = PBL.
      - Scheduled course work type cannot use CourseLevelCharacteristicDescription = PBL.

9. Create CourseCourseAssociation records between the College Courses A and D and the District Courses created for this association.
    - EducationOrganizationId = District ID
    - CourseCode = District Course Code
    - ToCourseEducationOrganizationId = College Course's PostSecondaryInstitutionId
    - ToCourseCode = College Course Code

10. Create CourseCourseAssociation records between the Direct Pay College Courses and the applicable State Course (PSEO Direct Pay)
    - EducationOrganizationId = College Education Organization ID
    - CourseCode = College Course Code
    - ToCourseEducationOrganizationId = State SEA id
    - ToCourseCode = State Course Code

## Resource: CourseOffering

### Description

Ed-Fi Description: This entity represents an entry in the course catalog of available courses offered by the school during a session. The MCCC collection in Ed-Fi will use Course Offering for collection of LocalCourseInformation that is not captured within the Ed-Fi Course record. The CourseOffering also links up the Course to the term and section, student and staff allowing grades and staff assignments to be captured.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- State, College and District Courses
- Sessions

### Scenarios

Create the following CourseOffering Records:

1. CourseOffering 1 References the District Course with Level Type = B
    - CourseReference
    - LocalCourseCode (this can match the District Course's Course Code – at the discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
2. CourseOffering 2 References the District Course with Course Level Type = G
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
3. CourseOffering 3 References the District Course with Course Level Type = E
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
4. CourseOffering 4 References the District Course with Course Level Type = D
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
5. CourseOffering 5 References the District Course with Course Level Type = A
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
6. CourseOffering 6 References the District Course Associated with Course Level Type = C CourseReference
    - LocalCourseCode (this can match the District Course's Course Code – at the discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
7. CourseOffering 7 References the District Course with Course Level Type = X
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
8. CourseOffering 8 References the District Course with Course Level Type = N
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
9. CourseOffering 9 References the District Course Associated with Course Level Type = P
    - CourseReference
    - LocalCourseCode (District Course's Code - at discretion of district)
    - SchoolId
    - SessionReference (SchoolYear, SchoolId, SessionName)
    - InstructionMinutesPerTerm
    - InstructionalApproach
      - InstructionalApproachDescriptor
      - ImplementationStatusDescriptor
    - siteBasedInitiative
      - siteBasedInitiativeDescriptor
      - ImplementationStatusDescriptor
10. CourseOffering 10 for Independent Study **(you will have one course offering for every Independent Study district course)**
    - CourseReference (reference to district course)
    - LocalCourseCode (District Course's Code - at discretion of district)
    - Schoolid
    - SessionReference (SchoolYear, SchoolId, SessionName = 'Unscheduled')
11. CourseOffering 11 for Direct Pay PSEO **(you will have a single course offering linked to a single district course set up as a placeholder)**
    - CourseReference (reference to district course)
    - LocalCourseCode (District Course's Code - at discretion of district)
    - Schoolid
    - SessionReference (SchoolYear, SchoolId, SessionName = 'Unscheduled')
12. CourseOffering 12 for Project Based **(not submitted by SIS vendors)** **- (Requires****a single course offering linked to a single course which is associated to all project-based college courses)**
    - CourseReference (reference to district course)
    - LocalCourseCode (District Course's Code - at discretion of district)
    - Schoolid
    - SessionReference (SchoolYear, SchoolId, SessionName = 'Unscheduled')

## Resource: Section

### Description

Ed-Fi Description: This entity represents a setting in which organized instruction of course content is provided, in-person or otherwise, to one or more students for a given period of time. A course offering may be offered to more than one section.Most MCCC CourseSectionInfo elements will be collected in the Ed-Fi Section Entity.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- State, College and District Courses (published to ODS by MDE)
- Sessions
- CourseOffering

### Scenarios

1. Create 9 Section Records to associate with the first 9 course offerings (not the IS, Project Based or Direct Pay PSEO courses yet – those will be done in step 2). Include the following elements:
    - SectionIdentifier
    - CourseOfferingReference
    - ClassPeriod (for Scheduled Section Enrollments)
    - SectionCharacteristicDescriptor (FP 'Fixed Period Indicator' for courses associated to a fixed period, or MA 'Marking Indicator' for sections where grades are recorded)
    - InstructionLanguageDescriptor (only for non-English, using MARSS language descriptor)
    - MediumOfInstructionDescriptor (required)
    - SequenceOfCourse (must be less than or equal to Section Limit of course referenced)
2. Create 3 Section Records, 1 for each of the following course offerings:
    - Independent Study (a section is required for every course offering)
      - SectionIdentifier: IS\_\&lt;LocalCourseCode\&gt;\_Section
      - CourseOfferingReference
    - Direct Pay PSEO (a single placeholder section is required all Direct Pay PSEO)
      - SectionIdentifier: DirectPayPSEO\_Section
      - CourseOfferingReference
    - Project Based (a single placeholder section is required all Project Based)
      - SectionIdentifier: ProjectBased\_Section
      - CourseOfferingReference

## Resource: StaffSectionAssociation

### Description

Ed-Fi Description: This association indicates the class sections to which a staff member is assigned.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- Staff (published to ODS by MDE)
- Sections

### Scenarios

1. Create StaffSectionAssociation for sections created for Course Level Types (A, B, C, D, E, G, N, X, P). Include the following elements:
    - StaffReference.staffUniqueId (FFN)
    - ClassroomPositionDescriptor = 'TOR'
    - SectionReference

## Resource: StudentSectionAssociation

### Description

Ed-Fi Description: This association indicates the course sections to which a student is assigned.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- Students
- Sections

### Scenarios

1. Create at least 1 StudentSectionAssociation Record for each Section loaded. Include the following elements:
    - StudentReference.studentUniqueId
    - SectionReference
    - BeginDate
    - College Course Reference (only applicable to Direct Pay PSEO)
    - Early Education fields (only for Couse Level Type 'P')
      - instructionalApproachDescriptor
      - implementationStatusDescriptor
      - siteBasedInitiativeDescriptor
      - implementationStatusDescriptor
    - SectionEnrollmentType
      - Match the enrollment type with the appropriate course/section.
        - Scheduled
        - Independent Study
        - Direct Pay PSEO
        - Project Based (if available)

## Resource: Grade

### Description

Ed-Fi Description: This educational entity represents an overall score or assessment tied to a course over a period of time (i.e., the grading period). Student grades are usually a compilation of marks and other scores. Most MCCC StudentSectionMark elements in Ed-Fi will be collected in the Ed-Fi Grade Entity.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- Students
- Sections
- StudentSectionAssociations

### Scenarios

1. Create 1 Grade Record for each StudentSectionAssociation loaded. Include the following elements:
    - StudentSectionAssociationReference
    - CollegeCreditsEarned
    - CollegeGradeEarned
    - LocalCreditEarned
    - NumericGradeEarned
    - LetterGradeEarned
    - SectionEnrollmentType

# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance to Digital Equity](sandbox_cert_f_digital_equity.md)
