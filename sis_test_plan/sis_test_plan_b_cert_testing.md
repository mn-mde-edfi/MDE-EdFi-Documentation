# Sandbox Certification Testing

## Accessing the MDE Ed-Fi 6.2 Test Sandbox Environment
- Test Sandbox Administration Portal: ``https://test.pub.education.mn.gov/edfisbadmin/``
- Test Sandbox Swagger Documentation: ``https://test.pub.education.mn.gov/edfiswag/``
- Test Sandbox API: ``https://test.api.education.mn.gov/edfiapi/``

### Test Sandbox Administration Portal
Vendors must have an MDE Ed-Fi [Test Sandbox Administration Portal](https://docs.ed-fi.org/reference/ed-fi-api/6.2/client-developers-guide/using-the-sandbox-administration-portal) account to create Test Sandbox instances. To request a Test Sandbox Administration Portal account, [contact MDE by email](mailto:EdFiProjectSupportMNIT.MDE@state.mn.us).

When certification begins, the SIS vendor will be required to create a "Minimal" (unpopulated) sandbox instance which generates a key and secret credentials to the Ed-Fi API Test Sandbox environment. 

This ODS will contain the Minnesota Education School and District records synchronized with [MDE ORG](https://pub.education.mn.gov/MdeOrgView/), [Ed-Fi Descriptors](https://pub.education.mn.gov/edfidocs/index.html), District Programs, and the State Course Catalog and Staff records required for the MCCC data collection. When submitting data for each of the Certification test scenarios, we ask that you choose a district you have access to and schools within that district.

### Swagger Online Documentation
Developers can access the [Ed-Fi API Swagger](https://test.pub.education.mn.gov/edfiswag/) website to access online API documentation and to test-drive Create, Read, Update, and Delete (CRUD) actions when building API integrations.

On the Swagger ODS / API Documentation v6.2 title page, please note:
- The API Profile list is alphabetical, not chronological, and includes SIS Vendor API Profiles for both the current school year and the prior school year.
- The year-specific SIS Vendor API Profiles are named by the school year. For example, the **2026-2027** school year data collection profile is named **Minnesota-Twenty-Six-Twenty-Seven-SISVendor-Profile**. 
- The Profile _Minnesota-Preview-SISVendor-Profile_ includes some resources that are currently not released and may not be used for production data submission to MDE's Ed-Fi API.
- The _Assessment-Read-Only_ and _Assessment-Read-Write"_ profile are only used for statewide assessment vendor integration.

 Once inside the Swagger UI, click the "Authorize" button to enter in the client id (key) and client secret you created in the Sandbox Admin site. This will allow you to test GET, PUT, and other API request via the Swagger UI. Do not use the "populated" credentials provided by default for anything other than general exploration.

### Sandbox Base and OAuth URLs
Developers can further test their code integrations at the URLs in this section.
- The base URL for the test ODS/API is: ```https://test.api.education.mn.gov/edfiapi/```
- The Data Management URL is: ```test.api.education.mn.gov/edfiapi/data/v3```

#### Extension vs. Core Resources
Note that Ed-Fi URLs vary based on whether or not core Ed-Fi standard or MN extensions are being accessed:
- **Extensions**: The URL for addressing MN extension resources should include 'mn' after v3. For example, when addressing _studentSection504PlanProgramAssociations_, a Minnesota extension entity, the URL is: ```…/api/data/v3/MN/studentSection504PlanProgramAssociations```
- **Core**: The URL for addressing core resources should include 'ed-fi' after v3. For example, when addressing _StudentSchoolAssociation_, a core Ed-Fi entity, the URL is: ```…/api/data/v3/ed-fi/StudentSchoolAssociation```

**Important Note:** the school year must be included after **“/v3/”** and before the core/extension namespace in Stage and Production, but **not in Sandbox**. For example:
```…/api/data/v3/2026/ed-fi/StudentSchoolAssociation```
```…/api/data/v3/2026/MN/studentSection504PlanProgramAssociations```

The Sandbox ODS/API oauth URL is: ```https://test.api.education.mn.gov/edfiapi/oauth/```

Authentication In Ed-Fi 3.x ODS/API uses two-legged OAuth 2.0 Client Credentials Grant Flow. More information and sample API calls are located in [the Ed-Fi tech docs](https://techdocs.ed-fi.org/display/ODSAPIS3V520/Authorization).

## Sandbox Tips
- In the staging and production environments, SIS vendor API keys will be associated with a claim set limiting access to only the API resources included in this documentation. This claim set has been enabled in the Sandbox environment. When you access a resource not included in the claim set you will receive the following message in the response: ```Access to the resource could not be authorized. Are you missing a claim?```
- In the sandbox, multiple SIS Vendor profiles have been created, limiting access to specific properties on each of the resources required in the referenced school year. These appear in the upper right "API Section" drop-down and are named as above.
- When creating a sandbox instance, you have the option "populate" to load a sample set of fake student data in the sandbox. The sample data used, is associated with St. Paul Public School District (LocalEducationAgencyId = 10625000). When you do not select the option to include sample data, your sandbox database will be loaded with an essentially empty ODS, except that it will include MN Schools and Districts, and other preliminary seed data such as MDE-customized Descriptors, State Course Codes, and District Programs. _Please note: if you do not see this "seed" data in a sandbox, it means MDE has not yet completed this process for the sandbox environment. You may need to destroy your current sandbox and create a new one once the synching process is conducted._
- The actual certification test will be conducted in a sandbox with no sample data loaded and you will reference your own data in the Scenarios, relating elements to MDE Schools, Districts and Descriptors as needed.
- The Sandbox environment ignores the School Year included in the API base URL. When prepping for submissions to Staging and Production, remember to include the year, i.e. "20##". 
- The School IDs and District IDs used for the ODS/API resources are the MDE State Organization IDs (stateOrganizationID). See the section below for details.
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

The Ed-Fi **LocalEducationAgencyId** and **SchoolId** are derived as follows: ```ttddddsss```.  The final three digits in ```sss``` are always zero filled (```000```) for the LocalEducationAgencyId. **Do not** use a leading zero in the LEA *type* portion.

Examples: 
- The MDE State Organization ID for [Mayo Senior High](https://pub.education.mn.gov/MdeOrgView/organization/show/2734) (an individual school) is ```10535315000```. The corresponding Ed-Fi SchoolId is ```10535315```.
- The MDE State Organization ID for [Rochester Public School District](https://pub.education.mn.gov/MdeOrgView/organization/show/527) (an LEA) is ```10535000000```. The corresponding Ed-Fi LocalEducationAgencyId is ```10535000```
- The MDE State Organization ID for [University of Minnesota Morris](https://pub.education.mn.gov/MdeOrgView/organization/show/137) (a Post Secondary Institution) is ```230005000000```. The corresponding Ed-Fi postSecondaryInstitutionId is ```230005000```

More information is available in [MDE ORG](https://pub.education.mn.gov/MdeOrgView/), including [this reference on LEA (organization) types](https://pub.education.mn.gov/MdeOrgView/reference/orgTypes).

### Identifiers: Schools vs. Buildings
MDE's system for identifying individual schools is independent of building or physical address. Therefore, a district may have multiple school identifiers assigned for the same building, especially if that building houses several different [school classifications](https://pub.education.mn.gov/MdeOrgView/reference/schoolClassTypes). 

For example, the Comfrey Public School District (0081-01, or ```10081000000```) houses its district office, [elementary](https://pub.education.mn.gov/MdeOrgView/organization/show/1135), and [secondary](https://pub.education.mn.gov/MdeOrgView/organization/show/1136) schools (along with several other programs) at 305 Ochre Street West in Comfrey (as of December 2020). However, each program gets an individual identifier, such as:
- *Comfrey Elementary*: Ed-Fi school ID: ```10081010``` (formatted ID: 0081-01-010)
- *Comfrey Secondary*: Ed-Fi school ID: ```10081020``` (formatted ID: 0081-01-020)

# Navigation
- [Return to SIS Test Plan Overview](README.md)
