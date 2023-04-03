#  Project "Carnegie" Private Preview Documentation

Welcome to the Project "Carnegie" private preview!

The Project "Carnegie" Private Preview API is a Cognitive Service that detects material that is potentially offensive, risky, or otherwise undesirable. The Project Carnegie preview will work on new functionalities offering state-of-the-art text, image and multi-modal models that will detect problematic content. Project "Carnegie" helps make applications and services safer from harmful user-generated and AI-generated content.

**The focus of the release `2022-12-30-private` is to add multi-severity risk levels and custom blocklist support with text APIs, as well as the new image APIs.**

## Disclaimer

The sample data and code may contain offensive content. User discretion is advised.

## Overview

- **[How It Works](#-how-it-works)** contains instructions for using the service general.

- **[Concepts / Read First](#concepts--read-first)** provides information you need before using the service.

- **Quickstarts** contain getting-started instructions to guide you through making requests to the service.
    - [Quickstart - prepare Azure Content Moderator resource](#quickstart---prepare-azure-content-moderator-resource)
    - [Quickstart - Text analysis](#quickstart---text-analysis)
    - [Quickstart - Text analysis with custom blocklist](#quickstart---text-analysis-with-custom-blocklist)
    - [Quickstart - Image analysis](#quickstart---image-analysis)

## 🔎 How It Works

Project "Carnegie" can be accessed through RESTful APIs.

### Types of analysis

There are different types of analysis available in our project. The following table describes the currently available API.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Detection  | Scans text for sexual conent, violence, hate speech, and self harm with multi-severity risk levels. |
| Image Detection | Scans image for sexual content and violence with multi-severity risk levels. |

### Language availability

Currently, this API supports English, German, Japanese, Spanish, and French. New languages are coming soon.

## Concepts / Read first

### Region / Location

To use the preview APIs, please create/re-use your Azure Content Moderator resource in the supported regions. Currently, the private preview features are only available in the following Azure regions: 
- East US and South Central US

Feel free to contact us if you require more regions for your business.

### SKU / Pricing Tier

Currently, the private preview features are only available in the **S0** pricing tier.

### Content Categories and Severity Levels

The API provides severity levels for four different categories, described below. For a comprehensive view of the category and severity levels definitions please refer to: [Categories and Severity Levels Guidelines](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Guidelines.md).

| Category                  | Description                                                  | 
| ----------------------------- | ------------------------------------------------------------ | 
| Hate                 | Hate refers to any content that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.  |                         
| Sexual                | Sexual describes language related to anatomical organs and genitals, romantic relationships, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography and abuse.  |
| Violence           | Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc.  | 
| Self-Harm               | Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.   |  

## 💡QuickStart - Create an Azure Content Moderator resource

Before you can begin to test the Project "Carnegie" or integrate it into your applications, you need to create an Azure Content Moderator resource and get the subscription keys to access the resource. If you had a Content Moderator resource before, you may re-use it instead of creating a new one.

### Whitelist your subscription ID

1. Fill out this form to give your Azure subscription permission to use this feature: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).

2. It can take up to 48 hours for the application to be approved. Once you receive a notification from Microsoft, you can go to the next step.

### Create an Azure Content Moderator resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Content Moderator Resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesContentModerator). Enter a unique name for your resource, select the subscription you entered on the application form, select a resource group, [supported region](#region--location) and [supported pricing tier](#sku--pricing-tier). Then select **Create**.
3. The resource will take a few minutes to deploy. After it finishes, Select **go to resource**. In the left pane, under **Resource Management**, select **Subscription Key and Endpoint**. The endpoint and either of the keys will be used to call APIs.

## QuickStart - Text analysis

### Call Text API with a sample request

The following is a sample request with Python. For other languages, please refer to [more samples](#more-samples).

1. Install [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a package containing many Python packages and allows for an easy start into the world of Python.
1. Find your Resource Endpoint URL in your Azure Portal in the **Resource Overview** page under the **Endpoint** field. 
1. Substitute the `<Endpoint>` term with your Resource Endpoint URL.
1. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.
1. Change the body of the request to whatever string of text you'd like to analyze.

> **NOTE:**
>
> The samples may contain offensive content, user discretion advised.

```python
  import requests
  import json

  url = "<Endpoint>/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"

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
    'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
    'Content-Type': 'application/json'
  }

  response = requests.request("POST", url, headers=headers, data=payload)


  print(response.status_code)
  print(response.headers)
  print(response.text)
```



The below fields must be included in the url:

| Name            | Description                                                  | Type        |
| :-------------- | :----------------------------------------------------------- | ----------- |
| **API Version** | (Required) This is the API version to be checked. Current version is: api-version=2022-12-30-preview. Example: <Endpoint>/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en | String      |
| **Language**    | (Required) Language code for text analysis. **Currently, we support English, German, Japanese, Spanish, and French.** Value can contain either the English language code of BCP 47 `"en"`, or if you want to detect other four supported languages, you should specify `"multi"`.                                    Example:<Endpoint>/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en | BCP 47 code |



The JSON fields that can be included in the request body are defined in this table:

| Name                  | Description                                                  | Type               |
| :-------------------- | :----------------------------------------------------------- | ------------------ |
| **Text**              | (Required) This is the raw text to be checked. Other non-ascii characters can be included. | String             |
| **Categories**        | (Optional) This is assumed to be an array of category names. See the **Concepts** section for a list of available category names. If no categories are specified, all four categories are used. We will use multiple categories to get scores in a single request. | String             |
| **BlockListIds**      | Custom list ID array. You could attach multiple listsID here. ListsID should be number. | Array with numbers |
| **BreakByBlocklists** | If set this field to `true`, once a blocklist is matched, the analysis will return immediately without model output. Default is `false`. | Boolean            |

See the following sample request body:

```json
{
  "text": "you are an idiot",
  "categories": [
   "Hate","Sexual","SelfHarm","Violence"
  ],
  "blockListIds": [
    "numbers"
  ],
  "breakByBlocklists": false
}
```

> **NOTE: Text size and granularity**
>
> The default maximum length for text submissions is **7K characters**. If you need to analyze longer blocks of text, you can split the input text (for example, using punctuation or spacing) across multiple related submissions. 
>
> Text granularity depends on the business context: what you plan to do with the scores afterward. Annotating multiple paragraphs sometimes becomes skewed by content ratios: suppose one paragraph has one sentence with a low severity of harm and another with a higher severity of harm. In that case, that low-severity sentence may be ignored in a longer document context.

> **NOTE: Sample Python Jupyter Notebook**
>
> Do the following steps if you want to run the Python sample in a Jupyter Notebook.
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download the [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs a github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get a load error from Jupyter.
>
> 3. Run the notebook.


### Interpret Text API response

You should see the Text moderation results displayed as JSON data in the console output. For example:

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

The JSON fields in the output are defined in the following table:

| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Category**   | Each output class that the API predicts. Classification can be multi-labeled. For example, when a text is run through a text moderation model, it could be classified as sexual content as well as violence. | String |
| **Risk Level** | Severity of the consequences.                                | Number |

The API provides severity levels for four different categories, described below. For a comprehensive view of the category and severity levels definitions please refer to: [Categories and Severity Levels Guidelines](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Guidelines.md) 


> **NOTE: Why risk level is not continuous**
>
> Currently, we only use levels 0, 2, 4, and 6. In the future, we may be able to extend the risk levels to 0, 1, 2, 3, 4, 5, 6, 7: seven levels with finer granularity.


## 💡QuickStart - Text analysis with custom blocklist

The default AI classifiers are sufficient for most content moderation needs. However, you might need to screen for terms that are specific to your use case.

You can create custom lists of terms to use with the Text API. The following steps help you get started. For more list operations samples, please refer to [more examples](#custom-list-operations).



The below fields must be included in the url:

| Name            | Description                                                  | Type        |
| :-------------- | :----------------------------------------------------------- | ----------- |
| **ListID**      | (Required) This is the listID to be checked.                                                                                                          Example: url = "<Endpoint>/contentmoderator/text/lists/{ListID}?api-version=2022-12-30-preview" | String      |
| **ItemID**      | (Required) This is the listID to be checked.                                                                                                          Example: url = "<Endpoint>/contentmoderator/text/lists/{ListID}/items/{ItemID}?api-version=2022-12-30-preview" | BCP 47 code |
| **API Version** | (Required) This is the API version to be checked. Current version is: api-version=2022-12-30-preview. Example: <Endpoint>/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en | String      |
| **Language**    | (Required) Language code for text analysis. **Currently, we support English, German, Japanese, Spanish, and French.** Value can contain either the English language code of BCP 47 `"en"`, or if you want to detect other four supported languages, you should specify `"multi"`.                                    Example:<Endpoint>/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en | BCP 47 code |



### Create or modify a terms list

> **NOTE:**
>
> There is a maximum limit of **5 term lists** per resource, with each list **not to exceed 10,000 terms**.


1. Use method **PATCH** to create a list or update an existing list's description or name.
1. The relative API path should be "/text/lists/{listId}?api-version=2022-12-30-preview".
1. In the **listId** parameter, enter the ID of the list that you want to add **in the url** (in our example, **1234**). The ID should be a number up to 64 characters.
1. Substitute `<Endpoint>` with your endpoint URL.
1. Paste your subscription key into `the Ocp-Apim-Subscription-Key` field.


```python
import requests
import json

url = "<Endpoint>/contentmoderator/text/lists/1234?api-version=2022-12-30-preview"

payload = json.dumps({
    "listId": "1234",
    "name": "MyList",
    "description": "This is a violence list"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)


print(response.status_code)
print(response.headers)
print(response.text)
```

The response code should be `201` and the URL to get the created list should be contained in the header, named **Location**


### Add or modify a term in the list


> **NOTE:**
>
> There will be some delay after you add or edit a term before it takes effect on text analysis, usually **not exceeding 5 minutes**.

1. Use method **PATCH**.
2. The relative path should be "/text/lists/{listId}/items/{itemId}?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to add (in our example, **1234**). 
4. In the **itemId** parameter, enter the ID of the term **in the url** (in our example, **01** )
5. In the **language** parameter, enter the language code **in the url** (for example, `"en"`, `"multi"`). 
5. Substitute `<Endpoint>` with your endpoint.
7. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.
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

url = "<Endpoint>/contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview"

payload = json.dumps({
    "itemId": "01",
    "description": "my first word",
    "text": "blood",
    "language": "en"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)


print(response.status_code)
print(response.headers)
print(response.text)
```

The response code should be `201` and the URL to get the created list should be contained in the header, named **Location**.



### Analyze text with a custom list

1. Change your method to **POST**.
1. The relative path should be "/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"
1. Verify that the term has been added to the list. In the **listId** parameter, enter the list ID **in the url** that you generated in the previous step. 
1. Set `breakByBlocklists: True`, so that once a blocklist is matched, the analysis will return immediately without model output. The default setting is `false`.
1. Enter your subscription key, and then select **Send**.
1. In the **Response content** box, verify the terms you entered. The custom list is literally matched by characters and do NOT support regex.

```python
import requests
import json
url = "[Endpoint]/contentmoderator/text:analyze?api-version=2022-12-30-preview&language=en"
payload = json.dumps({
  "text": "I want to beat you till you blood",
  "categories": [
    "Hate",
    "Sexual",
    "SelfHarm",
    "Violence"
  ],
  "blockListIds":["1234"],
  "breakByBlocklists": True
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

## QuickStart - Image analysis

### Call Image API with sample request

Now that you have an Azure Content Moderator resource and you have a subscription key for that resource, let's run some tests by using the Image moderation API.

Here is a sample request with Python:

1. Install the [Python](https://pypi.org/) or [Anaconda](https://www.anaconda.com/products/individual#Downloads). Anaconda is a nice package containing a lot of Python packages already and allows for an easy start into the world of Python.
1. Substitute the `<Endpoint>` with your resource endpoint URL.
1. Upload your image by one of two methods:**by  Base64 or by Blob url**. We only support JPEG and PNG image formats.
   - First method (Recommend): encoding your image to base64. You could leverage [this website](https://codebeautify.org/image-to-base64-converter)  to do encoding quickly. Put the path to your base 64 image in the _content_ parameter below.
   - Second method: [Upload image to Blob Storage Account](https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html). Put your Blob URL into the _url_ parameter below. Currently we only support system assigned Managed Identity to access blob storage, so you must enable system assigned Managed Identity for the Content Moderator instance and assign the role of "Storage Blob Data Contributor/Owner/Reader" to the identity:
     - Enable managed identity for content moderator instance. 

       ![enable-cm-mi-1](https://user-images.githubusercontent.com/36343326/213126427-2c789737-f8ec-416b-9e96-d96bf25de58e.png)

     - Assign the role of "Storage Blob Data Contributor/Owner/Reader" to the Managed identity. Any roles highlighted below should work.

       ![assign-role-2](https://user-images.githubusercontent.com/36343326/213126492-938bd351-7e53-45a7-97df-b9d8be94ad80.png)

       ![assign-role-3](https://user-images.githubusercontent.com/36343326/213126536-31efac53-1741-4ff6-97a0-324b9a7e67a9.png)

       ![assign-role-4](https://user-images.githubusercontent.com/36343326/213126616-03af2bc9-2328-42f6-abeb-766eff28cd8a.png)
   
1. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.
1. Change the body of the request to whatever image you'd like to analyze.

> **NOTE:**
>
> The samples could contain offensive content, user discretion advised.


```python
import requests
import json

url = "<Endpoint>/contentmoderator/image:analyze?api-version=2022-12-30-preview"

payload = json.dumps({
  "image": {
    #use content when upload image by base64
    "content": "[base64 encoded image]"
    
    #use url when upload image by blob url
    #"url": "[image blob url]"
  },
  "categories": [
    "Hate",
    "Sexual",
    "SelfHarm",
    "Violence"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.status_code)
print(response.headers)
print(response.text)
```

The JSON fields that can be included in the request body are defined in this table:


| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Content**    | (Optional) Upload your image by converting it to base64. You can either choose "Content"or "Url". | Base64 |
| **Url**        | (Optional) Upload your image by uploading it into blob storage. You can either choose "Content"or "Url". |        |
| **Categories** | (Optional) This is assumed to be multiple category names. See the **Concepts** part for a list of available category names. If no categories are specified, defaults are used, we will use multiple categories in a single request. | String |


> **NOTE: Image size requirements**
>
> The default maximum size for image submissions is **4MB** with at least **50x50** image dimensions.

> **NOTE: Sample Python Jupyter Notebook**
>
> 1. Install the [Jupyter Notebook](https://jupyter.org/install). Jupyter Notebook can also easily be installed using [Anaconda](https://www.anaconda.com/products/individual#Downloads). 
>
> 2. Download [Sample Python Notebook](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Sample%20Code%20for%20Text%20and%20Image%20API%20with%20Multi-severity.ipynb). Note: this needs github sign in to access. Please also note that you need to use "download ZIP" option from GitHub doc repo instead of "save as" or you will get a load error from Jupyter.
>
> 3. Run the notebook.

### Understand Image API response

> **NOTE:**
>
> For this release, we only supported two classifiers, `Sexual` and `Violence`, for image detection. `Hate` and `SelfHarm` will be released in the future.

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


## More samples

### Text analysis

#### cURL

Here is a sample request with cURL. You must have [cURL](https://curl.se/download.html) installed to run it.

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

#### Java

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

### Image analysis

#### cURL

Here is a sample request with cURL. You must have [cURL](https://curl.se/download.html) installed to run it.

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

#### Java

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

### Custom list operations

In addition to the operations mentioned in the quickstart, There are more operations to help you manage and use the custom list feature. These examples use Python.

#### Get all terms in a term list

1. Use method **GET**.
2. The relative path should be "/text/lists/{listId}/items?api-version=2022-12-30-preview".
3. In the **listId** parameter, enter the ID of the list that you want to get (in our example, **1234**). 
4. Substitute [Endpoint] with your endpoint.
5. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.
6. Enter the following JSON in the **Request body** field, for example:


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

#### Get all lists

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


#### Delete a term

> **NOTE:**
>
> There will be some delay after you delete a term before it takes effect on text analysis, usually **not exceed 5 minutes**.

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

```python
import requests
import json
url = "[Endpoint]/contentmoderator/text/lists/1234/items/01?api-version=2022-12-30-preview"
headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',
  'Content-Type': 'application/json'
}
response = requests.request("DELETE", url, headers=headers, data=payload)
print(response.status_code)
print(response.headers)
print(response.text)
```

#### Delete a term list and all of its contents

> **NOTE:**
>
> There will be some delay after you delete a list before it takes effect on text analysis, usually **not exceeding 5 minutes**.


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

```python
import requests
import json
url = "[Endpoint]/contentmoderator/text/lists/1234?api-version=2022-12-30-preview"
headers = {
  'Ocp-Apim-Subscription-Key': 'Please type your Subscription Key here',
  'Content-Type': 'application/json'
}
response = requests.request("DELETE", url, headers=headers, data=payload)
print(response.status_code)
print(response.headers)
print(response.text)
```


## Additional information

### Limits

#### Query per second

| Pricing Tier | Query per second (QPS) | 
| :----------- | :--------------------- | 
| S0           | 10                     | 

If you need a faster rate, please [contact us](mailto:acm-team@microsoft.com) to request.

### Latency

The service is designed for real-time scenarios, while various factors could affect the client-observed latency. To avoid the networking impact as much as possible, you may want to make API calls from the same region as the Content Moderator resource. Below are some benchmark performance numbers for your reference. If you observe unexpected high latency, please contact us.

| API         | Latency for reference                                                    |
| :---------- | :----------------------------------------------------------- |
| Text analysis        | 100~300ms                                                    |
| Image analysis       | 100~300ms                                                    |

### Response codes

The API may return the following HTTP response codes:

| Response code | Description                                                      |
| :---------- | :----------------------------------------------------------- |
| 200         | OK - Standard response for successful HTTP requests.              |
| 201         | Created - The request has been fulfilled, resulting in the creation of a new resource. |
| 204         | No content - The server successfully processed the request, and is not returning any content. Usually you will see it for DELETE operation.|
| 400         | Bad request – The server cannot or will not process the request due to a client error (e.g., malformed request syntax, size too large, invalid request message framing, or deceptive request routing). |
| 401         | Unauthorized – Authentication is required and has failed. |
| 403         | Forbidden – User not having the necessary permissions for a resource. |
| 404         | Not found - The requested resource could not be found. |
| 429         | Too many requests – The user has sent too many requests in a given amount of time. Please refer to "Quota Limit" section for limitations. |
| 500         | Internal server error – An unexpected condition was encountered on the server side. |
| 503         | Service unavailable – The server cannot handle the request temporarily. Please try again later. |
| 504         | Gateway timeout – The server did not receive a timely response from the upstream service. Please try again later. |


## Terms of use
- [Project Carnegie Private Preview Terms](https://github.com/Azure/Project-Carnegie-Private-Preview/blob/main/Private%20Preview%20Terms%20for%20Project%20Carnegie.pdf)

## Contact us

If you get stuck, [email us](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)
