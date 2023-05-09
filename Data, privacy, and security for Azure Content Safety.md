# Data, privacy, and security for Azure Content Safety

This article provides details regarding how data provided by you to the Azure Content Safety is processed, used, and stored. Azure Content Safety stores and processes data to provide the service and to monitor for uses that violate the applicable product terms. Please also see the [Microsoft Products and Services Data Protection Addendum](https://aka.ms/DPA), which governs data processing by the Azure Content Safety except as otherwise provided in the applicable [Product Terms](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftAzure/MCA#ServiceSpecificTerms).
Azure Content Safety was designed with privacy, and security in mind; however, the customer is responsible for its use and the implementation of this technology.



## How is data retained and what Customer controls are available?

The Azure Content Safety works to filter potentially harmful content. This system works by running the input through an ensemble of classification models . Once a customer's Azure Content Safety resource was created, the customer can submit texts and images to the model through the REST API, client libraries, or the Azure Content Safety Studio; the model generates outputs that are returned through the API.

Apart from blockitems, no input texts or images are stored in the model during these process, and user inputs are not used to train, retrain or improve the models.

- **Blocklist data**. The Blocklist API allows customers to upload their blockitems for the purpose of having a complimentary of the Azure Content Safety model. **This data is stored in Azure Storage, encrypted at rest by Microsoft Managed keys, within the same region as the resource and logically isolated with their Azure subscription and API Credentials**. Uploaded items can be deleted by the user via the DELETE API operation.

To learn more about Microsoft's privacy and security commitments visit the [Microsoft Trust Center](https://www.microsoft.com/TrustCenter/CloudServices/Azure/default.aspx).

### Is customer data processed by Azure Content Safety sent to Azure other service?

No. Microsoft hosts the Azure Content Safety models within our Azure infrastructure, and all customer data sent to Azure Content Safety remains within the Azure Content Safety.

### Is customer data used to train the Azure Content Safety models?

No. We do not use customer data to train, retrain or improve the models in the Azure Content Safety.

