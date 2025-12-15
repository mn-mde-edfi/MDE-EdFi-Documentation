# Sandbox Certification Scenarios for Postponed Data Collections from 2022
Several new data collections originally planned for rollout using Ed-Fi during the 2022-2023 school year are currently **postponed until further notice**. The certification scenarios for these postponed data collections are documented below.

> NOTE: Documentation has been removed for any postponed data collection that MDE has since decided is no longer needed.

  - [Language Academic Honors](#language-academic-honors) 
  - [Gender Identity and Preferred Pronouns](#gender-identity-and-preferred-pronouns)
  - [Student Preferred Name ](#student-preferred-name)
  - [Title I Part D Neglected Or Delinquent Program](#title-i-part-d-neglected-or-delinquent-program)
  - [Online Learning](./sandbox_cert/sandbox_cert_e_mccc.md#online-learning)

**School Attribute Certification Scenarios**

A new resource has been created for the purpose of collecting school-level data. Ed-Fi School records are currently created and maintained by MDE. A separate SchoolAttributes extension captures school-level data to be provided by the districts for their respective schools.

  - [Title I Part A School Designation](#title-i-part-a-school-designation)
  - [Virtual School Status](#virtual-school-status)
  
## Language Academic Honors
This collection object within the SEOA records one or more Student Academic distinctions awarded for languages including World Languages Proficiency Certificate, Bilingual Seal, and Multilingual Seal. 

Language Academic Honor information was previously collected from districts via a Microsoft Word Form in aggregate. For more information about this collection, we encourage vendors to visit:
  - The MDE web page about [World Languages](https://education.mn.gov/MDE/dse/stds/world/)
  - The [Microsoft Word Form](https://education.mn.gov/mdeprod/idcplg?IdcService=GET_FILE&dDocName=MDE086116&RevisionSelectionMethod=latestReleased&Rendition=primary) previously used to collect the information in aggregate.
  - The MDE web page about the [Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/)
  - The [FAQ page for the Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/PROD034397)

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

**Note 1:** The ```honor description``` text field is optional from a policy standpoint, but given the way we have it modeled after the Ed-Fi academic honor resource, that field is part of the unique identification of an honor for a student. Therefore, we are unable to make it optional in the API, and we recommend vendors repeat the short description of the Achievement Category within the ```honor description``` text field. If a student is receiving more than one honor, we recommend merely iterating the description, like "Bilingual or Multilingual Seals-1", "Bilingual or Multilingual Seals-2", etc. No matter how vendors choose to fill that field, it must be unique for the student.

**Note 2:** As of school year 2023-24, we do not have the structures of this collection exposed in the Swagger endpoints, because it is still postponed. If and when we begin this collection, we will work to ensure that the structures are visible in Swagger. Nevertheless, vendors programming in advance for this work should still be able to submit test records, and an [example SEOA JSON record](./data/2022-2023%20Extensions/StudentEducationOrganizationAssociation.json) is available to reference. 

## Gender Identity and Preferred Pronouns
The Gender Identity collection object records a Student's gender identity. (This may be different from SEOA.Sex & Student.BirthSex, which collect the student's gender as reported to the federal government). The Preferred Pronouns extension records a Student's personal preferred pronouns. Both are delivered via the SEOA.

Districts are expected to send both gender identity and preferred pronoun values, although they are optional.

**Prerequisite Data**
-	Schools
-	Students

**Scenarios**
1. Create a StudentEducationOrganizationAssociation with a single Gender Identity value and a single Preferred Pronoun value.
2. Create a StudentEducationOrganizationAssociation with multiple Gender Identity values and multiple Preferred Pronoun values.

## Student Preferred Name
The student's preferred name uses the "otherNames" collection element within the MN extension of ```studentEducationOrganizationAssociation```.

**Prerequisite Data**
-	Students
-	Student Education Organization Association

**Scenarios**
-	Demonstrate the ability to add a preferred name for a student
-	Demonstrate the ability to remove a preferred name for a student
-	Demonstrate the ability to change a preferred name for a student
-	Repeat for first, last, middle, and generation suffix

## Title I Part D Neglected Or Delinquent Program

**Description**
This association represents the Title I Part D Neglected or Delinquent program(s) that a student participates in or from which the Student receives services. Vendors may want to use [the sample JSON](../data/2022-2023%20Extensions/StudentNeglectedOrDelinquentProgramAssociations.json) for this association to better understand the data model.

**Prerequisite Data**
- 5 Students
- Student School Association
- Program - where ProgramTypeDescriptor = "Neglected or Delinquent" (MDE should have one of these pre-loaded for each LEA in the API, with a ```programName``` of "Neglected or Delinquent Program", and a ```programTypeDescriptor``` of ```"uri://education.mn.gov/ProgramTypeDescriptor#Neglected or Delinquent"```.)

Note: be sure to be testing code with a new, minimal sandbox in order to get the latest descriptor values, etc.

**Scenarios**

Using the ```/ed-fi/studentNeglectedOrDelinquentProgramAssociations``` resource, create a Neglected or Delinquent Program Association for 5 students as detailed below. For each scenario:
1. The programReference element should point to the appropriate LEA program preloaded (as described above in Prerequisite Data). 
2. Use the ```neglectedOrDelinquentProgramDescriptor``` element, and the appropriate descriptor value (see [this table](../descriptorTables/NeglectedOrDelinquentProgramDescriptor.csv)), to assign the specific Program Association (Neglected, Juvenile detention, At-risk, etc)
3. Begin Date and End Date for the Program Association are at the top level of the resource.
4. Math and ELA progress level descriptors are at the top level of the resource.
5. Program *Service* data, since there can be multiples, are in a collection called ```neglectedOrDelinquentProgramServices```. See [this table](../descriptorTables/NeglectedOrDelinquentProgramServiceDescriptor.csv) for descriptor values. Each of these needs a begin and end date and one value needs to be indicated as primary.
6. "In Program" and "Exited" outcomes are within the "mn" extension. Both types of outcomes reference the same outcome descriptor values (see [this table](../descriptorTables/NeglectedOrDelinquentProgramOutcomeDescriptor.csv)). Use ```neglectedOrDelinquentProgramOutcomeDescriptor``` to designate an in-program outcome, and ```exitedNeglectedOrDelinquentProgramOutcomeDescriptor``` to designate an exited outcome.

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

## Title I Part A School Designation

While the Title I Part A designation is available for *get* (read only) requests on the *school* resource in the API, using the School Attribute resource provides districts a way to *post* (write) information about this designation.

**Prerequisite Data**
  - Schools (loaded by MDE)
  - Use of an API endpoint containing:
    - the new /MN/schoolAttributes resource ("schoolAttributes")
    - ```titleIPartASchoolDesignationDescriptors```

**Scenarios**
 - Submit a designation of ```Schoolwide``` for an elementary school
 - Submit a designation of ```Targeted Assistance``` for a high school
 - Remove the ```Schoolwide``` designation from the elementary school

## Virtual School Status

Defines schools that are self-designating as virtual schools beyond state-designated Online Learning providers. For example, when using blended learning and other hybrid combinations.

**Prerequisite Data**
  - Schools (loaded by MDE)
  - Use of an API endpoint containing:
    - the new /MN/schoolAttributes resource ("schoolAttributes")
    - Indicator and Indicator Level Descriptors

**Scenarios**
  - Add the "VSS" Indicator Descriptor to two schools via the *schoolAttributes* resource and *educationOrganizationIndicators* collection, then:
    - For School 1 (a school that is not classified as type 46):
      - Set the Indicator Level Descriptor to FACEVIRTUAL
    - For School 2 (a school that is classified as 46):
      - Set the Indicator Level Descriptor to FACEVIRTUAL
  - Change School 1's Virtual School Status Level from FACEVIRTUAL to FULLVIRTUAL
  - Change School 2's Virtual School Status Level from FACEVIRTUAL to SUPPVIRTUAL
  - Change School 1's Virtual School Status Level from FULLVIRTUAL to NOTVIRTUAL

