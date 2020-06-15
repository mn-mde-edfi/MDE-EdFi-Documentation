# SIS Vendor and District Test Plan
This document contains an overview and references for the Student Information Systems (SIS) and District Test Plan for the Minnesota **2020-2021 School Year**, aligning with Ed-Fi version **3.1**. The documentation in this repository is maintained by Minnesota IT Services (MNIT), partnering with the the Minnesota Department of Education (MDE)

## Overview
The 20-21 School Year Certification is currently aligned with the [Ed-Fi 3.1 Data Standard](https://github.com/Ed-Fi-Alliance-OSS/Ed-Fi-Standard/releases/tag/v3.1.0) and ODS/API, with extensions customized for MDE.

SIS vendors integrating with MDE's Ed-Fi Automated Student Data Collection System are required to pass 2 levels of testing prior to being granted a district's API key and secret to the Production environment.

**First**, vendors are required to demonstrate their ability to submit the specific API resources and elements encompassed within the MARSS and Early Education Enrollment Data elements. This first phase is executed in the MNIT Ed-Fi Sandbox environment. Note two unique qualities of the Sandbox:

- The Sandbox environment does not include integration with the **Identities API endpoint**.
- API profiles are **not enforced** in the Sandbox environment, however you may be required to demonstrate appropriate implementation of API profile use in your API transactions.

**Second**, when all scenarios are verified in the Sandbox environment, the SIS vendor is granted access to the Staging environment. Vendors must perform a test load of their district's real student demographic data in the Staging environment. During this test, Student IDs will be validated against the Ed-Fi Identities Service to ensure valid ids are being inserted to the Ed-Fi ODS. MARSS comparison checks and additional data quality verifications are also executed in the Staging Environment. 

Once the Staging data reaches a satisfactory level of quality as determined by MDE, MNIT, and the District, MNIT will enable the vendor to obtain a key and secret for the Production environment.

## References
The following documents contain additional information:
1. [Sandbox Certification Testing](sis_test_plan_b_cert_testing.md)
2. Data Requirements and API Resources
3. Staging Environment Load and Quality Check