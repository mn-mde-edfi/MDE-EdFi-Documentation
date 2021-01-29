# Transactional Update Procedures
Unlike "bulk upload" data submission systems, the Ed-Fi API allows for more *transactional* processes to be used to maintain data. This means that maintaining the information can be done with smaller transactions that affect only the records you need to create, update, or delete. This document outlines some of the details around deleting or records.

## Deleting an Entire Record
If you need to delete a full record, submit a *Delete* call, including the resource id identifying the specific record to be deleted. You will have to handle dependencies in some cases.

## Updating a Record or Deleting Part of the Record
When you have to change information on an Ed-Fi resource, such as a student, you have three options, outlined in the sections below.

### Option 1: POST the Record Again Without Deleting it First  
- POST operates as an *upsert* (updating if possible, inserting if necessary), and requires the identity or primary key elements to execute the update, and can only be used for updates when the primary key of the resource has not changed. (Using the ```StudentSchoolAssociation``` example, any change in the EntryDate, SchoolId or Student Id submitted via POST will result in a new record being created because it affects the primary key elements.)
- To remove a property from the resource with a POST, you must explicitly exclude that property. For example, when ```stateAidCategoryDescriptor``` needs to be removed from the ```StudentSchoolAssociation```, POST the ```StudentSchoolAssociation``` without the ```stateAidCategoryDescriptor```.

### Option 2: Submit a PUT on the Record
- PUT will only update existing records using the api resource id to identify the record
- PUT allows the primary key to be modified in some cases. Again using ```StudentSchoolAssociation```, if you only needed to fix the EntryDate on the ```StudentSchoolAssociation```, this could be done with a PUT.
- Removing a property is done the same way as with POST - by excluding the property from the JSON when executing the PUT call.
- If cascading updates are not enabled on a particular entity, updates to the primary key will be blocked.

### Option 3: Delete the record and resubmit the updated version of the record
- This is an approach that is commonly used by vendors submitting in bulk, but it can work for individual transactions as well.
- It may require dependent data to also be deleted. For example, if you are trying to delete a student, you would have to delete the ```StudentSchoolAssociation``` and any ```programAssocations``` linked to that student first, and then delete the student resource. When you add the student back, you must add the relationships back in based on what your database currently reflects.

## Q&A
Since this topic came up based on some questions from a district, we'll reflect the answers to those questions here:
- **Q:** Are we supposed to send some sort of ‘delete’ existing record(s) to update a student's new entry date along with the new data?
- **A:** You could either delete the StudentSchoolAssociation and resubmit with the correct date OR submit a PUT to update the record. Using POST (upserting) won't work because the date is part of the natural key. The more straightforward option is likely just delete and resubmit.  
- **Q:** Should we plan on removing all existing data somehow so we can reload from scratch each time?
- **A:** This is generally discouraged because it bogs down the server with unnecessary api requests. Instead, sending deletes and reloads for individual records or students needing to be refreshed is preferred. 
- **Q:** Is this handled on the MDE side? If our new file no longer had records for a student with obsolete dates, does MDE assume the deletion when the data comes in?
- **A:** No, deletions at the record level are not assumed. The only time a deletion is assumed is when you omit something within a record you had submitted previously. For example, a POST call of a StudentSchoolAssociation without a previously submitted ```stateAidCategoryDescriptor``` will remove the ```stateAidCategoryDescriptor```. 
