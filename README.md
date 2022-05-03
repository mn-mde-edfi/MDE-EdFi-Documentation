# MDE-EdFi-Documentation

_NOTE: As of April 11, 2022, this "master" branch of our documentation is focusing on the 2022-2023 school year._ Additional branches may be built and then merged for specific **releases** of the 2022-2023 school year.

This repository contains documentation for Minnesota's implementation of the [Ed-Fi alliance standard](https://www.ed-fi.org/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more [at MDE's Ed-Fi web page](https://education.mn.gov/MDE/dse/datasub/edfi/) and at the following links:
- [Ed-Fi Technical Documentation](https://techdocs.ed-fi.org/)
- [Ed-Fi Data Standard](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Data+Standard)
- [Ed-Fi Operational Data Store (ODS) and API](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Operational+Data+Store+and+API)

## Markdown Documentation
MNIT supporting MDE is now complementing each collection year's documentation in markdown files. While the official documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent an effort to store and maintain the documentation in markdown, in particular:

- [SIS and Vendor Test Plan](sis_test_plan_a_toc.md)
- [Sandbox Certification Scenarios](sandbox_cert_a_toc.md)

By serving documentation in both Word and Markdown, MDE hopes to increase vendor access to the documentation as well as provide options for understanding and visualization changes over time.

### School Year 2022-2023 Plans
The following updates are currently in process and/or planned for school year 2022-2023:
- Upgrade to [Ed-Fi ODS/API version 5.2](https://techdocs.ed-fi.org/display/ODSAPIS3V520) and [Data Standard v3.3.0-a](https://techdocs.ed-fi.org/display/EFDS33/What%27s+New+-+v3.3-a)
- Move from ESCT to new Ed-Fi ODS Admin App
- Ed-Fi API 2022-2023 Data Mapping Matrix Changes for **AncestryEthnicOrigin**, **HighestCompletedLevelOfEducation**, and **StudentCharacteristicDescriptor**

Use the links above to access reference documentation from the Ed-Fi  website.

#### New Data Collections
The following new data collections are planned for school year 2022-2023, organized into a suite of releases:
- Release 1:
  - SEOA.LanguageAcademicHonors
  - SEOA.GenderIdentities
  - SEOA.PreferredPronouns
  - StudentNeglectedOrDelinquentProgramAssociation
- Release 2:
  - Online Learning Course Completion 
  - Virtual School Status 
  - Other LanguageInstructionProgramService Description
- Release 3 and beyond:
  - Student Preferred Name 
  - Direct Certification for NSLP and Applied But Did Not Qualify

#### Migration of Custom Descriptor Tables
Within the **2022-23 MDE Ed-Fi Documentation** folder, the MDE MNIT Team has undertaken a migration of our custom descriptor tables from the Data Mapping Matrix to a suite of CSV files that are automatically exported from our Ed-Fi database(s). These can be viewed in the **2022-23 MDE Ed-Fi Documentation/descriptorTables** folder. See [the about descriptor tables document](/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/AboutDescriptorTables.md) for more information.

As of **April 11, 2022**, this migration is still under way - so the custom descriptor tables are still viewable in the Data Mapping Matrix. But at some point they will be removed from that spreadsheet and viewable only through the descriptorTables folder.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding the system.
- [Transactional Update Procedures](transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- Additional Documentation is available on [MDE's Ed-Fi Documentation page](https://education.mn.gov/MDE/dse/datasub/edfi/doc/)

## Sample Data
JSON files of sample data are being loaded into the [data directory](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/tree/master/data) in an attempt to assist developers with understanding the Ed-Fi ODS API.

## Issues List
As part of this documentation effort, we are also using Github to manage technical issues. See the [Issue List](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/issues) for examples.

## Viewing Options
There are two ways to view this documentation: 
1. [in the Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation) where ```https://github.com/mn-mde-edfi/``` is in the beginning of the URL in your browser. Raw markdown files are in the "code" section, with links to each other. Github renders this markdown as readable content.
2. in a ["Web Version"](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/) in which Github attempts to automatically render the markdown files as HTML, and where ```https://mn-mde-edfi.github.io/``` is in the beginning of the URL in your browser

In the Github repository, you may have trouble viewing embedded images embedded in the markdown. You have two options to remedy this: "click through" to view the image in the repository, or view the web version.

In contrast, the web version does not render markdown tables into HTML tables, so tables are best viewed directly [in the Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation).
