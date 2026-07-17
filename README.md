# MDE-EdFi-Documentation

This repository contains technical documentation for Minnesota's implementation of [Ed-Fi ODS/API v6.2](https://docs.ed-fi.org/reference/ods-api/6.2) and [Ed-Fi Data Standard 4.0](https://docs.ed-fi.org/reference/data-exchange/data-standard/4/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more at [MDE's Ed-Fi data submissions web page](https://education.mn.gov/MDE/dse/datasub/edfi/).

The primary audience for this documentation is SIS vendors and State of Minnesota technical staff from MDE and MNIT.

## Markdown Documentation
MNIT supporting MDE composes each collection year's documentation in markdown and CSV files. While some documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent an effort to store and maintain the documentation in markdown and CSV, in particular:

- [SIS and Vendor Test Plan](./sis_test_plan/README.md)
- [Sandbox Certification Scenarios](./sandbox_cert/README.md)

By serving documentation in multiple formats, our goal is to increase vendor access to the documentation as well as provide options for understanding and visualization changes over time.

## Descriptor Tables
The new MDE [Ed-Fi API Descriptor Tables](https://pub.education.mn.gov/edfidocs/) website is generated from MDE's Ed-Fi API for the current school year.  This website replaces the old descriptor table CSV export files.

## Additional Documentation
The [reference](https://github.com/mn-mde-edfi/MDE-EdFi-Documentation/reference) folder contains additional documentation and links may be useful to Districts and Vendors, including:
- [Transactional Update Procedures](./reference/transactional_updates.md) covers some of the core concepts of updating records with individual transactions in lieu of bulk uploads, including some examples from Ed-Fi to illustrate.
- [Common Ed-Fi Errors](./reference/common_errors.md) provides additional documentation on some types of API errors that can arise for vendors and LEAs.
- [Ed-Fi Resources](https://education.mn.gov/MDE/dse/datasub/edfi/doc/) on MDE's website hosts additional documentation for districts / LEAs on state data reporting using Ed-Fi.

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
- The [Ed-Fi EE-MARSS Program Ambiguity Resolution](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/images/early_ed_marss_conflict_resolution.pdf) for school year 2023-24.
- The [Joint Powers Diagram](https://mn-mde-edfi.github.io/MDE-EdFi-Documentation/2024-25%20MDE%20Ed-Fi%20Documentation/Joint%20Powers%20District%20Scenarios%20Diagram.pdf).

