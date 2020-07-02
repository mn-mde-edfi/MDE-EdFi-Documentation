# 2020-2021 SIS Submitted MDE Ed-Fi API Resources: MARSS Data Collection
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

_Note:_ You will not be able to view or edit students until you claim them with the creation of an enrollment record via ```StudentSchoolAssociation``` (see next section).

## Resource: StudentSchoolAssociations

**Description**
This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation. _Remember_: when loading in data that references a Descriptor, you need to include a namespace, i.e. ```uri://education.mn.gov/[name of descriptor]#[code value]```.

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

This association indicates any relationship between a student and an education organization other than how the state views enrollment. Enrollment relationship semantics are covered by StudentSchoolAssociation. **MDE allows for the capture of student demographic data by school enrollment.** Therefore, a StudentEducationOrganizationAssociation record must be submitted for each ***school*** in which the student is enrolled to provide the student demographic data provided to the enrolling school by the parent(s). 

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
2.	Update Student 1's record to include Ancestry of Ethnic Origin = ai-cherokee
3.	Update Student 1's record to include a second Ancestry of Ethnic Origin = as-burmese
4.	Create a StudentEducationOrganizationAssociation between Student 2 and Middle School.
5.	Create a StudentEducationOrganizationAssociation between Student 2 and High School.
6.	Update Student 3's OptOutIndicator

## Resource: Calendar

**Description**
Ed-Fi Description: A set of dates associated with an organization. **MDE is not using the Calendar entity as collection of dates**; rather MDE captures the following key pieces of Calendar Metadata in the Calendar file: Instructional Days, Length of Day, and Kindergarten Schedule (when applicable). Calendar is captured at the School Level by grade. 

**Prerequisite Data**
- Schools (published to ODS by MDE)

***Changes from 19-20 to 20-21***
New properties: 
- DaysInSession
- Description
- New CalendarTypeDescriptor for MCCC

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

## Resource: Programs

Program Records for each of the following program types will be loaded for each district by MDE:
- The **educationOrganizationReference** for the **StudentProgramAssociation** is the **SchoolId**.  
- The **educationOrganizationReference** on the StudentProgramAssociation's **programReference** is the **LocalEducationAgencyId**.

# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance to StudentProgramAssociations](sandbox_cert_c_spas.md)
