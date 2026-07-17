# Special Education Data Reporting
### Student Special Education Program Associations Resource
#### Placing Local Education Agency Reference
The data element on the StudentSpecialEducationProgramAssociations resource called ```placingLocalEducationAgencyReference ``` is commonly referred to as the "Placing District". This optional element is intended for only students with IEPs who are enrolled in a joint powers or intermediate district. It is intended for a subset of students, and should not be automatically associated with any other LEA reference.

The scenario in which a student record would need ```placingLocalEducationAgencyReference ``` is:
- Student is a resident of district A and has an IEP.
- The student open enrolls to district B.
- District B places the student in a joint powers or intermediate district C.

In this scenario:
- A is the resident district
- B is probably the transporting district
- B is the placing district (should be a district type of 1, 2, 3 or 7)
- C is the enrolling/serving district

