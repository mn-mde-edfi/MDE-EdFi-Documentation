# MCCC Certification Scenarios - API Resources

## Resource: Students

### Description

This entity represents an individual for whom instruction, services, and/or care are provided in an early childhood, elementary, or secondary educational program under the jurisdiction of a school, education agency, or other institution or program. A student is a person who has been enrolled in a school or other educational institution.

### Prerequisite Data

- None

### Scenarios

1. Create 12 student records including the following elements.
  1. studentUniqueID
  2. birthdate
  3. birthSexDescriptor
  4. firstName
  5. generationCodeSuffix
  6. lastSurname
  7. middleName

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

Ed-Fi Description: A set of dates associated with an organization. MDE is not using the Calendar entity as collection of dates, rather MDE captures the following key pieces of Calendar Metadata in the Calendar file: Instructional Days, Length of Day, and Kindergarten Schedule (when applicable). Calendar is captured at the School Level by grade.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create MCCC Calendar for elementary, middle and high schools including
  1. Calendar Code
  2. School ID
  3. School Year
  4. CalendarType = &quot;MCCC&quot;
  5. Days In Session
  6. Instructional Days
  7. Description

## Resource: CalendarDate

### Description

Ed-Fi Description: The type of scheduled or unscheduled event for the day. MDE will be collecting the MCCC ScheduleInfo Start and End Dates using Calendar Date.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Calendar

### Scenarios

1. Create 2 Calendar Dates for each of the 3 calendars
  1. Date 1 – calendarEventDescriptor = STARTDT
  2. Date 2 – calendarEventDescriptor = ENDDT
  3. Both Dates should reference the MCCC Calendar created above

## Resource: ClassPeriod

### Description

Ed-Fi Description: This entity represents the designation of a regularly scheduled series of class meetings at designated times and days of the week. MDE will be collecting the MCCC PeriodInfo Data in this resource. This data must be submitted for each school.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create a series of Class Periods for elementary, middle and high school
  1. Each Period must include:
    1. ClassPeriodName
    2. ClassPeriodDescriptor
    3. SchoolID
    4. ClassPeriodDescription
    5. StartTime
    6. EndTime

## Resource: GradingPeriod

### Description

Ed-Fi Description: This entity represents the time span for which grades are reported. MCCC collection in Ed-Fi requires the creation of GradingPeriods in order to allow submission of grades. Grading Periods are defined at the School Level.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create a series of GradingPeriods for elementary, middle and high school

              1. Each Period must include:
                1. GradingPeriodDescriptor
                2. PeriodSequence
                3. SchoolId
                4. SchoolYear

## Resource: Session

### Description

Ed-Fi Description: A term in the school year, generally a unit of time into which courses are scheduled, instruction occurs and by which credits are awarded. Sessions may be interrupted by vacations or other events. The MCCC collection in Ed-Fi will use Session for collection of TermInfo.

### Prerequisite Data

- Schools (published to ODS by MDE)

### Scenarios

1. Create Sessions for elementary, middle and high school (Fall, Spring, and non-scheduled)
  1. Each Period must include:
    1. TermDescriptor (S for Semester, NS for non-scheduled)
    2. School Year
    3. SchoolId
    4. DaysInSession
    5. TotalInstructionalDays
    6. SessionName
    7. BeginDate
    8. EndDate
    9. TermNumber

## Resource: Course

### Description

Ed-Fi Description: This educational entity represents the organization of subject matter and related learning experiences provided for the instruction of students on a regular or systematic basis. The MCCC collection in Ed-Fi will use Course for collection of District, College and State Courses.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- State Courses (published to ODS by MDE)

### Scenarios

1. Create 8 **District** Courses (set up at least 1 course per school type – Elementary, Middle and High School)
  1. Course 1 Course Level Type = B
  2. Course 2 Course Level Type = G
  3. Course 3 Course Level Type = E
  4. Course 4 Course Level Type = D
  5. Course 5 Course Level Type = A
  6. Course 6 Course Level Type = C
  7. Course 7 Course Level Type = X
  8. Course 8 Course Level Type = N

Including the following elements:

    1. CourseDescription (only when associated with an Unclassified State Course)
    2. HighSchoolCourseRequirement
    3. CourseLevelCharacteristic for End of Course Indicator
    4. Course Code (Local)
    5. SequenceLimit
    6. LocalEducationAgencyId
    7. CourseTitle
    8. CourseDefinedByDescriptorId = &quot;LEA&quot;
    9. CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
    10. CourseIdentificationSystemDescriptor = &#39;LEA course code&#39;
    11. _LearningStandardid_ (not currently required)
1. Create an EE District Course
 Elements that must have valid values:
  1. Course Description (only required when associated with Unclassified State Course)
  2. Course Code (local)
  3. Course level Type (P)
  4. Sequence Limit (1)
  5. StandardId (State)
  6. High School Course Requirement (False)
  7. **Must NOT include CourseLevelCharacteristic for End of Course Indicator**
  8. CurriculumUsed
    1. CurriculumUsedDescriptor (CRCUE, HWOT)
    2. ImplementationStatusDescriptor (FULL, CEXP)
  9. AssessmentTool
    1. AssessmentToolDescriptor
    2. ImplementationStatusDescriptor
  10. CourseDefinedByDescriptorId = &#39;LEA&quot;
    1. CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
    2. CourseIdentificationSystemDescriptor = &#39;LEA course code&#39;
  11. LearningStandardid (99.E5.1)
2. District Courses to associate with College courses
  1. Create additional District courses to be associated with college course levels D and A
3. Create **College** Courses
  1. 1 with Course Level Type = D
  2. 1 with Course Level Type = A
  3. 2 college courses to be used for Direct Pay PSEO

Including the following elements:

    1. PostSecondaryInstitutionId
    2. MaximumAvailableCredits
    3. CourseCode (College Course Identifier – generally dept letters &amp; course number)
    4. CourseTitle
    5. CourseDefinedByDescriptorId = &#39;College&quot;
    6. CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
    7. CourseIdentificationSystemDescriptor = &#39;University course code&#39;
1. Create a District Course for Independent Study

**NOTE:** Independent Study course section enrollments did not previously require the setup of a course section – the Ed-Fi Model enforces the full set of master schedule entities (course, course offering and section) in order to associate a student with a course and record grades for that course.

Separate course, course offering and section records are required for your district to report ALC Independent Study records; however Course Offering and Section will not be used by MDE for reporting. (The Ed-Fi Model requires an entry in Course Offering linked to the non-scheduled term, and a section default.)

  1. Include the following elements:
    1. CourseLevelCharacteristic = IS
    2. Course Code
    3. CourseDescription
    4. HighSchoolCourseRequirement
    5. SequenceLimit
    6. LocalEducationAgencyId
    7. CourseTitle
    8. CourseDefinedByDescriptorId = &#39;LEA&quot;
    9. CourseIdentificationCode – repeat the CourseCode (this is an ed-fi requirement)
    10. CourseIdentificationSystemDescriptor = &#39;LEA course code&#39;
    11. LearningStandardid (k-12 Courses)
1. **Create a course** for Direct Pay PSEO section enrollments – the Ed-Fi Model requires course, course offering and section. At minimum, a **single Placeholder course, course offering, and section will be required for your district** to report Direct Pay PSEO Student Section Association records.
  1. Ed-Fi required elements:
    1. Course Code: Direct Pay PSEO
    2. Course Title
    3. Course Identification Code
    4. Number of Parts
    5. CourseDefinedByDescriptor = &quot;LEA&#39;
2. **Not applicable to SIS Vendors - Project Foundry Only -** Create a course for Project Based section enrollments – While these types of enrollments do not include MDE course, course offering or section requirements – the Ed-Fi Model enforces these entities in the Master Schedule. At minimum, a **single Placeholder course, course offering, and section will be required for your district** to report Project Based Student Section Association records.
  1. Ed-Fi required elements:
    1. Course Code: Project Based
    2. CourseLevelCharacteristic = PBL
    3. Course Title
    4. Course Identification Code
    5. Number of Parts
    6. CourseDefinedByDescriptor = &quot;LEA&#39;
3. Create CourseCourseAssociation records between the district Courses and State Level Courses (including IS, and Project Based if applicable)
  1. EducationOrganizationId = District ID
  2. CourseCode = District Course Code
  3. ToCourseEducationOrganizationId = State Course EducationOrganizationId
  4. ToCourseCode = State Course Code
    1. IS can only use state codes with CourseLevelCharacteristicDescription = IS and Project Based can only use state codes with CourseLevelCharacteristicDescription = PBL.
    2. Scheduled course work type cannot use CourseLevelCharacteristicDescription = PBL.
4. Create CourseCourseAssociation records between the College Courses A and D and the District Courses created for this association.
  1. EducationOrganizationId = District ID
  2. CourseCode = District Course Code
  3. ToCourseEducationOrganizationId = College Course&#39;s PostSecondaryInstitutionId
  4. ToCourseCode = College Course Code
5. Create CourseCourseAssociation records between the Direct Pay College Courses and the applicable State Course (PSEO Direct Pay)
  1. EducationOrganizationId = College Education Organization ID
  2. CourseCode = College Course Code
  3. ToCourseEducationOrganizationId = State SEA id
  4. ToCourseCode = State Course Code

## Resource: CourseOffering

### Description

Ed-Fi Description: This entity represents an entry in the course catalog of available courses offered by the school during a session. The MCCC collection in Ed-Fi will use Course Offering for collection of LocalCourseInformation that is not captured within the Ed-Fi Course record. The CourseOffering also links up the Course to the term and section, student and staff allowing grades and staff assignments to be captured.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- State, College and District Courses
- Sessions

### Scenarios

Create the following CourseOffering Records

1. CourseOffering 1 References the District Course with Level Type = B

    1. CourseReference
    2. LocalCourseCode (this can match the District Course&#39;s Course Code – at the discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
2. CourseOffering 2 References the District Course with Course Level Type = G

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
3. CourseOffering 3 References the District Course with Course Level Type = E

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
4. CourseOffering 4 References the District Course with Course Level Type = D

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
5. CourseOffering 5 References the District Course with Course Level Type = A

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
6. CourseOffering 6 References the District Course Associated with Course Level Type = C CourseReference

    1. LocalCourseCode (this can match the District Course&#39;s Course Code – at the discretion of district)
    2. SchoolId
    3. SessionReference (SchoolYear, SchoolId, SessionName)
    4. InstructionMinutesPerTerm
7. CourseOffering 7 References the District Course with Course Level Type = X

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
8. CourseOffering 8 References the District Course with Course Level Type = N

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
9. CourseOffering 9 References the District Course Associated with Course Level Type = P

    1. CourseReference
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. SchoolId
    4. SessionReference (SchoolYear, SchoolId, SessionName)
    5. InstructionMinutesPerTerm
    6. InstructionalApproach
      1. InstructionalApproachDescriptor
      2. ImplementationStatusDescriptor
    7. siteBasedInitiative
      1. siteBasedInitiativeDescriptor
      2. ImplementationStatusDescriptor
10. CourseOffering 10 for Independent Study **(you will have one course offering for every Independent Study district course)**

    1. CourseReference (reference to district course)
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. Schoolid
    4. SessionReference (SchoolYear, SchoolId, SessionName = &quot;Unscheduled&quot;)
11. CourseOffering 11 for Direct Pay PSEO **(you will have a single course offering linked to a single district course set up as a placeholder)**

    1. CourseReference (reference to district course)
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. Schoolid
    4. SessionReference (SchoolYear, SchoolId, SessionName = &quot;Unscheduled&quot;)
12. CourseOffering 12 for Project Based **(not submitted by SIS vendors)** **- (Requires****a single course offering linked to a single course which is associated to all project-based college courses)**

    1. CourseReference (reference to district course)
    2. LocalCourseCode (District Course&#39;s Code - at discretion of district)
    3. Schoolid
    4. SessionReference (SchoolYear, SchoolId, SessionName = &quot;Unscheduled&quot;)

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

1. Create 9 Section Records to associate with the first 9 course offerings (not the IS, Project Based or Direct Pay PSEO courses yet – those will be done in step 2)
  1. Include the following elements:
    1. SectionIdentifier
    2. CourseOfferingReference
    3. ClassPeriod (for Scheduled Section Enrollments)
    4. SectionCharacteristicDescriptor (FP &quot;Fixed Period Indicator&quot; for courses associated to a fixed period, or MA &quot;Marking Indicator&quot; for sections where grades are recorded)
    5. InstructionLanguageDescriptor (only for non-English, using MARSS language descriptor)
    6. MediumOfInstructionDescriptor (required)
    7. SequenceOfCourse (must be less than or equal to Section Limit of course referenced)
2. Create 3 Section Records. 1 for each of the following course offerings:
  1. Independent Study (a section is required for every course offering)
    1. SectionIdentifier: IS\_\&lt;LocalCourseCode\&gt;\_Section
    2. CourseOfferingReference
  2. Direct Pay PSEO (a single placeholder section is required all Direct Pay PSEO)
    1. SectionIdentifier: DirectPayPSEO\_Section
    2. CourseOfferingReference
  3. Project Based (a single placeholder section is required all Project Based)
    1. SectionIdentifier: ProjectBased\_Section
    2. CourseOfferingReference

## Resource: StaffSectionAssociation

### Description

Ed-Fi Description: This association indicates the class sections to which a staff member is assigned.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- Staff (published to ODS by MDE)
- Sections

### Scenarios

1. Create StaffSectionAssociation for sections created for Course Level Types (A, B, C, D, E, G, N, X, P)
  1. Include the following elements:
    1. StaffReference.staffUniqueId (FFN)
    2. ClassroomPositionDescriptor = &#39;TOR&#39;
    3. SectionReference

## Resource: StudentSectionAssociation

### Description

Ed-Fi Description: This association indicates the course sections to which a student is assigned.

### Prerequisite Data

- Schools (published to ODS by MDE)
- Districts (published to ODS by MDE)
- Students
- Sections

### Scenarios

1. Create at least 1 StudentSectionAssociation Record for each Section loaded
  1. Include the following elements:
    1. StudentReference.studentUniqueId
    2. SectionReference
    3. BeginDate
    4. College Course Reference (only applicable to Direct Pay PSEO)
    5. Early Education fields (only for Couse Level Type &#39;P&#39;)
      1. instructionalApproachDescriptor
      2. implementationStatusDescriptor
      3. siteBasedInitiativeDescriptor
      4. implementationStatusDescriptor
    6. SectionEnrollmentType
      1. Match the enrollment type with the appropriate course/section.
        1. Scheduled
        2. Independent Study
        3. Direct Pay PSEO
        4. Project Based (if available)

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

1. Create 1 Grade Record for each StudentSectionAssociation loaded
  1. Include the following elements:
    1. StudentSectionAssociationReference
    2. CollegeCreditsEarned
    3. CollegeGradeEarned
    4. LocalCreditEarned
    5. NumericGradeEarned
    6. LetterGradeEarned
    7. SectionEnrollmentType
