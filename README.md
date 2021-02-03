# MDE-EdFi-Documentation

****SY2021-2022 Branch ****

This repository contains documentation for Minnesota's implementation of the [Ed-Fi alliance standard](https://www.ed-fi.org/). The Minnesota Department of Education (MDE) is implementing Ed-Fi to help improve the collection of required educational data from Minnesota school districts. Learn more [at MDE's Ed-Fi web page](https://education.mn.gov/MDE/dse/datasub/edfi/) and at the following links:
- [Ed-Fi Technical Documentation](https://techdocs.ed-fi.org/)
- [Ed-Fi Data Standard](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Data+Standard)
- [Ed-Fi Operational Data Store (ODS) and API](https://techdocs.ed-fi.org/display/ETKB/Ed-Fi+Operational+Data+Store+and+API)

## Markdown Documentation
In June-July of 2020, MNIT supporting MDE converted much of the 2020-2021 school year documentation to markdown files. While the official documentation remains in Word and Excel within this repository, the markdown files at the top level of this repository represent a pilot of storing and maintaining the documentation in markdown, starting with:

- [SIS and Vendor Test Plan](sis_test_plan_a_toc.md)
- [Sandbox Certification Scenarios](sandbox_cert_a_toc.md)

### School Year 2021-2022 Additions
Adding MCCC and Digital Equity into Ed-Fi requires many of the same resources as the MARSS collection, therefore the certification scenarios added for SY2022 are frequently similar. Over time, MDE will cross-reference scenarios to each other in the markdown versions of these documents.

## Additional Documentation
We will also use this repository to store additional documentation and links that may be useful to Districts and Vendors. See the following:
- [Descriptors and Resources](descriptors_resources.md). This document contains additional information about specific descriptors and data resources that can prove useful in understanding the system.
- [MARSS Translation Guide](https://education.mn.gov/mdeprod/idcplg?IdcService=GET_FILE&dDocName=MDE033371&RevisionSelectionMethod=latestReleased&Rendition=primary). Also known as the "MDE Translation Guide", this document on the MDE website describes the technical specification and definitions used when extracting information out of the Ed-Fi ODS and translating into the data used by the Minnesota Automated Reporting Student System (MARSS).

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
