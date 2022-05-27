# Digital Equity Certification Scenarios - API Resources

## Overview of Digital Equity Data Collection

Details on Student access to the internet and primary learning devices will be stored in the ```StudentEducationOrganizationAssociation```. The goal for this data is to better understand the state of digital equity that exists among students based on demographics. Student Information Systems must add the appropriate data fields within their systems to capture the data (if currently not in place) and submit the data to the MDE Ed-Fi ODS starting in school year 21-22.

The Digital Equity Collection requires SIS vendors to capture and submit responses to specific data points for each student. These responses will be posted to the Student Indicator collection.

The elements within the Student Indicator in use for this collection are the following:

- **indicatorName**
- **indicator**
- **indicatorGroup** (always set to 'DigitalEquity')

### indicatorName

This is a code used to identify a question posed to the parent or guardian.

| Valid **IndicatorName** Values to submit to Ed-Fi | Associated Question to display on User Interface |
| --- | --- |
| InternetAccessInResidence | Does the student have access to the internet on their primary learning device at home? |
| InternetAccessTypeInResidence | What is the primary type of internet service used at the residence? |
| InternetPerformance | Can the student stream a video on their primary learning device without interruption? |
| DigitalDevice | What device does the student most often use to complete school work at home? |
| PrimaryLearningDeviceProvider | Who is the provider of the primary learning device? |
| PrimaryLearningDeviceAccess | Is the primary learning device shared or not shared with another individual? |

### indicator

This will capture the responses to the questions associated with the above IndicatorNames for the student:

| Question/IndicatorName | Valid **Indicator** Response Values to submit to Ed-Fi | Conditionality |
| --- | --- | --- |
| Does the student have access to the internet on their primary learning device at home? _**(InternetAccessInResidence)**_ | Yes; No - Not Available; No - Not Affordable; No - Other | Always collect |
| What is the primary type of internet service used at the residence? _**(InternetAccessTypeInResidence)**_ | ResidentialBroadband; CellularNetwork; SchoolProvidedHotSpot; Satellite; Dial-up; Other; Unknown | Only Collect when indicator for _InternetAccessInResidence_ _= 'Yes'_ |
| Can the student stream a video on their primary learning device without interruption? _**(InternetPerformance)**_ | Yes - No issues; Yes - But not consistent; No | Only collect when indicator for _InternetAccessInResidence_ _= 'Yes'_ |
| What device does the student most often use to complete school work at home? _**(DigitalDevice)**_ | Desktop/Laptop; Tablet; Chromebook; SmartPhone; None; Other | Always collect |
| Who is the provider of the primary learning device? _**(PrimaryLearningDeviceProvider)**_ | Personal; School; Other | Only collect when indicator for _DigitalDevice_ _Is not 'None'_ |
| Is the primary learning device shared or not shared with another individual? _**(PrimaryLearningDeviceAccess)**_ | Shared; Not Shared; Unknown | Only collect when indicator for _DigitalDevice_ _Is not 'None'_ |

Each of these elements are of data type "string". Because of this we strongly recommending that SIS vendors control the quality of data entry based on providing the desired values for selection in a 'drop down' on the user interface (manual text data entry will result in invalid indicator values). It is also recommended that conditionality of each of the questions as outlined below be applied to the user interface. For example, you would not require a user to answer the question for **PrimaryLearningDeviceProvider** when **DigitalDevice = 'None'**

## Resource: StudentEducationOrganizationAssociation

### Description

This association indicates any relationship between a student and an education organization other than how the state views enrollment. Enrollment relationship semantics are covered by StudentSchoolAssociation.

### Prerequisite Data

- Students
- EducationOrganizations (Schools)

### Scenarios

1. Submit a set of Digital Equity Student Indicators for 4 students by updating existing StudentEducationOrganizationAssociations where Student Indicators were not previously submitted. (Note - For each Digital Equity StudentIndicator submitted, always set IndicatorGroup = 'DigitalEquity'.)
    - Student 1:
        - InternetAccessInResidence = Yes
        - InternetAccessTypeInResidence = ResidentialBroadband
        - InternetPerformance = Yes - No issues
        - DigitalDevice = Desktop/Laptop
        - PrimaryLearningDeviceProvider = Personal
        - PrimaryLearningDeviceAccess = Shared
    - Student 2:
        - InternetAccessInResidence = Yes
        - InternetAccessTypeInResidence = CellularNetwork
        - InternetPerformance = Yes - But not consistent
        - DigitalDevice = None
    - Student 3:
        - InternetAccessInResidence = No - Not Available
        - DigitalDevice = Tablet
        - PrimaryLearningDeviceProvider = School
        - PrimaryLearningDeviceAccess = Not Shared
    - Student 4:
        - InternetAccessInResidence = No - Not Affordable
        - DigitalDevice = None
2. Submit updates to demonstrate ability to capture and submit all valid indicator values
    - UpdateStudent 4's indicator for **InternetAccessInResidence** to
        - No – Other
    - Update Student 1's indicator for **InternetAccessTypeInResidence** to
        - SchoolProvidedHotSpot
        - Satellite
        - Dial-up
        - Other
        - Unknown
    - Update Student 1's indicator for **InternetPerformance** to
        - No
    - Update Student 1's indicator for **DigitalDevice** to
        - Chromebook
        - SmartPhone
        - None
        - Other
    - Update Student 1's indicator for **PrimaryLearningDeviceProvider** to
        - Other
    - Update Student 1's indicator for **PrimaryLearningDeviceAccess** to
        - Unknown

3. Remove Digital Equity Student Indicators from Student 4

# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)
- [Advance to School Attribute](sandbox_cert_g_school_attribute.md)