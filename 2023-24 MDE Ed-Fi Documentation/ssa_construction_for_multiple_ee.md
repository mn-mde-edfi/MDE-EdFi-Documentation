# Instructions on Constructing SSAs for Multiple Early Education Program Associations
**NOTE: as of 2023-06-30, these instructions are in a DRAFT state. MDE teams are working to ensure the methods described here meet our essential requirements.**

During a certification call for school year 2023-24, a vendor asked for instructions on how to construct Student School Associations (SSAs) to send to Ed-Fi if a student has multiple early education program associations (SEEPAs), in particular if the begin/end dates on the program associations do not precisely match one another. This document attempts to provide instructions that will best meet MDE's needs for various program and enrollment requirements. In order to ensure proper translations of data into various MDE systems, vendors must follow these instructions precisely.

## Definitions
For the purposes of these instructions, "early education program" applies to any of the following program associations (the **bold** abbreviations used are from [Ed-Fi program types](/descriptorTables/ProgramTypeDescriptor.csv)), which will be used in the SEEPA records:
 - MARSS programs
   - **EE-ECS**, Early Childhood Screening (aka Preschool Screening)
   - **EE-ECSE**, Early Childhood Special Education
   - **EE-SR+**, School Readiness Plus
   - **EE-VPK**, Voluntary Pre-Kindergarten
 - Non-MARSS programs
   - **EE-ECFE**, Early Education - Early Childhood Family Education
   - **EE-SR**, Early Education - School Readiness
There will often be different requirements for MARSS programs vs. Non-MARSS programs, so delineating these is important to these instructions.

## Basic Principles
When constructing SSA records and SEEPA records, the following basic principles hold:
1. If you have a situation where MARSS would justify a new enrollment (for example, a change in transportation district or state aid category), as usual you must construct a new SSA to hold that information, with new begin and end dates. As a result, you must also construct a new SEEPA record (or records, if multiple programs apply) with matching begin and end dates.
    - One exception is an EE-ECS Early Childhood Screening (aka Preschool Screening) record; these records will continue to be translated as previously, and the begin date on the SEEPA should be the date the screening concluded. As explained in the Early Childhood Screening section of the Ed-Fi data guide, the LEA does not need to add an SSA record if the student is already reported in another grade. If no prior SSA exists for the student, an "EE" grade SSA record should be created in order to enable the EE-ECS SEEPA record.
2. For each program, the membership information (membership attendance units, membership, attendance, and percent enrolled) will come from the SEEPA record. All other "enrollment information" will be derived from the SSA record for MARSS programs.
    - If you find yourself in a situation where you have SEEPA records for both MARSS and non-MARSS programs with the same begin dates, bias the required enrollment elements on the matching SSA record toward the MARSS programs. Virtually all information required for the non-MARSS programs is held on the SEEPA record.
3.	As long as the combination of school, student, and begin date is unique, you may construct as many SSA records as you need in order to manage the various enrollment changes AND/OR the appropriate SEEPA records for the student.
4.	If the student is not already enrolled in a grade of Kindergarten or higher, the default grade level on the SSA should be "EE". (Please note that the ambiguity resolution eliminates many previously used grade descriptors that integrated program sections.)

## Example Situations
In each of the situations below, basic tables are used to demonstrate the specifics, in an effort to convey the guidance. We use a "pseudo MARSS format" in order to enhance understanding of the situations - but it is **important to remember** the following:
 - the "MARSS" enrollment format **should not** be used as a 1:1 translation to an Ed-Fi SSA (nor vice versa)
 - **no changes** to MARSS submissions or requirements are taking place as part of the EE ambiguity resolution

### Situation A: Two Overlapping MARSS Associations
We demonstrate this situation with a hypothetical student, using a pseudo-MARSS format to explain their enrollments:

|School     |MARSS#       |Grade|BeginDate |EndDate                        |MAU  |Membership|Attendance|%Enrolled|
|-----------|-------------|-----|----------|-------------------------------|-----|----------|----------|---------|
|0242-01-002|1231231231234|PA   |2023-09-07|2023-12-31                     |Days |180       |180       |100      |
|0242-01-002|1231231231234|EC\* |2023-09-15|2024-06-01|Hours|640       |580       |999      |

Note that this scenario of an overlapping EC record can **only happen** if the special education evaluation status is 2, and this is the **only valid combination** of overlapping records with MARSS programs.

For this situation, you must create two SSAs in Ed-Fi, using the following pattern. (Notice how membership elements are blank.)

|School  |StudentUniqueId|Grade|BeginDate |EndDate   |Non-membership required elements                                                                         |
|--------|---------------|-----|----------|----------|---------------------------------------------------------------------------------------------------------|
|10242002|1231231231234  |EE   |2023-09-07|2023-12-31|Fill in as required for the VPK program                                                                  |
|10242002|1231231231234  |EE   |2023-09-15|2024-06-01|Fill in as required for the EE-ECSE program. (specialEducationEvaluationStatusDescriptor **must** be "2")|

In order to complete the data in Ed-Fi, the above SSA **must** then be combined with the following **SEEPA** records (notice how the dates match the SSA records exactly):
|School  |StudentUniqueId|Program Type|Program Section|BeginDate |EndDate   |MAU  |Membership|Attendance|%Enrolled|
|--------|---------------|------------|---------------|----------|----------|-----|----------|----------|---------|
|10242002|1231231231234  |EE-VPK      |A              |2023-09-07|2023-12-31|Days |180       |180       |100      |
|10242002|1231231231234  |EE-ECSE     |               |2023-09-15|2024-06-01|Hours|640       |580       |999      |

If you encounter a situation where the EE-ECSE program begin date exactly matches the EE-VPK begin date, and you need to differentiate non-membership elements in the SSA, contact MDE for a workaround.

### Situation B: A MARSS Association Overlapping with a non-MARSS Association, same begin dates
We demonstrate this situation with a hypothetical student, using a pseudo-MARSS format to explain their enrollment in just the MARSS program:
|School     |MARSS#       |Grade|BeginDate |EndDate   |MAU  |Membership|Attendance|%Enrolled|
|-----------|-------------|-----|----------|----------|-----|----------|----------|---------|
|0242-01-002|1231231231234|EC   |2023-09-07|2024-06-01|Hours|640       |580       |999      |

In this situation, the student is also enrolled in a non-MARSS program, EE-ECFE. That participation starts at the **same** begin date and has a similar end date. Given the same begin date, we can only construct a **single SSA** in Ed-Fi, so we focus on what the EE-ECSE record needs:

|School  |StudentUniqueId|Grade|BeginDate |EndDate   |Non-membership required elements|
|--------|---------------|-----|----------|----------|--------------------------------|
|10242002|1231231231234  |EE   |2023-09-07|2024-06-01|Fill in for the EE-ECSE program |

In order to complete the data in Ed-Fi, the above SSA must then be combined with the following SEEPA records:

|School  |StudentUniqueId|Program Type|BeginDate |EndDate                        |MAU  |Membership|Attendance|%Enrolled|Other Elements               |
|--------|---------------|------------|----------|-------------------------------|-----|----------|----------|---------|-----------------------------|
|10242002|1231231231234  |EE-ECSE     |2023-09-07|2024-06-01                     |Hours|640       |580       |999      |                             |
|10242002|1231231231234  |EE-ECFE     |2023-09-07|2024-05-30|Hours|640       |580       |0        |Funding source, Reason Exited|

Notice how we acquire more details for the EE-ECFE program on the SEEPA record, making it rely less on the SSA.

### Situation C: Overlapping MARSS and non-MARSS Associations, different begin dates
This situation is similar to Situation A, except that the two programs consist of one MARSS program (i.e. VPK) and one non-MARSS program (ie ECFE). Therefore, it is resolved similarly: create two SSA records, one for each program. Use the exact same begin and end dates to create *matching* SEEPA records. This is demonstrated in the tables below, representing the SSA and SEEPA records.

Note the dates on the SSA records:
|School  |StudentUniqueId|Grade|BeginDate |EndDate   |Non-membership required elements          |
|--------|---------------|-----|----------|----------|------------------------------------------|
|10242002|1231231231234  |EE   |2023-09-07|2023-05-31|Fill in as required for the EE-VPK program|
|10242002|1231231231234  |EE   |2023-09-15|2024-06-01|Fill in as required for the EE-ECFE       |

Now look at the SEEPA records with matching dates:
|School  |StudentUniqueId|Program Type|Program Section|BeginDate |EndDate   |Membership required elements               |
|--------|---------------|------------|---------------|----------|----------|-------------------------------------------|
|10242002|1231231231234  |EE-VPK      |A              |2023-09-07|2023-05-31|Fill in as required for the EE-VPK program |
|10242002|1231231231234  |EE-ECFE     |               |2023-09-15|2024-06-01|Fill in as required for the EE-ECFE program|

### Handling Multiple Overlapping Associations
As noted in Situation A, there is only one known situation where two MARSS programs can overlap, so if an enrollment change justifies a new SSA, you should place an end date on the older SSA, place an end date on the related SEEPA, and then create a new SSA-SEEPA combination that describes that enrollment change. This could be due to any reason for an enrollment change, including a change in the MARSS EE program.

The same principle applies to non-MARSS programs: when in doubt, if more than one program is needed for a student, create two SSA records, and two matching SEEPA records. If you have a situation where a MARSS program starts on the same day as a non-MARSS program, you’ll only be able to use one SSA. Therefore, make sure the SSA-SEEPA combination has what is necessary for the MARSS program, and make sure the SEEPA has what is necessary for the non-MARSS program.
