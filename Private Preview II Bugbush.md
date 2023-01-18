#  Project "Carnegie" Private Preview Documentation !

Welcome to the Project "Carnegie" Private Preview!

The Project "Carnegie" Private Preview API is a Cognitive Service that detects certain material that is potentially offensive, risky, or otherwise undesirable. The initial version of Project Carnegie Preview will detect material in text and image. In later versions, we intend to update the API with new functionalities offering state of the art text, image and multi-modal models that will detect problematic content to help make applications & services safer from harmful User-generated-content and/or AI-generated-content.

**The focus of the 2022-12-30 Private Preview release is to add multi-severity risk levels with text API and new image API.**

## ⚠️ Disclaimer

The sample data and code could have offensive content, user discretion is advised.

##  📒 Overview 

This documentation site is structured into the following sections.

- **How It Works** contains instructions for using the service in more general ways.

- **Concepts** provides in-depth explanations of the service categories.

- **Other Sample Code** shows sample requests using the cURL, Python and Java.

- **QuickStart** goes over getting-started instructions to guide you through making requests to the service.

  

##  🔎How It Works

Project "Carnegie" can be accessed through RESTful APIs. 

- ### Type of analysis

There are different types of analysis available in our project. The following table describes **the currently available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Detection  | Scans text for sexual, violence, hate speech, and self harm with multi-severity risk level |
| Image Detection | Scans image for sexual, violence with multi-severity risk level |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.

##  🗃Concepts

###  Category

This feature of the API provides scores for 4 different categories. Here are brief guidelines for the categories our API can provide scores for. Please be aware that these are high level descriptions of the guidelines we use to build our categories. Please contact us for details about current detailed guidelines:

- **Category 1:** **Sexual** - Sexual describes language and images related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography.
- **Category 2:** **Violence** - Violence describes language and images related to physical actions intended to hurt, injure, damage or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 
- **Category 3:** **Hate** - Hate is defined as any language and images that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.
- **Category 4:** **SelfHarm**- SelfHarm describes language and images related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.


## 💡QuickStart - Before you begin

Before you can begin to test the Project "Carnegie" or integrate it into your applications, you need to create an Azure Content Moderator resource and get the subscription keys to access the resource.

### Step 1. Whitelist your subscription ID

1. Submit this form by filling your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).

2. The whitelist will take up to 48 hours to approve. Once you receive a notification from Microsoft, you can go to the next step.

### Step 2. Create an Azure Content Moderator resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).

2. [Create Content Moderator Resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator). Enter a unique name for your resource, select the **whitelisted subscription**, resource group, your preferred region in one of the **East US, West US 2 and  South Central US** and pricing tier. Select **Create**.
3. **The resource will take a few minutes to deploy.** After it does, go to the new resource. To access your Content Moderator resource, you'll need a subscription key; In the left pane, under **Resource Management**, select **Subscription Key and Endpoint**. Copy one of the subscription key values and endpoint for later use.

> **_📘 NOTE:_**
>
> Currently the private preview features are only available in S0 pricing tier and in three regions:  **East US, West US 2 and  South Central US**. Please create your Azure Content Moderator resource in these regions. Feel free to let us know your future production regions so we can plan accordingly.


## 💡QuickStart - Make a Text API Request

### Step 1. Text API with Sample Request

Now that you have a resource available in Azure Content Moderator and you have a subscription key for that resource, let's run some tests by using the text moderation API.

Here is a sample request with Python.

1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.
2. You can find your Resource Endpoint URL in your Azure Portal in the Resource Overview page under the "Endpoint" field. 
2. Substitute the [Endpoint] with your Resource Endpoint url. For example, "[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview"
3. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
4. Change the body of the request to whatever string of text you'd like to analyze.

 > **_📘 NOTE:_**
 >
 > The samples could contain offensive content, user discretion advised!!

  ```python
  import requests
  import json

  url = "[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"

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
    'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',
    'Content-Type': 'application/json'
  }

  response = requests.request("POST", url, headers=headers, data=payload)


  print(response.status_code)
  print(response.headers)
  print(response.text)
  ```

> **_📘 NOTE: Sample Python Jupyter Notebook_**
>
> The samples could contain offensive content, user discretion advised!!
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs a github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get a load error from Jupyter.
>
> 3. Run the notebook.

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

| Name                  | Description                                                  | Type    |
| :-------------------- | :----------------------------------------------------------- | ------- |
| **Text**              | (Required) This is assumed to be raw text to be checked. Other non-ascii characters can be included. | String  |
| **Categories**        | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available category names. If no categories are specified, defaults are used, we will use multiple categories to get scores in a single request. | String  |
| **Language**          | (Optional) Language code for text analysis. Value can contain only the language code (ex. "en", "fr") of BCP 47. If you did not mention the language code, by default, we will detect all supported languages. **For this release, we only support English.** | String  |
| **BlockListIds**      | Custom list Id array. You could attach multiple lists here.  | Array   |
| **BreakByBlocklists** | If set this field to true, once a blocklist is matched, the analysis will return immediately without model output. Default is false. | Boolean |

> **_📘 NOTE: Text size, and granularity_**
>
> The default maximum length for text submissions is **7K characters**. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions. 
>
> Text granularity depends on the business context: what you plan to do with the scores afterward. Annotating multi-paragraphs sometimes becomes skewed by content ratios. Suppose one paragraph has one sentence with a low severity of harm and another with a higher severity of harm. In that case, that low-severity sentence may be ignored in a longer document context. 

### Step 2. Text API with Sample Response

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
| Risk 2 – Notable/Questionable | Risk 2 category stands for unknown and the classifier assigns a Risk 2 to any piece of text that it cannot decipher. Risk 2 is in the middle of the spectrum precisely because its risk and severity are unknown; it could be a simple misspelling of a low-risk word, or it could be a manipulation of a high risk one. | zero, 5, dumb, touching, dress, cow, daddy,  taste, inept, street, lies. missing words, keyboard mashing (asdsdjhasdgah),  misspellings (purel) |
| Risk 4 - Mature               | Risk Level 4 stands for maturity. Words and phrases marked as a Risk 4 typically cover mature subject matters, utilize potentially inappropriate language, and are also heavily reliant on context. Examples: | mild forms of vulgarity, bullying, and hate speech, sharing of PII such as full names, phone numbers or addresses, discussions about controversial themes. |
| Risk 6- Dangerous             | Words and phrases marked as a Risk 6 are explicit and  often offensive in nature. Most times they do not require additional context  to be considered high risk. Examples: strong swear words, explicit sexual  talk, severe bullying, and hate speech. | strong swear words, explicit sexual talk, severe bullying, and hate speech. |

![Content Moderation-Pitch Deck 1207](https://user-images.githubusercontent.com/36343326/211787069-c1de12c3-ba48-452a-a64a-809df3c8fb43.png)



> **_📘 NOTE: Why the risk level is not continuous_**
>
> Currently, we only have 0, 2, 4,6 four high-level risk levels available to us. In the future, we may be able to extend the risk levels to 0, 1, 2, 3, 4, 5, 6, 7, seven levels with finer granularity. 



### Step 3. Check text against a custom list

The default AI classifiers are sufficient for most content moderation needs. However, you might need to screen for terms that are specific to your organization.

Now, you can create custom lists of terms to use with the Text Moderation API.

Below provides information and code samples to help you get started:

- Create a list.
- Add terms to a list.
- Get all lists.
- Check text against a custom list.
- Delete terms from a list.
- Delete a list.
- Edit list information.

#### Create a term list-PATCH

> **_📘 NOTE:_**
>
> There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.
>


1. Use method **PATCH** to create a list or update existing list's description or name.
2. The relative path should be "/text/lists/{listId}?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to add (in our example, **1234**). The ID shoud be a string.
3. Substitute [Endpoint] with your endpoint.
4. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
5. Enter the following JSON in the **Request body** field, for example:

```json
{
    "listId": "1234",
    "name": "MyList",
    "description": "This is a violence list"
}
```

```python
import requests
import json

url = "[Endpoint]/contentmoderator/text/lists/[ListId]?api-version=2022-12-30-preview"

payload = json.dumps({
    "listId": "1234",
    "name": "MyList",
    "description": "This is a violence list"
})
headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)


print(response.status_code)
print(response.headers)
print(response.text)
```

The response code should be `201` and the URL to get the created list should be contained in the header, named **Location**


#### Add a term to a term list-PATCH

1. Use method **PATCH**.
2. The relative path should be "/text/lists/{listId}/items/{itemId}?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to add (in our example, **1234**). 
4. In the **itemId** parameter, enter the ID of the term (in our example, **01** )
5. In the **language** parameter, enter the Language code (ex. "en", "fr") defined by BCP 47. If you did not mention the language code, by default, we will detect all supported languages. **For this release, we only support English.**
6. Substitute [Endpoint] with your endpoint.
7. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
8. Enter the following JSON in the **Request body** field, for example:

```json
{
    "itemId": "01",
    "description": "my first word",
    "text": "blood",
    "language": "en"
}
```

```python
import requests
import json

url = "[Endpoint]/contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview"

payload = json.dumps({
    "itemId": "01",
    "description": "my first word",
    "text": "blood",
    "language": "en"
})
headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)


print(response.status_code)
print(response.headers)
print(response.text)
```

The response code should be `201` and the URL to get the created list should be contained in the header, named **Location**.

#### Get all terms in a term list-GET

1. Use method **GET**.
2. The relative path should be "/text/lists/{listId}/items?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to add (in our example, **1234**). 
3. Substitute [Endpoint] with your endpoint.
4. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
5. Enter the following JSON in the **Request body** field, for example:



**Request content** with sample url: [Endpoint]/contentmoderator/text/lists/1234/items?api-version=2022-12-30-preview

```python
import requests
import json

url = "[Endpoint]/contentmoderator/text/lists/1234/items?api-version=2022-12-30-preview"

headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your key here',
  'Content-Type': 'application/json'
}

response = requests.request("GET", url, headers=headers)


print(response.status_code)
print(response.headers)
print(response.text)
```

The status code should be 200 and the response body should be like this:
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
#### Get all lists-GET

1. Use method **GET**.
2. The relative path should be "/text/lists?api-version=2022-12-30-preview".
3. Substitute [Endpoint] with your endpoint.
4. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
5. Enter the following JSON in the **Request body** field, for example:

**Request content** with sample url: [Endpoint]/contentmoderator/text/lists?api-version=2022-12-30-preview



```python

import requests

import json

url = "[Endpoint]/contentmoderator/text/lists?api-version=2022-12-30-preview"
headers = {

  'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',

  'Content-Type': 'application/json'

}

response = requests.request("GET", url, headers=headers)
print(response.status_code)
print(response.headers)
print(response.text)

```



The status code should be `200` .


#### Check text against a custom list-POST

1. Change your method to **POST**.
2. The path should be "[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"
3. To verify that the term has been added to the list; In the **listId** parameter, enter the list ID that you generated in the previous step. 
4. Set breakByBlocklists: true, If set this field to true, once a blocklist is matched, the analysis will return immediately without model output. The default setting is false.
5. Enter your subscription key, and then select **Send**.
6. In the **Response content** box, verify the terms you entered.

**Request content** with sample url: [Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en

```json
{
    "text": "I want to beat you till you blood",
    "categories": [
        "Hate",
        "Sexual",
        "SelfHarm",
        "Violence"
    ],
    "blocklistIds": [
        "1234"
    ],
    "breakByBlocklists": true
}
```

**Response content**

```json
{
    "blocklistMatchResults": [
        {
            "listId": "1234",
            "itemId": "01",
            "itemText": "blood",
            "offset": "28",
            "length": "5"
        }
    ]
}
```



#### Delete a term-DELETE

1. Use method **DELETE**.
2. The relative path should be "/text/lists/{listId}/items/{itemId}?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to delete a term from (in our example, **1234**). 
4. In the **itemId** parameter, enter the ID of the term that you want to delete.
5. Substitute [Endpoint] with your endpoint.
6. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field

**Request content** with sample url: [Endpoint]/contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview

```json
{
    "listId": "1234",
    "itemId": "01"
}
```
**Response content**

```json
204
```

#### Delete a term list and all of its contents-DELETE

1. Use method **DELETE**.
2. The relative path should be "/text/lists/{listId}?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to delete. 
5. Substitute [Endpoint] with your endpoint.
6. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.


Request content** with sample url: [Endpoint]/contentmoderator/text/lists/1234?api-version=2022-12-30-preview

```json

{
    "listId": "1234"
}

```

**Response content**

```json
204
```



## 💡QuickStart - Make a Image API Request

### Step 1. Image API with Sample Request

Now that you have a resource available in Azure Content Moderator and you have a subscription key for that resource, let's run some tests by using the Image moderation API.

   Here is a sample request with Python.

1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.
2. Substitute the [Endpoint] with your Resource Endpoint url. For example, "[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview"
3. **Image format**, we only support two image formats JPEG and PNG.
4. Upload your image with two methods:**by  Base64 or by Blob url**.
   - **First method (Recommend): encoding your image to base64**. You could leverage [this website](https://codebeautify.org/image-to-base64-converter)  to do encoding for a quick try. Put your base 64 into below "content" parameter.
   - Second method: [Upload to Blob Storage Account](https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html). Put your Blob url into below "url" parameter. To access your blob storage account, it's require to enable system assigned managed identity for content moderator instance and assign the role of "Storage Blob Data Contributor/Owner/Reader" to the identity.

> **_📘 NOTE:_**
>
> Currently we only support system assigned Managed Identity to access blob storage.
> 
     - Enable managed identity for content moderator instance. 
     ![enable-cm-mi-1](https://user-images.githubusercontent.com/36343326/213126427-2c789737-f8ec-416b-9e96-d96bf25de58e.png)
     - Assign the role of "Storage Blob Data Contributor/Owner/Reader" to the Managed identity. Any roles highlighted below should work.
     ![assign-role-2](https://user-images.githubusercontent.com/36343326/213126492-938bd351-7e53-45a7-97df-b9d8be94ad80.png)
     ![assign-role-3](https://user-images.githubusercontent.com/36343326/213126536-31efac53-1741-4ff6-97a0-324b9a7e67a9.png)
     ![assign-role-4](https://user-images.githubusercontent.com/36343326/213126616-03af2bc9-2328-42f6-abeb-766eff28cd8a.png)
     
5. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.
6. Change the body of the request to whatever image you'd like to analyze.

> **_📘 NOTE:_**
>
> The samples could contain offensive content, user discretion advised!!


```python
import requests
import json

url = "[Endpoint]/contentmoderator/image:analyze?api-version=2022-12-30-preview"

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
  'Ocp-Apim-Subscription-Key': '[Subscription Key]',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.status_code)
print(response.headers)
print(response.text)
```

> **_📘 NOTE: Sample Python Jupyter Notebook_**
>
> The samples could contain offensive content, user discretion advised!!
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get a load error from Jupyter.
>
> 3. Run the notebook.

```json
{
  "image": {
    "content": "string",
    "url": "string"
  },
  "categories": [
  "Sexual","Violence"
  ]
}

```


| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Content**    | (Optional) Upload your image by converting them to base64. You could either choose "Content"or "Url". | Base64 |
| **Url**        | (Optional) Upload your image by uploading them into blob storage. You could either choose "Content"or "Url". |        |
| **Categories** | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available category names. If no categories are specified, defaults are used, we will use multiple categories in a single request. | String |





> **_📘 NOTE: Image size, and granularity_**
>
> The default maximum size for image submissions is **4MB** with at least **50x50** image dimensions. 
>

### Step 2. Image API with Sample Response

> **_📘 NOTE:_**
>
> For this release, we only supported two classifiers: "Sexual" and "Violence" for image detection. "Hate" and "SelfHarm" will be released soon.
**Request content** with base 64:
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

> **_📘 Note: Why the risk level is not continuous_**
>
> Currently, we only have 0, 2, 4,6 four high-level risk levels available to us. In the future, we may be able to extend the risk levels to 1, 2, 3, 4, 5, 6, 7, seven levels with finer granularity. 

|                | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Category**   | Each output class that the API predicts.                     | String |
| **Risk Level** | 0 – Safe, 2 – Notable/Questionable, 4 - Mature, 6 - Dangerous | Number |



## ⚠️ Limitations

#### Quota Limit

By default, we set a quota limit:

| Pricing Tier | Query per second (QPS) | 
| :----------- | :--------------------- | 
| S0           | 10                     | 

If you need a quota increase, you may need to [shoot us an email](mailto:acm-team@microsoft.com) to request.

#### Latency & Reliability

We aim to keep our APIs fast enough to be used in real-time scenarios. Images and text APIs will have different latencies, while the below latencies only occur when the client data center and server data center are located in the same region. 

| API         | Latency                                                      |
| :---------- | :----------------------------------------------------------- |
| Text        | 100~300ms                                                    |
| Image       | 100~300ms                                                    |


##  🗃Response Code Reference

There are several types of errors you may encounter while using the text and image moderation API. The message and details fields will provide the information you need to understand the error.

| HTML Status | Meaning                                                      |
| :---------- | :----------------------------------------------------------- |
| 200         | Ok – everything worked!                                      |
| 201         | Created.                                                     |
| 204         | No Content. The server has fulfilled the request but does not need to return an entity-body. |
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
curl --location --request POST '[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en' \
--header 'Ocp-Apim-Subscription-Key: Please type your Subscription Key here' \
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
  .url("[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your Subscription Key here")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();

```



#### Image API

- #### cURL

Here is a sample request with cURL. 

Install the [cURL](https://curl.se/download.html).

```shell
curl --location --request POST '[Endpoint]/contentmoderator/image:analyze?api-version=2022-12-30-preview' \
--header 'Ocp-Apim-Subscription-Key: Please type your Subscription Key here' \
--header 'Content-Type: application/json' \
--data-raw '{
  "image": {
    "content": "Please Paste base 64 code here"
  }
}'
```

- #### Java

Here is a sample request with Java. 

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"image\": {\r\n    \"url\": \"https://cmsatest2023.blob.core.windows.net/images/adult.jpeg\"\r\n  },\r\n  \"categories\": [\r\n    \"Hate\",\"Sexual\",\"SelfHarm\",\"Violence\"\r\n  ]\r\n}");
Request request = new Request.Builder()
  .url("[Endpoint]contentmoderator/image:analyze?api-version=2022-12-30-preview")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "Please type your Subscription Key here")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();

```



##  📒 Key Reference 

- [Project Carnegie Private Preview Terms](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Private%20Preview%20Terms%20for%20Project%20Carnegie.pdf)

##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)

