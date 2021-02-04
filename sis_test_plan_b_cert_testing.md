# Sandbox Certification Testing
When certification begins, vendors will be provided a key and secret to a sandbox [Operational Data Store (ODS)](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Operational+Data+Store+and+API), accessible via API. This ODS will contain the Minnesota Education School and District records synchronized with [MDE ORG](https://public.education.mn.gov/MdeOrgView/), as well as the MN specific descriptors listed in this documentation. When submitting data for each of the Certification scenarios, we ask that you use a district you have access to, and schools within the district.

## Accessing the Sandbox
_Please note_ starting in 2020, sandbox environments were given ```sbYY_``` in the base paths for the API. Thus, for school year 2021-2022 the base sandbox URL is ```https://test.edfi.education.mn.gov/**sb21_**/```. This change will likely require a change in your integration code.

### Sandbox Admin Website
As part of Sandbox certification, you will need access to the [Sandbox Admin Site](https://test.edfi.education.mn.gov/sb21_/EdFi.Ods.Admin.Web). To request an account, [contact MDE by email](mailto:EdFiProjectSupportMNIT.MDE@state.mn.us). In the Sandbox Admin Site, you will be able to create ODS instances to use for development and testing of your integrations. ([The Ed-Fi TechDocs](https://techdocs.ed-fi.org/display/ODSAPI31/Using+the+Sandbox+Administration+Portal) have more detailed instructions on setting up sandboxes.)

### Swagger UI
Ed-Fi uses the [Swagger UI tool](https://swagger.io/tools/swagger-ui/) to visualize and interact with the ODS API. Developers can access this [UI for MDE's Sandbox](https://test.edfi.education.mn.gov/sb21_/EdFi.Ods.SwaggerUI/) to test-drive Create, Read, Update, and Delete (CRUD) actions before building integrations as necessary.

_Please note:_ MDE’s Swagger website has been customized to remove the generic "Resources" section. All MN Specific resources can be found under the Profiles for each School Year. Note the order of the following Profiles is alphabetical, not chronological:

- A preview of future releases is under the generic-named _Minnesota-Preview-SISVendor-Profile_.
- All MN Specific resources defined for the **2021-2022** School Collection can be previewed under the **Minnesota-Twenty-One-Twenty-Two-SISVendor-Profile.**
- All MN Specific resources defined for the _2020-2021_ School Collection can be found under the _Minnesota-Twenty-Twenty-One-SISVendor-Profile_.
- The Identities Section is not functional in the Sandbox and is provided as documentation only

Upon launch of the Swagger Sandbox UI, the site will finish loading the profiles and appear as follows:
![ODS API Landing Page Screen Capture](images/ods_api_sandbox_landing_3.1.1.png?raw=true "ODS API Landing Page")
Clicking one of the profile links will launch you into the Swagger UI for exploration. Once inside the Swagger UI, click the "Authorize" button to enter in the client id (key) and client secret created in the Sandbox Admin site.

### Sandbox Base and OAuth URLs
Developers can further test their code integrations at the URLs in this section. The base URL for the ODS/API is: ```https://test.edfi.education.mn.gov/sb21_/edfi.ods.webapi/data/v3/```

#### Extension vs. Core Resources
Note that Ed-Fi URLs vary based on whether or not core Ed-Fi standard or MN extensions are being accessed:
- **Extensions**: The URL for addressing MN extension resources should include ‘mn’ after v3. For example, when addressing _studentSection504PlanProgramAssociations_, a Minnesota extension entity, the URL is: ```…/edfi.ods.webapi/data/v3/MN/studentSection504PlanProgramAssociations```
- **Core**: The URL for addressing core resources should include ‘ed-fi’ after v3. For example, when addressing _StudentSchoolAssociation_, a core Ed-Fi entity, the URL is: ```…/edfi.ods.webapi/data/v3/ed-fi/StudentSchoolAssociation```

**Important Note:** the school year must be included after **“/v3/”** and before the core/extension namespace in Stage and Production, but **not in Sandbox**. For example:
```…/edfi.ods.webapi/data/v3/2022/ed-fi/StudentSchoolAssociation```
```…/edfi.ods.webapi/data/v3/2022/MN/studentSection504PlanProgramAssociations```

The Sandbox ODS/API oauth URL is: ```https://test.edfi.education.mn.gov/sb21_/edfi.ods.webapi/oauth/```

Authentication In Ed-Fi 3.x ODS/API uses two-legged OAuth 2.0 Client Credentials Grant Flow. More information and sample API calls are located in [the Ed-Fi tech docs](https://techdocs.ed-fi.org/display/ODSAPI32/Authentication).

## Sandbox Tips
- In the staging and production environments, SIS vendor API keys will be associated with a claim set limiting access to only the API resources included in this document. This claim set has been enabled in the Sandbox environment. When you access a resource not included in the claim set you will receive the following message in the response: ```Access to the resource could not be authorized. Are you missing a claim?```
- In the sandbox, multiple SIS Vendor profiles have been created, limiting access to specific properties on each of the resources required in the referenced school year. These appear in the right-hand side of the "Profiles" section and are named as above.
    - These profiles tied to your key and secret, and are auto-enabled in Staging and Production – meaning you will not have to include the profile in the “accept” or “content-type” headers of the request for the profile to take effect. (See more details in the [Staging Environment Load and Quality Check section](sis_test_plan_d_staging.md#staging-environment-load-and-quality-check))
- When creating a sandbox, you have the option of including a set of sample data in the sandbox. The sample data used, is associated with St. Paul Public School District (LocalEducationAgencyId = 10625000). When you do not select the option to include sample data, your sandbox database will be loaded with an essentially empty ODS, except that it will include MN Schools and Districts, and the Descriptors that MDE has customized for this implementation.  

- The actual certification test will be conducted in a sandbox with no sample data loaded and you will reference your own MDE Schools, Districts and Descriptors in the Scenarios.
- The Sandbox environment ignores the School Year included in the API base URL. When preparing submissions to Staging and Production, remember to include the year, i.e. "2022". 
- The School IDs and District IDs used for the ODS/API resources are the MDE State Organization IDs (stateOrganizationID). See section below for details.
- MN custom descriptor codes have been loaded under the namespace ```uri://education.mn.gov/```
- All Descriptor references require namespaces, and do not rely on the concept of a default operational context. Descriptor references must be formatted as follows: ```uri://[organization indicator]/[name of descriptor]#[code value]``` For example: ```uri://education.mn.gov/ProgramTypeDescriptor#Special Education```
  - This can be seen when updating a studentSchoolAssociation record. For example, within the MN extension part of the record (shown below), the code value for ```membershipAttendanceUnitDescriptor``` is not merely "Days", but **"MembershipAttendanceUnitDescriptor#Days"**:
  ```javascript
  "_ext": {
    "MN": {
      "homeboundServiceIndicator": true,
      "specialPupilIndicator": true,
      "residentLocalEducationAgencyReference": {
        "localEducationAgencyId": 10625000
      },
      "membership": {
        "membershipAttendanceUnitDescriptor": "uri://education.mn.gov/MembershipAttendanceUnitDescriptor#Days",
        "attendance": 180,
        "membership": 180,
        "percentEnrolled": 100
      },
      "transportation": {
        "transportationCategoryDescriptor": "uri://education.mn.gov/TransportationCategoryDescriptor#01",
        "transportingLocalEducationAgencyReference": {
          "localEducationAgencyId": 10625000
        }
      }
    }
  }
  ```
- StaffUniqueId will be loaded using the FFN in the Educator Licensing System.
- Post-Secondary Institution IDs will be pre-loaded by MDE; these college identifiers will come from the MDE-ORG system.


## Minnesota District and School IDs
The MDE **stateOrganizationID** (assigned in MDE ORG) is formatted as follows: ```ttddddsssmmm```, where:
- ``tt`` = district/LEA type (note most LEA types are a single digit)
- ``dddd`` = district number, left zero filled
- ``sss`` = school number, left zero filled, 000 for districts
- ``mmm`` = 000 for all organizations reported in Ed-Fi
 
The MDE **stateOrganizationID** value is stored in Ed-Fi on the Ed-Fi **EducationOrganizationIdentificationCodes** collection and is surfaced via the Ed-Fi **LocalEducationAgencies** and **Schools** resource endpoints. 

The Ed-Fi **LocalEducationAgencyId** and **SchoolId** are derived as follows: ```ttddddsss```.  The final three digits in ```sss``` are always zero filled (```000```) for the LocalEducationAgencyId. 

Examples: 
- The MDE State Organization ID for [Mayo Senior High](https://public.education.mn.gov/MdeOrgView/organization/show/2734) (an individual school) is ```10535315000```. The corresponding Ed-Fi SchoolId is ```10535315```.
- The MDE State Organization ID for [Rochester Public School District](https://public.education.mn.gov/MdeOrgView/organization/show/527) (an LEA) is ```10535000000```. The corresponding Ed-Fi LocalEducationAgencyId is ```10535000```

More information is available in [MDE ORG](https://public.education.mn.gov/MdeOrgView/), including [this reference on LEA (organization) types](https://public.education.mn.gov/MdeOrgView/reference/orgTypes).

### Identifiers: Schools vs. Buildings
MDE's system for identifying individual schools is independent of building or physical address. Therefore, a district may have multiple school identifiers assigned for the same building, especially if that building houses several different [school classifications](https://public.education.mn.gov/MdeOrgView/reference/schoolClassTypes). 

For example, the Comfrey Public School District (0081-01, or ```10081000000```) houses its district office, [elementary](https://public.education.mn.gov/MdeOrgView/organization/show/1135), and [secondary](https://public.education.mn.gov/MdeOrgView/organization/show/1136) schools (along with several other programs) at 305 Ochre Street West in Comfrey (as of December 2020). However, each program gets an individual identifier, such as:
- *Comfrey Elementary*: Ed-Fi school ID: ```10081010``` (formatted ID: 0081-01-010)
- *Comfrey Secondary*: Ed-Fi school ID: ```10081020``` (formatted ID: 0081-01-020)

# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)
- [Advance to Data Requirements and API Resources](sis_test_plan_c_data_reqs.md)