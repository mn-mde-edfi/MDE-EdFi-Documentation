# Migrant Data Reporting

There has been some confusion about the the [StudentCharacteristicDescriptor](https://pub.education.mn.gov/edfidocs/StudentCharacteristicDescriptor.html) code value for "Migrant". 

While we do not collect the Migrant indicator through Ed-Fi, we do collect that information via other sources (the MIS2000 system), which is then synced to the Ed-Fi ODS via a nightly update.

This Migrant indicator is available as a read-only attribute in the Ed-Fi API to allow SIS vendors to be able to read this information and display it to district users in their SIS. 

