# MDE-EdFi-Documentation

## SCHEDULE NOTES
- This documentation now partially reflects the MDE Ed-Fi implementation for **School Year 2025-26**. Note that an Azure migration is changing several details compared to the 2024-25 school year, and the MDE team is still working on integrating those changes. Note that the [descriptor tables](./descriptorTables/) contents should be correct.

Very few changes were implemented for the 2024-25 school year outside of some additional certification testing such as the [Deleting Resources Certification Scenarios](./sandbox_cert/sandbox_cert_h_deleting_resources.md) and [Joint Powers Certification Scenarios](./sandbox_cert/sandbox_cert_j_joint_powers.md). Overview documentation is available in [this folder](./2024-25%20MDE%20Ed-Fi%20Documentation/), including [this Joint Powers diagram](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2024-25%20MDE%20Ed-Fi%20Documentation/Joint%20Powers%20District%20Scenarios%20Diagram.pdf).
 - _NOTE: Several new elements remain delayed for future years_. When found in this repository, those elements are marked as **"Postponed until further notice"**.

This repository contains technical documentation for Minnesota's implementation of the [Ed-Fi alliance standard](https://www.ed-fi.org/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more [at MDE's Ed-Fi web page](https://education.mn.gov/MDE/dse/datasub/edfi/) and at the following links
- [Ed-Fi Technology Reference](https://docs.ed-fi.org/reference/)

The primary audience for this documentation is SIS vendors and State of Minnesota technical staff (from MDE and MNIT).

## Markdown Documentation
MNIT supporting MDE composes each collection year's documentation in markdown and CSV files. While some documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent an effort to store and maintain the documentation in markdown and CSV, in particular:

- [SIS and Vendor Test Plan](./sis_test_plan/README.md)
- [Sandbox Certification Scenarios](./sandbox_cert/README.md)
- [Descriptor Tables](./descriptorTables/)

By serving documentation in multiple formats, our goal is to increase vendor access to the documentation as well as provide options for understanding and visualization changes over time.

#### New Data Collections
_No new data collections are planned for school year 2024-2025. MDE anticipates piloting a solution for Joint Powers and Intermediate School Districts._

#### Certification Scenarios for Future Years
Several of the new data collections originally planned for prior school years are now **Postponed until further notice**. However, they are addressed in this documentation with either new or updated certification scenarios. A brief list of those scenarios is below.

  - [Language Academic Honors](./sandbox_cert/sandbox_cert_b_marss.md#language-academic-honors) (see [additional documentation](#language-academic-honor-documentation) below)
  - [Gender Identities and Preferred Pronouns](./sandbox_cert/sandbox_cert_b_marss.md#gender-identity-and-preferred-pronouns)
  - [Neglected Or Delinquent Program Association](./sandbox_cert/sandbox_cert_c_spas.md#resource-studentneglectedordelinquentprogramassociation)
  - [Online Learning](./sandbox_cert/sandbox_cert_e_mccc.md#online-learning)
  - [Virtual School Status](./sandbox_cert/sandbox_cert_g_school_attribute.md#virtual-school-status)
  - [Title I Part A School Designation](./sandbox_cert/sandbox_cert_g_school_attribute.md#title-i-part-a-school-designation)
  - [Student Preferred Name ](./sandbox_cert/sandbox_cert_b_marss.md#preferred-name)
  - [Displaced Students and Student Crisis Events](./sandbox_cert/sandbox_cert_b_marss.md#displaced-students-and-student-crisis-events)

#### Custom Descriptor Tables
The MDE Ed-Fi custom [descriptor tables folder](./descriptorTables/) reflects the most recent information about desciptor tables, either planned for the coming year (spring) or in effect for the current year (summer through winter). The current state of the tables within the folder will be detailed in the[ About Descriptor Tables](./descriptorTables/AboutDescriptorTables.md) markdown file. Viewing the commit history of the folder will allow vendors to more easily visualize changes from year to year.

The folder contains a suite of CSV files that are exported from our Ed-Fi database(s) and should be used as the "source of truth" reference.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](./reference/descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding MDE's Ed-Fi implementation.
- [Transactional Update Procedures](./reference/transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- Additional Documentation, particularly useful to districts/LEAs, is available on [MDE's Ed-Fi Documentation page](https://education.mn.gov/MDE/dse/datasub/edfi/doc/)
- The [Common Ed-Fi Errors page](./reference/common_errors.md) will attempt to provide additional documentation on the types of API errors that can arise for vendors and LEAs.

### Language Academic Honor Documentation
**Postponed until further notice**. Language Academic Honor information was previously collected from districts via a Microsoft Word Form in aggregate. For more information about this collection, we encourage vendors to visit:
  - The MDE web page about [World Languages](https://education.mn.gov/MDE/dse/stds/world/)
  - The [Microsoft Word Form](https://education.mn.gov/mdeprod/idcplg?IdcService=GET_FILE&dDocName=MDE086116&RevisionSelectionMethod=latestReleased&Rendition=primary) previously used to collect the information in aggregate.
  - The MDE web page about the [Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/)
  - The [FAQ page for the Minnesota Bilingual Seals Program](https://education.mn.gov/MDE/dse/stds/world/seals/PROD034397)

## Sample Data
JSON files of sample data can be found in the [data directory](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/tree/master/data). These files are intended to assist developers with understanding the Ed-Fi ODS API.

## Issues List
As part of this documentation effort, we attempted using Github to manage technical issues. See the [Issue List](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/issues) for examples. This effort has mostly been abandoned for lack of use. However, the MDE team is maintaining a [list of known issues and bugs](https://education.mn.gov/MDE/dse/datasub/edfi/issues/) in order to keep LEAs informed.

## Viewing Options
There are two ways to view this documentation: 
1. [in the Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation) where ```https://github.com/mn-mde-edfi/``` is in the beginning of the URL in your browser. Raw markdown files are in the "code" section, with links to each other. Github renders this markdown as readable content.
2. in a ["Web Version"](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/) in which Github attempts to automatically render the markdown files as HTML, and where ```https://mn-mde-edfi.github.io/``` is in the beginning of the URL in your browser.

In general we recommend using the GitHub repository version, given the limitations of the web version:
1.  the web version does not render markdown tables into HTML tables, so tables are best viewed directly [in the Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation). 
2. Viewing markdown files directly within GitHub also allows you to use their [table of contents functionality](https://github.blog/changelog/2021-04-13-table-of-contents-support-in-markdown-files/) to navigate.

However, the web version is occasionally advantageous, such as when viewing PDFs. For example:
1. [The Ed-Fi EE-MARSS Program Ambiguity Resolution](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2023-24%20MDE%20Ed-Fi%20Documentation/early_ed_marss_conflict_resolution.pdf) for school year 2023-24.
2. [The Joint Powers diagram](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2024-25%20MDE%20Ed-Fi%20Documentation/Joint%20Powers%20District%20Scenarios%20Diagram.pdf) for school year 2024-25.
