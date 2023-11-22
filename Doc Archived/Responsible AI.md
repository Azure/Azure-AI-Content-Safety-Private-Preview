# What is a Transparency Note?

An AI system includes not only the technology, but also the people who will use it, the people who will be affected by it, and the environment in which it is deployed. Creating a system that is fit for its intended purpose requires an understanding of how the technology works, what its capabilities and limitations are, and how to achieve the best performance. Microsoft’s Transparency Notes are intended to help you understand how our AI technology works, the choices system owners can make that influence system performance and behavior, and the importance of thinking about the whole system, including the technology, the people, and the environment. You can use Transparency Notes when developing or deploying your own system, or share them with the people who will use or be affected by your system. 

Microsoft’s Transparency Notes are part of a broader effort at Microsoft to put our AI Principles into practice. To find out more, see the [Microsoft AI principles](https://www.microsoft.com/ai/responsible-ai).

# The basics of Azure Content Safety

## Introduction

Azure Content Safety detects harmful user-generated and AI-generated content in applications and services. Azure Content Safety includes text, image, and multimodal APIs which allows you to detect material that is potentially offensive, risky, or otherwise undesirable. We also have an Interactive Studio that allows you to view, explore and try out for detecting harmful content across different modalities. 

## Key terms

**Content categories** 

The categories below describe the types of content which Azure Content Safety detects. 

 

| **Category** | **Description**                                              |
| ------------ | ------------------------------------------------------------ |
| Hate         | The hate category describes language attacks or  uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of  certain differentiating attributes of these groups including but not limited  to race, ethnicity, nationality, gender identity and expression, sexual  orientation, religion, immigration status, ability status, personal  appearance and body size. |
| Sexual       | The sexual category describes  language related to anatomical organs and genitals, romantic relationships, acts  portrayed in erotic or affectionate terms, pregnancy, physical sexual acts,  including those portrayed as an assault or a forced sexual violent act  against one’s will, prostitution, pornography and abuse. |
| Violence     | The violence category describes language related to  physical actions intended to hurt, injure, damage, or kill someone or  something; describes weapons, guns and related entities, such as manufacturing  weapons, associations, legislation, etc. |
| Self-Harm    | The self-harm category describes  language related to physical actions intended to purposely hurt, injure,  damage one’s body or kill oneself. |

 

**Severity levels**

Content flags applied by the service have a severity level rating, which indicate the potential severity of displaying the flagged content.

| Severity Level 0 – Safe    | Content may be related to violence, self-harm, sexual or hate &  fairness categories but the terms are used in general, journalistic,  scientific, medical and similar professional contexts which are appropriate  for most audiences. |
| -------------------------- | ------------------------------------------------------------ |
| Severity Level 2 – Low     | Content that expresses  prejudiced, judgmental or opinionated views, includes offensive use of  language, stereotyping, use cases exploring a fictional world (e.g., gaming,  literature) and depictions at low intensity. |
| Severity Level 4 –  Medium | Content that uses offensive, insulting, mocking,  intimidating, or demeaning language towards specific identity groups,  includes depictions on seeking and executing harmful instructions, fantasies,  glorification, promotion of harm at medium intensity. |
| Severity Level 6 – High    | Content that displays explicit and severe harmful  instructions, actions, damage and abuse, includes endorsement, glorification,  promotion of severe harmful acts, extreme or illegal forms of harm,  radicalization, and non-consensual power exchange or abuse. |

 

 

# Capabilities

## System behavior

Content safety service uses artificial intelligence to analyse user-generated and AI-generated content and flag any inappropriate content such as hate speech, sexual, violent and self-harm activities. Clear and understandable explanations are provided, allowing users to understand why content was flagged or removed.

Different types of analysis are available in Azure Content Safety: 

| **Type**                     | **Functionality**                                            |
| ---------------------------- | ------------------------------------------------------------ |
| Text Detection API           | Scans text for hate, sexual, violence,  and self-harm content, with multi-severity risk levels. |
| Image  Detection API         | Scans  images for hate, sexual, violence, and self-harm content, with multi-severity  risk levels. |
| Multimodal Detection API     | Scans both images and text (including  separate text or text extracted from an image using optical character  recognition) for hate content, with multi-severity risk levels. |
| Azure  Content Safety Studio | Azure  Content Safety Studio is an online tool that customers can use to visually  explore, understand, and evaluate the Azure Content Safety service. The  studio provides a platform for customers to experiment with the different Azure  Content Safety classifications and to interactively sample returned data  without writing any code. |

 

## Use cases

### Intended uses cases

Azure Content Safety can be used in multiple scenarios. The system’s intended uses include:

·    **Social media platforms:** Customers can use Azure Content Safety on their social media platforms  to prevent the spread of harmful and inappropriate content, such as hate speech, cyberbullying, and pornography.

·    **E-commerce websites:** E-commerce customers can use Azure Content Safety to screen product listings and reviews for inappropriate content, such as fake reviews and offensive language.

·    **Gaming platforms:** Gaming platforms can use Azure Content Safety to detect cheating, hacking, and other forms of misconduct, as well as to prevent inappropriate behavior in chats and forums.

·    **News websites:** News websites can use Azure Content Safety to ensure that user comments remain civil and respectful, and to prevent the spread of misinformation and hate speech.

·    **Video-sharing platforms**: Video-sharing platforms can use Azure Content Safety to detect and remove inappropriate content, such as violence, hate speech, and pornography.

 

### Considerations when choosing other use cases

We encourage customers to leverage Azure Content Safety in their innovative solutions or applications. However, here are some considerations when choosing a use case: 

- **Customization:** Different applications and solutions might have different     requirements when it comes to content safety. It’s important to experiment     with the thresholds for Azure Content Safety and set them to meet the     needs of your specific use case.
- **Transparency:** Some end users might want to understand     how your application or solution moderates content. When you choose to use     Azure Content Safety, it’s important to ensure that the service provides     transparency and clear communication with your users about how content is     moderated and why certain content might be flagged or removed.



# Limitations

 

## Technical limitations, operational factors, and ranges

Technical limitations: Azure Content Safety has some technical limitations that can affect performance. Some of these limitations are:

**Accuracy:** Azure Content Safety might not be 100% accurate in detecting inappropriate content. This is because the system relies on algorithms and machine learning, which can have biases and errors.

**Language barriers:** Azure Content Safety might not be able to detect inappropriate content in languages that it has not been trained or tested to process. Currently, Azure Content Safety is available in English, German, Japanese, Spanish, and French, Italian, Portuguese, Chinese.

**Image recognition:** Azure Content Safety might not be able to detect inappropriate content in images that are not clear or that have been edited.

**Evolving nature of content:** Azure Content Safety might not keep up with the evolving nature of online content. As new types of inappropriate content emerge, there may be a delay in Azure Content Safety’s ability to detect these new types of content.

Operational factors:

Azure Content Safety also has some operational factors that need to be considered for its effectiveness. Some of these factors are:

**Volume of content:** Azure Content Safety might struggle to handle large volumes of content. This can lead to delays in detecting inappropriate content.

**Time sensitivity:** Some types of inappropriate content require immediate action. Azure Content Safety might be unable to identify these types of content quickly in order to alert moderators.

**Contextual analysis:** Azure Content Safety might be unable to analyze content in context to determine whether it is inappropriate. For example, certain words might be appropriate in some contexts but not in others.

# System performance

In this section, we'll review what performance means for Azure Content Safety, best practices for improving performance, limitations as it relates to Azure Content Safety.

**General performance guidelines**

Because Azure Content Safety serves various uses, there's no universally applicable estimate of accuracy for every system. The performance of Azure Content Safety is affected by the customer use case and data. In the following sections we describe how to understand accuracy for Azure Content Safety at a high level. 

**Accuracy**

The performance of Azure Content Safety is measured by examining how well the system detects harmful content. For example, one might count the true prevalence of harmful content in some text based on human judgement, and then compare with the output of the system from processing the same text. Comparing human judgement with the system recognized entities would allow you to classify the events into two kinds of correct (or "true") events and two kinds of incorrect (or "false") events. The consequences of a false positive or a false negative will vary depending upon the intended use of the Azure Content Safety system. The following examples illustrate this variation and how you design the system may affect the outputs.

 

| **Error Type** | **Definition**                                               | **Example**                                                  |
| -------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| True Positive  | The model correctly identifies  inappropriate content.       | When harmful content such as  “you are an idiot” is flagged as hate, the system returns a severity level of  2. The system correctly rejects the harmful content. |
| False Positive | The model incorrectly  identifies appropriate content as inappropriate. | When harmless content such as  “you are a good person” is flagged as hate and returns a severity level of 4.  The system incorrectly blocks the content. |
| True Negative  | The model correctly identifies  appropriate content.         | When harmless content such as  “you are a good person”, has a system returns of 0. The system correctly  accepts the content. |
| False Negative | The model fails to identify  inappropriate content.          | When harmful content such as  “you are an idiot”, has a system returns of 0. The system incorrectly accepts  the content. |

 

**Severity levels, match severity levels, and matched conditions**

System configuration influences system accuracy. Azure Content Safety detects harmful content by comparing the model output severity levels for a given input and uses a match severity levels to accept or reject the input as a match. 

| **Term**                                              | **Definition**                                               |
| ----------------------------------------------------- | ------------------------------------------------------------ |
| Severity levels                                       | The higher the severity of  input content, the larger this value is. The values are: 0, 2, 4, or 6. |
| Match Severity Levels (Only  Studio has this feature) | Match severity is a  configurable value that determines the match severity level required to be considered a positive match. If the match severity level is set to 0, then  the system will accept any match severity levels; if the match severity level is set to 6, then it will only  accept inputs with a 6 (100%) match severity level. Studio has a default match severity level that you can change to suit your application. |

Adjust the match severity levels for your particular use case and validate your results by testing with your data. With your evaluation results, you can adjust the match severity levels for your specific use case (Only Azure Content Safety Studio has this feature). For example, games  for children typically have higher content safety requirements than games available for adults only. For children’s games, you might set the match severity level lower than the default match severity level to reduce false negatives. In contrast, for adults the match severity level could be higher than the default to reduce the false positives. Based on each evaluation result, you can iteratively adjust the match severity level until the trade-off between false positives and false negatives matches the needs in your use case.

**Best practices to improve accuracy**

Below are some recommendations to ensure the best results.

**Meet specifications**

The following specifications are important to be aware of:

- **Text and image format:** The current system only supports limited format: image and text.
- **Maximum length of text:** In Azure Content Safety API, the text input limit is 1000 characters per Text API call. The fewer characters, the more accurate the result will be.

**Design the system to support human judgment**

We recommend using Azure Content Safety to support people making accurate and efficient judgments, rather than fully automating a process. Meaningful human review is important to:

- Detect and resolve cases of misidentification or other failures.
- Provide support to people who believe their content was incorrectly flagged.

For example, in gaming scenarios, legitimate content can be rejected due to having a false positive. In this case, a human reviewer can intervene and help the customer verify the results.

## Best practices for improving system performance 
Do:

·    Monitor the system's performance regularly to ensure that the tradeoff is appropriate for your use case.

·    Adjust the risk levels for blocking based on user feedback and observed trends in content safety.

·    Consider the impact of the system's performance on different user populations and adjust accordingly . For example, certain words or images may be considered offensive in one culture but not in another, and the system should be trained to detect this and adjust its risk levels accordingly.

·    Take steps to mitigate any unintended consequences of adjusting the risk levels for blocking, such as over-removal of content or the spread of harmful content.

Don't:

·    Set the risk levels too high: If the risk levels for blocking are set too high, the system might flag a lot of content as hate speech even if it is not, leading to a large number of false positives. This can negatively affect user experience by making it difficult for users to post legitimate content without being flagged.

·    Setting the risk levels too low: Conversely, if the risk levels for blocking are set too low, the content safety system might not flag content as potentially harmful, leading to false negatives. This can harm users and communities by allowing inappropriate content to be disseminated.

·    Ignoring feedback from users and communities: Content safety systems are designed to serve the needs of users and communities, and it is important to listen to their feedback about the system's performance. For example, if users are consistently reporting false positives or false negatives, the system should be adjusted accordingly.

·    Over-relying on automated decision-making: Content safety systems often rely on automated decision-making to flag inappropriate content, but it is important to ensure appropriate human oversight and intervention to avoid errors and biases. For example, if the system flags a piece of content as inappropriate, a human moderator should review the decision to ensure that it is accurate and fair.

# Evaluation of Azure Content Safety

## Evaluation methods

The methods used to evaluate a system for content safety considerations typically involve analyzing large datasets of harmful content and evaluating the system's ability to accurately identify and flag potentially harmful or inappropriate content.

It’s important to evaluate how the system performs across different demographic and geographic areas. The groups of people that are included in the evaluation depend on the type of content that is being evaluated and the intended audience of the system. For example, if the system is designed to monitor social media posts, the dataset might include a diverse range of users from various geographic locations, backgrounds, and age groups. However, if the system is designed for use in a specific industry or niche market, the dataset might be limited to users who are in that specific group.

The evaluation itself might involve a combination of automated testing and manual review by content safety experts to ensure that the system is effectively identifying potentially harmful or inappropriate content. The results of the evaluation are then used to improve the system and to optimize its performance for real-world use.

## Evaluation results

Before a large-scale deployment or rollout of any Azure Content Safety, system owners should conduct an evaluation phase. This evaluation should be conducted in the context where you'll use the system, and with people who will interact with the system. Some best practices for evaluating Azure Content Safety include:

·    Work with your analytics and research teams to collect ground truth evaluation data.

·    Establish baseline accuracy, false positive and false negative rates.

·    Choose an appropriate match severity level for your use case.

·    Determine whether the error distribution is skewed towards specific groups of data or categories.

·    Evaluation is likely to be an iterative process. For example , you can start with 50 rows or images for each category.

·    In addition to analyzing accuracy data, you can also analyze feedback from the people making judgments based on the system output.

# Evaluating and integrating Azure Content Safety for your use

·    **Appropriate human oversight for the system is critical to ensure that it is being used effectively and responsibly.** This includes ensuring that the people who are responsible for oversight understand the system's intended uses, how to interact with the system effectively, how to interpret system behavior, and when and how to intervene in or override the system. Considerations such as UX and UI design and the use of risk levels can inform human oversight strategies and help prevent over-reliance on system outputs. For example, for a product like a content safety system, it is important to provide content moderators with the training and resources that they need to effectively oversee the system. This might involve providing access to training materials and documentation, as well as ongoing support from content safety experts. 

·    **Establish feedback channels for users and affected groups.**  AI-powered products and features require ongoing monitoring and improvement. Establish channels to collect questions and concerns from users as well as from people who are affected by the system. For example, build feedback features into the user experience. Invite feedback on the usefulness and accuracy of outputs, and give users a separate and clear path to report outputs that are problematic, offensive, biased, or otherwise inappropriate.

# Learn more about responsible AI

[Microsoft AI principles](https://www.microsoft.com/en-us/ai/responsible-ai)

[Microsoft responsible AI resources](https://www.microsoft.com/en-us/ai/responsible-ai-resources)

[Microsoft Azure Learning courses on responsible AI](https://docs.microsoft.com/en-us/learn/paths/responsible-ai-business-principles/)


# About this document

© <year> Microsoft Corporation. All rights reserved. This document is provided "as-is" and for informational purposes only. Information and views expressed in this document, including URL and other Internet Web site references, may change without notice. You bear the risk of using it. Some examples are for illustration only and are fictitious. No real association is intended or inferred.

Published: 05/05/2023

Last updated: 05/05/2023


