# MDE-EdFi-Documentation

## SCHEDULE NOTES
- _As of 2023-03-14, this documentation reflects the MDE Ed-Fi implementation for  **School Year 2023-24**._
 - _NOTE: Several new elements remain delayed for future years_. When found in this repository, those elements are marked as **"Postponed until further notice"**.

This repository contains technical documentation for Minnesota's implementation of the [Ed-Fi alliance standard](https://www.ed-fi.org/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more [at MDE's Ed-Fi web page](https://education.mn.gov/MDE/dse/datasub/edfi/) and at the following links:
- [Ed-Fi Technical Documentation](https://techdocs.ed-fi.org/)
- [Ed-Fi Data Standard](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Data+Standard)
- [Ed-Fi Operational Data Store (ODS) and API](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Operational+Data+Store+and+API)

The primary audience for this documentation is SIS vendors and State of Minnesota technical staff (from MDE and MNIT).

## Markdown Documentation
MNIT supporting MDE is now complementing each collection year's documentation in markdown files. While some documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent an effort to store and maintain the documentation in markdown, in particular:

- [SIS and Vendor Test Plan](sis_test_plan_a_toc.md)
- [Sandbox Certification Scenarios](sandbox_cert_a_toc.md)

By serving documentation in both Word and Markdown, our goal is to increase vendor access to the documentation as well as provide options for understanding and visualization changes over time.

### School Year 2023-2024 Plans
The following updates are currently being implemented for school year 2023-2024:
- Early Education / MARSS [Program Ambiguity Resolution](./2023-24%20MDE%20Ed-Fi%20Documentation/early_ed_disamb_resolution_v2023-03-10.pdf)
- Various descriptor changes (see the top-level ``descriptorTables`` folder)

Vendor certification scenarios are being updated for the Ambiguity Resolution change, and will be linked here once drafted. In the meantime, a description of the problem being resolved is available in the document linked above. For reference, [this workaround document](./early_ed_disamb_work.md) details the methods requested of vendors to work around this issue for school year 2022-23 and prior.

#### New Data Collections
No new data collections are planned for school year 2023-2024.

#### Certification Scenarios for Future Years
Several of the new data collections originally planned for school year 2022-2023 are now **Postponed until further notice**. However, they are addressed in this documentation with either new or updated certification scenarios. A brief list of those scenarios is below.

  - [Language Academic Honors](sandbox_cert_b_marss.md#language-academic-honors) (see [additional documentation](#language-academic-honor-documentation) below)
  - [Gender Identities and Preferred Pronouns](sandbox_cert_b_marss.md#gender-identity-and-preferred-pronouns)
  - [Neglected Or Delinquent Program Association](sandbox_cert_c_spas.md#resource-studentneglectedordelinquentprogramassociation)
  - [Online Learning](sandbox_cert_e_mccc.md#online-learning)
  - [Virtual School Status](sandbox_cert_g_school_attribute.md#virtual-school-status)
  - [Title I Part A School Designation](sandbox_cert_g_school_attribute.md#title-i-part-a-school-designation)
  - [Student Preferred Name ](sandbox_cert_b_marss.md#preferred-name)
  - [Applied But Did Not Qualify](sandbox_cert_b_marss.md#applied-but-did-not-qualify)
  - [Other Language Instruction Program Service Description](sandbox_cert_c_spas.md#resource-studentlanguageinstructionprogramassociation)
  - [Displaced Students and Student Crisis Events](sandbox_cert_b_marss.md#displaced-students-and-student-crisis-events)

#### Migration of Custom Descriptor Tables
For **school year 2023-24** the MDE MNIT team has *moved* the custom [descriptor tables folder](./descriptorTables/) to the top-level of this repository. Going forward, this folder will reflect the most recent information about desciptor tables, either planned for the coming year (spring) or in effect for the current year (summer through winter). The current state of the tables within the folder will be detailed in the[ About Descriptor Tables](./descriptorTables/AboutDescriptorTables.md) markdown file. Viewing the commit history of the folder will allow vendors to more easily visualize chnages from year to year.

The folder will continue to contain a suite of CSV files that are automatically exported from our Ed-Fi database(s), and should be used as the "source of truth" reference. Older versions of the Data Mapping Matrix still have them, but those are no longer being maintained.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding MDE's Ed-Fi implementation.
- [Transactional Update Procedures](transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- Additional Documentation, particularly useful to districts/LEAs, is available on [MDE's Ed-Fi Documentation page](https://education.mn.gov/MDE/dse/datasub/edfi/doc/)

### Language Academic Honor Documentation
**Postponed until further notice**. Language Academic Honor information was previously collected from districts via a Microsoft Word Form in aggregate. For more information about this collection, we encourage vendors to visit:
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

In contrast, the web version does not render markdown tables into HTML tables, so tables are best viewed directly [in the Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation). Viewing markdown files directly within GitHub also allows you to use their [table of contents functionality](https://github.blog/changelog/2021-04-13-table-of-contents-support-in-markdown-files/) to navigate.
