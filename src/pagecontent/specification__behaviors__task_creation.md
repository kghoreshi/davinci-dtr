Through interactions with the DTR application, a user may be prompted with a question that leads to the discovery of a needed action for the desired treatment to proceed. For example, a healthcare provider may be preparing an order for a Continuous Positive Airway Pressure (CPAP) device. In this example, the payer requires that the provider conduct a sleep study that shows a diagnosis of obstructive sleep apnea. While using the DTR application, it prompts the provider that it was unable to find a sleep study in the EHR system for the patient. The provider realizes that the sleep study has not yet been conducted and would like to generate a task for office staff to schedule a sleep study.

To facilitate this, the DTR application should allow users to create tasks. The details of the task should be represented by a FHIR Task resource. The DTR application should communicate the task information to the EHR system using the FHIR create interaction.

The DTR application should attempt to prepopulate as much of the Task resource as it can based on the context of the application. `Task.description` may draw from the text available in the currently active `Questionnaire.item.text`.

> Note to ballot comments
>
> This is an area the project is explicitly seeking comments on. Thoughts on the ability
> of EHR systems to accept Task resources as well as feedback on the constraints that
> should be placed on the task resource are welcome.