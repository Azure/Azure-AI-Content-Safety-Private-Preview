

#  Content Safety Private Preview Documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 

The Multimodal Private Preview API detects certain material that contains both text and images, and helps make applications & services safer from harmful user-generated or AI-generated content.

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

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Multimodal Detection | Scans both text and image harmful content for hate speech. |

- ### Language availability

Currently this API is only available in English. New languages will be supported in the future.



##  🗃Concepts

### Category

- **Category:** **Hate** - Hate harms refer to any content that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size. 

  


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

#### Prepare a sample image

Choose a sample image to analyze, and download it to your device.

We support JPEG, PNG, GIF, BMP, TIFF, or WEBP image formats. The maximum size for image submissions is 4 MB, and image dimensions must be between 50 x 50 pixels and 2,048 x 2,048 pixels. If your format is animated, we will extract the first frame to do the detection.

You can input your image by one of two methods: **local filestream** or **blob storage URL**.

- **Local filestream** (recommended): Encode your image to base64. You can use a website like [codebeautify](https://codebeautify.org/image-to-base64-converter) to do the encoding. Then save the encoded string to a temporary location.

- **Blob storage URL**: Upload your image to an Azure Blob Storage account. Follow the [blob storage quickstart](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal) to learn how to do this. Then open Azure Storage Explorer and get the URL to your image. Save it to a temporary location.

  Next, you need to give your Content Safety resource access to read from the Azure Storage resource. Enable system-assigned Managed identity for the Azure Content Safety instance and assign the role of **Storage Blob Data Contributor/Owner/Reader** to the identity:

  1. Enable managed identity for the Azure Content Safety instance.

     ![Screenshot of Azure portal enabling managed identity.](https://learn.microsoft.com/en-us/azure/cognitive-services/content-safety/media/role-assignment.png)

  2. Assign the role of **Storage Blob Data Contributor/Owner/Reader** to the Managed identity. Any roles highlighted below should work.

     ![Screenshot of the Add role assignment screen in Azure portal.](https://learn.microsoft.com/en-us/azure/cognitive-services/content-safety/media/add-role-assignment.png)

     ![Screenshot of assigned roles in the Azure portal.](https://learn.microsoft.com/en-us/azure/cognitive-services/content-safety/media/assigned-roles.png)

     ![Screenshot of the managed identity role.](https://learn.microsoft.com/en-us/azure/cognitive-services/content-safety/media/managed-identity-role.png)



#### **Request Format Reference**

1. Substitute the `<endpoint>` with your resource endpoint URL.
2. Replace `<your_subscription_key>` with your key.
3. Populate the `"image"` field in the body with either a `"content"` field or a `"blobUrl"` field. For example: `{"image": {"content": "<base_64_string>"}` or `{"image": {"blobUrl": "<your_storage_url>"}`.

```
curl --location '<Endpoint>contentsafety/imageWithText:analyze?api-version=2023-05-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <your_subscription_key>7' \
--header 'Content-Type: application/json' \
--data '{
  "image": {
      "content": "<image base 64 code>"
      "blobUrl": "<bLObUrl>"
 },
  "categories": ["Hate"],
  "enableOcr": true,
  "text": "want to kill you"
}'
```

| Name                   | Description                                                  | Type    |
| :--------------------- | :----------------------------------------------------------- | ------- |
| **Content or BlobUrl** | (Optional) The content or blob url of image could be base64 encoding bytes or blob url. If both are given, the request will be refused. The maximum size of image is 2048 pixels * 2048 pixels, no larger than 4MB at the same time. The minimum size of image is 50 pixels * 50 pixels. | String  |
| **Text**               | (Optional) The text attached to the image. We support at most 1000 characters (unicode code points) in one text request. | String  |
| **enableOcr**          | (Required) When set to true, our service will perform OCR and analyze the detected text with input image at the same time. We will recognize at most 1000 characters (unicode code points) from input image. The others will be truncated. | Boolean |
| **Categories**         | (Optional) The categories will be analyzed. Currently, only Hate is supported. | Enum    |




#### **Response Format Reference**

```json
{
    "hateResult": {
        "category": "Hate",
        "severity": 6
    }
}
```


| Name                | Description                                                  | Type    |
| :------------------ | :----------------------------------------------------------- | ------- |
| **Category**        | Each output class that the API predicts.                     | Enum    |
| **Severity levels** | The higher the severity of input content, the larger this value is. The values can be: 0,2,4,6. | Integer |


 ##  📝 Other Sample Code 
- #### Python

Here is a sample request with Python. 

```Python
import http.client
import json

conn = http.client.HTTPSConnection("<Endpoint>")
payload = "{\r\n  \"image\": {\r\n      \"content\": \r\n     },\r\n  \"categories\": [\"Hate\"],\r\n  \"enableOcr\": true,\r\n  \"text\": \"I want to kill you\"\r\n}"
headers = {
  'Ocp-Apim-Subscription-Key': '<your_subscription_key>',
  'Content-Type': 'application/json'
}
conn.request("POST", "//contentsafety/imageWithText:analyze?api-version=2023-05-30-preview", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

- #### C#

Here is a sample request with C#. 

```c#
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "<Endpoint>contentsafety/imageWithText:analyze?api-version=2023-05-30-preview");
request.Headers.Add("Ocp-Apim-Subscription-Key", "<your_subscription_key>");
var content = new StringContent("{\r\n  \"image\": {\r\n      \"content\": \r\n     },\r\n  \"categories\": [\"Hate\"],\r\n  \"enableOcr\": true,\r\n  \"text\": \"I want to kill you\"\r\n}", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());

```

- #### Java

Here is a sample request with Java. 

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n  \"image\": {\r\n      \"content\": \r\n     },\r\n  \"categories\": [\"Hate\"],\r\n  \"enableOcr\": true,\r\n  \"text\": \"I want to kill you\"\r\n}");
Request request = new Request.Builder()
  .url("<Endpoint>contentsafety/imageWithText:analyze?api-version=2023-05-30-preview")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "<your_subscription_key>")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```



##  📒 Key Reference 

- [Content Safety Doc](https://aka.ms/acs-doc)




##  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:acm-team@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! 

