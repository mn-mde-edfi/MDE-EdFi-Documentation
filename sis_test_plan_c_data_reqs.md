# 2020-2021 Data Requirements and API Resources
This document is part of the MDE Ed-Fi [Vendor and District Test Plan](sis_test_plan_a_toc.md). It is currently a stub and being built out to replace the similarly named section in the [official documentation](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/blob/master/2020-21%20MDE%20Ed-Fi%20Documentation/2020-21%20SIS%20Vendor%20and%20District%20Test%20Plan.docx).

## API Documentation
For each of the resources described in this document, the elements/properties required are included and browseable in the [Sandbox Swagger UI](https://test.edfi.education.mn.gov/sb20_/EdFi.Ods.SwaggerUI) (aka "Swagger") under the **Minnesota-SISVendor-Profile** and the **Minnesota-Twenty-Twenty-One-SISVendor-Profile**.

### Example
As an example, to view the required resource properties for **studentSchoolAssociations**, open the "POST" action in Swagger:
```POST /ed-fi/studentSchoolAssociations Creates or updates resources based on the natural key values of the supplied resource.```
- _Note:_ "ed-fi" in the path above indicates that this is a core resource.

Properties in the **studentSchoolAssociations** can be viewed as the JSON object sample by selecting **"Example Value"**. Definitions and Data Types in the **studentSchoolAssociations** can be viewed by selecting **“Model”**.


