#  Project "Carnegie" Private Preview Documentation !

[TOC]
Welcome to the Project "Carnegie" Private Preview!

The Project "Carnegie" Private Preview API is a Cognitive Service that detects certain material that is potentially offensive, risky, or otherwise undesirable. The initial version of Project Carnegie Preview will detect material in text and image. In later versions, we intend to update the API with new functionalities offering state of the art text, image and multi-modal models that will detect problematic content to help make applications & services safer from harmful User-generated-content and/or AI-generated-content.

**The focus of the December 2022 Private Preview release is to add multi-severity risk levels with text API and new image API.**

## ⚠️ Disclaimer

The sample data and code could have offensive content, user discretion is advised.

##  📒 Overview 

This documentation site is structured into the following sections.

- **How It works** contains instructions for using the service in more general ways.

- **Concepts** provides in-depth explanations of the service categories.

- **Sample Code** shows sample requests using the cURL, Python and Java.

- **QuickStart** goes over getting-started instructions to guide you through making requests to the service.

  

##  🔎How It works

Project "Carnegie" can be accessed through RESTful APIs. 

- ### Type of analysis

There are different types of analysis available in our project. The following table describes **the currently available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Detection  | Scans text for sexual, violence, hate speech, and self harm with multi-severity risk level |
| Image Detection | Scans image for sexual, violence, hate speech, and self harm with multi-severity risk level |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.

##  🗃Concepts

### Text and image category

This feature of the API provides scores for 4 different categories. Here are brief guidelines for the categories our API can provide scores for. Please be aware that these are high level descriptions of the guidelines we use to build our categories. Please contact us for details about current detailed guidelines:

- **Category 1:** **Sexual** - Sexual describes language and images related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography.
- **Category 2:** **Violence** - Violence describes language and images related to physical actions intended to hurt, injure, damage or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 
- **Category 3:** **Hate** - Hate is defined as any language and images that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.
- **Category 4:** **Self-Harm**- Self-harm describes language and images related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.


## 💡QuickStart - Before you begin

Before you can begin to test the Project "Carnegie" or integrate it into your applications, you need to create an Azure Content Moderator resource and get the subscription keys to access the resource.

### Step 1. Whitelist your subscription ID

1. Submit this form by filling your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).

2. The whitelist will take up to 48 hours to approve. Once you receive a notification from Microsoft, you can go to the next step.

### Step 2. Create an Azure Content Moderator resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).

2. [Create Content Moderator Resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator). Enter a unique name for your resource, select the **whitelisted subscription**, resource group, your preferred region in one of the **East US, West US 2 and  South Central US** and pricing tier. Select **Create**.

3. **The resource will take a few minutes to deploy.** After it does, go to the new resource. To access your Content Moderator resource, you'll need a subscription key; In the left pane, under **Resource Management**, select **API Keys and Endpoints**. Copy one of the subscription key values and endpoint for later use.

> **_📘 NOTE:_**
>
> Currently the private preview features are only available in three regions:  **East US, West US 2 and  South Central US**. Please create your Azure Content Moderator resource in these regions. Feel free to let us know your future production regions so we can plan accordingly.


## 💡 QuickStart - Make an Text API Request

### Step 1. Text API with sample Request

Now that you have a resource available in Azure for Content Moderator and you have a subscription key for that resource, let's run some tests by using the Text moderation API.

Here is a sample request with Python.

1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.

2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. You can find your Resource Endpoint URL in your Azure Portal in the Resource Overview page under the "Endpoint" field. For example, if your Resource URL is: "content-mod-test.cognitiveservices.azure.com/" replace "https://[Endpoint]contentmoderator/text:analyze?api-version=2022-12-30-preview" with **"https://content-mod-test.cognitiveservices.azure.com/contentmoderator/text:analyze?api-version=2022-12-30-preview"**

   > **_📘 NOTE:_**
   >
   > The samples could contain offensive content, user discretion advised!!

```python
import requests
import json

url = "https://[Endpoint]contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"

payload = json.dumps({
  "text": "you are an idiot",
  "categories": [
    "Hate",
    "Sexual",
    "SelfHarm",
    "Violence"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your key here',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

> **_📘 NOTE: Sample Python Jupyter Notebook_**
>
> The samples could contain offensive content, user discretion advised!!
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get load error from Jupyter.
>
> 3. Run the notebook.

1. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.

2. Change the body of the request to whatever string of text you'd like to analyze.

```json
{
  "text": "you are an idiot",
  "categories": [
   "Hate","Sexual","SelfHarm","Violence"
  ],
  "blockListIds": [
    "string"
  ],
  "breakByBlocklists": false
}
```

| Name                  | Description                                                  | Type   |
| :-------------------- | :----------------------------------------------------------- | ------ |
| **Text**              | (Required) This is assumed to be raw text to be checked. Other non-ascii characters can be included. | String |
| **Categories**        | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available category names. If no categories are specified, defaults are used, we will use multiple categories to get scores in a single request. | String |
| **BlockListIds**      | Custom list Id.                                              |        |
| **BreakByBlocklists** | The strategy means if detection will stop on block list  when returning true. |        |

> **_📘 NOTE: Text size, and granularity_**
>
> The default maximum length for text submissions is **7K characters**. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions. 
>
> Text granularity depends on the business context: what you plan to do with the scores afterward. Annotating multi-paragraphs sometimes becomes skewed by content ratios. Suppose one paragraph has one sentence with a low severity of harm and another with a higher severity of harm. In that case, that low-severity sentence may be ignored in a longer document context. 

### Step 2. Text API with sample Response

You should see the Text moderation results displayed as JSON data. For example:

```json
{
    "blocklistMatchResults": [],
    "hateResult": {
        "category": "Hate",
        "riskLevel": 2
    },
    "selfHarmResult": {
        "category": "SelfHarm",
        "riskLevel": 0
    },
    "sexualResult": {
        "category": "Sexual",
        "riskLevel": 0
    },
    "violenceResult": {
        "category": "Violence",
        "riskLevel": 0
    }
}
```

| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Category**   | Each output class that the API predicts. Classification can be multi-labeled. For example, when a text is run through a text moderation model, it could be classified as sexual content as well as violence. | String |
| **Risk Level** | Severity of the consequences.                                | Number |

**Risk map:**

| Risk level                    | Description                                                  | Example                                                      |
| ----------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Risk 0 – Safe                 | Words, phrases marked as Risk 0 will always be allowed, meaning they cannot be filtered. | hello, goodbye, thank  you.                                  |
| Risk 2 – Notable/Questionable | Risk 2 category stands for unknown and the classifier assigns a Risk 4 to any piece of text that it cannot decipher. Risk 2 is in the middle of the spectrum precisely because its risk and severity are unknown; it could be a simple misspelling of a low-risk word, or it could be a manipulation of a high risk one. | zero, 5, dumb, touching, dress, cow, daddy,  taste, inept, street, lies. missing words, keyboard mashing (asdsdjhasdgah),  misspellings (purel) |
| Risk 4 - Mature               | Risk Level 4 stands for maturity. Words and phrases marked as a Risk 5 typically cover mature subject matters, utilize potentially inappropriate language, and are also heavily reliant on context.Examples: | mild forms of vulgarity, bullying, and hate speech, sharing of PII such as full names, phone numbers or addresses, discussions about controversial themes. |
| Risk 6- Dangerous             | Words and phrases marked as a Risk 6 are explicit and  often offensive in nature. Most times they do not require additional context  to be considered high risk. Examples: strong swear words, explicit sexual  talk, severe bullying, and hate speech. | strong swear words, explicit sexual talk, severe bullying, and hate speech. |

![Content Moderation-Pitch Deck 1207](https://user-images.githubusercontent.com/36343326/211787069-c1de12c3-ba48-452a-a64a-809df3c8fb43.png)



> **_📘 NOTE: Why the risk level is not continuous_**
>
> Currently, we only have 0, 2, 4,6 four high-level risk levels available to us. In the future, we may be able to extend the risk levels to 1, 2, 3, 4, 5, 6, 7, seven levels with finer granularity. 



### Step 3. Check text against a custom list 

The default AI classfiers is sufficient for most content moderation needs. However, you might need to screen for terms that are specific to your organization.

Now, you can create custom lists of terms to use with the Text Moderation API.

Below provides information and code samples to help you get started:

- Create a list.
- Add terms to a list.
- Screen terms against the terms in a list.
- Delete terms from a list.
- Delete a list.
- Edit list information.

#### Create a term list-PATCH

> **_📘 NOTE:_**
>
> There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.
> 

1. In the **Request body**, enter values for **ListID, Name (for example, MyList) and **Description.
2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. https://[Endpoint]contentmoderator/text/lists/1234?api-version=2022-12-30-preview
3. Enter your subscription key, and then select **Send**.
4. In the **Response content** box, your list is created. Note the **ID** value that is associated with the new list. You need this ID for management functions.

**Request content**

```json
{
    "listId": "1234",
    "name": "MyList",
    "description": "This is a violence list"
}
```

**Response content**

```json
200
```

#### Add a term to a term list-PATCH

1. In the **listId** parameter, enter the list ID that you generated in previous step.
2. In the **Request body**, enter values for ** Text** (for example, blood) and type a value for **language**. 
2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. https://[Endpoint]contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview
3. Enter your subscription key, and then select **Send**.
4. In the **Response content** box, verify the terms you entered.

**Request content**

```json
{
    "itemId": "01",
    "description": "my first word",
    "text": "blood",
    "language": "en"
}
```

**Response content**

```json
200
```

#### Get all terms in a term list-GET

1. To verify that the term has been added to the list; In the **listId** parameter, enter the list ID that you generated in previous step. 
1. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. https://[Endpoint]contentmoderator/text/lists/1234/items?api-version=2022-12-30-preview
2. Enter your subscription key, and then select **Send**.
3. In the **Response content** box, verify the terms you entered.
4. Now, you successfully created a list including a term, you could screen text using a term list.

**Request content**

```json
{
    "listId": "1234"
}
```

**Response content**

```json
{
    "values": [
        {
            "itemId": "01",
            "description": "my first word",
            "text": "blood",
            "language": "en"
        }
    ]
}
```



#### Delete a term-DELETE

1. In the **listId** parameter, enter the ID of the list that you want to delete a term from (in our example, **1234**). 
2. Enter the ID of the term.
2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. https://[Endpoint]contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview
3. Enter your subscription key, and then select **Send**.

**Request content**

```json
{
    "listId": "1234",
    "itemId": "01"
}
```

**Response content**

```json
200
```



#### Delete a term list and all of its contents-DELETE

1. In the **listId** parameter, enter the ID of the list that you want to delete a term from (in our example, **1234**). 
1. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. https://[Endpoint]contentmoderator/text/lists/1234?api-version=2022-12-30-preview
2. Enter your subscription key, and then select **Send**.
3. **Request content**

```csharp
{
  "listId": "1234"
}
```

**Response content**

```json
200
```



## 💡 QuickStart - Make an Image API Request

### Step 1. Image API with sample Request

1. Now that you have a resource available in Azure for Content Moderator and you have a subscription key for that resource, let's run some tests by using the Text moderation API.

   Here is a sample request with Python.

   1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.

   2. Run the following commands substituting the [Endpoint] with your Resource Endpoint url. You can find your Resource Endpoint URL in your Azure Portal in the Resource Overview page under the "Endpoint" field. For example, if your Resource URL is: "content-mod-test.cognitiveservices.azure.com/" replace "https://[Endpoint]contentmoderator/text:analyze?api-version=2022-12-30-preview" with **"https://content-mod-test.cognitiveservices.azure.com/contentmoderator/text:analyze?api-version=2022-12-30-preview"**

   3. Upload your image with two methods:

      #### First method: Encode your image to base64. You could leverage [this website](https://codebeautify.org/image-to-base64-converter)  to do encoding for a quick try.

      #### **Second method**: [Upload to Storage Account](https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html) .

      > **_📘 NOTE:_**
      >
      > The samples could contain offensive content, user discretion advised!!


```python
import requests
import json

url = "https://[Endpoint]/contentmoderator/image:analyze?api-version=2022-12-30-preview"

payload = json.dumps({
  "image": {
    "content": "[base64 encoded image]"
  },
  "categories": [
    "Hate",
    "Sexual",
    "SelfHarm",
    "Violence"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '[Endpoint Key]',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

> **_📘 NOTE: Sample Python Jupyter Notebook_**
>
> The samples could contain offensive content, user discretion advised!!
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get load error from Jupyter.
>
> 3. Run the notebook.

1. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.

2. Change the body of the request to whatever string of text you'd like to analyze.

```json
{
  "image": {
    "content": "string",
    "url": "string",
    "format": "jpeg"
  },
  "categories": [
  "Hate","Sexual","SelfHarm","Violence"
  ]
}

```

| Name               | Description                                                  | Sample                                                       |
| :----------------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| **Content OR Url** | (Required) First way to upload your image is to optimize your images and convert them to base64. Second way is to upload your image to Blob and get a Blob Url for image. | Blob url:https://cmsatest2023.blob.core.windows.net/images/adult.jpeg |
| **Image format**   | (Required) This is assumed to be an image in JPEG, PNG format. | String                                                       |
| **Categories**     | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available category names. If no categories are specified, defaults are used, we will use multiple categories in a single request. | String                                                       |

> **_ 📘 NOTE: Image size, and granularity _**
>
> The default maximum size for image submissions is **4MB** with at least **50x50** image dimensions. 
>

### Step 2. Image API with sample Response

You should see the Image moderation results displayed as JSON data. For example:

```json
{
    "hateResult": {
        "category": "Hate",
        "riskLevel": 0
    },
    "selfHarmResult": {
        "category": "SelfHarm",
        "riskLevel": 0
    },
    "sexualResult": {
        "category": "Sexual",
        "riskLevel": 0
    },
    "violenceResult": {
        "category": "Violence",
        "riskLevel": 6
    }
}
```

> **_ 📘 NOTE: Why the risk level is not continuous _**
>
> Currently, we only have 0, 2, 4,6 four high-level risk levels available to us. In the future, we may be able to extend the risk levels to 1, 2, 3, 4, 5, 6, 7, seven levels with finer granularity. 

|                | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Category**   | Each output class that the API predicts.                     | String |
| **Risk Level** | 0 – Safe, 2 – Notable/Questionable, 4 - Mature, 6 - Dangerous | Number |



## ⚠️ Limitations

#### Quota limit

By default, we set a quota limit:

| Pricing Tier | Query per second (QPS) | Maximum value                         |
| :----------- | :--------------------- | ------------------------------------- |
| F0           | 1                      | 5000 requests per resource per month. |
| S0           | 10                     | No maximum limit.                     |

If you need a quota increase, you may need to [shoot us an email](mailto:acm-team@microsoft.com) to request.

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
| 504         | Gateway timeout – we are not able to fulfill your request at this time. Please try again later. |

## 📝 Other Sample Code 

#### Text API

- #### cURL

Here is a sample request with cURL. 

Install the [cURL](https://curl.se/download.html).

```shell
curl --location --request POST 'https://[Endpoint]contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en' \
--header 'Ocp-Apim-Subscription-Key: Please type your key here' \
--header 'Content-Type: application/json' \
--data-raw '{
  "text": "you are an idiot",
  "categories": [
   "Hate","Sexual","SelfHarm","Violence"
  ]
}'

```

- #### Java

Here is a sample request with Java. 

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"text\": \"you are an idiot\",\r\n  \"categories\": [\r\n   \"Hate\",\"Sexual\",\"SelfHarm\",\"Violence\"\r\n  ]\r\n}");
Request request = new Request.Builder()
  .url("https://[Endpoint]contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your key here")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();

```



#### Image API

- #### cURL

Here is a sample request with cURL. 

Install the [cURL](https://curl.se/download.html).

```shell
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"image\": {\r\n    \"url\": \"https://cmsatest2023.blob.core.windows.net/images/adult.jpeg\"\r\n  },\r\n  \"categories\": [\r\n    \"Hate\",\"Sexual\",\"SelfHarm\",\"Violence\"\r\n  ]\r\n}");
Request request = new Request.Builder()
  .url("https://[Endpoint]contentmoderator/image:analyze?api-version=2022-12-30-preview")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your key here")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```

- #### Java

Here is a sample request with Java. 

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"image\": {\r\n    \"url\": \"https://cmsatest2023.blob.core.windows.net/images/adult.jpeg\"\r\n  },\r\n  \"categories\": [\r\n    \"Hate\",\"Sexual\",\"SelfHarm\",\"Violence\"\r\n  ]\r\n}");
Request request = new Request.Builder()
  .url("https://[Endpoint]contentmoderator/image:analyze?api-version=2022-12-30-preview")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your key here")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();

```



##  📒 Key Reference 

- [API Reference](https://github.com/Azure/azure-rest-api-specs-pr/pull/9275/files#diff-839f177f03dd3162188a1fde0c3b7c44371aeb686a1096a38f3d590381ad3867)
- [Project Carnegie Private Preview Terms](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Private%20Preview%20Terms%20for%20Project%20Carnegie.pdf)

##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)

