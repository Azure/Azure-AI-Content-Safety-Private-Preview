# Code of conduct for Azure Content Safety  Service

The following Code of Conduct defines the requirements that all Azure Content Safety implementations must adhere to in good faith. This code of conduct is in addition to the Acceptable Use Policy in the [Microsoft Online Services Terms](https://www.microsoft.com/licensing/product-licensing/products).



## Access requirements

Azure Content Safety is a Limited Access service that requires registration and is only available to approved enterprise customers and partners. Customers who wish to use this service are required to [register through this form](https://forms.office.com/pages/responsepage.aspx?id=v4j5cvGGr0GRqy180BHbRw9O1shxIo9Ko5hvbIP4oP9UMzZQWTVSTDZEMlpFMDlLNldCT08zOVhKSy4u). 



## Responsible AI mitigation requirements

Integrations with Azure Content Safety must:

- Implement meaningful human oversight
- Implement strong technical limits on inputs and outputs to reduce the likelihood of misuse beyond the application's intended purpose
- Test applications thoroughly to find and mitigate undesirable behaviors
- Establish feedback channels
- Implement additional scenario-specific mitigations

To learn more, see the [Azure Content Safety transparency note](https://learn.microsoft.com/en-us/legal/cognitive-services/Azure Content Safety/transparency-note?context=/azure/cognitive-services/Azure Content Safety/context/context).



## Integrations with Azure Content Safety must not:

- be used in any way that violates Microsoft’s [Acceptable Use Policy](https://www.microsoft.com/licensing/terms/product/ForOnlineServices/all), including but not limited to any use prohibited by law, regulation, government order, or decree, or any use that violates the rights of others;
- be used in any way that is inconsistent with this code of conduct, including the Limited Access requirements, the Responsible AI mitigation requirements, and the Content requirements;
- exceed the use case(s) you identified to Microsoft in connection with your request to use the service;
- interact with individuals under the age of consent in any way that could result in exploitation or manipulation or is otherwise prohibited by law or regulation;
- generate or interact with content prohibited in this Code of Conduct;
- be presented alongside or monetize content prohibited in this Code of Conduct;
- make decisions without appropriate human oversight if your application may have a consequential impact on any individual’s legal position, financial position, life opportunities, employment opportunities, human rights, or result in physical or psychological injury to an individual;
- infer sensitive information about people without their explicit consent unless if used in a lawful manner by a law enforcement entity, court, or government official subject to judicial oversight in a jurisdiction that maintains a fair and independent judiciary; or
- be used for chatbots that **(i)** are erotic, romantic, or used for companionship purposes, or which are otherwise prohibited by this Code of Conduct; **(ii)** are personas of specific people without their explicit consent; **(iii)** claim to have special wisdom/insight/knowledge, unless very clearly labeled as being for entertainment purposes only; or **(iv)** enable end users to create their own chatbots without oversight.



## Report abuse

If you suspect that Azure Content Safety is being used in a manner that is abusive or illegal, infringes on your rights or the rights of other people, or violates these policies, you can report it with this [email](acm-team@microsoft.com).



## Report problematic content

If Azure Content Safety outputs problematic content that you believe should have been filtered, report it with this [email](acm-team@microsoft.com).





# Data, privacy, and security for Azure Content Safety

This article provides details regarding how data provided by you to the Azure Content Safety is processed, used, and stored. Azure Content Safety stores and processes data to provide the service and to monitor for uses that violate the applicable product terms. Please also see the [Microsoft Products and Services Data Protection Addendum](https://aka.ms/DPA), which governs data processing by the Azure Content Safety except as otherwise provided in the applicable [Product Terms](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftAzure/MCA#ServiceSpecificTerms).

Azure Content Safety was designed with compliance, privacy, and security in mind; however, the customer is responsible for its use and the implementation of this technology.



## How is data retained and what Customer controls are available?

The Azure Content Safety works to filter potentially harmful content. This system works by running the input through an ensemble of classification models . Once a customer's Azure Content Safety resource was created, the customer can submit texts and images to the model through the REST API, client libraries, or the Azure Content Safety Studio; the model generates outputs that are returned through the API.

Apart from blockitems, no input texts or images are stored in the model during these process, and user inputs are not used to train, retrain or improve the models.

- **Blocklist data**. The Blocklist API allows customers to upload their blockitems for the purpose of having a complimentary of the Azure Content Safety model. **This data is stored in Azure Storage, encrypted at rest by Microsoft Managed keys, within the same region as the resource and logically isolated with their Azure subscription and API Credentials**. Uploaded items can be deleted by the user via the DELETE API operation.

To learn more about Microsoft's privacy and security commitments visit the [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

### Is customer data processed by Azure Content Safety sent to Azure other service?

No. Microsoft hosts the Azure Content Safety models within our Azure infrastructure, and all customer data sent to Azure Content Safety remains within the Azure Content Safety.

### Is customer data used to train the Azure Content Safety models?

No. We do not use customer data to train, retrain or improve the models in the Azure Content Safety.
