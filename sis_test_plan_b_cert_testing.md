# Sandbox Certification Testing
When certification begins, vendors will be required to generate a key and secret to a "Minimal" sandbox [Operational Data Store (ODS)](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Operational+Data+Store+and+API) with no sample data pre-loaded. This ODS will contain the Minnesota Education School and District records synchronized with [MDE ORG](https://public.education.mn.gov/MdeOrgView/), MN specific descriptors, District Programs, and the State Course Catalog and Staff records required for the MCCC data collection. When submitting data for each of the Certification scenarios, we ask that you use a district you have access to, and schools within the district.

## Accessing the Sandbox
_Please note_ school years ending 2020 though 2022, sandbox environments were given ```sbYY_``` in the base paths for the API, affecting sandbox and Swagger URLs. For school year 2022-2023, the base sandbox URL is merely ``https://test.edfi5.education.mn.gov/swagger/`` - note the "edfi5" portion of the URL, but no ```sbYY_``` portion. Look for the ```sbYY_``` portion to return for the 2023-2024 school year.

### Sandbox Admin Website
As part of Sandbox certification, you will need access to the [Sandbox Admin Site](https://test.edfi5.education.mn.gov/admin/). To request an account, [contact MDE by email](mailto:EdFiProjectSupportMNIT.MDE@state.mn.us). In the Sandbox Admin Site, you will be able to create ODS instances to use for development and testing of your integrations. ([The Ed-Fi TechDocs](https://techdocs.ed-fi.org/display/ODSAPI31/Using+the+Sandbox+Administration+Portal) have more detailed instructions on setting up sandboxes.)

### Swagger UI
We continue to use the [Swagger UI tool](https://swagger.io/tools/swagger-ui/) to visualize and interact with the ODS API. Developers can access this [UI for MDE's Sandbox](https://test.edfi5.education.mn.gov/swagger/) to test-drive Create, Read, Update, and Delete (CRUD) actions before building integrations as necessary.

_Please note:_ MDE's Swagger website has been customized to remove the generic "Resources" section. All MN Specific resources can be found under the Profiles for each School Year. Note the order of the following Profiles is alphabetical, not chronological:

- A preview of future releases is under the generic-named _Minnesota-Preview-SISVendor-Profile_.
- All MN Specific resources defined for the _2021-2022_ School Collection can be previewed under the _Minnesota-Twenty-One-Twenty-Two-SISVendor-Profile._
- All MN Specific resources defined for the **2022-2023** School Collection can be found under the **Minnesota-Twenty-Two-Twenty-Three-SISVendor-Profile**.
- The Identities Section is not functional in the Sandbox and is provided as documentation only

Upon launch of the Swagger Sandbox UI, the site will finish loading the profiles and appear similarly to previous years, with a landing page where profiles can be selected. Clicking one of the profile links will launch you into the Swagger UI for exploration. Once inside the Swagger UI, click the "Authorize" button to enter in the client id (key) and client secret you created in the Sandbox Admin site. This will allow you to test GET, PUT, and other API request via the Swagger UI.

### Sandbox Base and OAuth URLs
Developers can further test their code integrations at the URLs in this section.
- The base URL for the ODS/API is: ```https://test.edfi5.education.mn.gov/api/```
- The Data Management URL is: ```https://test.edfi5.education.mn.gov/api/data/v3```

#### Extension vs. Core Resources
Note that Ed-Fi URLs vary based on whether or not core Ed-Fi standard or MN extensions are being accessed:
- **Extensions**: The URL for addressing MN extension resources should include 'mn' after v3. For example, when addressing _studentSection504PlanProgramAssociations_, a Minnesota extension entity, the URL is: ```…/api/data/v3/MN/studentSection504PlanProgramAssociations```
- **Core**: The URL for addressing core resources should include 'ed-fi' after v3. For example, when addressing _StudentSchoolAssociation_, a core Ed-Fi entity, the URL is: ```…/api/data/v3/ed-fi/StudentSchoolAssociation```

**Important Note:** the school year must be included after **“/v3/”** and before the core/extension namespace in Stage and Production, but **not in Sandbox**. For example:
```…/api/data/v3/2023/ed-fi/StudentSchoolAssociation```
```…/api/data/v3/2023/MN/studentSection504PlanProgramAssociations```

The Sandbox ODS/API oauth URL is: ```https://test.edfi5.education.mn.gov/sapi/oauth/```

Authentication In Ed-Fi 3.x ODS/API uses two-legged OAuth 2.0 Client Credentials Grant Flow. More information and sample API calls are located in [the Ed-Fi tech docs](https://techdocs.ed-fi.org/display/ODSAPIS3V520/Authorization).

## Sandbox Tips
- In the staging and production environments, SIS vendor API keys will be associated with a claim set limiting access to only the API resources included in this document. This claim set has been enabled in the Sandbox environment. When you access a resource not included in the claim set you will receive the following message in the response: ```Access to the resource could not be authorized. Are you missing a claim?```
- In the sandbox, multiple SIS Vendor profiles have been created, limiting access to specific properties on each of the resources required in the referenced school year. These appear in the right-hand side of the "Profiles" section and are named as above.
    - These profiles are tied to your key and secret, and are auto-enabled in Staging and Production – meaning you will not have to include the profile in the "accept" or "content-type" headers of the request for the profile to take effect. (See more details in the [Staging Environment Load and Quality Check section](sis_test_plan_d_staging.md#staging-environment-load-and-quality-check))
- When creating a sandbox, you have the option of including a set of sample data in the sandbox. The sample data used, is associated with St. Paul Public School District (LocalEducationAgencyId = 10625000). When you do not select the option to include sample data, your sandbox database will be loaded with an essentially empty ODS, except that it will include MN Schools and Districts, and other preliminary seed data such as: the Descriptors that MDE has customized for this implementation, State Course Codes and District Programs.
- The actual certification test will be conducted in a sandbox with no sample data loaded and you will reference your own data in the Scenarios, relating elements to MDE Schools, Districts and Descriptors as needed.
- The Sandbox environment ignores the School Year included in the API base URL. Since you will be submitting data to the 2022-2023 School year, to prep for submissions to Staging and Production, remember to include the year, i.e. "2023". 
- The School IDs and District IDs used for the ODS/API resources are the MDE State Organization IDs (stateOrganizationID). See section below for details.
- MN custom descriptor codes have been loaded under the namespace ```uri://education.mn.gov/```
- StaffUniqueId will be loaded using the FFN in the Educator Licensing System.
- Post-Secondary Institution IDs will be pre-loaded by MDE; these college identifiers will come from the MDE-ORG system.
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



## Minnesota District and School IDs
The MDE **stateOrganizationID** (assigned in MDE ORG) is formatted as follows: ```ttddddsssmmm```, where:
- ``tt`` = district/LEA type (note most LEA types are a single digit)
- ``dddd`` = district number, left zero filled
- ``sss`` = school number, left zero filled, 000 for districts
- ``mmm`` = 000 for all organizations reported in Ed-Fi (and excluded in the Ed-Fi ID)
 
The MDE **stateOrganizationID** value is stored in Ed-Fi on the Ed-Fi **EducationOrganizationIdentificationCodes** collection and is surfaced via the Ed-Fi **LocalEducationAgencies**, **Schools**, and **PostSecondaryEducation** resource endpoints. 

The Ed-Fi **LocalEducationAgencyId** and **SchoolId** are derived as follows: ```ttddddsss```.  The final three digits in ```sss``` are always zero filled (```000```) for the LocalEducationAgencyId. **Do not** use a leading zero in the LEA type portion.

Examples: 
- The MDE State Organization ID for [Mayo Senior High](https://public.education.mn.gov/MdeOrgView/organization/show/2734) (an individual school) is ```10535315000```. The corresponding Ed-Fi SchoolId is ```10535315```.
- The MDE State Organization ID for [Rochester Public School District](https://public.education.mn.gov/MdeOrgView/organization/show/527) (an LEA) is ```10535000000```. The corresponding Ed-Fi LocalEducationAgencyId is ```10535000```
- The MDE State Organization ID for [University of Minnesota Morris](https://public.education.mn.gov/MdeOrgView/organization/show/137) (a Post Secondary Institution) is ```230005000000```. The corresponding Ed-Fi postSecondaryInstitutionId is ```230005000```

More information is available in [MDE ORG](https://public.education.mn.gov/MdeOrgView/), including [this reference on LEA (organization) types](https://public.education.mn.gov/MdeOrgView/reference/orgTypes).

### Identifiers: Schools vs. Buildings
MDE's system for identifying individual schools is independent of building or physical address. Therefore, a district may have multiple school identifiers assigned for the same building, especially if that building houses several different [school classifications](https://public.education.mn.gov/MdeOrgView/reference/schoolClassTypes). 

For example, the Comfrey Public School District (0081-01, or ```10081000000```) houses its district office, [elementary](https://public.education.mn.gov/MdeOrgView/organization/show/1135), and [secondary](https://public.education.mn.gov/MdeOrgView/organization/show/1136) schools (along with several other programs) at 305 Ochre Street West in Comfrey (as of December 2020). However, each program gets an individual identifier, such as:
- *Comfrey Elementary*: Ed-Fi school ID: ```10081010``` (formatted ID: 0081-01-010)
- *Comfrey Secondary*: Ed-Fi school ID: ```10081020``` (formatted ID: 0081-01-020)

# Navigation
- [Return to SIS Test Plan Overview](sis_test_plan_a_toc.md)
- [Advance to Data Requirements and API Resources](sis_test_plan_c_data_reqs.md)