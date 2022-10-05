

#  Project Carnegie Private Preview Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 	

Welcome to the Azure Content Moderator v2 Private Preview!

The Azure Content Moderator v2 Private Preview API is a Cognitive Service that detects material that is potentially offensive, risky, or otherwise undesirable, in text. In upcoming v2 Private Preview versions, we are going to update the API with new functionalities that let developers and data scientists use new state of the art text, image and new multi-modal models to make applications & services safe from harmful user-generated-content and/or AI-generated-content.

The focus of the October 10th 2022 release is to detect harmful content in text. 

**In the October 10th release, APIs to detect harmful content in text are the focus of the release.**



## ⚠️ Disclaimer

The sample code could have offensive content, user discretion is advised.



##  📒 Overview 

This documentation site is structured into following sections.

- **How It works** contains instructions for using the service in more general ways.

- **Concepts** provides in-depth explanations of the service categories.
- **Sample Code** shows sample requests using the cURL, Python, C# and Java.

- **QuickStart** goes over getting-started instructions to guide you through making requests to the service.

  

##  🔎How It works

Azure Content Moderator v2 can be accessed through RESTful APIs. 

- ### Type of analysis

There are different types of analysis available in our project. The following table describes **the currently available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Moderation | Scans text for sexual, violence, hate speech, and self harm. |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.



##  🗃Concepts

### Text category

This feature of the API provides scores for 4 different categories. Here are brief guidelines of the categories our API can provide scores for. Please be aware that these are high level descriptions of the guidelines we use to build our categories. Please contact us for details about current extended guidelines:

- **Category 1:** **Sexual** - Sexual describes language related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography.
- **Category 2:** **Violence** - Violence describes language related to physical actions intended to hurt, injure, damage or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 
- **Category 3:** **Hate Speech** - Hate speech is defined as any speech that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.
- **Category 4:** **Self-Harm**- Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.




## 💡 QuickStart - Text moderation by using the API 

Before you can begin to test the Azure Content Moderator v2 or integrate it into your applications, you need to create a Content Moderator resource and get the subscription keys to access the resource.

> ###  📘 NOTE:
>
> The samples could contain offensive content, user discretion advised!!


### Step 1. Whitelist your subscription ID

1. Submit this form by filling your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).
2. The whitelist will take up to 48 hours to approve. Once you receive notification from Microsoft, you can go to next step.

### Step 2. Create a Content Moderator resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Content Moderator Resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator). Enter a unique name for your resource, select the **whitelisted subscription**, resource group, your preferred region in one of the **East US, West US 2 and  South Central US** and pricing tier. Select **Create**.
3. **The resource will take a few minutes to deploy.** After it does, go to the new resource. To access your Content Moderator resource, you'll need a subscription key; In the left pane, under **Resource Management**, select **API Keys and Endpoints**. Copy one of the subscription key values and endpoint for later use.

> ###  📘 NOTE:
>
> Currently the private preview features are only available in three regions:  **East US, West US 2 and  South Central US**. Please create your Content Moderator resource in these regions. Feel free to let us know your future production regions so we can plan accordingly.

### Step 3. Test with sample Request

Now that you have a resource available in Azure for Content Moderator and you have a subscription key for that resource, let's run some tests by using the Text moderation API.

Here is a sample request with Python.

1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.
2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url (e.g. content-moderator-test.cognitiveservices.azure.com/):

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

> ###  📘 NOTE: Sample Python Jupyter Notebook
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
> 2. Download [Sample Python Notebook](https://github.com/Azure/Content-Moderator/blob/main/Sample%20Python%20Notebook.ipynb). Note: this needs github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get load error from Jupyter.
> 3. Run the notebook.

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

> ### 📘NOTE: Text size and latency
>
> The default maximum length for text submissions is **7K characters**. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions.

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

Classification can be multi-labelled. For example, when a text is run through text moderation model, it could be classified as sexual content as well as violence.


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

> ###  📘 NOTE: **Why the score might change**
>
> We update our models regularly. Before updating, we thoroughly test to ensure models meet a high quality bar for the results of these tests.  However you may see that a specific score changed as a result of an update. Note that we are not able to notify users each time an update is released.



| Name                    | Description                                              | Type    |
| :---------------------- | :------------------------------------------------------- | ------- |
| **Category**            | Each output class that the API predicts.                 | String  |
| **Detected**            | Whether harmful content has been detected or not         | Boolean |
| **Score**               | Confidence score of predicted categories                 | Number  |
| **Model output detail** | Not supported for this version and will only show "null" | String  |
| **Diagnosis Detail**    | Not supported for this version and will only show "null" | String  |

### Step 5: Limitations

#### Quota limit

By default, we set a quota limit:

| Pricing Tier | Query per second (QPS) | Maximum value                         |
| :----------- | :--------------------- | ------------------------------------- |
| F0           | 1                      | 5000 requests per resource per month. |
| S0           | 10                     | No maximum limit.                     |

If you need a quota increase, you may need to [shoot us an email](mailto:acm-team@microsoft.com) to request a quota increase.

#### Latency & Reliability

We aim to keep text moderation API fast enough to be used in real-time scenarios, with response times around 100ms. Different categories will have different latencies. 

#### API Error Messages

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

 ##  📝 Other Sample Code 

- #### cURL

Here is a sample request with cURL. 

1. Install the [cURL](https://curl.se/download.html).
2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url (e.g. content-moderator-test.cognitiveservices.azure.com/):

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

