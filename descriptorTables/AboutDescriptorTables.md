# Descriptor Tables
This folder contains a series of CSV tables that list various descriptor values, typically of descriptors that are custom to the Minnesota Ed-Fi implementation. By moving such tables out of the "Mapping Matrix" Excel spreadsheet and into individual files, we accomplish several goals:
1. Allowing full names of descriptors to label a table, instead of being limited by Excel's character limit for tabs.
2. Reducing the size of the Mapping Matrix spreadsheet.
3. Enabling viewers to see when each individual descriptor was last updated
4. Enabling viewers a quick preview of each table when selecting it within GitHub

Refer to the CSVs in this folder for either the coming school year (spring), or the current school year in effect (summer, fall, and winter). See details below.

_Note_: occasionally special characters, such as em dashes, are stored in the database but do not translate well into CSV exports. An example is in code value 2 for ``SpecialEducationEvaluationStatusDescriptor``: "Shared-Time K-12 – Evaluated, EC – Evaluated" appears as "Shared-Time K-12 ? Evaluated, EC ? Evaluated". This is merely an artifact of character translations and can be ignored.

## Source Details
As of the most recent run, these tables are derived from the following database at MDE:
- **Version**: 5.2
- **School Year**: 2023-2024
- **Environment**: Test Sandbox
- **Database**: EdFi_sb24_Ods_Minimal_Template

**Exception**: The Calendar Type Descriptor values are pulled from production EdFi_Ods_2023 until such time the recent updates are reflected in 2024 databases.

Refer to the change/commit log in GitHub to see what the latest changes are for the tables in this folder.

### Assessment Descriptors
The following Descriptors used for **Assessment** purposes are pulled from  Staging EdFi_Ods_2023:
- [AccommodationDescriptor](AccommodationDescriptor.csv)
- [AssessmentFormatDescriptor](AssessmentFormatDescriptor.csv)
- [assessmentReportingMethodDescriptor](assessmentReportingMethodDescriptor.csv) - should be renamed to *AssessmentReportingMethodDescriptor*
- [AttemptLogicDescriptor](AttemptLogicDescriptor.csv) - should be renamed to *AttemptLogic**Met**Descriptor*
- [GeneralEnrollmentDescriptor](GeneralEnrollmentDescriptor.csv)
- [OperationalPassageDescriptor](OperationalPassageDescriptor.csv)
- [PerformanceLevelDescriptor](PerformanceLevelDescriptor.csv)
- [ReasonNotTestedDescriptor](ReasonNotTestedDescriptor.csv)
- [ResultDatatypeTypeDescriptor](ResultDatatypeTypeDescriptor.csv)

Note that Assessment vendors will also want to make use of the [AcademicSubjectDescriptor](AcademicSubjectDescriptor.csv) and [GradeLevelDescriptor](GradeLevelDescriptor.csv) tables; but these are pulled from the database listed in "Source Details" above.


## List of Custom Descriptors and Links
Below is a list of known custom descriptors, typically using the ```uri://education.mn.gov``` namespace, excluding any subfolders within that space. Links are to the CSV files that you can view inside this directory. This list is automatically generated out of the same database as above, but there may be broken links of certain descriptors that we have not yet exported.
- [AcademicHonorCategoryDescriptor](AcademicHonorCategoryDescriptor.csv)
- [AcademicSubjectDescriptor](AcademicSubjectDescriptor.csv)
- [AchievementCategoryDescriptor](AchievementCategoryDescriptor.csv)
- [AesTypeDescriptor](AesTypeDescriptor.csv)
- [AncestryEthnicOriginDescriptor](AncestryEthnicOriginDescriptor.csv)
- [AssessmentCategoryDescriptor](AssessmentCategoryDescriptor.csv)
- [AssessmentToolDescriptor](AssessmentToolDescriptor.csv)
- [BehaviorDescriptor](BehaviorDescriptor.csv)
- [BullyingHarassmentTypeDescriptor](BullyingHarassmentTypeDescriptor.csv)
- [CalendarEventDescriptor](CalendarEventDescriptor.csv)
- [CalendarTypeDescriptor](CalendarTypeDescriptor.csv)
- [ClassPeriodTypeDescriptor](ClassPeriodTypeDescriptor.csv)
- [ClassroomPositionDescriptor](ClassroomPositionDescriptor.csv)
- [ClassroomVolunteerDescriptor](ClassroomVolunteerDescriptor.csv)
- [CostToPropertyDescriptor](CostToPropertyDescriptor.csv)
- [CostToVictimDescriptor](CostToVictimDescriptor.csv)
- [CourseDefinedByDescriptor](CourseDefinedByDescriptor.csv)
- [CourseLevelCharacteristicDescriptor](CourseLevelCharacteristicDescriptor.csv)
- [CourseLevelTypeDescriptor](CourseLevelTypeDescriptor.csv)
- [CrisisEventDescriptor](CrisisEventDescriptor.csv)
- [CurriculumUsedDescriptor](CurriculumUsedDescriptor.csv)
- [DisabilityDescriptor](DisabilityDescriptor.csv)
- [DisciplineDescriptor](DisciplineDescriptor.csv)
- [DistrictTypeDescriptor](DistrictTypeDescriptor.csv)
- [DrugTypeDescriptor](DrugTypeDescriptor.csv)
- [EarlyChildhoodScreenerDescriptor](EarlyChildhoodScreenerDescriptor.csv)
- [EarlyChildhoodScreeningExitStatusDescriptor](EarlyChildhoodScreeningExitStatusDescriptor.csv)
- [EarlyEducationCourseLocationDescriptor](EarlyEducationCourseLocationDescriptor.csv)
- [Ed-Fi Core: CourseIdentificationSystemDescriptor](CourseIdentificationSystemDescriptor.csv)
- [Ed-Fi Core: LanguageUseDescriptor](LanguageUseDescriptor.csv)
- [Ed-Fi Core: SchoolCategoryDescriptor](SchoolCategoryDescriptor.csv)
- [Ed-Fi Core: SexDescriptor](SexDescriptor.csv)
- [EdFiSubmissionAccessDescriptor](EdFiSubmissionAccessDescriptor.csv)
- [EntryTypeDescriptor](EntryTypeDescriptor.csv)
- [ExitWithdrawTypeDescriptor](ExitWithdrawTypeDescriptor.csv)
- [FundingSourceDescriptor](FundingSourceDescriptor.csv)
- [GenderIdentityDescriptor](GenderIdentityDescriptor.csv)
- [GeneralEnrollmentDescriptor](GeneralEnrollmentDescriptor.csv)
- [GiftedTalentedParticipationDescriptor](GiftedTalentedParticipationDescriptor.csv)
- [GradeLevelDescriptor](GradeLevelDescriptor.csv)
- [GradeTypeDescriptor](GradeTypeDescriptor.csv)
- [GradingPeriodDescriptor](GradingPeriodDescriptor.csv)
- [HomelessPrimaryNighttimeResidenceDescriptor](HomelessPrimaryNighttimeResidenceDescriptor.csv)
- [ImplementationStatusDescriptor](ImplementationStatusDescriptor.csv)
- [IncidentLocationDescriptor](IncidentLocationDescriptor.csv)
- [IndicatorDescriptor](IndicatorDescriptor.csv)
- [IndicatorLevelDescriptor](IndicatorLevelDescriptor.csv)
- [InstructionalApproachDescriptor](InstructionalApproachDescriptor.csv)
- [InstructionalDeliveryModeDescriptor](InstructionalDeliveryModeDescriptor.csv)
- [KindergartenScheduleDescriptor](KindergartenScheduleDescriptor.csv)
- [LanguageDescriptor](LanguageDescriptor.csv)
- [LanguageInstructionProgramServiceDescriptor](LanguageInstructionProgramServiceDescriptor.csv)
- [LevelOfEducationDescriptor](LevelOfEducationDescriptor.csv)
- [MediumOfInstructionDescriptor](MediumOfInstructionDescriptor.csv)
- [MembershipAttendanceUnitDescriptor](MembershipAttendanceUnitDescriptor.csv)
- [NeglectedOrDelinquentProgramDescriptor](NeglectedOrDelinquentProgramDescriptor.csv)
- [NeglectedOrDelinquentProgramOutcomeDescriptor](NeglectedOrDelinquentProgramOutcomeDescriptor.csv)
- [NeglectedOrDelinquentProgramServiceDescriptor](NeglectedOrDelinquentProgramServiceDescriptor.csv)
- [OptOutIndicatorsDescriptor](OptOutIndicatorsDescriptor.csv)
- [OtherNameTypeDescriptor](OtherNameTypeDescriptor.csv)
- [PrecodeTypeDescriptor](PrecodeTypeDescriptor.csv)
- [PreferredPronounDescriptor](PreferredPronounDescriptor.csv)
- [ProgramSectionDescriptor](ProgramSectionDescriptor.csv)
- [ProgramTypeDescriptor](ProgramTypeDescriptor.csv)
- [ProgressLevelDescriptor](ProgressLevelDescriptor.csv)
- [RaceDescriptor](RaceDescriptor.csv)
- [ReasonExitedDescriptor](ReasonExitedDescriptor.csv)
- [RelationDescriptor](RelationDescriptor.csv)
- [SchoolClassificationDescriptor](SchoolClassificationDescriptor.csv)
- [SchoolFoodServiceProgramServiceDescriptor](SchoolFoodServiceProgramServiceDescriptor.csv)
- [SecondaryBehaviorDescriptor](SecondaryBehaviorDescriptor.csv)
- [SectionCharacteristicDescriptor](SectionCharacteristicDescriptor.csv)
- [SectionEnrollmentTypeDescriptor](SectionEnrollmentTypeDescriptor.csv)
- [SiteBasedInitiativeDescriptor](SiteBasedInitiativeDescriptor.csv)
- [SpecialEducationEvaluationStatusDescriptor](SpecialEducationEvaluationStatusDescriptor.csv)
- [SpecialEducationSettingDescriptor](SpecialEducationSettingDescriptor.csv)
- [StandardAddressedDescriptor](StandardAddressedDescriptor.csv)
- [StateAidCategoryDescriptor](StateAidCategoryDescriptor.csv)
- [StudentCharacteristicDescriptor](StudentCharacteristicDescriptor.csv)
- [StudentIdentificationSystemDescriptor](StudentIdentificationSystemDescriptor.csv)
- [TelephoneNumberTypeDescriptor](TelephoneNumberTypeDescriptor.csv)
- [TermDescriptor](TermDescriptor.csv)
- [TimeOfIncidentDescriptor](TimeOfIncidentDescriptor.csv)
- [TitleIPartAParticipantDescriptor](TitleIPartAParticipantDescriptor.csv)
- [TitleIPartASchoolDesignationDescriptor](TitleIPartASchoolDesignationDescriptor.csv)
- [TransportationCategoryDescriptor](TransportationCategoryDescriptor.csv)
- [WeaponDescriptor](WeaponDescriptor.csv)
- CareerClusterDescriptor - note that this descriptor is only used for courses defined by the SEA.