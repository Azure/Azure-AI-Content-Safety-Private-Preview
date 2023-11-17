# Adaptive Annotation API Private Preview Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview)

With the extensive capabilities of natural language understanding, it's been proven that GPT-4 reaches human parity in understanding the harmful content policy/community guideline and performing harmful content annotation task that is adaptive to each customer's use case.  

Alongside the practice of enforcing content safety techniques in products/communities in various industries, it's been found the "definition of harmful content" varies by use cases. Thus, there's usually an additional human review process after the content gets flagged by Azure AI Content Safety API to get the results adapted. The adaptive annotation API just helps to fill this gap and streamline the content moderation task in an adaptive and automatic way.  

## ⚠️ Disclaimer

The sample code could have offensive content, user discretion is advised.

## 📒 Overview

- **How It Works** contains instructions for using the service in more general ways.
- **Concepts** provides in-depth explanations of the service categories.
- **Sample Code** shows sample requests using the cURL, Python, C# and Java.
- **QuickStart** goes over getting-started instructions to guide you through making requests to the service.

## 🔎How It Works

- ### Type of analysis

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Customized Categories | Create, get, and delete a customized category or list all customized categories for further annotation task |
| Adaptive Annotate | Annotate input text with specified customized category |

- ### Language availability

Currently, this API is only available in English. While users can try guidelines in other languages, we don't commit the output (like the languages of reasoning). We output the reasoning in the language of provided guidelines by default. New languages will be supported in the future.

- ### Response label in output

In private preview, we only support outputting a single label but not multiple labels. If you want to define the final label out of multiple, please note in the emphasis, like "If the text hits multiple labels, output the maximum label".

## 🗃Concepts

### Community guideline

Community guidelines refer to a set of rules or standards that are established by an online community or social media platform to govern the behavior of its users. These guidelines are designed to ensure that all users are treated with respect, and that harmful or offensive content is not posted or shared. They may include rules around hate speech, harassment, nudity, violence, or other types of content that may be deemed inappropriate. Users who violate community guidelines may face consequences such as having their account suspended or banned.

### Category

A category refers to a specific type of prohibited content or behavior that is outlined in the guidelines. Categories may include things like hate speech, harassment, threats, nudity or sexually explicit content, violence, spam, or other forms of prohibited content. These categories are typically defined in broad terms to encompass a range of different behaviors and types of content that are considered to be problematic. By outlining specific categories of prohibited content, community guidelines provide users with a clear understanding of what is and is not allowed on the platform, and help to create a safer and more positive online community.

## 💡 QuickStart - Adaptive annotation by using the API

Before you can begin to test, you need to [create an Azure AI Content Safety resource]((https://aka.ms/acs-create)) and get the subscription keys to access the resource.

> ###  📘 NOTE
>
> The samples could contain offensive content, user discretion is advised!!

### Step 1. Whitelist your subscription ID

1. Submit this form by filling in your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).
2. The whitelist will take up to 48 hours to approve. Once you receive a notification from Microsoft, you can go to the next step.

### Step 2. Create an Azure Content Safety resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Content Safety Resource](https://aka.ms/acs-create). Enter a unique name for your resource, select the **whitelisted subscription**, resource group, and your preferred region in one of the **East US, West Europe** and pricing tier. Select **Create**.
3. **The resource will take a few minutes to deploy.** After it does, go to the new resource. To access your Content Safety resource, you'll need a subscription key; In the left pane, under **Resource Management**, select **API Keys and Endpoints**. Copy one of the subscription key values and endpoint for later use.

> ###  📘 NOTE
>
> Currently the private preview features are only available in two regions:  **East US, West Europe**. Please create your Content Safety resource in these regions. Feel free to let us know your future production regions so we can plan accordingly.
>

### Step 3. Bring your own Azure OpenAI resource

In private preview stage, you need to bring your own Azure OpenAI resource to perform the adaptive annotation task. Please make sure your deployment is built on GPT-4, for other model versions the annotation quality is not guaranteed. 

### Step 4. Test with sample request

Now that you have a resource available in Azure for Content Safety and you have a subscription key for that resource, let's run some tests by using the Adaptive Annotation API!

#### Create a customized category according to specific community guideline

The initial step is to convert your customized community guideline/content policy to one or multiple customized categories in Azure AI Content Safety. Then get it ready to be used for the following annotation task. 

| Name                   | Description                                                  | Type    |
| :--------------------- | :----------------------------------------------------------- | ------- |
| **CategoryName** | (Required) Category name should start with "Customized_", valid character set is "0-9A-Za-z._~-". The maximum length is 64 Unicode characters. | String  |
| **LabelDefinitions** | (Required) To define the labels within each category as the minimum annotation granularity, it could be a severity definition or a sub-category definition. The max label count is 10, min label count is 2. Within each label, you need to specify a label(integer) and a list of enumerations(list) to better describe the scope of the label. Max enumeration per label is 10. | List  |
| **PreDefinedConcepts**          | (Optional) Common concepts that may be referred in the guideline. The max concept count is 30. | List |
| **Emphases**         | (Optional) To finally emphasize the key points to GPT-4 here, for example, the input format, the target output format, etc. The max emphasis count is 10. | List    |
| **ExampleBlobUrl**   | (Optional) The file should end with ".txt", the maximum file size is 1MB in private preview, where each line is an example in json format.  | String    |

##### Request payload reference

```
{
  "categoryName": "Customized_AD0za6RSTFm5pqZzWD2aBrjYTckws",//required, Category name should start with "Customized_", valid character set is "0-9A-Za-z._~-". The maximum length is 64 Unicode characters.
  "labelDefinitions": [//required, the max label count is 10, min label count is 2. 
    {

      "label": 0, // label definition 
      "enumerations": [//required, to enumerate the detailed definitions per label here. Max enumeration per label is 10.
        "string"
      ]
    },
    {
      "label": 1, // label definition 
      "enumerations": [//required, to enumerate the detailed definitions per label here. Max enumeration per label is 10.
        "string"
      ]
    }
  ],

  "exampleBlobUrl": "string",//optional, The file should end with ".txt", the maximum file size is 1MB in private preview, where each line is an example in json format.  
  "preDefinedConcepts": [ //optional, Common concepts that may be referred in the guideline. The max concept count is 30. 
    {
      "concept": "string",
      "description": "string"
    }
  ],
  "emphases": [//optional, to finally emphasize the key points to GPT-4 here, for example, the input format, the target output format, etc. The max emphasis count is 10.
    "string"
  ]
}
```

##### Format requirement for examples

The examples that are provided for each label in the Blob URL need to follow below format requirements:

```
{
  "text": "The text of the example 1", //required, 
  "label": 0, //required, the label that the example describes
  "reasoning": "The reason for the annotation" //optional
}
{
  "text": "The text of the example 2", //required, 
  "label": 2, //required, the label that the example describes
  "reasoning": "The reason for the annotation" //optional
}
```

##### Sample Code

- Curl

```
curl --location --request PUT '<endpoint>/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "categoryName": "Customized_Test",
  "labelDefinitions": [
    {
      "label": 0,
      "enumerations": [
        "all cases that do not fall into Label 1"
      ]
    },
    {
      "label": 1,
      "enumerations": [
        "Animal abuse and torture",
        "Realistic or real-world depictions of extreme gore, graphic violence, or death"
      ]
    }
  ]
}'
```

- Python

```
import requests
import json

endpoint = "<endpoint>"
url = endpoint+"/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview"

headers = {
  "Ocp-Apim-Subscription-Key": '<api_key>',
  "Content-Type": "application/json"
}
payload = json.dumps({
  "categoryName": "Customized_Test",
  "labelDefinitions": [
    {
      "label": 0,
      "enumerations": [
        "all cases that do not fall into Label 1"
      ]
    },
    {
      "label": 1,
      "enumerations": [
        "Animal abuse and torture",
        "Realistic or real-world depictions of extreme gore, graphic violence, or death"
      ]
    }
  ]
})

response = requests.request("PUT", url, headers=headers, data=payload)

print(response.status_code)
print(response.text)
```

#### Perform annotation on input text

After the customized category is created successfully, you can provide the text to be annotated according to the guideline of the newly created category. The input is very simple of 'text' and 'category'.

| Name                   | Description                                                  | Type    |
| :--------------------- | :----------------------------------------------------------- | ------- |
| **Category** | (Required) Name of the newly created category. | String  |
| **Text** | (Required) String of the text to be annotated. The maximum length is 1000 Unicode characters. | String |

##### Request payload reference

```
{
    "text": "xxxx", //String of the text to be annotated.
    "category": "yyyy" //The newly defined category name.
}

```

##### Sample Code

- Curl

```
curl --location '<endpoint>/contentsafety/text:adaptiveAnnotate?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "text": "I want to kill a cat",
  "category": "Customized_Test"
}'
```

- Python

```
import requests
import json

endpoint = "<endpoint>"
url = endpoint+"/contentsafety/text:adaptiveAnnotate?api-version=2023-10-30-preview"

headers = {
  "Ocp-Apim-Subscription-Key": '<api_key>',
  "Content-Type": "application/json"
}
payload = json.dumps({
  "text": "I want to kill a cat",
  "category": "Customized_Test"
})

response = requests.request("POST", url, headers=headers, data=payload)

print(response.status_code)
print(response.text)
```

## Other Categories APIs

### Get Category

#### Sample Code

-Curl

```
curl --location '<endpoint>/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

-Python

```
import requests
import json

endpoint = "<endpoint>"
url = endpoint+"/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview"

headers = {
  "Ocp-Apim-Subscription-Key": '<api_key>',
  "Content-Type": "application/json"
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.status_code)
print(response.text)
```

### List Categories

#### Sample Code

-Curl

```
curl --location '<endpoint>/contentsafety/text/categories?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

-Python

```
import requests
import json

endpoint = "<endpoint>"
url = endpoint+"/contentsafety/text/categories?api-version=2023-10-30-preview"

headers = {
  "Ocp-Apim-Subscription-Key": '<api_key>',
  "Content-Type": "application/json"
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.status_code)
print(response.text)
```

### Delete Category

#### Sample Code

-Curl

```
curl --location --request DELETE '<endpoint>/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

-Python

```
import requests
import json

endpoint = "<endpoint>"
url = endpoint+"/contentsafety/text/categories/Customized_Test?api-version=2023-10-30-preview"

headers = {
  "Ocp-Apim-Subscription-Key": '<api_key>',
  "Content-Type": "application/json"
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.status_code)
print(response.text)
```

## 📒 Key Reference

- [Content Safety Doc](https://aka.ms/acs-doc)

## 💬 We're here to help

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here!
