This specification uses [Clinical Quality Language (CQL)](https://cql.hl7.org) for the expression of payer rules. By using CQL, this specification allows payers to query for patient information to check conformance with rules related to a particular treatment.

Payers should construct CQL to gather information needed and test expected conditions about a patient. The DTR application will provide the CQL access to FHIR resources for the patient in question. This CQL will be executed and the resulting information will be made available for further use by the DTR application. Mainly, this information will be used to populate a Questionnaire that is also supplied by the payer.

One of the core purposes of this specification is to automate the processing of payer rules in a maner that reduces provider burden. Authors of payer rules should keep this concept in mind as they create CQL. Due to differences in workflows or information systems, clinical information may be represented in different FHIR resources or with different codes or code systems. Therefore, payer CQL may have to examine different resources or use value sets to find patient information. It is preferable to have more extensive CQL or value sets than require a user to input values that the rules were unable to find.

### Guidance on Structure of CQL Logic
Like many other programming languages, CQL allows for statements to be nested within conditional logic. This creates instances where some statements may not be executed due to a prior condition being met. This behavior should be used intentionally by payers creating CQL.

This pattern of logic structure is referred to by several names, including "eager quitting", "early return" or "short circuiting". The goal is to avoid the execution of statements if they will not be relevant given other information available to the logic.

As an example, a payer may have a set of rules or information that must be gathered on a patient if they are currently pregnant. This information may be gathered through a series of CQL statements. When constructing this CQL for DTR, these statements should be nested in conditionals to first check if the patient is female and then check whether the patient is pregnant.

### Expression Naming Conventions
CQL allows the gathering of information through the use of `define` statements. These statements are given an identifier. When CQL execution is complete, a context will be created where these identifiers are populated with the results of the statement execution.

DTR makes use of the identifier names within the CQL. The DTR application will examine the payer supplied Questionnaire resource. This resource SHALL conform to the [CQF Questionnaire Profile](http://hl7.org/fhir/R4/cqf.html) when using FHIR R4 or [CQIF Questionnaire Profile](http://hl7.org/fhir/STU3/cqif/cqif-questionnaire.html) when using FHIR STU3. For each returned statement in CQL, the DTR application will attement to find a `Questionnaire.item` with a `valueEpression` (FHIR R4) or `cqif-calculatedValue` that contains the same as the statement identifier. The resulting value held in the identifier, unless `null` will be used to answer the question.

### CQL Constraints
CQL for use in DTR SHALL have a `context` of `Patient`.