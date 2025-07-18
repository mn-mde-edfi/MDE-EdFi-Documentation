# StudentProgramAssociations

## Resource: Student21stCenturyLearningCenterGrantProgramAssociation
**Description**
This association represents Students in the 21st Century Community Learning Centers Grant Program. _Note_: Attendance Days and Attendance Hours are both required, and they represent independent measures of total attendance. For example, if a student attended a program 4 days a week for exactly 3 hours a day, and exactly 10 weeks, Attendance Days would be 40, and Attendance Hours would be 120.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "21st Century Learning Center Grant"
- Students

**Scenarios**
- Associate Student 1 with this StudentProgramAssociation 
- Include required Start Date ("beginDate")
- Include program attendance in days (an integer value) AND hours (up to 2 decimal places)
  - For a school year, attendance days should be between 1-300.
  - Attendance amounts should not exceed the number of days (365) or hours in a year. (A reasonable maximum for attendance hours would be 2400.)
  - The minimum unit for attendance hours should be .25 hours
  - Attendance Hours divided by Attendance Days should never exceed 24
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
- Program - where ProgramTypeDescriptor = "EE-ECS"
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

**Note:** As of summer 2022, our Ed-Fi API implementation does not allow the same student to be submitted in multiple gifted & talented programs, at the same school, with the same start date. If you have a need to describe associate a student to multiple gifted & talented programs, an acceptable workaround is to use multiple records with a slight offset in the begin date. We are aware this is less than ideal and are investigating a solution.

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

## Resource: StudentNeglectedOrDelinquentProgramAssociation
**Postponed until further notice.**

### **Description**
This association represents the Title I Part D Neglected or Delinquent program(s) that a student participates in or from which the Student receives services. Vendors may want to use [the sample JSON](/data/2022-2023%20Extensions/StudentNeglectedOrDelinquentProgramAssociations.json) for this association to better understand the data model.

### **Prerequisite Data**
- 5 Students
- Student School Association
- Program - where ProgramTypeDescriptor = "Neglected or Delinquent" (MDE should have one of these pre-loaded for each LEA in the API, with a ```programName``` of "Neglected or Delinquent Program", and a ```programTypeDescriptor``` of ```"uri://education.mn.gov/ProgramTypeDescriptor#Neglected or Delinquent"```.)

Note: be sure to be testing code with a new, minimal sandbox in order to get the latest descriptor values, etc.

### **Scenarios**
Using the ```/ed-fi/studentNeglectedOrDelinquentProgramAssociations``` resource, create a Neglected or Delinquent Program Association for 5 students as detailed below. For each scenario:
1. The programReference element should point to the appropriate LEA program preloaded (as described above in Prerequisite Data). 
2. Use the ```neglectedOrDelinquentProgramDescriptor``` element, and the appropriate descriptor value (see [this table](/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/NeglectedOrDelinquentProgramDescriptor.csv)), to assign the specific Program Association (Neglected, Juvenile detention, At-risk, etc)
3. Begin Date and End Date for the Program Association are at the top level of the resource.
4. Math and ELA progress level descriptors are at the top level of the resource.
5. Program *Service* data, since there can be multiples, are in a collection called ```neglectedOrDelinquentProgramServices```. See [this table](/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/NeglectedOrDelinquentProgramServiceDescriptor.csv) for descriptor values. Each of these needs a begin and end date and one value needs to be indicated as primary.
6. "In Program" and "Exited" outcomes are within the "mn" extension. Both types of outcomes reference the same outcome descriptor values (see [this table](/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/NeglectedOrDelinquentProgramOutcomeDescriptor.csv)). Use ```neglectedOrDelinquentProgramOutcomeDescriptor``` to designate an in-program outcome, and ```exitedNeglectedOrDelinquentProgramOutcomeDescriptor``` to designate an exited outcome.

Then, unique elements for each student are further described below:
 - Assign Program Association of **"Neglected" to Student 1**, including a begin date and an end date
   - Attach Program Service descriptors, including begin and end dates for each:
      - Attach a Program Service of "GED" to this student. Indicate this service as the Primary service.
      - Attach a Program Service of "Credit" to this student
      - Attach a Program Service of "Transitional Career Counseling Services" to        this student
      - Demonstrate that the Program Service begin and end dates cannot be entered outside the Program Association begin and end dates
   - Assign a Progress Level of "up to one full grade" to this student for Math
   - Assign a Progress Level of "no change" to this student for ELA
   - Assign a Program Outcome of "Earned high school course credits" as an in-program outcome for this student
   - Assign a Program Outcome of "Earned a GED" as an exited outcome for this student
   - Assign a Program Outcome of "Obtained employment" as an exited outcome for this student
 - Assign Program Association of **"Juvenile detention" to Student 2**, including only a begin date
    - Attach Program Service descriptors:
      - Attach a Program Service of "Mental Health Services" to this student. Indicate this service as the Primary service and include a begin date.
      - Attach a Program Service of "Credit" to this student. Include a begin date and end date.
   - Assign a Progress Level of "negative change" to this student for Math
   - Assign a Progress Level of "more than one full grade" to this student for ELA
   - Assign a Program Outcome of "Earned high school course credits" as an in-program outcome for this student
   - Assign a Program Outcome of "Enrolled in job training courses/programs" as an exited outcome for this student
 - Assign Program Association of **"At-risk programs" to Student 3**
   - Attach Program Service descriptors, including begin and end dates for each:
     - Attach a Program Service of "GED" to this student. Indicate this service as the Primary    service.
     - Attach a Program Service of "Tutoring, Mentoring Services" to this student
     - Attach a Program Service of "College and Career Readiness" to this student
     - Attach a Program Service of "Industrial Certification" to this student
     - Attach a Program Service of "Personal Education Plans" to this student
     - Attach a Program Service of "Family and Student involvement" to this student
     - Attach a Program Service of "Job Placement Services or Apprenticeship" to this student
     - Attach a Program Service of "Assistance Obtaining Student Financial Aid" to this student
   - Assign a Progress Level of "no change" to this student for Math
   - Assign a Progress Level of "no change" to this student for ELA
   - Assign a Program Outcome of "Obtained high school diploma" as an in-program outcome for this student
   - Assign a Program Outcome of "Were accepted and/or enrolled into post-secondary education" as an exited outcome for this student
 - Assign Program Association of **"Juvenile correction" to Student 4**
   - Attach Program Service descriptors, including begin and end dates for each:
      - Attach a Program Service of "Family and Student involvement" to this student. Indicate this     service as the Primary service.
      - Attach a Program Service of "Job Placement Services or Apprenticeship" to this student
      - Attach a Program Service of "Assistance Obtaining Student Financial Aid" to this student
   - Assign a Progress Level of "no change" to this student for Math
   - Assign a Progress Level of "no change" to this student for ELA
   - Assign a Program Outcome of "Obtained high school diploma" as an in-program outcome for this student
   - Assign a Program Outcome of "Enrolled in job training courses/programs" as an exited outcome for this student
 - Assign Program Association of **"Other" to Student 5**
   - Attach Program Service descriptors, including begin and end dates for each:
      - Attach a Program Service of "Family and Student involvement" to this student. Indicate this service as the Primary service.
    - Assign a Progress Level of "no change" to this student for Math
    - Assign a Progress Level of "no change" to this student for ELA
    - Assign a Program Outcome of "Enrolled in job training courses/programs" as an exited outcome for this student

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
This association represents the school food services program(s), such as the **Free or Reduced Price Lunch Program**, that a student participates in, or from which the Student receives services. This includes the ability for a district to identify whether or not the "Direct Certification" report was used to determine student eligibility. (See [this quick reference document](/2022-23%20MDE%20Ed-Fi%20Documentation/MDE%20MARSS%20Translation%20Logic%20for%20School%20Food%20Service%20with%20Direct%20Certification.docx) for MARSS translation logic.)

**Notes:** 
1. In early Ed-Fi implementations, schoolFoodServicesEligibility was tracked as a separate field under StudentSchoolAssociation. This element is now tracked using SchoolFoodServiceProgramService on studentSchoolFoodServicesProgramAssociation.
2. Usage of the [Applied but Did Not Qualify](sandbox_cert_b_marss.md#applied-but-did-not-qualify) element in the Student Education Organization Association has been **Postponed until further notice.**

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "School Food Service"
- Students

**Scenarios**
1. Associate Student 11 with this StudentProgramAssociation using SchoolFoodServiceProgramServiceDescriptor = 2 (Free)
2. Change SchoolFoodServiceProgramServiceDescriptor to 1 (Reduced)

**Direct Certification**

The following scenarios were added in school year 2022-23 to test for _Direct Certification_:
  1. Associate Student 1 as code **2 (Free)** based on the application for educational benefits. Demonstrate that this student's default value for Direct Certification is **False**. Then set the Direct Certification element to **True** for this student, which will display as a 7 after the MARSS translation.
  2. Associate Student 2 as **1 (Reduced)** on the application for educational benefits. Demonstrate that this student's default value for Direct Certification is **False**. Then set the Direct Certification element to **True** for this student. Which will then display as an 8 after the MARSS translation. Then, set the Direct Certification element to **False**.
  3. Demonstrate that Student 3 is not eligible by default (no association). Now associate this student to **2 (Free)** and set the Direct Certification element to **True**, which will display as a 7 after the MARSS translation.
  4. Return to Student 1, and change the Direct Certification value back to **False**.
  5. Return to Student 2 and set the **end date** for the entire program association to the end of the school year in order to demonstrate that they will no longer be eligible after this year.

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
This association represents the special education program(s) that a student participates in or receives services from. The association is an extension of the StudentProgramAssociation particular for special education programs. _Note_: Placing Local Education Agency Reference is an optional element, intended only for students with IEPs who are enrolled in a joint powers or intermediate district. See the [notes on Placing LEA](descriptors_resources.md#placing-local-education-agency-reference).

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
1. Associate Student 13 with this StudentProgramAssociation include a disability with order of priority = 1
2. Change disability code to 12, set special education service hours to 1100.5
3. Add a Placing Local Education Agency Reference (placingLocalEducationAgencyReference) to Student 13

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
- [Return to Sandbox Certification Overview](README.md)
- [Advance Early Education Enrollment Certification Scenarios](sandbox_cert_d_earlyed.md)