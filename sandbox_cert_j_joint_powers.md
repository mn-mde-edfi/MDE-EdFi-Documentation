# Joint Powers Certification Patterns & Scenarios
For MARSS data reporting, Minnesota has several education organizations with a joint powers agreement to manage certain programs for their member districts. These programs include State Approved Alternative Programs.

These joint powers agreements pose a challenge for syncing MARSS data to MDE using Ed-Fi. Typically student data must first be shared between the joint powers district and their member districts before reporting MARSS data to MDE.

During the 2024-25 school year, MDE will pilot Ed-Fi support for students served in programs under these joint powers agreements. The patterns and scenarios listed here are intended to help vendors understand how the Ed-Fi API can support a data submission via the Student Education Organization Responsibility Association (SEORA), and typical situations when such a submission is desirable.

## Reference Information
In order to facilitate understanding of these situations, patterns, and scenarios, we have provided the following reference documents for vendors:
- The [Joint Powers Diagram](./2024-25%20MDE%20Ed-Fi%20Documentation/Joint%20Powers%20District%20Scenarios%20Diagram.pdf) that compares typical Ed-Fi submissions for MARSS data to a submission that leverages a SEORA record. This diagram explains the purpose behind those two situations and provides other useful notes.
- The [Certification Pattern Spreadsheet](./2024-25%20MDE%20Ed-Fi%20Documentation/Joint_Powers_Vendor_Certification_Pattern_Data.xlsx) that provides a readme explanatory tab, and tabs with example data for each of the two patterns below, along with additional useful information.

The MDE and MNIT teams highly recommend reviewing these documents before programming an implementation of SEORA records, and asking questions of the Ed-Fi Project Support team (EdFiProjectSupportMNIT.MDE@state.mn.us) as necessary.

## Patterns & Scenarios
The following two patterns contain collections of individual student scenarios. The reasoning behind using the patterns, along with sample data for each, are available in the [Certification Pattern Spreadsheet](./2024-25%20MDE%20Ed-Fi%20Documentation/Joint_Powers_Vendor_Certification_Pattern_Data.xlsx).

Both patterns have a **prerequisite** of a Sandbox loaded with Education Organizations and ``ResponsibilityDescriptor``. Vendors can expect to be certified on those sandboxes.

Within each pattern, scenarios are presented on a student-by-student enrollment record basis, because MDE expects that SIS software will benefit from tight integration between SSA and SEORA records. However, if vendors prefer to be tested on a resource-by-resource basis (first SSAs, then SEORAs), that is acceptable.

Student and School Identifiers used in the scenarios below are **for reference only** in order to demonstrate the required integration. Vendors are expected to generate their own student identifiers and to use school IDs from districts they support. Any additional school identifiers needed can be acquired from the ODS API, as detailed in the [Read-Only Endpoints](./sis_test_plan_c_data_reqs.md#read-only-api-endpoints) section of the Data Requirements and API Resources document. 

### Pattern 1: Member SEORA

#### Prerequisite Data
- Five Students, designated A through E
- Unique IDs of students provided to MDE team

#### Student A Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10271009
 - StudentUniqueId: 0009000001111
 - EntryDate: 2023-07-11
 - EntryType: 0
 - EntryGradeLevel: 12
 - ExitWithdrawDate: 2023-08-03
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 46
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10271000
 - MembershipAttendanceUnit: Days
 - Attendance: 0.0
 - Membership: 0
 - PercentEnrolled: 100
 - TransportationCategory: 0
 - TransportationLEA: 10271000

##### SEORA
 - EdOrgReference SchoolID: 10271009
 - StudentUniqueId: 0009000001111
 - ReportingEdOrgReference SchoolID: 60917600
 - BeginDate: 2023-07-11
 - EndDate: 2023-08-03
 - ResponsibiltyDescriptor: MARSS

#### Student A Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10271009
 - StudentUniqueId: 0009000001111
 - EntryDate: 2023-08-28
 - EntryType: 0
 - EntryGradeLevel: 12
 - ExitWithdrawDate: 2024-05-30
 - ExitWithdrawType: 8
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 19
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10271000
 - MembershipAttendanceUnit: Days
 - Attendance: 151.0
 - Membership: 168
 - PercentEnrolled: 100
 - TransportationCategory: 3
 - TransportationLEA: 10271000

##### SEORA
 - EdOrgReference SchoolID: 10271009
 - StudentUniqueId: 0009000001111
 - ReportingEdOrgReference SchoolID: 60917030
 - BeginDate: 2023-08-28
 - EndDate: 2024-05-30
 - ResponsibiltyDescriptor: MARSS

#### Student B Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10194510
 - StudentUniqueId: 0009000001112
 - EntryDate: 2023-07-31
 - EntryType: 4
 - EntryGradeLevel: 10
 - ExitWithdrawDate: 2023-08-04
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 1
 - StateAidCategory: 77
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10194000
 - MembershipAttendanceUnit: Hours 
 - Attendance: 13.0
 - Membership: 13
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10194000

##### SEORA
 - EdOrgReference SchoolID: 10194510
 - StudentUniqueId: 0009000001112
 - ReportingEdOrgReference SchoolID: 60917105
 - BeginDate: 2023-07-31
 - EndDate: 2023-08-04
 - ResponsibiltyDescriptor: MARSS

#### Student B Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10194510
 - StudentUniqueId: 0009000001112
 - EntryDate: 2023-09-08
 - EntryType: 24
 - EntryGradeLevel: 11
 - ExitWithdrawDate: 2023-10-17
 - ExitWithdrawType: 20
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 27
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10194000
 - MembershipAttendanceUnit: Hours
 - Attendance: 95.0
 - Membership: 95
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10194000

##### SEORA
 - EdOrgReference SchoolID: 10194510
 - StudentUniqueId: 0009000001112
 - ReportingEdOrgReference SchoolID: 60917105
 - BeginDate: 2023-09-08
 - EndDate: 2023-10-17
 - ResponsibiltyDescriptor: MARSS

#### Student C Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10199027
 - StudentUniqueId: 0009000001113
 - EntryDate: 2023-09-05
 - EntryType: 4
 - EntryGradeLevel: 11
 - ExitWithdrawDate: 2023-10-17
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 27
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10199000
 - MembershipAttendanceUnit: Hours
 - Attendance: 105.5
 - Membership: 106
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10199000

##### SEORA
 - EdOrgReference SchoolID: 10199027
 - StudentUniqueId: 0009000001113
 - ReportingEdOrgReference SchoolID: 60917105
 - BeginDate: 2023-09-05
 - EndDate: 2023-10-17
 - ResponsibiltyDescriptor: MARSS

#### Student C Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10199027
 - StudentUniqueId: 0009000001113
 - EntryDate: 2023-10-23
 - EntryType: 24
 - EntryGradeLevel: 11
 - ExitWithdrawDate: 2024-06-06
 - ExitWithdrawType: 40
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 27
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10199000
 - MembershipAttendanceUnit: Hours
 - Attendance: 565.3
 - Membership: 627
 - PercentEnrolled: 999
 - TransportationCategory: 6
 - TransportationLEA: 10199000

##### SEORA
 - EdOrgReference SchoolID: 10199027
 - StudentUniqueId: 0009000001113
 - ReportingEdOrgReference SchoolID: 60917104
 - BeginDate: 2023-10-23
 - EndDate: 2024-06-06
 - ResponsibiltyDescriptor: MARSS

#### Student D Enrollment
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10271502
 - StudentUniqueId: 0009000001114
 - EntryDate: 2023-12-01
 - EntryType: 4
 - EntryGradeLevel: EE
 - ExitWithdrawDate: 2024-05-24
 - ExitWithdrawType: 40
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 19
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10271000
 - MembershipAttendanceUnit: Hours
 - Attendance: 46.0
 - Membership: 59
 - PercentEnrolled: 999
 - TransportationCategory: 3
 - TransportationLEA: 10271000

##### SEORA
 - EdOrgReference SchoolID: 10271502
 - StudentUniqueId: 0009000001114
 - ReportingEdOrgReference SchoolID: 60917700
 - BeginDate: 2023-12-01
 - EndDate: 2024-05-24
 - ResponsibiltyDescriptor: MARSS

#### Student E Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10199226
 - StudentUniqueId: 0009000001115
 - EntryDate: 2023-09-05
 - EntryType: 4
 - EntryGradeLevel: 11
 - ExitWithdrawDate: 2023-11-08
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 1
 - StateAidCategory: 3
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10199000
 - MembershipAttendanceUnit: Hours
 - Attendance: 213.1
 - Membership: 258
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10199000

##### SEORA
 - EdOrgReference SchoolID: 10199226
 - StudentUniqueId: 0009000001115
 - ReportingEdOrgReference SchoolID: 60917080
 - BeginDate: 2023-09-05
 - EndDate: 2023-11-08
 - ResponsibiltyDescriptor: MARSS

#### Student E Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 10199226
 - StudentUniqueId: 0009000001115
 - EntryDate: 2023-11-09
 - EntryType: 24
 - EntryGradeLevel: 11
 - ExitWithdrawDate: 2024-06-06
 - ExitWithdrawType: 40
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 1
 - StateAidCategory: 3
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10199000
 - MembershipAttendanceUnit: Hours
 - Attendance: 592.8
 - Membership: 780
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10199000

##### SEORA
 - EdOrgReference SchoolID: 10199226
 - StudentUniqueId: 0009000001115
 - ReportingEdOrgReference SchoolID: 60917080
 - BeginDate: 2023-11-09
 - EndDate: 2024-06-06
 - ResponsibiltyDescriptor: MARSS

### Pattern 2: JP SEORA
#### Prerequisite Data
- Two Students, designated I and J
- Unique IDs of students provided to MDE team

#### Student I Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 616004070
 - StudentUniqueId: 0009000002211
 - EntryDate: 2023-07-03
 - EntryType: 0
 - EntryGradeLevel: EE
 - ExitWithdrawDate: 2023-07-31
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 0
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10549000
 - MembershipAttendanceUnit: Hours
 - Attendance: 9.0
 - Membership: 9
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10549000

##### SEORA
 - EdOrgReference SchoolID: 616004070
 - StudentUniqueId: 0009000002211
 - ReportingEdOrgReference SchoolID: 10549010
 - BeginDate: 2023-07-03
 - EndDate: 2023-07-31
 - ResponsibiltyDescriptor: MARSS

#### Student I Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 616004070
 - StudentUniqueId: 0009000002211
 - EntryDate: 2023-09-05
 - EntryType: 24
 - EntryGradeLevel: EE
 - ExitWithdrawDate: 2024-05-31
 - ExitWithdrawType: 40
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 0
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10549000
 - MembershipAttendanceUnit: Hours
 - Attendance: 39.0
 - Membership: 39
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10549000

##### SEORA
 - EdOrgReference SchoolID: 616004070
 - StudentUniqueId: 0009000002211
 - ReportingEdOrgReference SchoolID: 10549010
 - BeginDate: 2023-09-05
 - EndDate: 2024-05-31
 - ResponsibiltyDescriptor: MARSS

#### Student J Enrollment 1
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 616004070
 - StudentUniqueId: 0009000002212
 - EntryDate: 2023-09-12
 - EntryType: 5
 - EntryGradeLevel: EE
 - ExitWithdrawDate: 2023-10-13
 - ExitWithdrawType: 99
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 2
 - StateAidCategory: 0
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10549000
 - MembershipAttendanceUnit: Hours
 - Attendance: 3.0
 - Membership: 3
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10549000

##### SEORA
 - EdOrgReference SchoolID: 616004070
 - StudentUniqueId: 0009000002212
 - ReportingEdOrgReference SchoolID: 10549010
 - BeginDate: 2023-09-12
 - EndDate: 2023-10-13
 - ResponsibiltyDescriptor: MARSS

#### Student J Enrollment 2
##### SSA
 - SchoolYear: 2024
 - SchoolReference SchoolID: 616004070
 - StudentUniqueId: 0009000002212
 - EntryDate: 2023-10-16
 - EntryType: 24
 - EntryGradeLevel: EE
 - ExitWithdrawDate: 2024-05-31
 - ExitWithdrawType: 40
 - CalendarReference: {fillAsNecessary}
 - SpecialEdEvalStatus: 4
 - StateAidCategory: 0
 - HomeboundService: N
 - SpecialPupil: N
 - ResidentLEAReference: 10549000
 - MembershipAttendanceUnit: Hours
 - Attendance: 39.0
 - Membership: 39
 - PercentEnrolled: 999
 - TransportationCategory: 0
 - TransportationLEA: 10549000

##### SEORA
 - EdOrgReference SchoolID: 616004070
 - StudentUniqueId: 0009000002212
 - ReportingEdOrgReference SchoolID: 10549010
 - BeginDate: 2023-10-16
 - EndDate: 2024-05-31
 - ResponsibiltyDescriptor: MARSS
