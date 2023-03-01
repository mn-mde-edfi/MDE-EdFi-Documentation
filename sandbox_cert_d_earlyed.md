# Early Education Enrollment Certification **Scenarios**: API Resources
_Please note: the following scenarios are example situations, intended to demonstrate that your application can update the MDE Ed-Fi ODS appropriately. They do not necessarily demonstrate all valid combinations; for example, all funding source codes can be used for both School Readiness (SR) and Early Childhood Family Education (ECFE). **These scenarios will be updated for school year 2023-2024, which resolves the Early Education disambiguation issue.**_

For more information, see the [Early Education Enrollment and Parent collection dependencies section](sis_test_plan_c_data_reqs.md#early-education-enrollment-and-parent-collection) of the SIS Vendor test plan data requirements document.

## Resource: StudentSchoolAssociations
**Description:**
This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation.

**Prerequisite Data:**
- Students
- Schools

**Scenarios:**
1.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = EE) 
    - Required elements
        - School Id
        - Student Unique Id
        - Entry Grade Level = EE
        - Entry Type (Last Location Code) = 0
        - Entry Date = 9/5/2020
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
2.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = 1) 
    - School Id
    - Student Unique Id
    - Entry Grade Level = 1
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/6/2020
    - Exit Withdraw Date (Defaulted to end of school year)
    - Exit Withdraw Type = 40
    - Homebound Service Indicator = N
    - Resident Local Education Agency
    - Special Pupil Indicator = N
3.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = PA) 
    - School Id
    - Student Unique Id
    - Entry Grade Level = PA
    - Entry Type (Last Location Code) = 4
    - Entry Date = 9/6/2020
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

_Note_: The ```highestCompletedLevelOfEducationDescriptor``` element has been moved from the MN extenstion to Ed-Fi Core in v5.2, which is being implemented for **School Year 2022-23**.

## Resource: StudentParentAssociation
**Description:**
This association relates students to their parents, guardians, or caretakers.

**Prerequisite Data:**
- Students
- Parents
- StudentSchoolAssociations

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
1.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel EE
    - Include all elements except StudentCharacteristicsDescriptors (ADP, RAEL, IMMIGRANT, SLIFE)
2.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel 1
3.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel PA

## Resource: StudentEarlyEducationProgramAssociations
**Description:**
This association represents Students in either School Readiness or Early Childhood Family Education programs. Notes:
- The "EE-SR" and "EE-ECFE" program types are the programs intended for use with Early Education Data. These can also be used to cover the Early Ed programs formerly described as "SR/AB" and "ECFE/AB", respectively.
- "End Reason Code" below correlates to "reasonExitedDescriptor" (see the similarly named Data Mapping Matrix tab)

**Prerequisite Data:**
- Schools
- Program - where ProgramTypeDescriptor = "EE-SR"
- Program - where ProgramTypeDescriptor = "EE-ECFE"
- Students

**Scenarios:**
1.	Associate gradelevel EE Enrolled Student with this SR StudentEarlyEducationProgramAssociation
    - Begin Date: 9/5/2020
    - End Date: 6/11/2021 (default to last day in the school year)
    - End Reason Code = PE-01
    - Membership: 640
    - Attendance: 580
    - Submit funding sources PF and CC
2.	Associate same gradelevel EE Enrolled Student with this ECFE StudentEarlyEducationProgramAssociation
    - Begin Date =  9/5/2020
    - End Date = 10/15/2020 
    - End Reason Code = PE-02
    - Membership Hours = 40
    - Attendance Hours = 30
    - Submit funding sources PF, CC and TITLE
3.	Associate gradelevel 1 Enrolled Student with an ECFE StudentEarlyEducationProgramAssociation
    - Begin Date: 10/6/2020
    - End Date: 6/11/2020  (default to last day in the school year)
    - Membership: 640
    - Attendance: 580
    - Submit funding sources ECFE and CC
4.	Associate gradelevel PA Enrolled Student with an SR StudentEarlyEducationProgramAssociation
    - Begin Date: 9/7/2020
    - End Date: 6/11/2020  (default to last day in the school year)
    - Membership: 640
    - Attendance: 580
    - Submit funding sources CSPF and OD

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
