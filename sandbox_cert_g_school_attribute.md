# School Attribute Certification Scenarios
A new resource has been created for the purpose of collecting school specific information. Ed-fi School records are currently created and maintained by MDE, which necessitated a new extension entity to capture school specific data to be provided by the districts for their respective schools.

## Virtual School Status
**Postponed until after school year 2022-23.**

Defines schools that are self-designating as virtual schools beyond state-designated Online Learning providers. For example, when using blended learning and other hybrid combinations.

**Prerequisite Data**
  - Schools (loaded by MDE)
  - Use of an API endpoint containing:
    - the new /MN/schoolAttributes resource ("schoolAttributes")
    - Indicator and Indicator Level Descriptors

**Scenarios**
  - Add the "VSS" Indicator Descriptor to two schools via the *schoolAttributes* resource and *educationOrganizationIndicators* collection, then:
    - For School 1 (a school that is not classified as type 46):
      - Set the Indicator Level Descriptor to FACEVIRTUAL
    - For School 2 (a school that is classified as 46):
      - Set the Indicator Level Descriptor to FACEVIRTUAL
  - Change School 1's Virtual School Status Level from FACEVIRTUAL to FULLVIRTUAL
  - Change School 2's Virtual School Status Level from FACEVIRTUAL to SUPPVIRTUAL
  - Change School 1's Virtual School Status Level from FULLVIRTUAL to NOTVIRTUAL

## Title I Part A School Designation
**Postponed until after school year 2022-23.**

While the Title I Part A designation is available for *get* (read only) requests on the *school* resource in the API, using the School Attribute resource provides districts a way to *post* (write) information about this designation.

### **Prerequisite Data**
  - Schools (loaded by MDE)
  - Use of an API endpoint containing:
    - the new /MN/schoolAttributes resource ("schoolAttributes")
    - ```titleIPartASchoolDesignationDescriptors```

### **Scenarios**
 - Submit a designation of ```Schoolwide``` for an elementary school
 - Submit a designation of ```Targeted Assistance``` for a high school
 - Remove the ```Schoolwide``` designation from the elementary school


# Navigation
- [Return to Sandbox Certification Overview](sandbox_cert_a_toc.md)