# MDE School Food Service Mapping from MARSS to Ed-Fi

|Requirement|MARSS economicIndicator|Ed-Fi Data Collection|
|-----------|---------------------|---------------------|
|Ineligible for free or reduced price meals|0|No Student School Food Service Program Association|
|Eligible for reduced price meals|1|Student School Food Service Program Association SchoolFoodServiceProgramService = 1|
|Eligible for free meals|2|Student School Food Service Program Association SchoolFoodServiceProgramService = 2|
|Direct-certified for free meals|7|Student School Food Service Program Association SchoolFoodServiceProgramService = 2 and DirectCertification = True|
|Direct-certified for reduced price meals|8|Student School Food Service Program Association SchoolFoodServiceProgramService = 1 and DirectCertification = True|

