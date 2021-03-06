Users of the DTR application are likely to be performing many tasks to support patient care or administration of the provider organization. As such, it should be expected that users may need to halt interaction with the DTR application and resume at a later time.

The DTR application should anticipate that users may not be able to complete a full interaction between launch from a CDS Hooks Card to providing a response back to the payer. It is recommended that DTR conformant SMART on FHIR applications preserve state automatically as a user interacts with it. In this manner, the user does not need to explicitly take action to save their state.

Exact mechanisms for saving state are outside the scope of this implementation guide. The following sections describe mechanisms that a DTR application may use to establish the data necessary to store and retrieve state.

### SMART on FHIR applications and Servers
SMART on FHIR applications must be launched by a host that is accessible to the launching EHR. Once launched, a SMART on FHIR application may communicate with the host that it was initially launched from. This may be to retrieve data to assist in the functionality of the SMART on FHIR application, or it may be to record actions taken by the application user.

In the case of DTR, the SMART on FHIR application may be launched from a number of locations. A likely scenario is that the DTR conformant SMART on FHIR application will be hosted by a Payer IT system.

The DTR application may send information back to the host it was launched from to save application state. As mentioned in the previous section, the services and formats used to communicate state information are outside the scope of this implementation guide.

### Requesting User Identity
To persist application state, the DTR application will need to know who is currently using the application. SMART on FHIR provides methods for the application to obtain this information.

#### SMART on FHIR App Launch Framework IG
Using the SMART on FHIR App Launch Framework IG, the DTR application should request [scopes for requesting identity data](http://hl7.org/fhir/smart-app-launch/scopes-and-launch-context/index.html#scopes-for-requesting-identity-data), namely `openid` and `fhirUser`. The DTR application can then retrieve the FHIR resource representing the current person and extract whatever identifiers it deems necessary for the persistance of application state.

### Usage Sessions
The DTR application is initially launched in response to a Coverage Requirements Discovery request. This request is for a given set of orders for a particular patient.

The DTR application usage session binds this set of orders and patient to a particular user. When persisting application state, it is the responsibility of the DTR application to record the relationship between the orders, patient and user.

The DTR application application may be launched outside the context of a CRD request, at which point, it must be able to restore a usage session. This will be covered in detail in Section 4.4.8 - Launch outside of CRD

#### Visibility of Usage Sessions to Other Users
Depending on workflows within an organization, it may be desirable for one user to start a usage session, but for it to be completed by another user. Rules for which users of a DTR application should be authorized to see information on a particular set of patients are outside the scope of this implementation guide.

The SMART on FHIR App Launch Framework IG and FHIR specification provide methods for discovering information about the user and how that user fits into the provider organization. With this information, the DTR application, possibly consulting with the Payer IT system, can decide which usage sessions to expose to a given user.

As an example, the DTR application may retrieve a Practitioner resource by retrieving the URL supplied in the `fhirUser` claim. The DTR application may then query the CareTeam or PractitionerRole resources to determine their relationship to other staff in the provider organization and determine if their usage sessions should also be made available.

### Session Expiration
While a user may need to suspend interaction with the DTR application, there may be a limit on the amount of time that a set of documentation templates and rules is valid. For example, it is unreasonable to resume the DTR application for an order that was started five years in the past.

Payers SHOULD use the `Questionnaire.effectivePeriod` element to describe the period over which the documentation templates and rules are valid. This element is available in the FHIR STU3 and well as the FHIR R4 versions of the Questionnaire resource. The DTR application SHALL NOT allow completion of a usage session if the current time has exceeded the end of the `effectivePeriod`.