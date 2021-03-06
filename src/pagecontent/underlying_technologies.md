### FHIR
This implementation guide uses terminology, notations and design principles that are
specific to FHIR. Before reading this implementation guide, it's important to be familiar with some of the basic principles of FHIR as well
as general guidance on how to read FHIR specifications. Readers who are unfamiliar with FHIR are encouraged to read (or at least skim) the following
prior to reading the rest of this implementation guide.

* [FHIR overview]({{site.data.fhir.path}}overview.html)
* [Developer's introduction]({{site.data.fhir.path}}overview-dev.html)
* (or [Clinical introduction]({{site.data.fhir.path}}overview-clinical.html))
* [FHIR data types]({{site.data.fhir.path}}datatypes.html)
* [Using codes]({{site.data.fhir.path}}terminologies.html)
* [References between resources]({{site.data.fhir.path}}references.html)
* [How to read resource & profile definitions]({{site.data.fhir.path}}formats.html)
* [Base resource]({{site.data.fhir.path}}resource.html)

This implementation guide also leverages the US Core set of profiles defined by HL7 for sharing human EHR data in the US.  Additional information is located at: [US-Core](http://hl7.org/fhir/us/core/2019Jan/)

This implementation guide supports the [STU3](http://hl7.org/fhir/STU3) and [R4]({{site.data.fhir.path}}index.html) versions of the FHIR standard. FHIR services based on STU3 are being moved into production by EHR vendors. R4 is just recently published and the goal is to ensure the implementation guide is aligned with the current direction of the FHIR standard. Initial implementations will focus on STU3.

This implementation guide also builds on the US Core Implementation Guide and implementers need to familiarize themselves with the profiles in those Implementation Guides:

| FHIR Version |
| ------------ |
| [FHIR R4 US Core](http://hl7.org/fhir/us/core/2019Jan/) |
| [FHIR STU3 US Core (1.0.1)](http://hl7.org/fhir/us/core/1.0.1) |

Implementers should also familiarize themselves with the FHIR resources used within the guide:

| STU3 | R4 |
| ---- | -- |
| [Questionnaire](http://hl7.org/fhir/STU3/questionnaire.html) | [Questionnaire](http://hl7.org/fhir/R4/questionnaire.html) |
| [QuestionnaireResponse](http://hl7.org/fhir/STU3/questionnaireresponse.html) |[QuestionnaireResponse](http://hl7.org/fhir/R4/questionnaireresponse.html) |
| [Task](http://hl7.org/fhir/STU3/task.html) | [Task](http://hl7.org/fhir/R4/task.html) |

### US Core
Clinical systems will use the specification and workflows defined by [US Core](http://www.hl7.org/fhir/us/core/) to initiate Document Template and Rule with the payers. Implementers should be familiar with this specification.

### CDS Hooks
Clinical systems will use the specification and workflows defined by [CDS Hooks](https://cds-hooks.hl7.org) to initiate Document Template and Rule functionality with the payers. Implementers should be familiar with this specification.

### CRD
Clinical systems will use the specification and workflows defined by [CRD](http://build.fhir.org/ig/HL7/davinci-crd/) to initiate Document Template and Rule functionality with the payers. Implementers should be familiar with this specification.

### SMART on FHIR
Client systems conformant to this implementation guide SHALL also serve as a SMART on FHIR client. This is to allow Document Template and Rule functionality to be invoked outside of regular clinical workflows using a SMART on FHIR application to provide a consistent way of edvaluating "what if?" scenarios across EHR implementations. As such client implementers will also need to be familiar with the [SMART on FHIR](http://hl7.org/fhir/smart-app-launch) specification.  Because the SMART on FHIR app will interact with payer systems through the CDS Hooks interface, payer implementers only need to be familiar with the SMART on FHIR specification if they plan to develop SMART apps for launch by CDS Hooks or for other purposes.

### SDC
Clinical systems will use the specification and workflows defined by [SDC](http://hl7.org/fhir/us/sdc/) to initiate Document Template and Rule functionality with the payers. Implementers should be familiar with this specification.

### CQL
Clinical systems will use the specification and workflows defined by [CQL](https://cql.hl7.org/STU2/) to initiate Document Template and Rule functionality with the payers. Implementers should be familiar with this specification.