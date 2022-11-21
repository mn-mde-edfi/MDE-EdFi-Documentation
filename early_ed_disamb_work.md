# Early Education Disambiguation Workaround
>For **school year 2023-24**, MDE will be implementing an "Early Education disambiguation project" that will allow districts to enroll students in both a "non-MARSS Early Education program" and a "MARSS Early Education program" at the same school, at the same time period. 

This document describers the *workaround* for **school years 2021-22 and 2022-23** when building and submitting records for these students. We are including tabular descriptions designed for a district audience, and links to JSON examples designed for vendors.

This scenario detailed here describes a student enrolled in an ECSE school (such as [Bloomington ECSE 0271-01-502](https://public.education.mn.gov/MdeOrgView/organization/show/1800)) that is also attending ECFE **and** School Readiness programs. For brevity, we are describing **only** the unique elements required to understand this workaround, not all of the requirements of each record.

## Student School Association Records
Student School Association (SSA) records can be considered enrollment records. This scenario requires *two* SSA records to be built in order to handle the MDE requirements. 

**SSA Record 1 - Grade EC**
This record will be used to meet MDE's MARSS requirements. As a result, the grade will be "EC" and the enrollment date will be the actual enrollment date of the student in the school.

| Data Element | Data to Enter |Ed-Fi element| Notes / Description |
| ---- |:-----:|-----| ---|
|School ID | **10271502**|  "schoolReference": "schoolId" | |
|Student ID |**10271000999001**|   "studentReference": "studentUniqueId"|Use MARRS number |
|Enrollment Date| **2022-09-06** |"entryDate" |Should be the **actual enrollment date** of the student |
|Grade| **EC**|"entryGradeLevelDescriptor" |Be sure the record with the actual enrollment date is for EC|

**SSA Record 2 - Grade EE**
This record will be used to satisfy MDE's Early Education program participation requirements. As a result, the grade will be "EE". In order to allow two SSA records at the same school, offset the enrollment date by one day.
| Data Element | Data to Enter |Ed-Fi element| Notes / Description |
| ---- |:-----:|-----| ---|
|School ID | **10271502**|  "schoolReference": "schoolId" |Same as SSA record 1 |
|Student ID |**10271000999001**|   "studentReference": "studentUniqueId"|Same as SSA record 1 |
|Enrollment Date| **2022-09-07** |"entryDate" |**Unofficial Date**: Offsetting the date by one day from the actual enrollment allows you to submit multiple SSA records for the same student, but with different grade levels. |
|Grade| **EE**|"entryGradeLevelDescriptor" | |

## Student Early Education Program Association Records
Student Early Education Program Association (SEEPA) records are specific types of Program Association Records. Now that our example student has been associated to the ECSE school with two unique records, the SEEPA records must be built as follows in order to properly enable MDE processing.

**SEEPA Record 1 - Grade EC for ECFE**
| Data Element | Data to Enter |Ed-Fi element| Notes / Description |
| ---- |:-----:|-----| ---|
|School ID | **10271502**| "educationOrganizationReference": "educationOrganizationId" | |
|Student ID |**10271000999001**|   "studentReference": "studentUniqueId"||
|Enrollment Date| **2022-09-06** |"beginDate" |Should match the **actual enrollment date** of the student, as described in SSA record 1 |
|Program| **EE-ECFE**|  "programReference": "programTypeDescriptor" ||

**SEEPA Record 2 - Grade EE for EE-SR**
| Data Element | Data to Enter |Ed-Fi element| Notes / Description |
| ---- |:-----:|-----| ---|
|School ID | **10271502**|  "educationOrganizationReference": "educationOrganizationId" ||
|Student ID |**10271000999001**|   "studentReference": "studentUniqueId"||
|Enrollment Date| **2022-09-07** |"beginDate" |Should match the **unofficial date** used in SSA record 2 |
|Program| **EE-SR**|"programReference": "programTypeDescriptor" | |

*Note*: technically the date and other data can be the same for each SEEPA, and both records will be created (the second one will not overwrite the first one, even with the same date). Offsetting the date on the EE-SR record helps us process the program association properly with this workaround.