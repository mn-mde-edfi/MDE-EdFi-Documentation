# 2020-2021 Data Requirements and API Resources
This document is part of the MDE Ed-Fi [Vendor and District Test Plan](sis_test_plan_a_toc.md). It is intended to complement and build upon the similarly named section in the [official documentation](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/blob/master/2020-21%20MDE%20Ed-Fi%20Documentation/2020-21%20SIS%20Vendor%20and%20District%20Test%20Plan.docx). For details on the API Resources and Certification Scenarios, see the [Sandbox Certification Scenarios documentation](sandbox_cert_a_toc.md)

## API Documentation
For each of the resources described in this document, the elements/properties required are included and browseable in the [Sandbox Swagger UI](https://test.edfi.education.mn.gov/sb20_/EdFi.Ods.SwaggerUI/) (aka "Swagger") under the **Minnesota-SISVendor-Profile** and the **Minnesota-Twenty-Twenty-One-SISVendor-Profile**.

### Example
As an example, to view the required resource properties for a **studentSchoolAssociation**, open the "POST" action in Swagger:
```POST /ed-fi/studentSchoolAssociations Creates or updates resources based on the natural key values of the supplied resource.```
- _Note:_ "ed-fi" in the path above indicates that this is a core resource.

Properties in a **studentSchoolAssociation** can be viewed as an [example/template JSON object](data\example_template_studentSchoolAssociation.json) by selecting **"Example Value"**:
![ODS API Swagger studentSchoolAssociations Screen Capture](images/ods_api_swagger_studentSchoolAssociations_3.1.1.png?raw=true "ODS API studentSchoolAssociations Example Value")

Definitions and Data Types in the **studentSchoolAssociations** can be viewed by selecting **“Model”** just to the right of the "Example Value" option. Required components are marked with a red *. Often, the actual data posting for an individual record can be much less than what is in the model, as demonstrated in [this example record](data\example_value_studentSchoolAssociation.json).

## Mapping Documentation
School Year 21-22 will introduce the Ed-Fi collection of Minnesota Common Course Catalogue (MCCC) and Graduation Requirements (GRR). (These can be previewed in the 2021-2022 Sandbox Profile.) MCCC will not implement any of the Early Childhood elements at this time.

In addition, MDE is beginning to work toward the eventual collection of Assessment pre-code and Assessment results data for the MCA and MTAS Assessment.  

(In School Year 19-20, MDE implemented an Ed-Fi based MARSS collection.)

For context around how each MDE collection maps to the Ed-Fi Data Standard please view the following spreadsheets:
- [MARSS 2019-2020 Mapping Review Matrix Ed-Fi 3.1.xls spreadsheet](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/blob/master/2020-21%20MDE%20Ed-Fi%20Documentation/2020-21%20Student%20Enrollment%20Data%20Mapping%20Matrix%20Ed-Fi%203.1.xlsx) (MARSS)
- MCCC Mapping Matrix (link TBD)
- GRR Mapping Matrix (link TBD)
- Mapping Matrix MN Assessment Pre-code to Ed-Fi 3.1 (link TBD) (MCA/MTAS Precode and Assessment Results)

The Mapping Review Matrix documents include the mappings between MDE elements and Ed-Fi core and extension entities and elements, in the **Data Elements** tab. Additionally, the Descriptor values applicable to each Collection are also included in these documents for reference, in the remaining tabs of the spreadsheet.

## School Year 20-21 Collection Updates Summary

School Year 20-21 will continue collection of MARSS and Ancestry of Ethnic Origin data via Ed-Fi. In addition, MDE will begin collecting Early Education Enrollment along with Early Education Parent data.

- EE Enrollment includes:
  - StudentSchoolAssociation
  - StudentEducationOrganizationAssociation
  - StudentEarlyEducationProgramAssociation
- EE Parent includes:
  - Parent
  - StudentParentAssociation

**IMPORTANT NOTE:**  The API for MDE’s MCCC, GRR, and MCA/MTAS Assessments has been developed and made available in the 3.1 codebase and in the School Year 20-21 sandbox environment, however integration with the endpoints encompassed in these domains will not be rolled out to districts until 2021-2022.  

The inclusion of these API resources at this early stage is intended to assist vendors with the work required to integrate your application with these collections and begin planning your development effort. With this early release we hope that you will have the ability to plan for the size of the project and plan accordingly. 

Ed-Fi MCCC will start with the 2021-22 data collection based on the current schedule. Additional details coming soon include a mapping of the current data collection to the Ed-Fi standard and details on validations added to EDVP that had been previously done via XML. Timelines for GRR and Assessments via Ed-Fi are to be determined.

## Education Organization Id usage by Resource

Education Organization References in the Ed-Fi API allow an API client to submit either a Local Education Agency, School Id, or PostSecondaryInstitutionId; however the MDE implementation requires that the following ids must be used for Education Organization References:
| Resource  | Element  | ID |
| ----------|----------|----|
| StudentEducationOrganizationAssociation | educationOrganizationReference.educationOrganizationId | School Id|
| StudentProgramAssociation (all program types) | educationOrganizationReference. educationOrganizationId | School Id |
| StudentProgramAssociation (all program types) | programReference.educationOrganizationId | Local Education Agency Id |

## API Resources and Certification Scenarios
For details on the 2020-2021 API Resources and Certification Scenarios, see the [Sandbox Certification Scenarios documentation](sandbox_cert_a_toc.md). That documentation contains resources and scenarios for MARSS, StudentProgramAssociations, and 2020-2021 Early Education Enrollment.

## 2020-2021 MDE Submitted Data Requirements: API Resources
Several of the required data elements are provided by MDE within the ODS. This section details those elements.
### Resource: LocalEducationAgencies

**Description**
This entity represents an administrative unit at the local level which exists primarily to operate schools or to contract for educational services. It includes school districts, charter schools, charter management organizations, or other local administrative organizations.

**Prerequisite Data**
- None

Note: All required Local Education Agency data will be loaded by MDE.

### Resource: Schools

**Description**
This entity represents an educational organization that includes staff and students who participate in classes and educational activity groups.

**Prerequisite Data**
- None

Note: All required School data will be loaded by MDE.

### Resource: Programs

**Description**

*Ed-Fi Description*: This entity represents any program designed to work in conjunction with, or as a supplement to, the main academic program. Programs may provide instruction, training, services, or benefits through federal, state, or local agencies. Programs may also include organized extracurricular activities for students. **MDE will create the following programs for each district with these program types**: 

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

## Ed-Fi Model Dependency Graphs
### MARSS collection
![Ed-Fi Model Dependency Graph for MARSS](images/ed-fi_model_dependency_marss_3.1.1.PNG?raw=true "Ed-Fi Model Dependency Graph for MARSS")
The above image describes the dependencies required to work with the MDE Ed-Fi model as part of MARSS collections. In detail:
1.	Descriptors must be loaded first, as all other resources contain references to descriptor values.
2.	Once descriptors are loaded, Education Organization data must be loaded by MDE.
3.	Though MARSS is centered around student demographics and enrollment, the core Student records must be loaded before students may be enrolled.
4.	Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records. 
5.	Once student enrollment data is loaded, student demographics may be provided via StudentEducationOrganizationAssociation. 
6.	Programs must be loaded for all districts submitting data to the ODS.
7.	StudentProgramAssociations can be loaded once Programs and StudentSchoolAssociations have been loaded.

### Early Education Enrollment and Parent collection
![Ed-Fi Model Dependency Graph for Early Ed](images/ed-fi_model_dependency_early_ed_parent_3.1.1.PNG?raw=true "Ed-Fi Model Dependency Graph for Early Ed")
The above image describes the dependencies required to work with the MDE Ed-Fi model as part of Early Education Enrollment and Parent collection. In detail:
1.	Descriptors must be loaded first, as all other resources contain references to descriptor values.
2.	Once descriptors are loaded, Education Organization data must be loaded by MDE.
3.	The core Student records must be loaded before students may be enrolled.
4.	Student enrollment data must be provided via StudentSchoolAssociation in order to establish a valid security claim before any other updates may be made to student records. 
5.	Once student enrollment data is loaded, student demographics may be provided via StudentEducationOrganizationAssociation. 
6.	Early Education Programs must be loaded for all districts submitting data to the ODS.
7.	StudentProgramAssociations can be loaded once Programs and StudentSchoolAssociations have been loaded.
8.	Parent Records, Students and Enrollment records are required prior to setting the Student Parent Association.

# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)
- [Advance to Staging Environment Load and Quality Check](sis_test_plan_d_staging.md)