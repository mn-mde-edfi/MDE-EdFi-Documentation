# Early Education Enrollment Certification **Scenarios**: API Resources
_Please note: the following scenarios are example situations, intended to demonstrate that your application can update the MDE Ed-Fi ODS appropriately. They do not necessarily demonstrate all valid combinations; for example, all funding source codes can be used for both School Readiness (SR) and Early Childhood Family Education (ECFE). **Updates have been applied to these scenarios for school year 2023-2024, resolving the Early Education program ambiguity issue.** Please note that this resolution also involves [Calendar recsources](./sandbox_cert_b_marss.md#resource-calendar) and [StudentEarlyChildhoodScreeningProgramAssociations](./sandbox_cert_c_spas.md#resource-studentearlychildhoodscreeningprogramassociations)._

For more information, see the [Early Education Enrollment and Parent collection dependencies section](sis_test_plan_c_data_reqs.md#early-education-enrollment-and-parent-collection) of the SIS Vendor test plan data requirements document.

## Resource: StudentSchoolAssociations
**Description:**
This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation. Please take the time to read the [Instructions on Constructing SSAs for Multiple Early Education Program Associations](/2023-24%20MDE%20Ed-Fi%20Documentation/ssa_construction_for_multiple_ee.md) document with respect to handling SSAs when multiple SEEPAs are involved.

**Prerequisite Data:**
- Students (create 6 students, referenced as students A-F below)
- Schools

**Scenarios:**
1.	1.	Submit a StudentSchoolAssociation record for **Student A**
    - Required elements
        - School Id
        - Student Unique Id
        - Entry Grade Level = **EE**
        - Entry Type (Last Location Code) = 0
        - Entry Date = 9/5/2023
        - Exit Withdraw Date (Defaulted to end of school year)
        - Exit Withdraw Type = 20
        - Homebound Service Indicator = N
        - Resident Local Education Agency
        - Special Pupil Indicator = N
    - Data **not** collected for Early Education
        - State Aid Category (see [issue #16](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/issues/16))
        - Membership Attendance Units
        - Membership Attendance Percent Enrolled
        - Special Education Eval Status
        - Transportation
2.	Submit a StudentSchoolAssociation record for **Student B**
    - School Id
    - Student Unique Id
    - Entry Grade Level = **1**
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/5/2023
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N
3.	Submit a StudentSchoolAssociation record for **Student C**
    - School Id
    - Student Unique Id
    - Entry Grade Level = **EE**
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/5/2023
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N
4.	Submit a StudentSchoolAssociation record for **Student D**
    - School Id
    - Student Unique Id
    - Entry Grade Level = **EE**
    - Entry Type (Last Location Code) = 4
    - Entry Date = 10/17/2023
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N
5.	Submit a StudentSchoolAssociation record for **Student E**
    - School Id
    - Student Unique Id
    - Entry Grade Level = **EE** 
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/5/2023
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N
6.	Submit a StudentSchoolAssociation record for **Student F**
    - School Id
    - Student Unique Id
    - Entry Grade Level = **EE** 
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/5/2023
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N


## Resource: Parent 
**Description:**
This entity represents a parent or guardian of a student, such as mother, father, or caretaker.

**Prerequisite Data:**
None

**Scenarios:**
1.	Submit Parent Records for the following Early Ed Student in Gradelevel EE
    - Required Elements:
        - Parent Unique Id
        - firstName
        - lastSurname
        - MiddleName
        - generationCodeSuffix
        - [highestCompletedLevelOfEducationDescriptor](descriptors_resources.md#levelofeducationdescriptors) (see note below)
        - householdIncome
        - householdSize
        - receivingInterpreterAssistance
        - classroomVolunteerDescriptor
        - birthDate
        - sexDescriptor
2. Submit Parent Records for the following Early Ed Student in Gradelevel 1
3. Submit Parent Records for the following Early Ed Student in Gradelevel PA

_Note_: The ```highestCompletedLevelOfEducationDescriptor``` element has been moved from the MN extenstion to Ed-Fi Core in v5.2, which was implemented for school year 2022-23.

## Resource: StudentParentAssociation
**Description:**
This association relates students to their parents, guardians, or caretakers.

**Prerequisite Data:**
- Students
- Parents
- StudentSchoolAssociations
- Calendar Records with an "EE" grade, but with specific length of day and instructional days for VPK and School Readiness Plus

**Scenarios:**
1.	Submit Student Parent Association Record for the Early Education Student in Gradelevel EE
    - Required Elements:
        - Parent Unique Id
        - Student Unique Id
        - Relation Descriptor
2.	Submit Student Parent Association Record for the Early Education Student in Gradelevel 1
3.	Submit Student Parent Association Record for the Early Education Student in Gradelevel PA

## Resource: StudentEducationOrganizationAssociation
**Description:**
This association indicates any relationship between a student and an education organization other than how the state views enrollment. Enrollment relationship semantics are covered by StudentSchoolAssociation. **MDE allows for the capture of student demographic data by school enrollment.** Therefore, a StudentEducationOrganizationAssociation record must be submitted for each **school** in which the student is enrolled to provide the student demographic data provided to the enrolling school by the parent(s). 

**Prerequisite Data:**
- Students
- EducationOrganizations (Schools)

**Scenarios:**
1.	Create a StudentEducationOrganizationAssociation for **Student A**
    - Include all elements except StudentCharacteristicsDescriptors (ADP, RAEL, IMMIGRANT, SLIFE)
2.	Create a StudentEducationOrganizationAssociation for **Student B**
3.	Create a StudentEducationOrganizationAssociation for **Student E**

## Resource: StudentEarlyEducationProgramAssociations
**Description:**
This association now represents Students in either MARSS (School Readiness Plus, Early Childhood Special Education, or Voluntary Pre-Kindergarten) or non-MARSS (School Readiness or Early Childhood Family Education) early education programs. Notes:
- MARSS Early Childhood Screening (aka Preschool Screening) is covered in [this program association](/sandbox_cert_c_spas.md#resource-studentearlychildhoodscreeningprogramassociations).
- The "EE-SR" and "EE-ECFE" program types are the programs intended for use with Early Education Data. These can also be used to cover the Early Ed programs formerly described as "SR/AB" and "ECFE/AB", respectively.
- "End Reason Code" below correlates to "reasonExitedDescriptor" (see the similarly named Data Mapping Matrix tab). Please note that this is important information to include on the SEEPA record especially for non-MARSS program associations.
- Note that a calendar reference has been added to the VPK and SR+ scenarios in order to relate specific calendar records to sections of those programs. Sample JSON files for calendars and program associations are available in the [EE-MARSS Ambiguity Resolution](/data/EE-MARSS%20Ambiguity%20Resolution/) folder of the data directory.
- Note that *custom* membership and attendance elements on these associations have been replaced with an element similar to the Student School Association. For ECFE and SR program types, units must be ``Hours`` and percentEnrolled should be either zero or omitted. (A zero is likely the best approach to avoid API errors.) For the other early learning program types, the rules for membership & attendance data elements remain the same as they have been as defined by MARSS; the data elements are merely shifted to this resource instead of on the Student School Association. (For example, percentEnrolled is required for ECSE, VPK and SR+)

**Prerequisite Data:**
- Schools
- Program - where ProgramTypeDescriptor = "EE-SR"
- Program - where ProgramTypeDescriptor = "EE-SR+"
- Program - where ProgramTypeDescriptor = "EE-ECFE"
- Program - where ProgramTypeDescriptor = "EE-ECSE"
- Program - where ProgramTypeDescriptor = "EE-VPK"
- Students
- Calendar records with grade "EE" for use with VPK and SR+ programs

**Scenarios:**
1.	Associate **Student A** with an EE-SR Program 
    - Begin Date: 9/5/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - End Reason Code = PE-01
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 0 or omitted
    - Membership: 640
    - Attendance: 580
    - Submit funding sources PF and CC
2.	Add an association for **Student A**, with an EE-ECFE Program
    - Begin Date = 9/5/2023
    - End Date = 10/15/2023
    - End Reason Code = PE-02
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 0 or omitted
    - Membership = 40
    - Attendance = 30
    - Submit funding sources PF, CC and TITLE
3.	Demonstrate how **Student A** can be simultaneously associated with an Early Childhood Screening Association (aka Preschool Screening) with the same Begin Date of 9/5/2023. (In other words, add an Early Childhood Screening Association record for Student A.) 
    - **NOTE:** As described in the [EE ambiguity resolution](/2023-24%20MDE%20Ed-Fi%20Documentation/early_ed_marss_conflict_resolution.pdf), the descriptor value for Early Childhood Screening has changed for SY2023-24. Reference the specific [Student Program Association scenario](sandbox_cert_c_spas.md#resource-studentearlychildhoodscreeningprogramassociations) for more information.
4.	Associate **Student B** with an EE-ECFE Program 
    - Begin Date: 10/6/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 0 or omitted
    - Membership: 640
    - Attendance: 580
    - Submit funding sources ECFE and CC
5.	Associate **Student C** with an EE-SR Program 
    - Begin Date: 9/7/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 0 or omitted
    - Membership: 640
    - Attendance: 580
    - Submit funding sources CSPF and OD
6.	Add an association for **Student C** with an EE-ECSE Program starting on the same date demonstrating that they can be associated with both EE-ECSE and EE-SR at the same time.
    - Begin Date: 9/7/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 999
    - Membership: 640
    - Attendance: 580
7.	Associate **Student D** with an EE-ECSE Program
    - Begin Date: 10/17/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - Membership / Attendance Units: Hours
    - Percent Enrolled: 999
    - Membership: 540
    - Attendance: 500
8.	Associate **Student E** with an EE-SR+ Program
    - Begin Date: 9/5/2023
    - End Date: 6/11/2024 (default to last day in the school year)
    - Program Section Descriptor of Section D
    - Membership / Attendance Units: Days
    - Percent Enrolled: 100
    - Membership: 60
    - Attendance: 50
    - Calendar Reference: link to the EE calendar set up for School Readiness Plus
9.	Associate **Student F** with an EE-VPK Program
    - Begin Date: 9/5/2023 
    - End Date: 6/11/2024 (default to last day in the school year)
    - Program Section Descriptor of Section F
    - Membership / Attendance Units: Days
    - Percent Enrolled: 100
    - Membership: 60
    - Attendance: 50
    - Calendar Reference: link to the EE calendar set up for VPK
10.	Change **Student C's** association from EE-SR to EE-VPK
    - Demonstrate how both a Program Section Descriptor and a Calendar Reference will now be required, describing Section J for this school year
11.	Please demonstrate how your software differentiates between various program choices, in particular how users will tell the difference between Early Childhood Screening (EE-ECS) and Early Childhood Special Education (EE-ECSE).

## Resource: StudentHomelessProgramAssociation
**Description:**
This association represents the McKinney-Vento Homeless Program program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data:**
- Schools
- Program - where ProgramTypeDescriptor = "Homeless"
- Students

**Scenarios:**
1.	Submit a StudentHomelessProgramAssociation for the EE enrolled student 
    - Primary Nighttime Residence  = SHR
    - Begin Date = 9/5/2019
    - End Date = 12/25/2020

## Resource: StudentLanguageInstructionProgramAssociation

**Description:**
This association represents the Title III Language Instruction for Limited English Proficient and Immigrant Students program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data:**
- Schools
- Program - where ProgramTypeDescriptor = "English Learner"
- Students

**Scenarios:**
1.	Submit StudentLanguageInstructionProgramAssociation for EE enrolled Student
    - Begin Date = 9/5/2019	
    - End Date = 5/25/2021
    - Lang Service Code = Transitional Bilingual
    - EL Participation = 1

# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance to MCCC](sandbox_cert_e_mccc.md)
