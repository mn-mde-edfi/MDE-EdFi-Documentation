# Guidance on Constructing a Single SSA for Multiple Early Education Program Associations
**NOTE: as of 2023-06-26, this guidance should be considered DRAFT ONLY. MDE teams are working to ensure it meets our essential requirements.**

During a certification call for school year 2023-24, a vendor asked for guidance on how to construct a single Student School Association (SSA) to send to Ed-Fi if a student has multiple early education program associations (SEEPAs), in particular if the begin/end dates on the program associations do not precisely match one another. This document attempts to provide that guidance. Depending on  individual SIS entry screens, this guidance may or not be useful to specific vendors. 

Please note that MDE will only use the begin and end date elements on the SEEPA records to "translate" the data into appropriate MDE-required data systems, such as MARSS; the only true requirement for the SSA is to associate the student with a school, in the grade that reflects their enrollment within that school. **(KEEP THIS PARAGRAPH? Is it accurate? Is it necessary?)**

## Questions this Guidance Needs to Answer
1. If an SSA applies to more than one SEEPA, how should the begin and end dates be constructed?
2. How should membership elements be treated in that SSA? Should it combine information or be left blank/zero?
3. Assuming the student isn't already enrolled in Kindergarten or a higher grade level, what should the *default* grade level be for the SSA? (All our documentation points to "EE" for this.)
4. How should other elements of the SSA be constructed, such as the following?
- entryTypeDescriptor / LastLocationOfAttendance
- ExitWithdrawTypeDescriptor
- mn.StateAidCategoryDescriptor
- mn.SpecialPupilIndicator
- mn.SpecialEducationEvaluationStatusDescriptor
- mn.transLocalEducationAgencyReference
- mn.ResidentLocalEducationAgencyReference
- mn.HomeboundServiceIndicator


## Guidelines
When constructing an SSA that relates to multiple SEEPAs, the following guidelines hold:
1. The **earliest begin date** from the *combined* SEEPA records should be used as the begin date for the SSA.
2. Similarly, the **latest end date** from the *combined* SEEPA records should be used as the end date for the SSA.
3. Assuming the SSA is only set up for early education, membership information (units, attendance, membership, percentEnrolled) should be left blank if possible. (The official record of membership information must be transmitted with the SEEPA records.)

## Example Situations
In each of the situations below, basic tables are used to demonstrate the specifics, in an effort to convey the guidance. We use a "pseudo MARSS format" in order to enhance understanding of the situations - but it is **important to remember** the following:
- that "MARSS" enrollment format **should not** be used as a 1:1 translation to an Ed-Fi SSA
- **no changes** to MARSS submissions or requirements are taking place as part of the EE ambiguity resolution

### Situation A: Two Overlapping Associations
We demonstrate this situation with a hypothetical student, using a pseudo-MARSS format to explain their enrollments:
| **School**  | **MARSS#**    | **Grade** | **BeginDate** | **EndDate** | **MAU** | **Membership** | **Attendance** | **%Enrolled** |
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 0242-01-002 | 1231231231234 | PA| 2023-09-07    | 2023-12-31  | Days    | 180 | 180  | 100  |
| 0242-01-002 | 1231231231234 | EC | 2023-09-15    | 2024-06-01  | Hours   | 640   | 580  | 999  |

For the **SSA** in Ed-Fi, using the recommended guidance, these can be combined into a single SSA simlar to below, to cover the full MARSS EE enrollment period. (Notice how membership elements are blank.)
| **School** | **StudentUniqueId** | **Grade** | **BeginDate** | **EndDate** | **MAU** | **Membership** | **Attendance** | **%Enrolled** |
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 10242002   | 1231231231234 | EE| 2023-09-07    | 2024-06-01  |  |  |   |  |

In order to complete the data in Ed-Fi, the above SSA **must** then be combined with the following **SEEPA** records:

| **School** | **StudentUniqueId** | **Program Type** | **Program Section** | **BeginDate** | **EndDate** | **MAU** | **Membership** | **Attendance** | **%Enrolled** |
| -- | -- | -- | - | -- | -- | -- | -- | -- | -- |
| 10242002   | 1231231231234| EE-VPK| A| 2023-09-07| 2023-12-31  | Days    | 180 | 180| 100 |
| 10242002   | 1231231231234 | EE-ECSE | | 2023-09-15    | 2024-06-01  | Hours   | 640  | 580 | 999 |

### Situation B: Three Overlapping Associations
This situation *builds on* Situation A by adding a "non MARSS" EE program (ECFE in this example). Therefore, assume the pseudo-MARSS data above holds true for this student.

To better demonstrate this situation, we work in reverse order of the Ed-Fi requirements, starting with the **SEEPA** records. Notice how there is now an *additional record* for the ECFE program association, with a later end date than previously described in Situation A:

| **School** | **StudentUniqueId** | **Program Type** | **Program Section** | **BeginDate** | **EndDate** | **MAU** | **Membership** | **Attendance** | **%Enrolled** |
| -- | -- | -- | -- | -- | -- | - | -- | -- | -- |
| 10242002   | 1231231231234| EE-VPK| A | 2023-09-07    | 2023-12-31  | Days| 180| 180| 100|
| 10242002   | 1231231231234| EE-ECSE| | 2023-09-15| 2024-06-01  | Hours   | 640| 580| 999|
| 10242002   | 1231231231234| EE-ECFE| | 2024-03-01    | 2024-06-30  | Hours| 120| 120| 0|

As a result of the additional ECFE association, we now recommend extending the end date of the **SSA**, as follows:
| **School** | **StudentUniqueId** | **Grade** | **BeginDate** | **EndDate** | **MAU** | **Membership** | **Attendance** | **%Enrolled** |
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
| 10242002   | 1231231231234| EE| 2023-09-07    | 2024-06-30  | | | | |

### Situation C: Two Non-Overlapping Associations
We demonstrate this new situation with pseudo-MARSS format again:
|**School** |**MARSS#**   |**Grade**|**BeginDate**|**EndDate**|**MAU**|**Membership**|**Attendance**|**%Enrolled**|
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
|0242-01-002|1231231231234|PA |2023-09-07   |2023-12-31 |Days   |180 |180 |100 |
|0242-01-002|1231231231234|EC |2024-02-15   |2024-06-01 |Hours  |340 |280 |999 |

Again, to demonstrate how key information is contained in the **SEEPA** records, this is how those would be submitted via Ed-Fi:
|**School**|**StudentUniqueId**|**Program Type**|**Program Section**|**BeginDate**|**EndDate**|**MAU**|**Membership**|**Attendance**|**%Enrolled**|
| -- | -- | -- | -- | -- | -- | - | -- | -- | -- |
|10242002  |1231231231234 |EE-VPK |A |2023-09-07   |2023-12-31 |Days   |180 |180 |100 |
|10242002  |1231231231234 |EE-ECSE | |2024-02-15   |2024-06-01 |Hours  |340 |280 |999 |

There are two ways to approach this situation with respect to SSAs - see below.

#### One SSA Option
This is the recommended option to keep things simple: merely construct a single **SSA** with the earliest begin and latest end dates:
|**School**|**StudentUniqueId**|**Grade**|**BeginDate**|**EndDate**|**MAU**|**Membership**|**Attendance**|**%Enrolled**|
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
|10242002  |1231231231234 |EE |2023-09-07 |2024-06-01 | | | | |

#### Two SSA Option
If it is easier within your SIS configuration, you could represent this scenario as two separate **SSAs**:
|**School**|**StudentUniqueId**|**Grade**|**BeginDate**|**EndDate**|**MAU**|**Membership**|**Attendance**|**%Enrolled**|
| -- | -- | -- | -- | -- | -- | -- | -- | -- |
|10242002  |1231231231234 |EE |2023-09-07 |2023-12-31 | | | | |
|10242002  |1231231231234 |EE |2024-02-15 |2024-06-01 | | | | |

### Situation D: Three Associations, Mixed Overlaps
This situation might be rare, but could be described as a mix of the above situations: two early education programs where the dates overlap (for example, September-November and November-December), and a third where the dates are completely separate (for example, February-March). In this situation, we again recommend keeping a single, simple SSA, which uses the earliest begin date, and latest end date, of all the early education associations combined.