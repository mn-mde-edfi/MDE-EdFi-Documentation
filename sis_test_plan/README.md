# SIS Vendor and District Test Plan
This document contains an overview and references for the Student Information Systems (SIS) and District Test Plan for the Minnesota **2026-2027 School Year**, aligning with [Ed-Fi ODS/API v6.2](https://docs.ed-fi.org/reference/ods-api/6.2) and [Ed-Fi Data Standard 4.0](https://docs.ed-fi.org/reference/data-exchange/data-standard/4/). 

## Overview
Student Information System (SIS) vendors integrating with MDE's Ed-Fi Automated Student Data Collection System are required to pass [Sandbox Certification Testing](sis_test_plan_b_cert_testing.md) prior to approval to release their product to Minnesota LEA customers for access to MDE's Production Ed-Fi environment.

In MDE's Ed-Fi Test Sandbox environment, vendors are required to demonstrate their ability to submit the specific API resources and elements encompassed within the various program (MARSS, Early Education, MCCC, etc) elements. 

NOTES:
- API profiles are **not enforced** in the Test Sandbox environment. However you may be required to demonstrate appropriate implementation of API profile use in your API transactions.
- The Test Sandbox environment does not support testing Student ID System integration using the [Identities API endpoint](sis_test_plan_d_ssid_testing.md).

This documentation repository includes the requirements for both scenario-based Sandbox Certification Testing and Student ID System integration testing.

## References
The following documents contain additional information:
1. [Sandbox Certification Testing](sis_test_plan_b_cert_testing.md)
2. [Data Requirements and API Resources](sis_test_plan_c_data_reqs.md)
3. [Student ID System Testing](sis_test_plan_d_ssid_testing.md)

## Additional Resources
Vendors may wish to review the Ed-Fi 6.2 [API Client Developer's Guide](https://docs.ed-fi.org/reference/ed-fi-api/6.2/client-developers-guide/) which includes documentation on using the Ed-Fi [Swagger Online Documentation](https://docs.ed-fi.org/reference/ed-fi-api/6.2/client-developers-guide/using-the-online-documentation) and the [Test Sandbox Administration Portal](https://docs.ed-fi.org/reference/ed-fi-api/6.2/client-developers-guide/using-the-sandbox-administration-portal).