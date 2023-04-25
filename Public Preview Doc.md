




# Overview
# 1. Overview
##  What is Azure Content Safety

Welcome to the Azure Content Safety public preview!

The Azure Content Safety Public Preview is a Cognitive Service that detects material that is potentially offensive, risky, or otherwise undesirable. The Azure Content Safety public preview will work on new functionalities offering state-of-the-art text, image and multi-modal APIs and the studio that will detect problematic content. Azure Content Safety helps make applications and services safer from harmful user-generated and AI-generated content.

Azure Content Safety can be accessed through RESTful APIs.

### Product Types

There are different types of analysis available in our product. 

| Type                        | Functionality                                                |
| :-------------------------- | :----------------------------------------------------------- |
| Text Detection API          | Scans text for sexual, violence, hate speech, and self harm with severity levels. |
| Image Detection API         | Scans image for sexual, violence, hate speech, and self harm with multi-severity levels. |
| Azure Content Safety Studio | ACS Studio is an online tool to visually explore, understand, evaluate  the ACS service. The studio provides a platform for you to experiment with the different ACS classifies and sample their returned data in an interactive manner without the need to write code. |



### Azure Content Safety Studio

#### What is Azure Content Safety Studio?

Azure Content Moderator Studio provides templates and customized workflows for users to choose and build their own content moderation workflows on multilingual and multimodal like text, image and video. The moderation within this studio not only contains the out-of-the-box AI models but leveraging Microsoft built-in lists which already proved the coverage of the profanities and could keep update to new trends swiftly, meanwhile, user custom lists could also be uploaded to enrich the coverage of harmful contents that certain industries care. All these cool capabilities are handled by the studio and its backend, customers don’t need to worry about the model development and could onboard their data for quick validation and monitor the KPIs accordingly like the tech metrics – latency, accuracy, recall, or the business metrics – blocking rate, blocked volume, category proportion, language proportion and more. With simply operations and configurations, the customers could test different solutions quickly and find the best-fit one, instead of wasting time experimenting with seas of models and spending that much on human moderating. 

### Language availability

Currently, this API supports 8 languages, English, German, Japanese, Spanish, French, Italian, Portuguese, Chinese. New languages are coming soon.

You do not need to specify language code for text analysis. 

### Pricing

Currently, the public preview features are  available in the **F0 and S0** pricing tier.

### Service Limits

#### Region / Location

To use the public preview APIs, please create Azure Content Safety resource in the supported regions. Currently, the public preview features are only available in the following Azure regions: 

- East US and West Europe

Feel free to contact us if you require more regions for your business.

#### Request per second

| Pricing Tier | Request per second (RPS) |
| :----------- | :----------------------- |
| F0           | 5                        |
| S0           | 10                       |

If you need a higher RPS, please [contact us](mailto:acm-team@microsoft.com) to request.



# 2. QuickStart

## Text analysis

### Disclaimer

The sample data and code may contain offensive content. User discretion is advised.

### Create an Azure Content Safety resource

Before you can begin to use the Azure Content Safety or integrate it into your applications, you need to create an Azure Content Safety resource and get the subscription keys to access the resource.

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Azure Content Safety Resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicescontentsafety). Enter a unique name for your resource, select the subscription you entered on the application form, select a resource group, [supported region](#region--location) and [supported pricing tier](#sku--pricing-tier). Then select **Create**.
3. The resource will take a few minutes to deploy. After it finishes, Select **go to resource**. In the left pane, under **Resource Management**, select **Subscription Key and Endpoint**. The endpoint and either of the keys will be used to call APIs.

### Call Text API with a sample request 

1. Find your Resource Endpoint URL in your Azure Portal in the **Resource Overview** page under the **Endpoint** field. 
1. Substitute the `<Endpoint>` term with your Resource Endpoint URL.
1. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.
1. Change the body of the request to whatever string of text you'd like to analyze.

> **NOTE:**
>
> The samples may contain offensive content, user discretion advised.

#### Python

```python
import requests
import json

url = "<Endpoint>contentsafety/text:analyze?api-version=2023-04-30-preview"

payload = json.dumps({
  "text": "You are an idiot.",
  "categories": [
    "Hate",
    "SelfHarm",
    "Sexual",
    "Violence"
  ],
  "blocklistNames": [],
  "breakByBlocklists": False
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

#### cURL

Here is a sample request with cURL. You must have [cURL](https://cURL.se/download.html) installed to run it.

```shell
cURL --location '<Endpoint>contentsafety/text:analyze?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "text": "You are an idiot.",
  "categories": ["Hate","SelfHarm", "Sexual", "Violence"],
  "blocklistNames": [],
  "breakByBlocklists": False
}'
```


The below fields must be included in the url:

| Name            | Description                                                  | Type   |
| :-------------- | :----------------------------------------------------------- | ------ |
| **API Version** | (Required) This is the API version to be checked. Current version is: api-version=2023-04-30-preview. Example: <Endpoint>/contentsafety/text:analyze?api-version=2023-04-30-preview | String |

The parameter in the request body are defined in this table:
| Name                  | Type     | Description                                                  | Type    |
| :-------------------- | -------- | :----------------------------------------------------------- | ------- |
| **text**              | Required | This is the raw text to be checked. Other non-ascii characters can be included. | String  |
| **categories**        | Optional | This is assumed to be an array of category names. See the **Concepts** section for a list of available category names. If no categories are specified, all four categories are used. We will use multiple categories to get scores in a single request. | String  |
| **blocklistNames**    | Required | Text blocklist Name. Only support following characters: 0-9 A-Z a-z - . _ ~. You could attach multiple lists name here. | Array   |
| **breakByBlocklists** | Required | When set to `true`, further analyses of harmful content will not be performed in cases where blocklists are hit. When set to `false`, all analyses of harmful content will be performed, whether or not blocklists are hit. | Boolean |

> **NOTE: Text size and granularity**
>
> The default maximum length for text submissions is **1K characters**. If you need to analyze longer blocks of text, you can split the input text (for example, using punctuation or spacing) across multiple related submissions. 
>



#### Python SDK

@Patrick @ Meng AI  The following is a sample request with PythonSDK . 

@Meng AI, please refer this to write the python sample step by step https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/client-libraries?tabs=visual-studio&pivots=programming-language-python

```json

```

```python

```



#### .Net SDK

The following is a sample request with .Net.

### Interpret Text API response

You should see results displayed as JSON data in the console output. For example:

```json
{
    "blocklistsMatchResults": [],
    "hateResult": {
        "category": "Hate",
        "severity": 0
    },
    "selfHarmResult": {
        "category": "SelfHarm",
        "severity": 0
    },
    "sexualResult": {
        "category": "Sexual",
        "severity": 0
    },
    "violenceResult": {
        "category": "Violence",
        "severity": 0
    }
}
```

The JSON fields in the output are defined in the following table:

| Name         | Description                                                  | Type    |
| :----------- | :----------------------------------------------------------- | ------- |
| **category** | Each output class that the API predicts. Classification can be multi-labeled. For example, when a text is run through a text content safmodel, it could be classified as sexual content as well as violence. | String  |
| **severity** | The higher the severity of input content, the larger this value is. The values could be: 0,2,4,6. | Integer |


> **NOTE: Why severity level is not continuous**
>
> Currently, we only use levels 0, 2, 4, and 6. In the future, we may be able to extend the severity levels to 0, 1, 2, 3, 4, 5, 6, 7: seven levels with finer granularity.



### Create a  blocklist

The default AI classifiers are sufficient for most content safety needs. However, you might need to screen for terms that are specific to your use case.

You can create custom lists of terms to use with the Text API. The following steps help you get started. 

The below fields must be included in the url:

| Name              | Type     | Description                                                  | Type        |
| :---------------- | -------- | :----------------------------------------------------------- | ----------- |
| **blocklistName** | Required | Text blocklist Name. Only support following characters: 0-9 A-Z a-z - . _ ~                                                                                                                      Example: url = "<Endpoint>/contentsafety/text/blocklists/{blocklistName}?api-version=2023-04-30-preview" | String      |
| **blockItems**    | Required | This is the blocklistName to be checked.                                                                                                          Example: url = "<Endpoint>/contentsafety/text/blocklists/{blocklistName}/blockitems/{blockItems}?api-version=2023-04-30-preview" | BCP 47 code |
| **API Version**   | Required | This is the API version to be checked. Current version is: api-version=2023-04-30-preview. Example: <Endpoint>/contentsafety/text:analyze?api-version=2023-04-30-preview | String      |

> **NOTE:**
>
> There is a maximum limit of **10,000 terms**.The maximum term limit is applied on the sum of terms from all lists.


1. Use method **PATCH** to create a list or update an existing list's description or name.
1. The relative API path should be "/text/blocklists/{blocklistName}?api-version=2023-04-30-preview".
1. In the **blocklistName** parameter, enter the Name of the list that you want to add **in the url** (in our example, **1234**). Text blocklist name only supports the following characters: 0-9 A-Z a-z - . _ ~
1. Substitute `<Endpoint>` with your endpoint URL.
1. Paste your subscription key into `the Ocp-Apim-Subscription-Key` field.

#### Python


```python
import requests
import json

url = "<Endpoint>contentsafety/text/blocklists/1234?api-version=2023-04-30-preview"

payload = json.dumps({
  "description": "This is a sample blocklist"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)

print(response.text)


```

#### cURL

Here is a sample request with cURL. You must have [cURL](https://cURL.se/download.html) installed to run it.

```shell
cURL --location --request PATCH '<Endpoint>contentsafety/text/blocklists/1234?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key:<enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "description": "This is a sample blocklist"
}'
```

The response code should be `201` .


### Add a blockitem/blockitems 


> **NOTE:**
>
> We will support to add multiple blockitems within one API call.

1. Use method **PATCH**.
2. The relative path should be "/text/blocklists/{blocklistName}:addBlockItems?api-version=2023-04-30-preview".
3. In the url path  parameter, enter the **blocklistName** that you want to add (in our example, **1234**). 
4. In the description parameter, enter the description (in our example: this is a sample item ), the maximum length of dscritpion is 1024 characters. 
5. In the text parameter, enter the blockterm (in our example: idiot ), we support **array of blockItems** to add, the maximum length of blockitem is 128 characters. 
6. Substitute `<Endpoint>` with your endpoint.
7. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.

#### Python

```json
import requests
import json

url = "<Endpoint>contentsafety/text/blocklists/1234:addBlockItems?api-version=2023-04-30-preview"

payload = json.dumps({
  "blockItems": [
    {
      "description": "This is a sample item",
      "text": "idiot"
    }
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

#### cURL

```json
cURL --location '<Endpoint>contentsafety/text/blocklists/1234:addBlockItems?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "blockItems": [
    {
      "description": "This is a sample item",
      "text": "idiot"
    }
  ]
}'
```

The response code should be `201` with the response body will be the below:

```json
{
  "blocklistName": "string",
  "description": "string"
}
```



### Analyze text with a custom list

1. Change your method to **POST**.
1. The relative path should be "/contentsafety/text:analyze?api-version=2023-04-30-preview"
1. Verify that the term has been added to the list. In the **blocklistNames** parameter, enter the list Name you generated in the previous step. 
1. Set `breakByBlocklists: true`, so that once a blocklist is matched, the analysis will return immediately without model output. The default setting is `false`.
1. Enter your subscription key, and then select **Send**.
1. In the **Response content** box, verify the terms you entered. The custom list is literally matched by characters and do NOT support regex.

#### cURL

```python
cURL --location '<Endpoint>contentsafety/text:analyze?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "text": "You are an idiot.",
  "categories": ["Hate","SelfHarm", "Sexual", "Violence"],
  "blocklistNames": ["1234"],
  "breakByBlocklists": True
}'
```

#### Python

```python
import requests
import json

url = "<Endpoint>contentsafety/text:analyze?api-version=2023-04-30-preview"

payload = json.dumps({
  "text": "You are an idiot.",
  "categories": [
    "Hate",
    "SelfHarm",
    "Sexual",
    "Violence"
  ],
  "blocklistNames": [
    "1234"
  ],
  "breakByBlocklists": True
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

**Response content**

```json
{
    "blocklistsMatchResults": [
        {
            "blocklistName": "1234",
            "blockItemId": "a27f61c3-2282-41ea-8068-6226cdd8adb4",
            "blockItemText": "idiot",
            "offset": "11",
            "length": "5"
        }
    ],
    "hateResult": {
        "category": "Hate",
        "severity": 0
    },
    "selfHarmResult": {
        "category": "SelfHarm",
        "severity": 0
    },
    "sexualResult": {
        "category": "Sexual",
        "severity": 0
    },
    "violenceResult": {
        "category": "Violence",
        "severity": 0
    }
}
```

### Custom list operations

In addition to the operations mentioned above. There are more operations to help you manage and use the custom list feature. 

#### Get all blockItems by blocklistName

1. Use method **GET**.
2. The relative path should be "/text/blocklists/{blocklistName}/blockitems?api-version=2023-04-30-preview".
3. In the **blocklistName** parameter, enter the Name of the list that you want to get (in our example:**1234**). 
4. Substitute [Endpoint] with your endpoint.
5. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.

##### Python

```python
import requests

url = "<Endpoint>contentsafety/text/blocklists/1234/blockItems?api-version=2023-04-30-preview"

payload = ""
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

##### cURL

```python
cURL --location '<Endpoint>contentsafety/text/blocklists/1234/blockItems?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--data ''
```

The status code should be 200 and the response body should be like this:

```json
{
  "value": [
    {
      "blockItemId": "string",
      "description": "string",
      "text": "string"
    }
  ],
  "nextLink": "string"
}
```

#### Get all text blocklists

1. Use method **GET**.
2. The relative path should be "/text/blocklists?api-version=2023-04-30-preview".
3. Substitute [Endpoint] with your endpoint.
4. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field.

##### Python


```python
import requests

url = "<Endpoint>contentsafety/text/blocklists?api-version=2023-04-30-preview"

payload = ""
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)

```

##### cURL


```python
cURL --location '<Endpoint>contentsafety/text/blocklists?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--data ''

```

The status code should be 200 and the response body should be like this:

```json
{
  "value": [
    {
      "blocklistName": "string",
      "description": "string"
    }
  ],
  "nextLink": "string"
}
```



#### Delete a blocklist

> **NOTE:**
>
> There will be some delay after you delete a term before it takes effect on text analysis, usually **not exceed 5 minutes**.

1. Use method **DELETE**.
2. The relative path should be "/text/blocklists/{blocklistName}?api-version=2023-04-30-preview".
3. In the url **blocklistName** parameter, enter the Name of the list that you want to delete  (in our example:**1234**). 
4. Substitute [Endpoint] with your endpoint.
5. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field

##### Python

```json
import requests
import json

url = "<Endpoint>contentsafety/text/blocklists/1234?api-version=2023-04-30-preview"

payload = json.dumps({
  "description": "Test happy path"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)

```

##### cURL

```json
curl --location --request DELETE '<Endpoint>contentsafety/text/blocklists/1234?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "description": "Test happy path"
}'
```

**Response content**

```json
204
```



#### Remove a blockitem

> **NOTE:**
>
> We support to remover multiple blockitems within one API call.

1. Use method **POST**.
2. The relative path should be "/text/blocklists/{blocklistName}:removeBlockItems?api-version=2023-04-30-preview".
3. In the url **blocklistName** parameter, enter the Name of the list that you want to delete a term from (in our example: **1234**). 
4. In the request body blockItemIds parameter, enter the singe or array of blockItemIds to remove.
5. Substitute [Endpoint] with your endpoint.
6. Paste your subscription key into the **Ocp-Apim-Subscription-Key** field

##### Python

```json
import requests
import json

url = "<Endpoint>contentsafety/text/blocklists/1234:removeBlockItems?api-version=2023-04-30-preview"

payload = json.dumps({
  "blockItemIds": [
    "c4491d5b-9ea9-4d2a-97c7-70ae8e6fc8c1"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)


```

##### cURL

```json
cURL --location '<Endpoint>contentsafety/text/blocklists/1234:removeBlockItems?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "blockItemIds": [
    "c4491d5b-9ea9-4d2a-97c7-70ae8e6fc8c1"
  ]
}'
```

**Response content**

```json
204
```



## Image analysis
### Call Image API with sample request

Now that you have an Azure Content Safety resource and you have a subscription key for that resource, let's run some tests by using the Image content safety API.

1. Substitute the `<Endpoint>` with your resource endpoint URL.

1. Upload your image by one of two methods: **by content (Base64) or by BlobUrl**. We only support **Jpeg, Png, Gif, Bmp,Tiff and Webp** image formats, If your format is animated, we will extract the first frame to do the detection.

   - First method (Recommend): encoding your image to base64. You could leverage [this website](https://codebeautify.org/image-to-base64-converter)  to do encoding quickly. Put the path to your base 64 image in the _content_ parameter below.

   - Second method: [Upload image to Blob Storage Account](https://statics.teams.cdn.office.net/evergreen-assets/safelinks/1/atp-safelinks.html). Put your Blob URL into the _url_ parameter below. Currently we only support system assigned Managed Identity to access blob storage, so you must enable system assigned Managed identity for the Azure Content Safety instance and assign the role of "Storage Blob Data Contributor/Owner/Reader" to the identity:

     - Enable managed identity for Azure Content Safety instance. 

       ![enable-cm-mi-1](https://user-images.githubusercontent.com/36343326/213126427-2c789737-f8ec-416b-9e96-d96bf25de58e.png)

     - Assign the role of "Storage Blob Data Contributor/Owner/Reader" to the Managed Nameentity. Any roles highlighted below should work.

       ![assign-role-2](https://user-images.githubusercontent.com/36343326/213126492-938bd351-7e53-45a7-97df-b9d8be94ad80.png)

       ![assign-role-3](https://user-images.githubusercontent.com/36343326/213126536-31efac53-1741-4ff6-97a0-324b9a7e67a9.png)

       ![assign-role-4](https://user-images.githubusercontent.com/36343326/213126616-03af2bc9-2328-42f6-abeb-766eff28cd8a.png)

1. Paste your subscription key into the `Ocp-Apim-Subscription-Key` field.

1. Change the body of the request to whatever image you'd like to analyze.

##### Python

```python
import requests
import json

url = "<Endpoint>contentsafety/image:analyze?api-version=2023-04-30-preview"

payload = json.dumps({
  "image": {
    "content": "base 64 code"
  },
  "categories": [
    "Hate",
    "SelfHarm",
    "Sexual",
    "Violence"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<enter_your_subscription_key_here>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

#### cURL
```python

cURL --location '<Endpoint>contentsafety/image:analyze?api-version=2023-04-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <enter_your_subscription_key_here>' \
--header 'Content-Type: application/json' \
--data '{
  "image": {"BlobUrl": "Please paste your blob url here"
  },
  "categories": ["Hate","SelfHarm", "Sexual", "Violence"]
}'

```

The parameters in the request body are defined in this table:


| Name                    | Description                                                  | Type              |
| :---------------------- | :----------------------------------------------------------- | ----------------- |
| **content and BlobURL** | The content or BlobUrl of image, could be base64 encoding bytes or blob url. If both are given, the request will be refused. The maximum size of image is 2048 pixels * 2048 pixels, no larger than 4MB at the same time. The minimum size of image is 50 pixels * 50 pixels. | Base64 or BlobUrl |
| **categories**          | The categories will be analyzed. If not assigned, a default set of the categories' analysis results will be returned. | String            |

#### Python SDK

@Patrick @ Meng AI  The following is a sample request with PythonSDK . 



```json

```

```python

```

#### .Net SDK

The following is a sample request with .Net. 

```json

```

```python

```

### Understand Image API response

You should see results displayed as JSON data. For example:

```json
{
  "hateResult": {
    "category": "Hate",
    "severity": 0
  },
  "selfHarmResult": {
    "category": "Hate",
    "severity": 0
  },
  "sexualResult": {
    "category": "Hate",
    "severity": 0
  },
  "violenceResult": {
    "category": "Hate",
    "severity": 0
  }
}
```



## Azure Content Safety Studio


@louise

# 3. Samples

@Meng AI github link with sdk, each languages should put into different SDK repos, please refer below link to write samples

## Python SDK

https://learn.microsoft.com/en-us/samples/azure/azure-sdk-for-python/formrecognizer-samples/?view=form-recog-3.0.0



## .Net SDK

https://learn.microsoft.com/en-us/samples/azure/azure-sdk-for-net/azure-form-recognizer-client-sdk-samples/?view=form-recog-3.0.0



# 4. Concepts 
### Content Categories 

| Category  | Description                                                  |
| --------- | ------------------------------------------------------------ |
| Hate      | Hate refers to any content that attacks or uses pejorative or discriminatory language with reference to a person or identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size. |
| Sexual    | Sexual describes language related to anatomical organs and genitals, romantic relationships, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography and abuse. |
| Violence  | Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. |
| Self-Harm | Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself. |



### Severity Levels

| Severity | Description |
| -------- | ----------- |
| 0        | Safe        |
| 2        | Low         |
| 4        | Medium      |
| 6        | High        |



# 6. Reference

@Meng AI Restful API link



# 7. Responsible use of AI

@Patrick need to add this page 



## Transparency Notes



# 8. Resources

## Terms of use

- [Azure Content Safety public Preview Terms](https://github.com/Azure/Project-Carnegie-public-Preview/blob/main/public%20Preview%20Terms%20for%20Project%20Carnegie.pdf)

## Contact us

If you get stuck, [email us](mailto:acm-team@microsoft.com) or use the feedback wNameget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)
