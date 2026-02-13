# MDE-EdFi-Documentation

This repository contains technical documentation for Minnesota's implementation of [Ed-Fi ODS/API v6.2](https://docs.ed-fi.org/reference/ods-api/6.2) and [Ed-Fi Data Standard 4.0](https://docs.ed-fi.org/reference/data-exchange/data-standard/4/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more at [MDE's Ed-Fi data submissions web page](https://education.mn.gov/MDE/dse/datasub/edfi/).

The primary audience for this documentation is SIS vendors and State of Minnesota technical staff from MDE and MNIT.

## Markdown Documentation
MNIT supporting MDE composes each collection year's documentation in markdown and CSV files. While some documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent an effort to store and maintain the documentation in markdown and CSV, in particular:

- [SIS and Vendor Test Plan](./sis_test_plan/README.md)
- [Sandbox Certification Scenarios](./sandbox_cert/README.md)
- [Descriptor Tables](./descriptorTables/)

By serving documentation in multiple formats, our goal is to increase vendor access to the documentation as well as provide options for understanding and visualization changes over time.

#### Custom Descriptor Tables
The MDE Ed-Fi custom [descriptor tables folder](./descriptorTables/) reflects the most recent information about desciptor tables, either planned for the coming year (spring) or in effect for the current year (summer through winter). This folder contains CSV files exported from the current year Ed-Fi ODS database and should be used as the "source of truth" reference.

See [About Descriptor Tables](./descriptorTables/AboutDescriptorTables.md) for the current state of the tables within the descriptor tables folder. Viewing the commit history of the folder will allow vendors to more easily visualize changes from year to year.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](./reference/descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding MDE's Ed-Fi implementation.
- [Transactional Update Procedures](./reference/transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- [Common Ed-Fi Errors](./reference/common_errors.md) provides additional documentation on some types of API errors that can arise for vendors and LEAs.
- Additional Documentation, particularly useful to districts/LEAs, is available on [MDE's Ed-Fi Documentation page](https://education.mn.gov/MDE/dse/datasub/edfi/doc/)

## Sample Data
JSON files of sample data can be found in the [data directory](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/tree/master/data). These files are intended to assist developers with understanding the Ed-Fi ODS API.

## Issues List
The MDE team maintains a [list of known issues and bugs](https://education.mn.gov/MDE/dse/datasub/edfi/issues/) on MDE's public web site.

## Viewing Options
There are two ways to view this documentation: 
- In the [Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation) where ```https://github.com/mn-mde-edfi/``` is in the beginning of the URL in your browser. Raw markdown files are in the "code" section, with links to each other. Github renders this markdown as readable content.
- In a ["Web Version"](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/) in which Github attempts to automatically render the markdown files as HTML, and where ```https://mn-mde-edfi.github.io/``` is in the beginning of the URL in your browser.

In general we recommend using the GitHub repository version, given the limitations of the web version:
- The web version does not render markdown tables into HTML tables, so tables are best viewed directly in the [Github repository](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation). 
- Viewing markdown files directly within GitHub also allows you to use their [table of contents functionality](https://github.blog/changelog/2021-04-13-table-of-contents-support-in-markdown-files/) to navigate.

However, the web version is occasionally advantageous, such as when viewing PDFs. For example:
- The [Ed-Fi EE-MARSS Program Ambiguity Resolution](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2023-24%20MDE%20Ed-Fi%20Documentation/early_ed_marss_conflict_resolution.pdf) for school year 2023-24.
- The [Joint Powers Diagram](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2024-25%20MDE%20Ed-Fi%20Documentation/Joint%20Powers%20District%20Scenarios%20Diagram.pdf).

