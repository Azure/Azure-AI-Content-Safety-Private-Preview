

#  Project Carnegie Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 	

Welcome to the Project Carnegie! 

The Project Carnegie is a private preview of Azure Cognitive Service that checks text, image and video content that is potentially offensive, risky, or otherwise undesirable. In the upcoming private preview, we are going to introduce a reboot of Azure Content Moderator, which lets developers and data scientists use new state-of-the-art text, image, audio video and multi-modal models to make the applications using the new AI generative models by OpenAI (like GPT-X, Dall-E 2 and Codex, which powers GitHub Copilot) and Microsoft products safe to use. The new models are not only good at making AIs safe, but they are also targeted at user-generated content on social media, game chat rooms, forums, etc.

**In the Sept 2022 release, APIs to detect harmful content in text are the focus of the release.**

##  📒 Overview 

This documentation site is structured into following sections

- **How It works** contain instructions for using the service in more general ways.

- **Concepts** provide in-depth explanations of the service categories.
- **Sample Code** are sample request using the cURL, Python, C# and Java.

- **QuickStart** are getting-started instructions to guide you through making requests to the service.

  

##  🔎How It works

The Project Carnegie can be accessed through RESTful APIs. 

- ### Type of analaysis

There are different types of analysis available in our project. The following table describes **the currently available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Moderation | Scans text for sexual, violence, hate speech, and self harm. |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.


##  🗃Concepts

### Text category

This feature of the API provide scores for several different categories. Here are some of the categories our API can provide scores for:

- **Category 1:** **Sexual** - Sexual describes language related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography and Child Sexual Abuse Material (CSAM).
- **Category 2:** **Violence** - Violence describes language related to physical actions intended to hurt, injure, damage or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 
- **Category 3:** **Hate Speech** - Hate speech is defined as any speech that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.
- **Category 4:** **Self-harm**- Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.




## 💡 QuickStart - Text moderation by using the API 

Before you can begin to test the Project Carnegie or integrate it into your custom applications, you need to create and subscribe to a Content Moderator resource and get the subscription key for accessing the resource.

### Step 1. Whitelist your subscription ID

1. Submit this form by filling your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).
2. The whitelist will take a few minutes to approve. After it does, go to next step.

### Step 2. Create and subscribe to a Content Moderator resource

1. Sign in to the [Azure portal](https://portal.azure.com/).
2. Then [Create Content Moderator - Microsoft Azure](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator) resource. Enter a unique name for your resource, select the **whitelisted subscription**, resource group, your preferred region in one of the **East US, West US 2 and  South Central US** and pricing tier. 
3. Select **Create**.

> ### 🚧NOTE:
>
> Currently service only support three regions:  **East US, West US 2 and  South Central US**. Please create an Azure subscription in these regions accordingly.

The resource will take a few minutes to deploy. After it does, go to the new resource. To access your Content Moderator resource, you'll need a subscription key:

10. In the left pane, under **Resource Management**, select **Keys and Endpoints**.

11. Copy one of the subscription key values for later use.

### Step 3. Sample Request

Now that you have a resource available in Azure for Content Moderator and you have a subscription key for that resource, let's run some tests by using the Text moderation API.

Here is a sample request with Python.

```python
import requests

url = "https://[Endpoint]contentmoderator/moderate/text/detect?api-version=2022-09-30-preview"

payload = {"text": "You are an idiot."}
headers = {
    "accept": "application/json",
    "content-type": "application/json",
    "Ocp-Apim-Subscription-Key": "Please type your key here"
}

response = requests.post(url, json=payload, headers=headers)

print(response.text)
```

> ### 🚧DOWNLOAD:
>
> [Sample Python Notebook](https://github.com/Azure/Content-Moderator/blob/main/Sample%20Python%20Notebook.ipynb)

#### **Request Format Reference**

1. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.
2. Change the body of the request to whatever string of text you'd like to analyze.

```json
{
    "text":"You are an idiot.",
    "categories": ["HateSpeech","Sexual","SelfHarm","Violence"]
}
```

| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Text**       | (Required) This is assumed to be raw text to be checked. Other non-ascii characters can be included. | String |
| **Categories** | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available categories names. If no category are specified, defaults are used, we will use multiple categories to get scores in a single request. | String |

> ### 🚧NOTE: Text size and latency
>
> The default maximum length for text submissions is **10K characters**. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions.

>

### Step 4. Evaluate the response

You should see the Text moderation results displayed as JSON data. For example:

```json
{
    "value": [
        {
            "category": "SelfHarm",
            "detected": false,
            "score": 1.055202E-4,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "Violence",
            "detected": false,
            "score": 0.0,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "Sexual",
            "detected": false,
            "score": 2.038020E-4,
            "modelOutputDetail": null,
            "diagnoses": null
        },
        {
            "category": "HateSpeech",
            "detected": true,
            "score": 0.9882153,
            "modelOutputDetail": null,
            "diagnoses": null
        }
    ]
}
```

#### **Response Format Reference**

Classification models can be multi-headed. For example, when a text is run through text moderation model, one head might classify sexual content while another head might classify violence.

The confidence score is from 0 to 1. A higher score indicates a greater likelihood that a reader would perceive the comment as containing the given category. For example, a comment like “ You are an idiot ” may receive a probability score of 0.99 for category Hate Speech. 

```json
{
            "category": "HateSpeech",
            "detected": true,
            "score": 0.9882153,
            "modelOutputDetail": null,
            "diagnoses": null
        }
```

> ### 🚧NOTE: **Why the score might change**
>
> We update our models regularly. Before updating, we thoroughly test to ensure models meet a high quality bar for the results of these tests.  However you may see that a specific score changed as a result of an update. Note that we are not able to notify users each time an update is released.



| Name                    | Description                                                  | Type    |
| :---------------------- | :----------------------------------------------------------- | ------- |
| **Category**            | Each output class that the API predicts.                     | String  |
| **Detected**            | Whether harmful content has been detected or not             | Boolean |
| **Score**               | Confidence score of predicted categories                     | Number  |
| **Model output detail** | Risk level (Not supported for this version and will only show "null") | String  |
| **Diagnosis Detail**    | You'll see that the email, IP address, phone, and address values are under a JSON array value of PII. You will see these values in diagnosis. | String  |

### Step 5: Limitations

#### Quota limit

By default, we set a quota limit:

| Pricing Tier | Query per second (QPS) | Maximum value                         |
| :----------- | :--------------------- | ------------------------------------- |
| F0           | 1                      | 5000 requests per resource per month. |
| S0           | 1                      | No maximum limit.                     |

If you're running a production website, you may need to [request a quota increase](acm-team@microsoft.com).

#### Latency & Reliability

We aim to keep text moderation API fast enough to be used in real-time scenarios as comments are being written, with response times around 100ms. Different categories will have different latencies. 

#### API Errors

There are several types of errors you may encounter while using the Text moderation API. The message and details fields will provide the information you need to understand the error.

| HTML Status | Meaning                                                      |
| :---------- | :----------------------------------------------------------- |
| 200         | Ok – everything worked!                                      |
| 400         | Bad request – the request could not be accepted.             |
| 403         | Unauthorized – there is an issue with the API key.           |
| 404         | Not found.                                                   |
| 429         | Too many requests – you’ve made too many requests to our API, please try again in a few minutes. |
| 500         | Internal service error – we had a problem with our server. Please try again later. |
| 503         | Service unavailable – we are temporarily offline for maintenance. Please try again later. |
| 504         | Gateway timeout – we are not able to fulfil your request at this time. Please try again later. |

 ## 💡 Other Sample Code 

- #### cURL

Here is a sample request with cURL. 

```shell
curl --location --request POST 'https://[Endpoint]contentmoderator/moderate/text/detect?api-version=2022-09-30-preview' \
--header 'Ocp-Apim-Subscription-Key: {Please type your key here}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "text":"You are an idiot.",
    "categories": []
}'
```

- #### C#

Here is a sample request with C#. 

```c#
var client = new RestClient("https://[Endpoint]contentmoderator/moderate/text/detect?api-version=2022-09-30-preview");
var request = new RestRequest(Method.POST);
request.AddHeader("accept", "application/json");
request.AddHeader("content-type", "application/json");
request.AddHeader("Ocp-Apim-Subscription-Key", "Please type your key here");
request.AddParameter("application/json", "{\"text\":\"You are an idiot.\"}", ParameterType.RequestBody);
IRestResponse response = client.Execute(request);
```

- #### Java

Here is a sample request with Java. 

```java
OkHttpClient client = new OkHttpClient();

MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\"text\":\"You are an idiot.\"}");
Request request = new Request.Builder()
  .url("https://[Endpoint]contentmoderator/moderate/text/detect?api-version=2022-09-30-preview")
  .post(body)
  .addHeader("accept", "application/json")
  .addHeader("content-type", "application/json")
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your key here")
  .build();

Response response = client.newCall(request).execute();
```



##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)

