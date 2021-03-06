### Retrieval of patient FHIR resources to supply to CQL execution engine
The execution engine determines which FHIR resources to retrieve by analyzing the CQL. The SMART on FHIR application MUST be provided with a token that allows it to access all relevant information for the patient in question. The CQL execution engine SHOULD attempt to constrain queries as much as possible to reduce data transfer, however it MAY retrieve more data than is necessary (for example, if the CQL logic filters for medications meeting certain conditions, it is acceptable if the engine retrieves all medications for the patient, even if a more constrained query was possible).

As discussed in the Execution Results section below, it's possible not every CQL statement will be executed (for example if some questions are only relevant given certain answers to prior questions). In order to reduce data transfers and increase overall speed, data MAY be fetched as needed. However, the execution engine MAY be implemented using a different strategy (for example by doing bulk fetches before starting execution).

### Engine Execution

The package containing the CQL and Questionnaire resources can contain helper libraries that are called from other CQL files. The engine SHALL make available to the execution context all CQL libraries that are found in the package.

It is likely that different versions of CQL will need to be created for different FHIR versions, as the same information could be in a different resource. The SMART on FHIR application will have access to the FHIR endpoint, it should check the version and then retrieve the package that has been created for the correct FHIR version.

Consideration must also be made regarding the CQL version.

#### Behavior when receiving malformed CQL
If the CQL is malformed (is not syntactically correct) in any way, the execution engine SHALL not attempt any execution, and the user SHALL be notified with an appropriate on screen error message. The application SHALL log failures and ensure the maintainer of the CQL/Questionnaire package is notified. To Commenters: The method of ensuring the maintainer is notified should probably be further specified.
#### Behavior when encountering execution errors

If any errors are encountered during execution, the engine SHALL not attempt any further execution, and the user SHALL be notified with an appropriate on screen error message. The application SHALL log failures and ensure the maintainer of the CQL/Questionnaire package is notified. 

Note that a query for data that returns no results is never considered a failure.

### Execution Results

The flow of execution of the CQL will be determined by the associated questionnaire. The application will proceed through the questionnaire, and for any question that is associated with the result of a CQL statement, that specific CQL statement will be executed. The engine will use result caching so that each statement should be executed either zero or one time.