# MDE-EdFi-Documentation

_NOTE: As of August 3, 2022, this documentation is focusing on the changes implemented for the 2022-2023 school year._ Several new elements have been delayed for future years, but documentation remains in this repository, marked as **"Postponed until after school year 2022-23"**.

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
The following updates are currently being implemented for school year 2022-2023:
- Upgrade to [Ed-Fi ODS/API version 5.2](https://techdocs.ed-fi.org/display/ODSAPIS3V520) and [Data Standard v3.3.0-a](https://techdocs.ed-fi.org/display/EFDS33/What%27s+New+-+v3.3-a)
- Move from ESCT to new Ed-Fi ODS Admin App
- Ed-Fi API 2022-2023 Data Mapping Matrix Changes for **AncestryEthnicOrigin**, **HighestCompletedLevelOfEducation**, and **StudentCharacteristicDescriptor**
- New Data Collection for Direct Certification (see below)

Use the links above to access reference documentation from the Ed-Fi  website.

#### New Data Collections
For an overview of new data collections that were originally planned for school year 2022-2023, please refer to the [MDE 2022-2023 School Year Ed-FI Collection Updates](2022-23%20MDE%20Ed-Fi%20Documentation/MDE%202022-2023%20School%20Year%20Ed-FI%20Collection%20Updates.docx) document. All _new_ collections except for the "Direct Certification" data have been **delayed to a future year**. Note:
- New certification scenarios for Direct Certification for NSLP have been added to the [Student School Food Service Program Association Section](sandbox_cert_c_spas.md#resource-studentschoolfoodserviceprogramassociation) - see those marked "New for School Year 2022-23"
- Vendors will be asked to double check their programming against changes implemented as part of the v5.2 API update, such as moving AncestryEthnicOrigin in the StudentEducationOrganizationAssociation entity from the MN extension to a core Ed-Fi data element.

#### New and Updated Certification Scenarios for Future Years
Several of the new data collections originally planned for school year 2022-2023 are now **postponed until after school year 2022-23**. However, they are addressed in this documentation with either new or updated certification scenarios. A brief list of those scenarios is below.

  - [Language Academic Honors](sandbox_cert_b_marss.md#language-academic-honors) (see [additional documentation](#language-academic-honor-documentation) below)
  - [Gender Identities and Preferred Pronouns](sandbox_cert_b_marss.md#gender-identity-and-preferred-pronouns)
  - [Neglected Or Delinquent Program Association](sandbox_cert_c_spas.md#resource-studentneglectedordelinquentprogramassociation)
  - [Online Learning](sandbox_cert_e_mccc.md#online-learning)
  - [Virtual School Status](sandbox_cert_g_school_attribute.md#virtual-school-status)
  - [Title I Part A School Designation](sandbox_cert_g_school_attribute.md#title-i-part-a-school-designation)
  - [Student Preferred Name ](sandbox_cert_b_marss.md#preferred-name)
  -  and [Applied But Did Not Qualify](sandbox_cert_b_marss.md#applied-but-did-not-qualify)
  - [Other Language Instruction Program Service Description](sandbox_cert_c_spas.md#resource-studentlanguageinstructionprogramassociation)
  - [Displaced Students and Student Crisis Events](sandbox_cert_b_marss.md#displaced-students-and-student-crisis-events)

#### Migration of Custom Descriptor Tables
Within the **2022-23 MDE Ed-Fi Documentation** folder, the MDE MNIT Team has undertaken a migration of our custom descriptor tables from the Data Mapping Matrix to a suite of CSV files that are automatically exported from our Ed-Fi database(s). These can be viewed in the **2022-23 MDE Ed-Fi Documentation/descriptorTables** folder. See [the about descriptor tables document](/2022-23%20MDE%20Ed-Fi%20Documentation/descriptorTables/AboutDescriptorTables.md) for more information.

As of **April 11, 2022**, this migration is still under way - so the custom descriptor tables are still viewable in the Data Mapping Matrix. But at some point they will be removed from that spreadsheet and viewable only through the descriptorTables folder.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding the system.
- [Transactional Update Procedures](transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- Additional Documentation is available on [MDE's Ed-Fi Documentation page](https://education.mn.gov/MDE/dse/datasub/edfi/doc/)

### Language Academic Honor Documentation
**Postponed until after school year 2022-23**. Language Academic Honor information was previously collected from districts via a Microsoft Word Form in aggregate. For more information about this collection, we encourage vendors to visit:
  - The MDE web page about [World Languages](https://education.mn.gov/MDE/dse/stds/world/)
  - The [Microsoft Word Form](https://education.mn.gov/mdeprod/idcplg?IdcService=GET_FILE&dDocName=MDE086116&RevisionSelectionMethod=latestReleased&Rendition=primary) previously used to collect the information in aggregate.
  - The MDE web page about the [Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/)
  - The [FAQ page for the Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/PROD034397)

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
