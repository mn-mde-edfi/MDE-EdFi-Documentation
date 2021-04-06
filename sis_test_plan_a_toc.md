# SIS Vendor and District Test Plan
This document contains an overview and references for the Student Information Systems (SIS) and District Test Plan for the Minnesota **2021-2022 School Year**, aligning with Ed-Fi version **3.1**. The documentation in this repository is maintained by Minnesota IT Services (MNIT), partnering with the the Minnesota Department of Education (MDE).

## Overview
The 2021-22 School Year Certification is currently aligned with the [Ed-Fi 3.1 Data Standard](https://github.com/Ed-Fi-Alliance-OSS/Ed-Fi-Standard/releases/tag/v3.1.0) and ODS/API, with extensions customized for MDE.

Student Information System (SIS) vendors integrating with MDE's Ed-Fi Automated Student Data Collection System are required to pass 2 levels of testing prior to being granted a district's API key and secret to the Production environment.

**First**, vendors are required to demonstrate their ability to submit the specific API resources and elements encompassed within the various program (MARSS, Early Education, MCCC, etc) elements. This first phase is executed in the MNIT Ed-Fi Sandbox environment. Note two unique qualities of the Sandbox:

- The Sandbox environment does not include integration with the **Identities API endpoint**.
- API profiles are **not enforced** in the Sandbox environment, however you may be required to demonstrate appropriate implementation of API profile use in your API transactions.

**Second**, when all scenarios are verified in the Sandbox environment, the SIS vendor is granted access to the Staging environment. Vendors must perform a test load of their district's real student demographic data in the Staging environment. During this test, Student IDs will be validated against the Ed-Fi Identities Service to ensure valid ids are being inserted to the Ed-Fi ODS. MARSS comparison checks and additional data quality verifications are also executed in the Staging Environment. 

Once the Staging data reaches a satisfactory level of quality as determined by MDE, MNIT, and the District, MNIT will enable the vendor to obtain a key and secret for the Production environment.

This documentation repository includes the certification requirements for both the scenario-based sandbox testing and staging environment data loading.

### Potential Hangups
As you move from Sandbox to Staging for SY2022, remember the following:
- Pay attention to the URLs, years in the API path, and key and secret details identified [in the staging load and quality check section](sis_test_plan_d_staging.md#staging-environment-load-and-quality-check). To wit:
  - Staging and Production require profile-specific coding, as your key and secret will be for a single profile (different profiles for different years)
  - You will get new key/secret combinations for the 21-22 ODS in production - you won't be able to re-use those issued for prior years. So, for example, your key and secret for the 2020-21 ODS is only associated with the **Twenty_Twenty_One_SISVendor_Profile** and will only work for that profile.
- You may only get keys and secrets for individual districts at a time

## References
The following documents contain additional information:
1. [Sandbox Certification Testing](sis_test_plan_b_cert_testing.md)
2. [Data Requirements and API Resources](sis_test_plan_c_data_reqs.md)
3. [Staging Environment Load and Quality Check](sis_test_plan_d_staging.md)

## Additional Resources
Vendors may wish to review the Ed-Fi Alliance's help on [Using the Online Documentation](https://techdocs.ed-fi.org/display/ODSAPI34/Using+the+Online+Documentation) before working in the MDE Sandbox and Swagger User Interface.