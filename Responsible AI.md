# 1. What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft’s Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system. 

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

# The basics of Azure Content Safety

## Introduction

Azure Content Safety is a part of Azure Cognitive Services that detects material that is potentially offensive, risky, or otherwise undesirable. Azure Content Safety works on new functionalities that offer state-of-the-art text, image, and multimodal APIs and Interactive Studio that detects problematic content. Azure Content Safety helps make applications and services safer by redacting harmful user-generated and AI-generated content.

## Key terms

**Content categories** 

| **Category** | **Description**                                              |
| ------------ | ------------------------------------------------------------ |
| Hate         | *Hate* refers to any content  that attacks or uses pejorative or discriminatory language with reference to  a person or identity group on the basis of certain differentiating attributes   including but not limited to race,  ethnicity, nationality, gender identity and expression, sexual orientation,  religion, immigration status, ability status, personal appearance, and body  size. |
| Sexual       | *Sexual* describes language that is related to anatomical  organs and genitals; romantic relationships; acts portrayed in erotic or  affectionate terms; pregnancy; physical sexual acts, including those  portrayed as an assault or as a forced sexual, violent act against one’s will;  prostitution; pornography; and abuse. |
| Violence     | *Violence*  describes language that is related to physical actions that are intended to  hurt, injure, damage, or kill someone or something; or describes weapons,  guns, and related entities, such as manufacturers, associations, or  legislation. |
| Self-Harm    | *Self-harm* describes language that is related to physical  actions that are intended to purposely hurt, injure, or damage one’s body or to  kill oneself. |

 **Severity levels**  

Every content flag the service applies also comes  with a risk level rating. The risk level is meant to indicate the severity of  the consequences of showing the flagged content.

| Severity | Label  |
| -------- | ------ |
| 0        | Safe   |
| 2        | Low    |
| 4        | Medium |
| 6        | High   |

 



 

# Capabilities

## System behavior

Different types of analysis are available in Azure Content Safety: 

| **Type**                     | **Functionality**                                            |
| ---------------------------- | ------------------------------------------------------------ |
| Text Detection API           | Scans text for hate, sexual, violence, and self-harm  content, with multi-severity risk levels. |
| Image Detection  API         | Scans images  for hate, sexual, violence, and self-harm content, with multi-severity risk  levels. |
| Multimodal Detection API     | Scans both images and text (including separate text  or text from OCR from an image) for hate content, with multi-severity risk  levels. |
| Azure Content  Safety Studio | Azure Content Safety  Studio is an online tool that you can use to visually explore, understand, and  evaluate the Azure Content Safety service. The studio provides a platform for  you to experiment with the different Azure Content Safety classifications and  to interactively sample returned data without writing any code. |

 

## Use cases

### Intended uses cases

Azure Content Safety can be used in multiple scenarios. The system’s intended uses include:

·    **Social media platforms:** Content safety systems are commonly used by social media customers to prevent the spread of harmful and inappropriate content, such as hate speech, cyberbullying, and pornography.

·    **E-commerce websites:** E-commerce customers use Azure Content Safety content safety systems to screen product listings and reviews for inappropriate content, such as fake reviews and offensive language.

·    **Gaming platforms:** Gaming platforms use content safety systems to detect cheating, hacking, and other forms of misconduct, as well as to prevent inappropriate behavior in chats and forums.

·    **News websites:** Content safety systems are used by news websites to ensure that user comments remain civil and respectful, and to prevent the spread of fake news and hate speech.

·    **Video-sharing platforms**: Video-sharing platforms use content safety systems to detect and remove inappropriate content, such as violence, hate speech, and pornography.

 

### Considerations when choosing other use cases

We encourage customers to leverage Azure Content Safety in their innovative solutions or applications. However, here are some considerations when choosing a use case: 

- **Compliance:**     Depending on the nature of your     application or solution, you might need to comply with certain regulations     or standards that are related to content safety, including the Children's     Online Privacy Protection Act (COPPA) or the General Data Protection Regulation (GDPR). 
- **Customization:**     Different applications and solutions might     have different requirements when it comes to content safety. It's     important to choose a solution that can be customized to meet your     specific needs and that can integrate with your existing workflows and processes. Azure Content Safety may allow you to set the match severity level for detection, help you mitigate some risks, however, we have the  limitation for customization.
- **Transparency:**   Some of your users might want to     understand how your application or solution moderates content. When you     choose to use Azure Content Safety, it's important to ensure that the     service provides transparency and clear communication with your users  about how content is moderated and why certain content might be flagged or  removed.

Unsupported uses

- **Illegal activities**: Azure Content Safety should not be used to support or facilitate illegal activities, such as the distribution of child pornography or the promotion of hate speech.

# Limitations

## Technical limitations, operational factors, and ranges

Technical limitations: Content safety systems have some technical limitations that can affect their effectiveness. Some of these limitations are:

**Accuracy:** Our systems are not always 100% accurate, and there is a risk of false positives or false negatives. When you choose to use Azure Content Safety, it's important to evaluate its accuracy and to ensure that it meets your specific needs.

**Language barriers:** Content safety systems might not be able to detect inappropriate content in languages that they are not programmed to understand.

**Image recognition:** Content safety systems might not be able to detect inappropriate content in images that are not clear or that have been edited.

**Evolving nature of content:** Content safety systems might struggle to keep up with the evolving nature of online content and as new types of inappropriate content emerge.

Operational factors:

Content safety systems also have some operational factors that need to be considered for their effectiveness. Some of these factors are:

**Volume of content:** Content safety systems might struggle to handle large volumes of content. This can lead to delays in detecting inappropriate content.

**Time sensitivity:** Some types of inappropriate content require immediate action. Content safety systems might be unable to identify these types of content quickly and alert moderators.

**Contextual analysis:** Content safety systems might be unable to analyze content in context to determine whether it is inappropriate. For example, certain words might be appropriate in some contexts but not in others.

Ranges for content safety systems:

Content safety systems can cover a range of content. For example:

**Text-based content:** This includes social media posts, comments, and messages.

**Image-based content:** This includes photos and videos.

# System performance

In this section, we'll review what performance means for Azure Content Safety, best practices for improving performance, limitations as it relates to the Azure Content Safety feature.

**General performance guidelines**

Because Azure Content Safety serves various uses, there's no universally applicable estimate of accuracy for every system. The performance of Azure Content Safety is therefore affected by these other components.

**Accuracy**

The consequences of a false positive or a false negative will vary depending upon the intended use of the Azure Content Safety system. The following examples illustrate this variation and the how choices you make in designing the system affect the people who are subject to it. The design of the whole system, including fallback mechanisms, determines the consequences for people when errors occur.

**Severity levels, match match severity levels, and matched conditions**

System configuration influences system accuracy. By comparing the model output severity levels and uses a match severity levels to decide whether to accept or reject the input as a match. It's important to understand the trade-off between the rates of false positives and false negatives. The table below gives more details description.

| **Term**                                            | **Definition**                                               |
| --------------------------------------------------- | ------------------------------------------------------------ |
| Severity levels                                     | The higher the severity of input content, the larger  this value is. The values could be: 0,2,4,6. |
| Match Severity Levels(Only Studio has this feature) | Match severity is a configurable value that  determines the match severity level required to be considered a positive  match. If the match match severity level is set to 0, then the system will  accept any match severity levels and the false accept rate would be high; if  the match match severity level is set to 6, then it will only accept an input  with a 6 (100%) match severity level and the false reject rate would be high.  Studio has a default match match severity level that you can change to suit  your application. |

Because the match severity levels vary highly with use cases or scenarios, the Speaker Verification API decides whether to accept or reject based on a default severity levels of 2. Adjust the match severity levels for each scenario and validate the results by testing your data.

| **Error Type**  | **Definition**                                               | **Example**                                                  |
| --------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| True  Positive  | The model  correctly identifies inappropriate content.       | When the  real harmful content such as “you are an idiot” access as Hate, the system  returns a severity level of 2. The system correctly rejects the harmful  content. |
| False  Positive | The model  incorrectly identifies appropriate content as inappropriate. | When a  not harmful content such as “you are a good person”, the system returns 6,  The system incorrectly block the content. |
| True  Negative  | The model  correctly identifies appropriate content.         | When a  not harmful content such as “you are a good person”, the system returns 0,  The system correctly accept the content. |
| False  Negative | The model  fails to identify inappropriate content.          | When a  harmful content such as “you are an idiot”, the system returns a level of 0.  The system incorrectly accepts the content. |

With your evaluation results, you can adjust the match severity levels to better suit the scenario(Only Azure Content Safety Studio has this feature). For example, because the gaming industry for child plans usually prefers high content safety, you might set the match severity level higher than the default match severity level to reduce false accept errors. By contrast, because the adult plan might prefer lower safety, you might set the match severity level lower than the default to reduce the false reject errors. Based on each evaluation result, you can iteratively adjust the match severity level until the trade-off between false positives and false negatives meets your objectives.

**Best practices to improve accuracy**

Here are some specific actions you can take to ensure the best results. 

**Meet specifications**

The following specifications are important to be aware of:

- **Text and image format:** The current system only supports limited     format.
- **Maximum length of text:** In Azure Content Safety API, the text input     is 1000 characters. The fewer characters, the more accurate the result     will be. 

**Design the system to support human judgment**

We recommend using Azure Content Safety to support people making accurate and efficient judgments, rather than fully automating a process. Meaningful human review is important to:

- Detect and resolve     cases of misidentification or other failures.
- Provide support to     people who believe their results were incorrect.

For example, in gaming scenarios, a legitimate content can be rejected due to having a false postive. In this case, a human agent can intervene and help the customer verify the rusults.

 

## Best practices for improving system performance 

Do:

·    Monitor the system's performance regularly to ensure that the tradeoff is appropriate for the use case. For example, tradeoff for precision and recall.

·    Adjust the risk levels for blocking based on user feedback and observed trends in content safety.

·    Consider the impact of the system's performance on different user populations and adjust accordingly. For example, in gaming industry, the adult plan and the family plan for content safety may different.

·    Take steps to mitigate any unintended consequences of adjusting the risk levels for blocking, such as over-removal of content or the spread of harmful content.

Don't:

·    Set the risk levels for blocking too high, which might lead to a large number of false positives, which can negatively affect user experience.

·    Set the risk levels for blocking too low, which might lead to a large number of false negatives, which can harm users and communities.

·    Ignore feedback from users and communities about the system's performance.

·    Over-rely on the system's automated decision-making capabilities without ensuring appropriate human oversight and intervention.

# Evaluation of Azure Content Safety

## Evaluation methods

The methods that are used to evaluate a system for content safety considerations typically involve analyzing large datasets of harmful content and evaluating the system's ability to accurately identify and flag potentially harmful or inappropriate content.

It’s important to evaluate how the system performs across different demographic and geographic areas. The groups of people that are included in the evaluation depend on the type of content that is being evaluated and the intended audience of the system. For example, if the system is designed to monitor social media posts, the dataset might include a diverse range of users from various geographic locations, backgrounds, and age groups. However, if the system is designed for use in a specific industry or niche market, the dataset might be limited to users who are in that specific group.

The evaluation itself might involve a combination of automated testing and manual review by content safety experts to ensure that the system is effectively identifying potentially harmful or inappropriate content. The results of the evaluation are then used to improve the system and to optimize its performance for real-world use.

# Evaluating and integrating Azure Content Safety for your use

Before a large-scale deployment or rollout of any Azure Content Safety, system owners should conduct an evaluation phase. Do this evaluation in the context where you'll use the system, and with people who will interact with the system. 

·    Work with your analytics and research teams to collect ground truth evaluation data.

·    Establish baseline accuracy, false positive and false negative rates.

·    Choose an appropriate match severity level for your scenario.

·    Determine whether the error distribution is skewed towards specific groups of data or categories..

·    Evaluation is likely to be an iterative process. For example, you can start with 50 rows or images for each category. 

·    In addition to analyzing accuracy data, you can also analyze feedback from the people making judgments based on the system output. 

# Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/en-us/ai/responsible-ai)

[Microsoft responsible AI resources](https://www.microsoft.com/en-us/ai/responsible-ai-resources)

[Microsoft Azure Learning courses on responsible AI](https://docs.microsoft.com/en-us/learn/paths/responsible-ai-business-principles/)

# Learn more about Azure Content Safety

<Insert links here to relevant resources for learning more about the product or feature including contracts (OST/trust center), marketing materials, and technical documentation.>

# About this document

© <year> Microsoft Corporation. All rights reserved. This document is provided "as-is" and for informational purposes only. Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred.

Published: 04/04/2023

Last updated: 04/04/2023



# 2. Code of conduct for Azure Content Safety  Service

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





# 3. Data, privacy, and security for Azure Content Safety

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

