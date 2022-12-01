# MARSS and Ancestry of Ethnic Origin Certification Scenarios – Ed-Fi API Resources
*Note: Several MARSS resources are related to the MCCC collection. As a result, in this markdown document, those resource sections are also listed here, and link to the appropriate sections within the MCCC certification scenarios.*

## Resource: Students

**Description**
This entity represents an individual for whom instruction, services, and/or care are provided in an early childhood, elementary, or secondary educational program under the jurisdiction of a school, education agency or other institution or program. A student is a person who has been enrolled in a school or other educational institution.

**Prerequisite Data**
- None

**Certification Scenarios**
1.	Create 14 student records including the following elements:
    - studentUniqueID
    - birthdate
    - birthSexDescriptor
    - firstName
    - generationCodeSuffix
    - lastSurname
    - middleName

_Notes:_ 
- You will not be able to view or edit students until you claim them with the creation of an enrollment record via ```StudentSchoolAssociation``` (see next section). Within Swagger, only one record can be created at a time. See [this example record](data/example_value_student_record.json) for specific JSON formatting.
- The student's legal name should be used and stay consistent over time unless the student legally changes their name.

## Resource: StudentSchoolAssociations

**Description**
This association represents the School in which a student is enrolled. Note that the semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation. _Remember_: when loading in data that references a Descriptor, you need to include a namespace, i.e. ```uri://education.mn.gov/[name of descriptor]#[code value]```. See more details in [this example record](data/example_value_studentSchoolAssociation.json).

**Prerequisite Data**
- Students
- Schools

**Certification Scenarios**
1.	Enroll student 1 at Elementary School, including:
    - homeboundServiceIndicator
    - specialPupilIndicator
2.	Enroll student 2 at Middle School. 
3.	Withdraw student from Middle School.
4.	Enroll student 2 at High School.
5.	Create the following records for Student 2:
    - An enrollment
    - Withdrawal 
    - Re-enrollment of a student who changes resident districts but does not change schools.  Place a 20 day gap between records. 
6.	Update Student 1's Percent Enrolled to 50% and set membershipAttendanceUnitDescriptor to days, set membership and attendance.
7.	Update Student **1's Percent Enrolled to 100%**, membershipAttendanceUnitDescriptor to hours and adjust membership and attendance accordingly.
8.	Update Student 2's Transportation Category.
9.	Update Student 3's StateAid Category.
10.	Create 2 enrollment records (a, b) for a student that is in two different schools within the same district at the same time.  Enrollment dates 09/10/17 through 06/10/18.  
11.	Create the records for: 
    - An enrollment, 
    - Withdrawal and 
    - Re-enrollment for a kindergarten student who receives an IEP mid-year – send updated special education evaluation status. (Grade change from KA to HK, and specialEducationEvaluationStatus updated)

## Resource: StudentEducationOrganizationAssociation
**Description**

The Student Education Organization Association (SEOA) indicates any relationship between a student and an education organization other than how the state views enrollment. (Enrollment relationship semantics are covered by StudentSchoolAssociation.) **MDE allows for the capture of student demographic data by school enrollment.** Therefore, a StudentEducationOrganizationAssociation record must be submitted for each ***school*** in which the student is enrolled to provide the student demographic data provided to the enrolling school by the parent(s).

Please note that additional collections integrated into SEOA have been **postponed until after school year 2022-23**. These are described in separate headings below the original scenario.

**Prerequisite Data**
- Students
- EducationOrganizations (Schools)

**Scenarios**
1.	Create a StudentEducationOrganizationAssociation between Student 1 and an Elementary School, Include the following data points:
    - EthnicCode by sending a StudentCharacteristic = 'American Indian - Alaskan Native (Minnesota)'
    - Race = 'American Indian - Alaska Native'
    - Birthdate
    - sexDescriptor
    - firstName, middleName, lastName, generationCodeSuffix
    - hispanicLatinoEthnicity
    - languageDescriptor
    - languageUseDescriptor = 'Home Language'
    - studentIdentificationCodes
    - studentIdentificationSystemDescriptor = 'Local'
    - assigningOrganizationIdentificationCode = 'District Id'
    - identificationCode = local use code
2.	Update Student 1's record to include Ancestry of Ethnic Origin = ai-cherokee (see Note 2 below)
3.	Update Student 1's record to include a second Ancestry of Ethnic Origin = as-burmese
4.	Create a StudentEducationOrganizationAssociation between Student 2 and Middle School.
5.	Create a StudentEducationOrganizationAssociation between Student 2 and High School.
6.	Update Student 3's OptOutIndicator

_Note 1_: as in the Student record, the student's legal name should be used in the StudentEducationOrganizationAssociation.
_Note 2_: for **school year 2022-23**, with upgrading to version 5.2, the ```ancestryEthnicOrigins``` element is now part of Ed-Fi core, and not in the Minnesota extension.

### Applied but Did Not Qualify
**Postponed until after school year 2022-23:** This provides the ability for the district to identify a student that applied for the National School Lunch Program (NSLP) but did not qualify and is not served Free or Reduced Price meals.

**Scenario**
- Designate **Student 2** accordingly by adding ```studentCharacteristicDescriptor``` codeValue 10 (Applied for National School Lunch Program but did not qualify) to the ```studentCharacteristics``` collection.

### Displaced Students and Student Crisis Events
**Postponed until after school year 2022-23:** This provides a way to identify crisis events that may have displaced students in the district. 

**Scenario**
- Designate **Student 3** as displaced by setting the ```displacedStudentIndicator``` to true
- Describe the crisis event inside the ```crisisEventDescriptor``` element using code 4, 'Displaced by War in Ukraine'
- Demonstrate dynamic loading of crisis event descriptors via the API within your software's interface, in order to facilitate rapid designation of students for future events.

### Language Academic Honors
**Postponed until after school year 2022-23.** This collection object within the SEOA records one or more Student Academic distinctions awarded for languages including World Languages Proficiency Certificate, Bilingual Seal, and Multilingual Seal. See [additional documentation](README.md#language-academic-honor-documentation) in the readme file.

**Prerequisite Data**
 - School
 - 4 Student records
 - Student School Association (for the school where the student is enrolled when being awarded the honor)
 - Student Education Organization Association to update

**Honor Scenarios**
 - Create a Bilingual honor record for **Student 1** with:
   - Academic Honor Category of Bilingual Seal
   - Academic Achievement Category using one of:
     - bilingualGold
     - bilingualPlatinum
 - Create a Multilingual Seals honor record for **Student 2** with:
   - Academic Honor Category of Multilingual Seals
   - Academic Achievement Category using one of the following Achievement Categories:
     - multilingualGold
     - multilingualPlatinum
 - Create a World Language Proficiency honor record for **Student 3** with:
   - Academic Honor Category of World Languages Proficiency Certificate
   - Academic Achievement Category of World Languages Proficiency Certificate
 - Create multiple honor records for **Student 4** with:
   - a World Language Proficiency honor record:
     - Academic Honor Category of World Languages Proficiency Certificate
     - Academic Achievement Category of World Languages Proficiency Certificate
   - a Bilingual honor record:
     - Academic Honor Category of Bilingual Seal
     - Academic Achievement Category of bilingualGold
 - For **each** honor record, include an Honor Award Date. 
   - For Multilingual and Bilingual honors, demonstrate that the year of this date must match the year of the student graduation date. (Note that World Language Proficiency can be awarded in any year.)
 - For **each** record, include a collection of languages
   - Demonstrate that only one non-English language can be submitted for Student 1 (Bilingual Seal)
   - Demonstrate that two or more non-English languages must be submitted for Student 2 (Multilingual Seal)
   - Demonstrate that only one non-English language can be submitted for Student 3 (World Language Proficiency)
   - Follow the same rules for Student 4
 - For **each** record, include an assessment category
   - For Student 1, assign code 7, "Minnesota Bilingual Seals Assessments"
   - For Student 2, assign code 3, "AVANT STAMP WS and Minnesota Bilingual Seals Assessment"
   - For Student 3, assign code 6, "IB DP Language B Exam"
   - For Student 4, assign code 0, "Other language assessment" to the World Language Proficiency honor. Demonstrate that the Assessment Title text will be required to describe the assessment with this category. (Note this is optional for other assessment category codes.)
   - For Student 4, assign code 7, "Minnesota Bilingual Seals Assessments" to the Bilingual honor
   - Demonstrate that only codes 0-9 (**not** codes beginning with '00') for [Assessment Category Descriptors](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/blob/master/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/AssessmentCategoryDescriptor.csv) can be used for Language Academic Honors.
 - For **each** record, add a grade level for when the student was tested for the award
   - Demonstrate that the student's current enrollment grade level in the student school association is the highest available value that can be assigned to this element
 - For **each** record add an assessed school year value
   - Demonstrate that future school years cannot be assigned to this element. (Note either current or past school year values are valid.)

_**Note** that the ```honor description``` text field is optional from a policy standpoint. Unfortunately, the way we have it modeled after the Ed-Fi academic honor resource, that field is part of the unique identification of an honor for a student. Therefore, we are unable to make it optional in the API, and we recommend vendors repeat the short description of the Achievement Category within the ```honor description``` text field._

### Gender Identity and Preferred Pronouns
**Postponed until after school year 2022-23.** The Gender Identity collection object records a Student's gender identity. (This may be different from SEOA.Sex & Student.BirthSex, which collect the student's gender as reported to the federal government). The Preferred Pronouns extension records a Student's personal preferred pronouns. Both are delivered via the SEOA.

Districts are expected to send both gender identity and preferred pronoun values, although they are optional.

**Prerequisite Data**
-	Schools
-	Students

**Scenarios**
1. Create a StudentEducationOrganizationAssociation with a single Gender Identity value and a single Preferred Pronoun value.
2. Create a StudentEducationOrganizationAssociation with multiple Gender Identity values and multiple Preferred Pronoun values.

### Preferred Name
**Postponed until after school year 2022-23.** The student's preferred name, using the "otherNames" collection element within the MN extension of ```studentEducationOrganizationAssociation```.

**Prerequisite Data**
-	Students
-	Student Education Organization Association

**Scenarios**
-	Demonstrate the ability to add a preferred name for a student
-	Demonstrate the ability to remove a preferred name for a student
-	Demonstrate the ability to change a preferred name for a student
-	Repeat for first, last, middle, and generation suffix

## Resource: Calendar

**Description**
Ed-Fi Description: A set of dates associated with an organization. **MDE is not using the Calendar entity as collection of dates**; rather MDE captures the following key pieces of Calendar Metadata in the Calendar file: Instructional Days, Length of Day, and Kindergarten Schedule (when applicable). Calendar is captured at the School Level by grade. 

**NOTE:** MDE expects districts to only send **one** calendar *per grade level, per school* to MDE's Ed-Fi API, selecting specifically the calendar which is expected to be used for MARSSWES financial reporting.

**Prerequisite Data**
- Schools (published to ODS by MDE)

**Scenarios**
**MARSS**

1.	Create calendar record for Elementary School grades 1 through 5 (do not include kindergarten as grade level)
    - Length of day = 360
    - Instructional Days = 167
2.	Update calendar created in scenario one by reducing the Instructional Days from 167 to 166
3.	Create calendar record for Elementary School for Kindergarten only - use grade KG
    - Length of day = 360
    - Instructional Days = 165
4.	Create Full Year School Readiness Plus calendar for Elementary School grade RA
    - Length of day = 150
    - Instructional Days = 148
5.	Create Half Year School Readiness Plus calendar for Elementary School grade RB
    - Length of day = 150
    - Instructional Days = 78
6.	Create Middle School Calendar
7.	Create High School Calendar

## Resource: ClassPeriod

See [Resource: ClassPeriod section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-classperiod)

## Resource: GradingPeriod

See [Resource: GradingPeriod section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-gradingperiod)

## Resource: Session

See [Resource: Session section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-session)

## Resource: Course

See [Resource: Course section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-course)

## Resource: CourseOffering

See [Resource: CourseOffering section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-courseoffering)

## Resource: Section

See [Resource: Section section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-section)

## Resource: StaffSectionAssociation
See [Resource: StaffSectionAssociation section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-staffsectionassociation)

## Resource: StudentSectionAssociation

See [Resource: StudentSectionAssociation section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-studentsectionassociation)

## Resource: Grade

See [Resource: Grade section in MCCC certification scenarios.](sandbox_cert_e_mccc.md#resource-grade)

## Resource: Programs

Program Records for each of the following program types will be loaded by MDE for each LEA known to be active in the school year. Note that within a Student Program Association record, the organization identifiers will appear in multiple places:
•	The educationOrganizationReference near the top of the StudentProgramAssociation - this should carry the **school ID**
•	The educationOrganizationReference inside the programReference element of the StudentProgramAssociation - this should be the **LEA ID**.


# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance to StudentProgramAssociations](sandbox_cert_c_spas.md)
