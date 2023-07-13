# cynqedDocs

<b>DO’s</b>
* Classes, methods, variables, and components must have the most restrictive access modifier necessary (i.e.: always prefer private over public and only use global for webservices).  
* Debug statements should have proper context and a logging level of FINE, FINEST, or ERROR. DEBUG-level statements can be used in testing environments but must not be committed to the repository.  
* In Javascript, all logging statements should not be committed to the repository (the general public does not need to know the inner workings of our application). Console.error statements can be used, but only to report errors.  
* Properly comment on your code. It helps our support team understand what’s happening without having to decipher the code.  
* All fields, objects, LWC Components, and Aura components must have a description that documents the element’s use.  o ALL Object/Field Names and ALL Descriptions that will be part of the shared core data model MUST be approved by the Salesforce Team 
* Use tabs for indentation. (Tabs consume only one character). Check that your editor is not changing the tab to 4 spaces.  
* URLs should be, in this order: o Relative (i.e.: starts with /, not HTTP).  o If not relative, use the Site class methods to retrieve the URL dynamically. o Redirection between communities should use the OneIdUtils methods to fetch URLs (only works for  logged users).  o Only as a last resort, use a custom setting to store the value (if available, always use the custom domain – i.e.: portal.instancename.org instead of customer-portal-instancename.force.com).  
* Before creating a new label/custom setting, check if you can reuse an already existing one. Add a category to the label.  
* Before creating new Profiles, Permission Sets, LWC Components, Aura Components, and Visualforce Components,  check if you can reuse or adapt an already existing one.  
* Components (LWC, Aura, and Visualforce) must be made in a generic manner to be as reusable as possible. If you have a logic that’s very specific for your project, consider splitting it into two components a generic wrapper and a specific core.  o Non-LWC MUST be approved by the salesforce team o New lightning components must use the LWC framework. 
* LWC and Aura components must be able to inherit the branding from the community/page where it’s inserted. This also means that you should move the branding styling to the community assets and leave only very specific styling on the component CSS resource.  
* Use named credentials to store endpoints and handle authentication.  
* Use the singleton approach to access configuration objects (e.g.: RecordTypeSingleton).  
* Create code in a concise manner. (i.e.: instead of using “if(something == anotherthing) v = true; else v = false;”, use “v = (something == anotherthing);”.  
* Use semantic names for variables, methods, and classes (i.e.: use “financeContactsToUpdate” instead of “contactList”).  
* All code must be in English.  
* Create proper unit tests that check for good, bad, and bulk outcomes. Use asserts to check if the logic is working. Coverage should be 85% or higher.  
* Use formula fields to avoid queries in triggers.  
* Catch statements must be properly handled, having a system.debug is not useful.  
* Use child relationship query whenever possible (e.g. I need to query accounts and contact. Do something like “select id, name, (select id, name from contacts) from account "): queries time does not count against CPU time Limit!  
* All new fields and objects must comply with the existing Data Model. If you are not using something already in the current data model, you need to check with the salesforce lead or bring it to the Technical Review Board.  
* All new components that support descriptions, must have proper descriptions.  
* All new developments must comply with existing frameworks, if applicable.  
* All changes to managed environments (SIT, QA, PREPROD, or Production) must be approved by the Release Manager or a member of the platform team.  
* Cutover activities, post-refresh activities, and manual configurations must be documented and submitted along with the pull request to PREPROD.  
* All emails sent through APEX must be validated by the platform team.  
* Add filter criteria before publishing platform events.  
* For every new Validation Rule, ensure existing records are not failing, which means we need to update those records, and so, add this as part of cutover activities.  

<b>DON’Ts </b>
* DON’T comment on unused code. Delete it. We have source control for this reason.  
* DON’T duplicate code. Reuse, adapt, or overload.  
* DON’T use empty try/catches (only use a catch if you are doing custom handling on the error).  
* DON’T perform queries unless needed. In a trigger this means that you need to loop through the records at least once before performing queries.  
* DON’T perform unnecessary operations (i.e.: if a list is empty, don’t insert it or don’t perform a query with a filter based on it – use a return statement if the code is not going to be needed).  
* DON’T create a variable if it’s going to be used only once (saves heap size, CPU time, and characters).  
* DON’T use nested for loops, in most cases a map is preferable.  
* DON’T create a method if that code is not reusable/generic.  o Exception: To avoid creating overly large methods, it’s acceptable to create methods that encapsulate a finite logic process (even if it is not going to be reused). In these cases, ALWAYS comment on your code (you should be commenting anyway). 
* DON’T use workflow or process builder to perform field updates on processes related to a case, account, or contact (triggers consume less CPU time and avoid recursion).  
* DON’T use HTML inline styling (I.e.: the style property on an html tag).  
* DON’T override salesforce SLDS classes styling. Use a new custom class.  
* DON’T use “!important” statements in CSS, proper Specificity usually can solve the issue.  
* DON’T create new fields on Case, Account, and Contact before they have been reviewed and approved by the review board.  
* DON’T expose sensitive information in unprotected records and logs (ex. Don’t print a password in a debug statement).  
* DON’T use literal values! Use static final string.  
* DON’T schedule a class via Workbench or the console.  
* DON’T create fields longer than required. Digits and characters up to the maximum required value (critical on custom settings and metadata).  
* DON’T change permissions directly in a new environment of the release path, as with other components these changes should be part of the continuous integration.  
