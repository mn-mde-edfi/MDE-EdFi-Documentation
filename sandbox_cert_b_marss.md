_This document is a stub and is currently being built. In the official documentation, the data resource and sandbox certification scenarios were repeated in both the test plan an dthe certification scenarios documents. In the Markdown versions, we'll consolidate that information into this certification scenarios area, performing random spot-checks of cross-references.
--mdolbow 2020.06.22_
# 2020-2021 SIS Submitted MDE Ed-Fi API Resources: MARSS Data Collection
## Resource: Students

**Description**

This entity represents an individual for whom instruction, services, and/or care are provided in an early childhood, elementary, or secondary educational program under the jurisdiction of a school, education agency or other institution or program. A student is a person who has been enrolled in a school or other educational institution.

**Prerequisite Data**

- None

**Certification Scenarios**
1.	Create 14 student records including the following elements:
    a.	studentUniqueID
    b.	birthdate
    c.	birthSexDescriptor
    d.	firstName
    e.	generationCodeSuffix
    f.	lastSurname
    g.	middleName

## Resource: StudentSchoolAssociations

**Description**

This association represents the School in which a student is enrolled. The semantics of enrollment may differ slightly by state. Non-enrollment relationships between a student and an education organization may be described using the StudentEducationOrganizationAssociation.


**Prerequisite Data**

- Students
- Schools

**Certification Scenarios**

1.	Enroll student 1 at Elementary School, including:
    a.	homeboundServiceIndicator
    b.	specialPupilIndicator
2.	Enroll student 2 at Middle School. 
3.	Withdraw student from Middle School.
4.	Enroll student 2 at High School.
5.	Create the following records for Student 2:
    a.	An enrollment
    b.	Withdrawal 
    c.	Re-enrollment of a student who changes resident districts but does not change schools.  Place a 20 day gap between records. 
6.	Update Student 1’s Percent Enrolled to 50% and set membershipAttendanceUnitDescriptor to days, set membership and attendance.
7.	Update Student 1’s Percent Enrolled to 100% membershipAttendanceUnitDescriptor to hours and adjust membership and attendance accordingly.
8.	Update Student 2’s Transportation Category.
9.	Update Student 3’s StateAid Category.
10.	Create 2 enrollment records (a, b) for a student that is in two different schools within the same district at the same time.  Enrollment dates 09/10/17 through 06/10/18.  
11.	Create the records for: 
    a.	An enrollment, 
    b.	Withdrawal and 
    c.	Re-enrollment for a kindergarten student who receives an IEP mid-year – send updated special education evaluation status. (Grade change from KA to HK, and specialEducationEvaluationStatus updated)