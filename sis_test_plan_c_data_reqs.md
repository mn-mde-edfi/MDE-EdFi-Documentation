# 2022-2023 Data Requirements and API Resources
This document is part of the MDE Ed-Fi [Vendor and District Test Plan](sis_test_plan_a_toc.md). It is intended to complement and build upon the similarly named section in the [official documentation](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/blob/master/2021-22%20MDE%20Ed-Fi%20Documentation/2021-22%20SIS%20Vendor%20and%20District%20Test%20Plan.docx). For details on the API Resources and Certification Scenarios, see the [Sandbox Certification Scenarios documentation](sandbox_cert_a_toc.md)

## API Documentation
For each of the resources described in this document, the elements/properties required are included and browseable in the [Sandbox Swagger UI](https://test.edfi5.education.mn.gov/swagger/) (aka "Swagger") under the current profile.

### Example
As an example, to view the required resource properties for a **studentSchoolAssociation**, open the "POST" action in Swagger:
```POST /ed-fi/studentSchoolAssociations Creates or updates resources based on the natural key values of the supplied resource.```
- _Note:_ "ed-fi" in the path above indicates that this is a core resource.

Properties in a **studentSchoolAssociation** can be viewed as an [example/template JSON object](data\example_template_studentSchoolAssociation.json) by selecting **"Example Value"**:
![ODS API Swagger studentSchoolAssociations Screen Capture](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ods_api_swagger_studentSchoolAssociations_3.1.1.png?raw=true "ODS API studentSchoolAssociations Example Value")

Definitions and Data Types in the **studentSchoolAssociation** can be viewed by selecting **“Model”** just to the right of the "Example Value" option. Required components are marked with a red *. Often, the actual data posting for an individual record can be much less than what is in the model, as demonstrated in [this example record](data\example_value_studentSchoolAssociation.json).

## Mapping Documentation
For context around how each MDE collection maps to the Ed-Fi Data Standard please view the Mapping Matrix spreadsheets published in the "(YYYY-YY School Year) MDE Ed-Fi Documentation" folders [at the top of this repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation).

Each school year's Data Mapping Matrix spreadsheet includes the mappings between MDE elements and Ed-Fi core and extension entities and elements, in the **Data Elements** tab. Additionally, the Descriptor values applicable to each Collection are also included in these documents for reference, in the remaining tabs of the spreadsheet. (We are currently testing out a process to automate custom descriptor CSVs as exports from the database, allowing you to view individual descriptor tables as well as more easily visualize changes and history.)

## Education Organization Id usage by Resource

Education Organization References in the Ed-Fi API allow an API client to submit either a Local Education Agency, School Id, or PostSecondaryInstitutionId; however the MDE implementation **requires** that the following identifiers must be used for Education Organization References:
| Resource  | Element  | ID |
| ----------|----------|----|
| StudentEducationOrganizationAssociation | educationOrganizationReference.educationOrganizationId | School Id|
| StudentProgramAssociation (all program types) | educationOrganizationReference. educationOrganizationId | School Id |
| StudentProgramAssociation (all program types) | programReference.educationOrganizationId | Local Education Agency Id |
|Course |educationOrganizationReference.educationOrganizationId|District Course – **LocalEducationAgencyId**; State Course (loaded by MDE) – **StateEducationAgencyId**; College Course – **postSecondaryInstitutionId**|
| CourseOffering | SchoolReference; CourseReference | SchoolId; EducationOrganizationId on the Course record |
| ClassPeriod | SchoolReference | SchoolId |
| Section | CourseOfferingReference; ClassPeriodReference | SchoolId; SchoolId |
| studentSectionAssociation | sectionReference.CourseOfferingReference | SchoolId |
| StaffSectionAssociation | sectionReference.CourseOfferingReference | SchoolId |
| Grade | StudentSectionAssociationReference.sectionReference.CourseOfferingReference | SchoolId |
| GradingPeriod | SchoolReference | SchoolId |

## API Resources and Certification Scenarios
For details on the current API Resources and Certification Scenarios, see the [Sandbox Certification Scenarios documentation](sandbox_cert_a_toc.md). That documentation contains resources and scenarios for the various programs MDE has incorporated into Ed-Fi.

## Read-Only API endpoints 
Several of the required data elements are provided by MDE within the ODS. This section details those elements.

### Resource: LocalEducationAgencies

**Description**
This entity represents an administrative unit at the local level which exists primarily to operate schools or to contract for educational services. It includes school districts, charter schools, or other local administrative organizations.

**All required Local Education Agency data will be loaded by MDE.**

### Resource: Schools

**Description**
This entity represents an educational organization that includes staff and students who participate in classes and educational activity groups.

**All required School data will be loaded by MDE.**

### Resource: Post-Secondary Institutions

**Description**

An organization that provides educational programs for individuals who have completed or otherwise left educational programs in secondary school(s).

**All required College data will be loaded by MDE.**

### Resource: Course (State Level Only)

**Description**

This educational entity represents the organization of subject matter and related learning experiences provided for the instruction of students on a regular or systematic basis.

**Prerequisite Data**

- Education Organization for State Education Agency (SEA)

**All required State Course data will be loaded by MDE.**

### Resource: Staff

**Description**

This entity represents an individual who performs specified activities for any public or private education institution or agency that provides instructional and/or support services to students or staff at the early childhood level through high school completion. For example, this includes:

1. An "employee" who performs services under the direction of the employing institution or agency is compensated for such services by the employer and is eligible for employee benefits and wage or salary tax withholdings.
2. A "contractor" or "consultant" who performs services for an agreed upon fee or an employee of a management service contracted to work on site.
3. A "volunteer" who performs services on a voluntary and uncompensated basis.
4. An in-kind service provider.
5. An independent contractor or businessperson working at a school site.

**Sync process will be created by MDE to populate Staff Tables.**

### Resource: Program

**Description**

*Ed-Fi Description*: This entity represents any program designed to work in conjunction with, or as a supplement to, the main academic program. Programs may provide instruction, training, services, or benefits through federal, state, or local agencies. Programs may also include organized extracurricular activities for students. **MDE will create the following programs with these program types**: 

- Section 504 Plan
- Title I Part A
- English Learner
- Gifted and Talented
- Special Education
- 21st Century Learning Center Grant
- Alternative Delivery Of SIS
- Coordinated Early Intervening Services
- Homeless
- PSEO Concurrent
- PSEO Program
- School Food Service
- Early Childhood Screening
- SAAP
- School Readiness
- Early Childhood Family Education

## Ed-Fi Model Dependency
Ed-Fi uses a data-dependency security model that enforces the order of creation when inserting various records via the API. This is often encountered via API errors such as the following:
>```Authorization denied. The claim does not have any established relationships with the requested resource.```

The Ed-Fi Alliance calls this type of error "Dependency order enforced by authorization". More documentation on dependency order by entity relationships or by authorization is available in the [Ed-Fi 5.2 tech docs](https://techdocs.ed-fi.org/display/ODSAPIS3V520/Resource+Dependency+Order).

Graphs demonstrating the dependencies of various data resources in MDE's collections are below, and a [basic overview PDF](images/ed-fi_model_dependency_mde_collections.pdf) of the various MDE collections is available.

### MARSS collection
![Ed-Fi Model Dependency Graph for MARSS](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ed-fi_model_dependency_marss_3.1.1.PNG?raw=true "Ed-Fi Model Dependency Graph for MARSS")
The above image describes the dependencies required to work with the MDE Ed-Fi model as part of MARSS collections. In detail:
1.	Descriptors must be loaded first, as all other resources contain references to descriptor values.
2.	Once descriptors are loaded, Education Organization data must be loaded by MDE.
3.	Though MARSS is centered around student demographics and enrollment, the core Student records must be loaded before students may be enrolled.
4.	Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records. 
5.	Once student enrollment data is loaded, student demographics may be provided via StudentEducationOrganizationAssociation. 
6.	Programs must be loaded for all districts submitting data to the ODS.
7.	StudentProgramAssociations can be loaded once Programs and StudentSchoolAssociations have been loaded.

### MCCC Collection
![Ed-Fi Model Dependency Graph for MCCC](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ed-fi_model_dependency_mccc_3.1.1.PNG?raw=true "Ed-Fi Model Dependency Graph for MCCC")

The above image describes the dependencies required to work with the MDE Ed-Fi model as part of the MCCC collection. In detail:
1. Descriptors must be loaded first, as all other resources contain references to descriptor values.
2. Once descriptors are loaded, Education Organization data must be loaded by MDE. For the MCCC data collection, Colleges will be loaded to the PostSecondaryInstitution resource to allow the association of a college to a college level course. State courses are associated with the StateEducationAgency.
3. The core Student records must be loaded before students may be enrolled in courses.
4. Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records
5. Courses, course offerings, and sections can be loaded after Education Organizations. State Courses are pre-loaded by MDE. 
6. Class Periods can be loaded after Education Organizations.
7. Staff, Staff Section Associations, and StudentSectionAssociations can be loaded after Sections. 
8. Once student section enrollment data is loaded, grades and grading period assications can be assigned.

### Early Education Enrollment and Parent collection
![Ed-Fi Model Dependency Graph for Early Ed](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ed-fi_model_dependency_early_ed_parent_3.1.1.PNG?raw=true "Ed-Fi Model Dependency Graph for Early Ed")
The above image describes the dependencies required to work with the MDE Ed-Fi model as part of Early Education Enrollment and Parent collection. In detail:
1.	Descriptors must be loaded first, as all other resources contain references to descriptor values.
2.	Once descriptors are loaded, Education Organization data must be loaded by MDE.
3.	The core Student records must be loaded before students may be enrolled.
4.	Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records. (See more details below.) 
5.	Once student enrollment data is loaded, student demographics may be provided via StudentEducationOrganizationAssociation. 
6.	Early Education Programs must be loaded for all districts submitting data to the ODS.
7.	StudentProgramAssociations can be loaded once Programs and StudentSchoolAssociations have been loaded.
8.	Parent Records, Students and Enrollment records are required prior to setting the Student Parent Association.

#### Grade / Enrollment Requirements for Early Education Enrollment
As described above, each student must first have a StudentSchoolAssociation record (an enrollment record). For EE Enrollment, allowable grades are EC, K-3 or EE. 
* Use Grade EE if the student is not already enrolled in a regular grade
* Use Grade EE if the EE program service is provided in a different school than the regular grade.

Once the enrollment record exists, one or both of the EE Program Associations may then be assigned to the student.
* Students in Grade EC, K-3 may only have an EE-ECFE program assigned; they cannot have an EE-SR program assignment.
* Only Grade EE students may have an EE-SR program.
* Grade EE students may also have an EE-ECFE program alone or in combination with an EE-SR program.


# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)
- [Advance to Staging Environment Load and Quality Check](sis_test_plan_d_staging.md)