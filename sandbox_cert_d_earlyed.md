# 2020-2021 Early Education Enrollment Certification **Scenarios**: API Resources

## Resource: StudentSchoolAssociations
**Description**
This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation.

**Prerequisite Data**
- Students
- Schools

**Scenarios**
1.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = EE) 
    a.	Required elements
        i.	School Id
        ii.	Student Unique Id
        iii.	Entry Grade Level = EE
        iv.	Entry Type (Last Location Code) = 0
        v.	Entry Date = 9/5/2020
        vi.	Exit Withdraw Date (Defaulted to end of school year)
        vii.	Exit Withdraw Type = 20
        viii.	Homebound Service Indicator = N
        ix.	Resident Local Education Agency
        x.	Special Pupil Indicator = N
    b.	Data not collected for Early Education
        i.	State Aid Category
        ii.	Membership Attendance Units
        iii.	Membership Attendance Percent Enrolled
        iv.	Special Education Eval Status
        v.	Transportation
2.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = 1) 
    a.	School Id
    b.	Student Unique Id
    c.	Entry Grade Level = 1
    d.	Entry Type (Last Location Code) = 4
    e.	Entry Date = 9/6/2020
    f.	Exit Withdraw Date (Defaulted to end of school year)
    g.	Exit Withdraw Type = 40
    h.	Homebound Service Indicator = N
    i.	Resident Local Education Agency
    j.	Special Pupil Indicator = N
3.	Submit an Early Education Enrollment record (StudentSchoolAssociation with entrygradelevel = PA) 
    a.	School Id
    b.	Student Unique Id
    c.	Entry Grade Level = PA
    d.	Entry Type (Last Location Code) = 4
    e.	Entry Date = 9/6/2020
    f.	Exit Withdraw Date (Defaulted to end of school year)
    g.	Exit Withdraw Type = 40
    h.	Homebound Service Indicator = N
    i.	Resident Local Education Agency
    j.	Special Pupil Indicator = N


## Resource: Parent 
**Description**
This entity represents a parent or guardian of a student, such as mother, father, or caretaker.

**Prerequisite Data**
None

**Scenarios**
1.	Submit Parent Records for the following Early Ed Student in Gradelevel EE
    a.	Required Elements:
        i.	Parent Unique Id
        ii.	firstName
        iii.	lastSurname
        iv.	MiddleName
        v.	generationCodeSuffix
        vi.	highestCompletedLevelOfEducationDescriptor
        vii.	householdIncome
        viii.	householdSize
        ix.	receivingInterpreterAssistance
        x.	classroomVolunteerDescriptor
        xi.	birthDate
        xii.	sexDescriptor
    b.	Submit Parent Records for the following Early Ed Student in Gradelevel 1
    c.	Submit Parent Records for the following Early Ed Student in Gradelevel PA

## Resource: StudentParentAssociation
**Description**
This association relates students to their parents, guardians, or caretakers.

**Prerequisite Data**
- Students
- Parents
- StudentSchoolAssociations

**Scenarios**
1.	Submit Student Parent Association Record for the Early Education Student in Gradelevel EE
    a.	Required Elements:
        i.	Parent Unique Id
        ii.	Student Unique Id
        iii.	Relation Descriptor
2.	Submit Student Parent Association Record for the Early Education Student in Gradelevel 1
3.	Submit Student Parent Association Record for the Early Education Student in Gradelevel PA

## Resource: StudentEducationOrganizationAssociation
**Description**
This association indicates any relationship between a student and an education organization other than how the state views enrollment. Enrollment relationship semantics are covered by StudentSchoolAssociation. **MDE allows for the capture of student demographic data by school enrollment.** Therefore, a StudentEducationOrganizationAssociation record must be submitted for each school in which the student is enrolled to provide the student demographic data provided to the enrolling school by the parent(s). 

**Prerequisite Data**
- Students
- EducationOrganizations (Schools)

**Scenarios**
1.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel EE
    a.	Include all elements except StudentCharacteristicsDescriptors (ADP, RAEL, IMMIGRANT, SLIFE)
2.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel 1
3.	Create a StudentEducationOrganizationAssociation for the Student Enrolled in Gradelevel PA

## Resource: StudentEarlyEducationProgramAssociations
**Description**
This association represents Students in either School Readiness or Early Childhood Family Education programs.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "SR"
- Program - where ProgramTypeDescriptor = "ECFE"
- Students

**Scenarios**
1.	Associate gradelevel EE Enrolled Student with this SR StudentEarlyEducationProgramAssociation
    a.	Begin Date: 9/5/2020
    b.	End Date: 6/11/2021 (default to last day in the school year)
    c.	End Reason Code = PE-01
    d.	Membership: 640
    e.	Attendance: 580
    f.	Submit funding sources PF and CC
2.	Associate same gradelevel EE Enrolled Student with this ECFE StudentEarlyEducationProgramAssociation
    a.	Begin Date =  9/5/2020
    b.	End Date = 10/15/2020 
    c.	End Reason Code = PE-02
    d.	Membership Hours = 40
    e.	Attendance Hours = 30
    f.	Submit funding sources PF, CC and TITLE
3.	Associate gradelevel 1 Enrolled Student with an ECFE StudentEarlyEducationProgramAssociation
    a.	Begin Date: 10/6/2020
    b.	End Date: 6/11/2020  (default to last day in the school year)
    c.	Membership: 640
    d.	Attendance: 580
    e.	Submit funding sources ECFE and CC
4.	Associate gradelevel PA Enrolled Student with an SR StudentEarlyEducationProgramAssociation
    a.	Begin Date: 9/7/2020
    b.	End Date: 6/11/2020  (default to last day in the school year)
    c.	Membership: 640
    d.	Attendance: 580
    e.	Submit funding sources CSPF and OD

## Resource: StudentHomelessProgramAssociation
**Description**
This association represents the McKinney-Vento Homeless Program program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "Homeless"
- Students

**Scenarios**
1.	Submit a StudentHomelessProgramAssociation for the EE enrolled student 
    a.	Primary Nighttime Residence  = SHR
    b.	Begin Date = 9/5/2019
    c.	End Date = 12/25/2020

## Resource: StudentLanguageInstructionProgramAssociation

**Description**
This association represents the Title III Language Instruction for Limited English Proficient and Immigrant Students program(s) that a student participates in or from which the Student receives services.

**Prerequisite Data**
- Schools
- Program - where ProgramTypeDescriptor = "English Learner"
- Students

**Scenarios**
1.	Submit StudentLanguageInstructionProgramAssociation for EE enrolled Student
    a.	Begin Date = 9/5/2019	
    b.	End Date = 5/25/2021
    c.	Lang Service Code = Transitional Bilingual
    d.	EL Participation = 1
