#  Content Moderator Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 	
Welcome to Azure Content Moderator service! 

The Content Moderator service is powered by Microsoft artificial intelligence and runs on Azure. The service can scan text and images for potentially risky, offensive, or undesirable aspects. Having a large amount of content to moderate can be time consuming. Using a service, such as Azure Content Moderator, you can automate much of this process and set up the need for human review as appropriate.

##  📒 Overview 

This documentation contains the following article types:

- **How the content moderator works** contain instructions for using the service in more general ways.

- **Concepts** provide in-depth explanations of the service categories.

- **QuickStart** are getting-started instructions to guide you through making requests to the service.

  

##  🔎How Content Moderator works

Using the Content Moderator service requires an Azure subscription and a Content Moderator resource. The Content Moderator service can be accessed through REST. 

- ### The APIs

There are different types of APIs available in Content Moderator. The following table describes **the current available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Moderation | Scans text for sexual, violence, profanity, hate speech, self harm and personal data. |

- ### Language availability

The API is only available to use in English. The team is constantly developing models to support new languages.



##  🗃Concepts

### Text category

This feature of the API provide scores for several different categories. Here are some of the categories our API can provide scores for:

- **Category 1:** **Sexual** - Sexual describes language related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography and Child Sexual Abuse Material (CSAM).

- **Category 2:** **Violence** - Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 

- **Category 3:** **Hate Speech** - Hate speech is defined as any speech that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.

- **Category 4:** **Profanity** - Profanity is defined as any socially offensive use of language, which may also be called cursing, cussing, swearing, obscenities or expletives. It can show a debasement of someone or something or be considered an expression of strong feelings towards something. 

- **Category 5:** **Self-harm**- Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.

- **Category 6:** **Personally identifiable information(PII)** - Personally identifiable information (PII) detects if any values in the text might be considered PII before you release it publicly. Key aspects that are detected include:

  - Email addresses

  - US mailing addresses

  - IP addresses

  - US phone numbers

  - UK phone numbers

  - Social Security numbers
  
    

## 💡 QuickStart - Text moderation by using the API 

Before you can begin to test content moderation or integrate it into your custom applications, you need to create and subscribe to a Content Moderator resource and get the subscription key for accessing the resource.

### 1. Create and subscribe to a Content Moderator resource

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. In the left pane, select **Create a resource**.
3. In the search box, enter **Content Moderator**, and then press Enter.
4. From the search results, select **Content Moderator**.
5. Select **Create**.
6. Enter a unique name for your resource, select a subscription, and select a location close to you.
7. Select the pricing tier for this resource.
8. Create a new resource group.
9. Select **Create**.

The resource will take a few minutes to deploy. After it does, go to the new resource.

To access your Content Moderator resource, you'll need a subscription key:

1. In the left pane, under **Resource Management**, select **Keys and Endpoints**.
2. Copy one of the subscription key values for later use.

### 2. Sample Requests

Now that you have a resource available in Azure for content moderation, and you have a subscription key for that resource, let's run some tests by using the API.

You can test the API with cURL:

```json
curl -X POST "https://cm-vnext-ppe-lixiang.ppe.cognitiveservices.azure.com/contentmoderator/moderate/Text/Detect?api-version=2022-09-30-preview"
-H "Ocp-Apim-Subscription-Key: {subscription key}"
-H "Content-Type: application/json" 
-d "{ "text": "Is this a crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052" }"
```

1. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.
2. Change the body of the request to whatever string of text you'd like to analyze.

> ### 🚧NOTE:
>
> The default maximum length for text submissions is 10K characters. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions.

### 3. Evaluate the response

You should see the text moderation results displayed as JSON data. For example:

```json
{
    "value": [
        {
            "category": "Sexual",
            "isHitted": false,
            "score": 5.1635565E-5,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "Violence",
            "isHitted": false,
            "score": 0.0012748118,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "HateSpeech",
            "isHitted": false,
            "score": 0.11488042,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "Profanity",
            "isHitted": false,
            "score": 0.0,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "SelfHarm",
            "isHitted": false,
            "score": 0.002663622,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "PII",
            "isHitted": true,
            "score": 1.0,
            "modelOutputDetail": null,
            "diagnoses": [
                {
                    "start": 21,
                    "end": 36,
                    "isHitted": true,
                    "score": 1.0,
                    "diagnosisDetail": {
                        "entity_type": "EMAIL_ADDRESS"
                    }
                },
                {
                    "start": 61,
                    "end": 76,
                    "isHitted": true,
                    "score": 0.95,
                    "diagnosisDetail": {
                        "entity_type": "IP_ADDRESS"
                    }
                },
                {
                    "start": 45,
                    "end": 55,
                    "isHitted": true,
                    "score": 1.0,
                    "diagnosisDetail": {
                        "entity_type": "AU_MEDICARE"
                    }
                },
                {
                    "start": 45,
                    "end": 55,
                    "isHitted": false,
                    "score": 0.05,
                    "diagnosisDetail": {
                        "entity_type": "US_BANK_NUMBER"
                    }
                },
                {
                    "start": 95,
                    "end": 102,
                    "isHitted": true,
                    "score": 0.85,
                    "diagnosisDetail": {
                        "entity_type": "LOCATION"
                    }
                },
                {
                    "start": 45,
                    "end": 55,
                    "isHitted": false,
                    "score": 0.01,
                    "diagnosisDetail": {
                        "entity_type": "US_DRIVER_LICENSE"
                    }
                },
                {
                    "start": 45,
                    "end": 55,
                    "isHitted": true,
                    "score": 0.75,
                    "diagnosisDetail": {
                        "entity_type": "PHONE_NUMBER"
                    }
                },
                {
                    "start": 28,
                    "end": 36,
                    "isHitted": true,
                    "score": 0.5,
                    "diagnosisDetail": {
                        "entity_type": "URL"
                    }
                },
                {
                    "start": 107,
                    "end": 112,
                    "isHitted": true,
                    "score": 0.85,
                    "diagnosisDetail": {
                        "entity_type": "DATE_TIME"
                    }
                }
            ]
        }
    ]
}

```

**Response Format Reference**

A classifier classifies an input (an entire sentence of text) into different categories. It assigns a confidence score for categories.

Classification models can be multi-headed. For example, when a text is run through text moderation model, one head might classify sexual content while another head might classify violence.

The confidence scores for each model head sum to 1.

| Name                    | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| **Category**            | Each output class that the API predicts.                     |
| **Is hitted**           | Whether harmful content has been detected or not             |
| **Score**               | Confidence score of predicted class                          |
| **Model output detail** | Risk level                                                   |
| **Start_char_index**    | First character processed.                                   |
| **End_char_index**      | Last character processed.                                    |
| **Diagnosis Detail**    | You'll see that the email, IP address, phone, and address values are under a JSON array value of PII. You will see these values in diagnosis. |

### 4. Error Codes

| HTML Status | Meaning                                                      |
| :---------- | :----------------------------------------------------------- |
| 200         | Ok – everything worked!                                      |
| 400         | Bad request – the request could not be accepted.             |
| 403         | Unauthorized – there is an issue with the API key.           |
| 404         | Not found – the page could not be found.                     |
| 429         | Too many requests – you’ve made too many requests to our API, please try again in a few minutes. |
| 500         | Internal service error – we had a problem with our server. Please try again later. |
| 503         | Service unavailable – we are temporarily offline for maintenance. Please try again later. |
| 504         | Gateway timeout – we are not able to fulfil your request at this time. Please try again later. |



##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)

