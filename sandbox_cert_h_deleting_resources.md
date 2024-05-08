# Deleting Resources Certification Scenarios
For school year 2024-25, vendors will be required to demonstrate their customer's ability to delete data from MDE's Ed-Fi ODS/API. This document will outline scenarios for these capabilities, focusing on the MARSS-related data resources and elements.

## References and Background
Before reading these scenarios, please refer to the [Ed-Fi Model Dependency Diagrams](sis_test_plan_c_data_reqs.md#ed-fi-model-dependency), particularly the [MARSS collection diagram](sis_test_plan_c_data_reqs.md#marss-collection) section. Understanding data dependencies in the Ed-Fi data model is critical to implementing the ability to delete data. For example, a student record cannot be deleted before a related student school association record, because the latter relies on the former.

Districts and LEAs should not be expected to understand the entirety of these dependencies in order to delete data. Instead, MDE suggests that vendors build warnings and logic dialogs into SIS software asking users for confirmation/reversal of deletion attempts, if the vendor deems it necessary for their users.

For example, if Student XYZ has the following associated records:
- Student School Association (SSA)
- Student Education Organization Association (SEOA)
- Student Program Association (ie ``StudentCEISProgramAssociation``)
...then an attempt to delete Student XYZ *could* come with a prompt asking the user to confirm deletion of each of the above records, or to reverse the decision. Such a prompt is **not** required to pass these scenarios.

These scenarios assume the ability to successfully **create** new data as outlined in other certification documents, such as for [MARSS enrollment](sandbox_cert_b_marss.md) and [Student Program Associations](./sandbox_cert_c_spas.md).

## Prerequisite Data
- Schools, Programs, Descriptors
- Students Listed Below:
    - **Student A**:
        - enrolled in an elementary school via SSA
        - with demographics via an SEOA
        - associated with a ``StudentGiftedTalentedProgramAssociation``
    - **Student B**:
        - enrolled in a middle school (or middle-equivalent grade such as 5-8) via SSA
        - with demographics via an SEOA
        - associated with a ``StudentHomelessProgramAssociation``
    - **Student C**:
        - enrolled in a high school via SSA
        - with demographics via an SEOA
        - associated with a ``StudentLanguageInstructionProgramAssociation``

## Scenarios
In each of the scenarios below, the vendor should be prepared to demonstrate how when data is deleted **within** the SIS user interface and databases, the pertinent data is then **also** deleted in the Ed-Fi ODS via appropriate API calls, either through regular automated synching procedures or manual procedures available to the district user.

_Note:_ The scenarios below are **not** intended to test situations where the end goal is updated record(s). Whether vendor- or district-directed, if records are updated by a process/strategy executed as "first delete, then add back with updated information", the vendor does not need to demonstrate that capability.

### Scenario A: Delete Data at the Bottom of the Hierarchy
This scenario focuses on deleting data at the bottom of the data hierarchy. Presumably when a district is deleting a record at the lower end of the dependency model, they are likely not needing to delete a whole student record, but **associated** records. 

For **Student A**, demonstrate the ability to delete, in this order:
1. The ``StudentGiftedTalentedProgramAssociation``
2. The ``StudentEducationOrganizationAssociation``

Each step can be executed in the SIS first, then synched to the ODS via separate process. At the end of the scenario, only the elementary school ``StudentSchoolAssociation`` and the Student A record itself should remain in the ODS.

### Scenario B: Delete All Dependent Data Along with Student
This scenario starts from the assumption that an entire student record, along with **all** dependent data, can be deleted from one step in the SIS, if that is desired by the user. Presumably when a district is deleting a student record at the **top** of the dependency model, they want all dependent data deleted as well - but they may need to be warned about those deletions and given an opportunity to reverse course. 

Such warnings are optional, so vendors will be asked to choose from one of the following options:

#### Option 1: With Warnings
If the vendor opts to include warnings, demonstrate the following abilities for **Student B**:
1. If the district attempts to delete the student, the user is warned that the middle school ``StudentSchoolAssociation``, the ``StudentEducationOrganizationAssociation``, and the ``StudentHomelessProgramAssociation`` will also be deleted, with some indication of the hierarchy. The user should be able to reverse course and **cancel** this action.
2. If the district **confirms** the desire to delete the student and all dependent records, then via one action, the following records should be deleted via the Ed-Fi API, in order:
- The ``StudentHomelessProgramAssociation``
- The ``StudentEducationOrganizationAssociation``
- The middle school ``StudentSchoolAssociation``
- The student record itself

#### Option 2: Without Warnings
If the vendor deems warnings unnecessary, demonstrate how the district can initiate the deletion of all data associated with  **Student B**, and then demonstrate how that data is then deleted from the ODS via either automated or manual synching procedures. Then the following records should be deleted via the Ed-Fi API, in order:
- The ``StudentHomelessProgramAssociation``
- The ``StudentEducationOrganizationAssociation``
- The middle school ``StudentSchoolAssociation``
- The student record itself

At the end of the scenario, all records associated with Student B should be eliminated from the ODS.

### Scenario C: Mixed Deletions in the Middle of the Hierarchy
This scenario assumes that the district wants to delete most of the dependent records, but keep the student itself. MDE also suggests that the process may benefit from conveying those hierarchies to the user via warnings.

For **Student C**, if a district deletes the high school ``StudentSchoolAssociation`` in the SIS, demonstrate how both the ``StudentEducationOrganizationAssociation`` and the ``StudentLanguageInstructionProgramAssociation`` will first be deleted from the ODS before the ``StudentSchoolAssociation`` is also deleted.

At the end of the scenario, all but the **student** record for Student C should be eliminated from the ODS.