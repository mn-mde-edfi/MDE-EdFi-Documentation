# Data Requirements and API Resources
This document is part of the MDE Ed-Fi [Vendor and District Test Plan](sis_test_plan_a_toc.md).  For details on the API Resources and Certification Scenarios, see the [Sandbox Certification Scenarios documentation](sandbox_cert_a_toc.md)

## API Documentation
For each of the resources described in this document, the elements/properties required are included and browseable in the Sandbox Swagger UI (aka "Swagger") under the current profile. (More information about Swagger is in the [Sandbox Certification Testing document](sis_test_plan_b_cert_testing.md).)

### Example
As an example, to view the required resource properties for a **studentSchoolAssociation**, open the "POST" action in Swagger:
```POST /ed-fi/studentSchoolAssociations Creates or updates resources based on the natural key values of the supplied resource.```
- _Note:_ "ed-fi" in the path above indicates that this is a core resource.

Properties in a **studentSchoolAssociation** can be viewed as an [example/template JSON object](data\example_template_studentSchoolAssociation.json) by selecting **"Example Value"**:
![ODS API Swagger studentSchoolAssociations Screen Capture](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ods_api_swagger_studentSchoolAssociations_3.1.1.png?raw=true "ODS API studentSchoolAssociations Example Value")

Definitions and Data Types in the **studentSchoolAssociation** can be viewed by selecting **“Model”** just to the right of the "Example Value" option. Required components are marked with a red *. Often, the actual data posting for an individual record can be much less than what is in the model, as demonstrated in [this example record](data\example_value_studentSchoolAssociation.json).

## Mapping Documentation
For context around how each MDE collection "maps" to the Ed-Fi Data Standard please view the Mapping Matrix spreadsheets published in the "(YYYY-YY School Year) MDE Ed-Fi Documentation" folders [at the top of this repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation).

Each school year's Data Mapping Matrix spreadsheet includes the mappings between MDE elements and Ed-Fi core and extension entities and elements, in the **Data Elements** tab. Whereas previously these spreadsheets also contained tabs for custome descriptor values, those are now accessible within the [descriptorTables folder](./descriptorTables/). (See the "AboutDescriptorTables" markdown document within that folder.)

## Education Organization Id usage by Resource

Education Organization References in the Ed-Fi API allow an API client to submit either a Local Education Agency, School Id, or PostSecondaryInstitutionId; however the MDE implementation **requires** that the following identifiers must be used for Education Organization References:
| Resource  | Element  | ID |
| ----------|----------|----|
| StudentEducationOrganizationAssociation | educationOrganizationReference.educationOrganizationId | School Id|
| StudentProgramAssociation (all program types) | educationOrganizationReference.educationOrganizationId | School Id |
| StudentProgramAssociation (all program types) | programReference.educationOrganizationId | Local Education Agency Id |
|Course |educationOrganizationReference.educationOrganizationId|District Course - **LocalEducationAgencyId**; State Course (loaded by MDE) - **StateEducationAgencyId**; College Course - **postSecondaryInstitutionId**|
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

*Ed-Fi Description*: This entity represents any program designed to work in conjunction with, or as a supplement to, the main academic program. Programs may provide instruction, training, services, or benefits through federal, state, or local agencies. Programs may also include organized extracurricular activities for students. **MDE will automatically create programs for each LEA** with the program types identified in the [ProgramTypeDescriptor table](/descriptorTables/ProgramTypeDescriptor.csv).

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
![Ed-Fi Model Dependency Graph for MCCC](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/ed-fi_model_dependency_mccc_5.2.PNG?raw=true "Ed-Fi Model Dependency Graph for MCCC")

The above image describes the dependencies required to work with the MDE Ed-Fi model as part of the MCCC collection. In detail:
1. Descriptors must be loaded first, as all other resources contain references to descriptor values.
2. Several other dependencies are loaded by MDE:
    - Education Organizations
    - Colleges (in the PostSecondaryInstitution resource) 
    - State Courses (associated with the StateEducationAgency)
    - Staff records 
3. The core Student records must be loaded before students may be enrolled in courses.
4. Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records.
5. Grading Periods can be created after Education Organizations, and must be created before students can be assigned course grades.
6. Sessions and Class Periods can be loaded after Education Organizations. Sessions must be loaded before Course Offerings, and Class Periods must be loaded before Sections.
7. Courses and CourseCourse Associations can be loaded after Education Organizations.
8. After Courses are created, Course Offerings can be loaded, and then Sections after that.
9. Staff Section Associations, and StudentSectionAssociations can be loaded after Sections. 
10. Once Student Section Associations are created, course Grades can be assigned using references to the Grading Periods.

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
As described above, each student must first have a StudentSchoolAssociation record (an enrollment record). Starting in SY2023-24, all EE enrollments used grade 'EE' due to the resolution described in the [EE-MARSS conflict resolution document](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2023-24%20MDE%20Ed-Fi%20Documentation/early_ed_marss_conflict_resolution.pdf).

# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)
- [Advance to Staging Environment Load and Quality Check](sis_test_plan_d_staging.md)