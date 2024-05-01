# Deleting Resources Certification Scenarios
For school year 2024-25, vendors will be required to demonstrate the ability to delete data from MDE's Ed-Fi ODS/API. This document will outline scenarios for these capabilities, focusing on the MARSS-related data resources and elements.

## References and Background
Before reading these scenarios, please refer to the [Ed-Fi Model Dependency Diagrams](sis_test_plan_c_data_reqs.md#ed-fi-model-dependency), particularly the [MARSS collection diagram](sis_test_plan_c_data_reqs.md#marss-collection) section. Understanding data dependencies in the Ed-Fi data model is critical to implementing the ability to delete data. For example, a student record cannot be deleted before a related student school association record, because the latter relies on the former.

Districts and LEAs should not be expected to understand the entirety of these dependencies in order to delete data. Instead, vendors should build warnings and logic dialogs into SIS software asking users for confirmation/reversal of deletion attempts.

For example, if Student XYZ has the following associated records:
- Student School Association (SSA)
- Student Education Organization Association (SEOA)
- Student Program Association (ie ``StudentCEISProgramAssociation``)
...then an attempt to delete Student XYZ should come with a prompt asking the user to confirm deletion of each of the above records, or to reverse the decision.

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

### Scenario A: Delete Data via Reverse Dependency
This scenario focuses on deleting data in reverse (bottom-up) of the data hierarchy. If users execute deletion in a similar order, where dependencies aren't violated, errors need not be raised. Presumably when a district is deleting a record at the lower end of the dependency model, they are likely not needing to delete a whole student record, but **associated** records. Nevertheless, the scenario tests the entire deletion sequence.

For **Student A**, demonstrate the ability to delete, in this order:
1. The ``StudentGiftedTalentedProgramAssociation``
2. The ``StudentEducationOrganizationAssociation``
3. The elementary school ``StudentSchoolAssociation``
4. The student record itself

At the end of the scenario, all records associated with Student A should be eliminated from the ODS.

### Scenario B: Delete All Dependent Data Along with Student
This scenario starts from the assumption that an entire student record, along with **all** dependent data, can be deleted from one step in the SIS, if that is desired by the user. Presumably when a district is deleting a student record at the **top** of the dependency model, they want all dependent data deleted as well - but they need to be warned about those deletions and given an opportunity to reverse course.

For **Student B**, demonstrate the following abilities:
1. If the district attempts to delete the student, the user is warned that the middle school ``StudentSchoolAssociation``, the ``StudentEducationOrganizationAssociation``, and the ``StudentHomelessProgramAssociation`` will also be deleted, with some indication of the hierarchy. The user should be able to reverse course and **cancel** this action.
2. If the district **confirms** the desire to delete the student and all dependent records, then via one action, the following records should be deleted via the Ed-Fi API, in order:
- The ``StudentHomelessProgramAssociation``
- The ``StudentEducationOrganizationAssociation``
- The middle school ``StudentSchoolAssociation``
- The student record itself

At the end of the scenario, all records associated with Student B should be eliminated from the ODS.

### Scenario C: Mixed Deletions in the Middle of the Hierarchy
This scenario assumes that the district wants to delete certain dependent records, but keep the student itself. This requires that the vendor understand the hierarchical dependencies, and may benefit from conveying those hierarchies to the user.

For **Student C**, demonstrate the following:
1. If a district attempts to delete the student, they should  have the opportunity to delete individual dependencies at the bottom of the hierarchy, such as the ``StudentLanguageInstructionProgramAssociation``. They should have a way to select and confirm that they only want to delete that record.
2. If the district attempts to delete the high school ``StudentSchoolAssociation``, they should be warned that this will also delete the ``StudentEducationOrganizationAssociation``, and then be able to either confirm that choice, or reverse course and **cancel** this action.

At the end of the scenario, all but the **student** record for Student C should be eliminated from the ODS.