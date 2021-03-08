# StudentProgramAssociations

## Resource: Student21stCenturyLearningCenterGrantProgramAssociation
**Description**
This association represents Students in the 21st Century Community Learning Centers Grant Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "21st Century Learning Center Grant"
- Students

**Scenarios**
- Associate Student 1 with this StudentProgramAssociation 
- Include required Start Date (“beginDate”)
- Include program attendance in days (an integer value) AND hours (up to 2 decimal places)
  - Attendance amounts should not exceed the number of days or hours in a year
- In a separate transaction, add an End Date to this program association for Student 1


## Resource: StudentCEISProgramAssociation
**Description**
This association represents Students in the Coordinated Early Intervening Service Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Coordinated Early Intervening Services"
- Students

**Scenarios**
- Associate Student 2 with this StudentProgramAssociation 
- Delete this Student Program Association 
- Delete Student 2's Middle School StudentEducationOrganizationAssociation record.
- Delete student 2's Middle School enrollment record.  

## Resource: StudentEarlyChildhoodScreeningProgramAssociations
**Description**
This association represents Students in the Early Childhood Screening Association Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Early Childhood Screening"
- Students

**Scenarios**
1.	Associate Student 3 with this StudentProgramAssociation
2.	Change the earlyChildhoodScreenerDescriptor to 'Head Start' and earlyChildhoodScreeningExitStatusDescriptor to 'Rescreen'

## Resource: StudentGiftedTalentedProgramAssociation
**Description**
This association represents Students in the Gifted Talented Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Gifted and Talented"
- Students

**Scenarios**
1.	Associate Student 4 with this StudentProgramAssociation
2.	Change the gifted talented participation code to 'Full-time services'

## Resource: StudentADSISProgramAssociation
**Description**
This association represents Students in the Alternative Delivery of Specialized Instruction (ADSIS) Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Alternative Delivery Of SIS"
- Students

**Scenarios**
1.	Associate Student 5 with this StudentProgramAssociation

## Resource: StudentHomelessProgramAssociation
**Description**
This association represents the McKinney-Vento Homeless Program program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Homeless"
- Students

**Scenarios**
1.	Associate Student 6 with this StudentProgramAssociation
2.	Change the primary nighttime residence code to 'Doubled-Up' and Unaccompanied Youth to True
3.	Submit a StudentHomelessProgramAssociation for the EE enrolled student 
      - Primary Nighttime Residence  = SHR
      - Begin Date 9/5/2019
      - End Date 12/25/2020

## Resource: StudentLanguageInstructionProgramAssociation
**Description**
This association represents the Title III Language Instruction for Limited English Proficient and Immigrant Students program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "English Learner"
- Students

**Scenarios**
1.	Associate Student 7 with this StudentProgramAssociation where English Learner Participation is set to True (Indicates EL Served)
2.	Change the English Learner Participation to False, to Indicate EL Identified, but not served
3.	Associate another student with this program and set the language service code to 'Newcomer Program'

## Resource: StudentPSEOConcurrentProgramAssociation
**Description**
This association represents Students in the PSEO Concurrent Enrollment Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "PSEO Concurrent"
- Students

**Scenarios**
1.	Associate Student 8 with this StudentProgramAssociation

## Resource: StudentPSEOProgramAssociation
**Description**
This association represents Students in the PSEO Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "PSEO Program"
- Students

**Scenarios**
1.	Update PSEO High School Hours to 650
2.	Associate Student 9 with this StudentProgramAssociation

## Resource: StudentSAAPProgramAssociation
**Description**
This association represents Students in a State Approved Alternative Program.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "SAAP"
- Students

**Scenarios**
1.	Associate Student 10 with this StudentProgramAssociation
2.	Change SAAP Credits to 5.75 and Set Independent Study indicator to True and SAAP concurrent indicator to Yes

## Resource: StudentSchoolFoodServiceProgramAssociation
**Description**
This association represents the school food services program(s), such as the **Free or Reduced Lunch Program**, that a student participates in, or from which the Student receives services.

**Note:** in School Year 18-19 schoolFoodServicesEligibility was tracked as a separate field under StudentSchoolAssociation.  This element is now tracked using SchoolFoodServiceProgramService  on studentSchoolFoodServicesProgramAssociation. 

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "School Food Service"
- Students

**Scenarios**
1.	Associate Student 11 with this StudentProgramAssociation with SchoolFoodServiceProgramService  = 2
2.	Change FRP Meal Code to 1

## Resource: StudentSection504PlanProgramAssociation
**Description**
Students who have a Section 504 plan.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Section 504 Plan"
- Students

**Scenarios**
1.	Associate Student 12 with this StudentProgramAssociation

## Resource: StudentSpecialEducationProgramAssociation
**Description**
This association represents the special education program(s) that a student participates in or receives services from. The association is an extension of the StudentProgramAssociation particular for special education programs.

**Important Notes on Order of Disability**

MDE collects the primary disability code for a student during an enrollment period.
- Disability codes must be reported to Ed-Fi with the 'order of disability' as 1 to designate the primary disability.
- Although additional disability codes for a student might be reported for a particular begin date, they will be ignored by MDE and not collected or stored in the MDE transformations. In other words, only the disability code with 'order of disability' 1 will be used for any begin date.
- If multiple disability codes for a student are reported with the same begin date, there must only be one with an order of disability = 1.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Special Education"
- Students

**Scenarios**
1.	Associate Student 13 with this StudentProgramAssociation include a disability with order of priority = 1
2.	Change disability code to 12, set special education service hours to 1100.5

## Resource: StudentTitleIPartAProgramAssociations
**Description**
This association represents the Title I Part A program(s) that a student participates in or from which the Student receives services. The association is an extension of the StudentProgramAssociation particular for Title I Part A programs.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Title I Part A"
- Students

**Scenarios**
1.	Associate Student 14 with this StudentProgramAssociation

# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance Early Education Enrollment Certification Scenarios](sandbox_cert_d_earlyed.md)