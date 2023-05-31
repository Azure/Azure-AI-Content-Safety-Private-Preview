

#  Multimodal API Private Preview Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 

The Multimodal Private Preview API detects certain material that contains both text and images, and helps make applications & services safer from harmful user-generated or AI-generated content.

**The focus of the 05-30 Private Preview release is Multimodal capability.**



## ⚠️ Disclaimer

The sample code could have offensive content, user discretion is advised.


##  📒 Overview 

This documentation site is structured into following sections.

- **How It works** contains instructions for using the service in more general ways.

- **Concepts** provides in-depth explanations of the service categories.
- **Sample Code** shows sample requests using the cURL, Python, C# and Java.

- **QuickStart** goes over getting-started instructions to guide you through making requests to the service.

  

##  🔎How It works

- ### Type of analysis

There are different types of analysis available in our project. The following table describes **the currently available API**.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Multimodal Detection | Scans both text and image for hate speech. |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.



##  🗃Concepts

### Category

- **Category:** **Hate Speech** - Hate speech is defined as any speech that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.


## 💡 QuickStart - Multimodal Detection by using the API 

Before you can begin to test, you need to create an Azure AI Content Safety resource and get the subscription keys to access the resource.

> ###  📘 NOTE:
>
> The samples could contain offensive content, user discretion advised!!


### Step 1. Whitelist your subscription ID

1. Submit this form by filling your subscription ID to whitelist this feature to you: [Microsoft Forms](https://forms.office.com/r/38GYZwLC0u).
2. The whitelist will take up to 48 hours to approve. Once you receive notification from Microsoft, you can go to next step.

### Step 2. Create an Azure Content Safety resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Content Safety Resource](https://aka.ms/acs-create). Enter a unique name for your resource, select the **whitelisted subscription**, resource group, your preferred region in one of the **East US, West Europe** and pricing tier. Select **Create**.
3. **The resource will take a few minutes to deploy.** After it does, go to the new resource. To access your Content Safety resource, you'll need a subscription key; In the left pane, under **Resource Management**, select **API Keys and Endpoints**. Copy one of the subscription key values and endpoint for later use.

> ###  📘 NOTE:
>
> Currently the private preview features are only available in two regions:  **East US, West Europe**. Please create your Content Safety resource in these regions. Feel free to let us know your future production regions so we can plan accordingly.

### Step 3. Test with sample Request

Now that you have a resource available in Azure for Content Safety and you have a subscription key for that resource, let's run some tests by using the Multimodal API.

#### **Request Format Reference**

1. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.
2. Change the body of the request to whatever string of text you'd like to analyze.

```
curl --location '<Endpoint>contentsafety/imageWithText:analyze?api-version=2023-05-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <your_subscription_key>7' \
--header 'Content-Type: application/json' \
--data '{
  "image": {
      "content": "<image base 64 code>"
 },
  "categories": ["Hate"],
  "enableOcr": true,
  "text": "want to kill you"
}'
```

| Name           | Description                                                  | Type   |
| :------------- | :----------------------------------------------------------- | ------ |
| **Content**    | (Required) Encode your image to base64. You can use a website like codebeautify to do the encoding. Then save the encoded string to a temporary location. | String |
| **Text**       | (Required) This is assumed to be raw text to be checked. Other non-ascii characters can be included. | String |
| **enableOcr**  | (Required) We allow the user to set enable OCR=false when only image is provided, in this case, the model will process the image input and concatenate into the text filed, if the total characters exceed 1000 characters, we will truncate those characters >=1000.. | String |
| **Categories** | (Optional) This is assumed to be multiple categories' name. See the **Concepts** part for a list of available categories names. If no category are specified, defaults are used, we will use multiple categories to get scores in a single request. | String |




#### **Response Format Reference**

```json
{
    "hateResult": {
        "category": "Hate",
        "severity": 6
    }
}
```


| Name                    | Description                                              | Type    |
| :---------------------- | :------------------------------------------------------- | ------- |
| **Category**            | Each output class that the API predicts.                 | String  |
| **Severity levels**     | The higher the severity of input content, the larger this value is. The values can be: 0,2,4,6.         | Boolean |


 ##  📝 Other Sample Code 


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



##  📒 Key Reference 

- [Content Safety Doc](https://aka.ms/acs-doc![image](https://github.com/Azure/Project-Carnegie-Private-Preview/assets/36343326/b2008fe1-171f-498a-a036-c471eb99fa06)




##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! 

