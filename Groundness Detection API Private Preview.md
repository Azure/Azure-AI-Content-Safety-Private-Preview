

#  Groundedness detection API private preview documentation  ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview) 

The Groundedness detection API detects whether the text responses of large language models (LLMs) are grounded in the source materials provided by the users. Ungroundedness refers to instances where the LLMs produce information that is non-factual or inaccurate from what was present in the source materials.


##  Key Features
- **Domain Selection**: This feature offers the option of predefined domains: either `medical` or `generic`. Users can choose an established domain to ensure more tailored detection that aligns with the specific needs of their field.
- **Task Specification**: This feature lets you select the task you're doing, such as QnA (questioning & answering) and Summarization, with adjustable settings according to the task types.
- **Speed vs Interpretability**: There are two modes that trade off speed with performance.
   - Non-Reasoning mode: Offers fast detection capability, easy to embed into online applications.
   - Reasoning mode: Offers detailed explanation for detected ungrounded segments easy for understanding and mitigation.


This documentation site is structured into the following sections.

- **Concepts** This section offers a deep dive into the fundamental principles and theories underlying the Groundedness detection API. It covers key concepts such as the definition of 'ungroundedness' in the context of AI-generated content.
- **Use cases** provides comprehensive details about the various tasks the API can perform.
- **QuickStart** step-by-step instructions to help users begin making requests to the service.
- **Sample Code** demonstrates practical usage with examples in cURL, Python, C#, and Java.


##  Concepts

- **Retrieval Augmented Generation (RAG)**: RAG is a technique for augmenting LLM knowledge with additional data. LLMs can reason about wide-ranging topics, but their knowledge is limited to the public data up to a specific point in time that they were trained on. If you want to build AI applications that can reason about private data or data introduced after a model’s cutoff date, you need to augment the knowledge of the model with the specific information it needs. The process of bringing the appropriate information and inserting it into the model prompt is known as Retrieval Augmented Generation (RAG). For more information, see [Retrieval-augmented generation (RAG)](https://python.langchain.com/docs/use_cases/question_answering/).

- **Groundedness and Ungroundedness in LLMs**: This refers to the extent to which the model’s outputs are based on provided information or reflect reliable sources accurately. A grounded response adheres closely to the given information, avoiding speculation or fabrication. In groundedness measures, source information is crucial and serves as the grounding source. 

- **Hallucination in LLMs**: Hallucination involves generating text that contains fabricated, false, or misleading information. Hallucination in LLMs is a broader concept that generally includes ungroundedness. It refers to the generation of text that is not only ungrounded, but also fabricated, false, or misleading. Hallucination encompasses a wider range of inaccuracies, including completely made-up information that may not have any basis in the provided data or known facts.
    - While all hallucinated content is ungrounded, not all ungrounded content is a hallucination. Hallucination is a broader term that includes any kind of fabricated or false information, whereas ungroundedness specifically refers to deviations from provided information or known facts.

##  Use cases

The Groundedness detection supports text-based Summarization and QnA tasks to ensure that the generated summaries or answers are accurate and reliable. Here are some examples of each use case:

**Summarization tasks**:
- Medical summarization: In the context of medical news articles, Groundedness detection can be used to ensure that the summary does not contain fabricated or misleading information, guaranteeing that readers obtain accurate and reliable medical information.
- Academic paper summarization: When generating summaries of academic papers or research articles, the function can help ensure that the summarized content accurately represents the key findings and contributions without introducing false claims.
- Legal document summarization: In legal environments, where summarizing lengthy legal documents is common, the function can confirm that the summary does not contain any erroneous statements or omissions that could lead to legal disputes.

**QnA tasks**:
- Customer support chatbots: In customer support, the function can be used to validate the answers provided by AI chatbots, ensuring that customers receive accurate and trustworthy information when they ask questions about products or services.
- Medical QnA: For medical QnA, the function assists in verifying the accuracy of medical answers and advice provided by AI systems to healthcare professionals and patients, reducing the risk of medical errors.
- Educational QnA: In educational settings, the function can be applied to QnA tasks to confirm that answers to academic questions or test prep queries are factually accurate, supporting the learning process.
- Financial and investment queries: For financial and investment-related questions, the function can validate the answers given by AI systems, helping users make informed financial decisions based on accurate information.

## Limitations

**Language availability**
Currently, the Groundedness detection API supports the English language. While our API does not restrict the submission of non-English content, we cannot guarantee the same level of quality and accuracy in the analysis of other language content. We recommend that users submit content primarily in English to ensure the most reliable and accurate results from the API.

**Text length limitations**
Please note that the maximum character limit for the grounding sources is 55K characters, and for the text and query, it is 7.5K characters for each API call. If your input (either text or grounding sources) exceeds these character limitations per API call, you will encounter an error.

**Regions**
To use this API, you must create your Azure AI Content Safety resource in the supported regions. Currently, it is available in the following Azure regions:
- East US 2
- East US (only for non-reasoning)
- West US
- Sweden Central

**RPS limitations**

| Pricing Tier | Requests per 10 second (RPS) |
| :----------- | :--------------------------- |
| F0           | 10                           |
| S0           | 10                           |

If you need a higher RPS, please [contact us](mailto:contentsafetysupport@microsoft.com) to request.

## Quickstart 

### Create an Azure Content Safety resource

1. Sign in to the [Azure Portal](https://portal.azure.com/).
2. [Create Content Safety Resource](https://aka.ms/acs-create). Enter a unique name for your resource, select your whitelisted subscription, resource group, region and pricing tier. Currently the private preview Groundedness detection API is available in three regions: **East US2, West US, Sweden Central**. Please create your Content Safety resource in one of these regions.
3. The resource will take a few minutes to deploy. After it does, go to the new resource. In the left pane, under **Resource Management**, select **API Keys and Endpoints**. Copy one of the subscription key values and endpoint to a temporary location for later use.

### Test with a sample request

Now that you have a resource available in Azure for Content Safety and you have a subscription key for that resource, run some tests with the Groundedness detection API.

1. Substitute the `<endpoint>` with your resource endpoint URL (skip the `https://` in the URL), such as <endpoint>/contentsafety/text:detectGroundedness?api-version=2024-02-15-preview.
1. Replace `<your_subscription_key>` with your key.


```json
{
    "Domain": "GENERIC",
    "Task": "QNA",
    "qna": {
            "query": "How much does she currently get paid per hour at the bank?"
           },
    "Text": "12/hour.",
    "GroundingSources": [
        "I'm 21 years old and I need to make a decision about the next two years of my life. Within a week. I currently work for a bank that requires strict sales goals to meet. IF they aren't met three times (three months) you're canned. They pay me 10/hour and it's not unheard of to get a raise in 6ish months. The issue is, **I'm not a salesperson**. That's not my personality. I'm amazing at customer service. I have the most positive customer service \"reports\" done about me in the short time I've worked here. A coworker asked \"do you ask for people to fill these out? You have a ton\". That being said, I have a job opportunity at Chase Bank as a part time teller. What makes this decision so hard is that at my current job, I get 40 hours and Chase could only offer me 20 hours/week. Drive time to my current job is also 21 miles **one way** while Chase is literally 1.8 miles from my house, allowing me to go home for lunch. I do have an apartment and an awesome roommate that I know wont be late on his portion of rent, so paying bills with 20 hours a week isn't the issue. It's the spending money and being broke all the time.\n\nI previously worked at Wal-Mart and took home just about 400 dollars every other week. So I know i can survive on this income. I just don't know whether I should go for Chase as I could definitely see myself having a career there. I'm a math major likely going to become an actuary, so Chase could provide excellent opportunities for me **eventually**.",
       
    ],
    "Reasoning": true,
    "llmResource": {
        "resourceType": "AzureOpenAI",
        "azureOpenAIEndpoint": "<Your_GPT_Endpoint>",
        "azureOpenAIDeploymentName": "<Your_GPT_Deployment>"
    }
}
```


| Name                   | Description                                                  | Type    |
| :--------------------- | :----------------------------------------------------------- | ------- |
| **Domain** | (Optional) `MEDICAL` or `GENERIC`. Default value: `GENERIC`. | Enum  |
| **Task**               | (Optional) Type of task: `QnA`, `Summarization`. Default value: `Summarization`. | Enum |
| - **`qna`**              | (Optional) This parameter is only used when the task type is QnA.  | String  |
| - **`qna > query`**              | (Optional) This is used to submit a question or a query in a Questions and Answers task. Character limit: 7,500. | String  |
| **Text**          | (Required) The text that needs to be checked. Character limit: 7500. |  String  |
| **GroundingSources**         | (Required) Uses an array of grounding sources to validate AI-generated text. Restrictions on the total amount of grounding sources that can be analyzed in a single request are 55K characters. | String array    |
| **Reasoning**         | (Optional) Specifies whether to use the reasoning feature. The default value is `False`. If `True`, the service uses our default GPT resources to provided an explanation and included the "ungrounded" sentence. Be careful: using reasoning will increase the processing time and incur extra fees.| Boolean   |
| **llmResource**         | (Optional) If you want to use your own GPT resources instead of our default GPT resources, add this field manually and include the subfield below for the GPT resources used. If you do not want to use your own GPT resources, remove this field from the input. | String   |
| - `resourceType `| Specifies the type of resource being used, for this version, only allows: `AzureOpenAI`. | Enum|
| - `azureOpenAIEndpoint `| Endpoint URL for Azure's OpenAI service.  | String |
| - `azureOpenAIDeploymentName` | Name of the specific deployment to use. | String|

### Managed identity
The Groundedness detection API provides the option to include _reasoning_ in the API response. If you opt for reasoning, you must either utilize your own GPT resources or use our provided default GPT resources. In this case, the response will include an additional reasoning value. This value details specific instances and explanations for any detected ungroundedness. If you choose not to receive reasoning, the API will classify the submitted content as `true` or `false` and provide a confidence score.

To allow your Content Safety resource to access Azure OpenAI resources using a managed identity, you'd typically follow these steps.

 1. Enable Managed Identity for Azure AI Content Safety.

Navigate to your Azure AI Content Safety instance in the Azure portal. Find the "Identity" section under the "Settings" category. Enable the system-assigned managed identity. This action grants your Azure AI Content Safety instance an identity that can be recognized and used within Azure for accessing other resources. 

  ![image](https://github.com/Azure/Azure-AI-Content-Safety-Private-Preview/assets/36343326/dfa6677f-1c13-4a80-9c1b-f0b2c19b849f)

 2. Assign Role to Managed Identity.

Navigate to your Azure AI Content Safety instance, click on "Add role assignment" to start the process of assigning a role to the Azure AI Content Safety managed identity. Choose a role that grants the necessary permissions for the tasks you want to perform. Based on your needs, this could be "Contributor" or "User". The specific roles and permissions might vary based on what you're looking to achieve.
  ![image](https://github.com/Azure/Azure-AI-Content-Safety-Private-Preview/assets/36343326/0bdab704-2825-4a78-b9b4-56e72aa19718)

  ![image](https://github.com/Azure/Azure-AI-Content-Safety-Private-Preview/assets/36343326/5df9be34-0929-4dfa-8e5a-edfd653d0e02)
   

### Output

```json
{
    "ungrounded": true,
    "confidenceScore": 1,
    "ungroundedPercentage": 1,
    "ungroundedDetails": [
     {
        "text": "string",
        "offset": {
        "utf8": 0,
        "utf16": 0,
        "codePoint": 0
      },
        "length": {
        "utf8": 0,
        "utf16": 0,
        "codePoint": 0
      },
      "reason": "string"
    }
  ]
}
```


| Name                | Description                                                  | Type    |
| :------------------ | :----------------------------------------------------------- | ------- |
| **ungrounded**        | Indicates whether the text exhibits ungroundedness.  | Boolean    |
| **confidenceScore** | The confidence value of the _ungrounded_ designation. The score will range from 0 to 1.	 | Float	 |
| **ungroundedPercentage** | Specifies the proportion of the text identified as ungrounded, expressed as a number between 0 and 1, where 0 indicates no ungrounded content and 1 indicates entirely ungrounded content.| Float	 |
| **ungroundedDetails** | Provides insights into ungrounded content with specific examples and percentages.| String |
| -**`Text`**   |  The specific text that is ungrounded.  | String   |
| -**`offset`**   |  An object describing the position of the ungrounded text in various encoding.  | String   |
| - `offset > utf8`       | The offset position of the ungrounded text in UTF-8 encoding.             | number                                                                                |
| - `offset > utf16`      | The offset position of the ungrounded text in UTF-16 encoding.              | number                                                                              |
| - `offset > codePoint`  | The offset position of the ungrounded text in terms of Unicode code points.               |number                                                                   |
| -**`length`**   |  An object describing the length of the ungrounded text in various encoding. (utf8, utf16, codePoint), similar to the offset. | String   |
| - `length > utf8`       | The length of the ungrounded text in UTF-8 encoding.             | number                                                                                |
| - `length > utf16`      | The length of the ungrounded text in UTF-16 encoding.              | number                                                                              |
| - `length > codePoint`  | The length of the ungrounded text in terms of Unicode code points.               |number                                                                   |
| -**`Reason`** |  Offers explanations for detected ungroundedness. | String  |

##  📝 Sample Code 
### Python

Python sample request:

```Python

import http.client
import json

conn = http.client.HTTPSConnection("<Endpoint>/contentsafety/text:detectGroundedness?api-version=2024-02-15-preview")
payload = json.dumps({
  "domain": "Generic",
  "task": "QnA",
  "qna": {
    "query": "How much does she currently get paid per hour at the bank?"
  },
  "text": "12/hour",
  "groundingSources": [
    "I'm 21 years old and I need to make a decision about the next two years of my life. Within a week. I currently work for a bank that requires strict sales goals to meet. IF they aren't met three times (three months) you're canned. They pay me 10/hour and it's not unheard of to get a raise in 6ish months. The issue is, **I'm not a salesperson**. That's not my personality. I'm amazing at customer service, I have the most positive customer service \"reports\" done about me in the short time I've worked here. A coworker asked \"do you ask for people to fill these out? you have a ton\". That being said, I have a job opportunity at Chase Bank as a part time teller. What makes this decision so hard is that at my current job, I get 40 hours and Chase could only offer me 20 hours/week. Drive time to my current job is also 21 miles **one way** while Chase is literally 1.8 miles from my house, allowing me to go home for lunch. I do have an apartment and an awesome roommate that I know wont be late on his portion of rent, so paying bills with 20hours a week isn't the issue. It's the spending money and being broke all the time.\n\nI previously worked at Wal-Mart and took home just about 400 dollars every other week. So I know i can survive on this income. I just don't know whether I should go for Chase as I could definitely see myself having a career there. I'm a math major likely going to become an actuary, so Chase could provide excellent opportunities for me **eventually**."
  ],
  "reasoning": False
})
headers = {
  'Ocp-Apim-Subscription-Key': '<your_subscription_key>',
  'Content-Type': 'application/json'
}
conn.request("POST", "/contentsafety/text:detectGroundedness?api-version=2024-02-15-preview", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))
```

### C#

C# sample request:

```csharp
var client = new HttpClient();
var request = new HttpRequestMessage(HttpMethod.Post, "<Endpoint>/contentsafety/text:detectGroundedness?api-version=2024-02-15-preview");
request.Headers.Add("Ocp-Apim-Subscription-Key", "<your_subscription_key>");
var content = new StringContent("{\r\n    \"domain\": \"Generic\",\r\n    \"task\": \"QnA\",\r\n    \"qna\": {\r\n        \"query\": \"How much does she currently get paid per hour at the bank?\"\r\n    },\r\n    \"text\": \"12/hour\",\r\n    \"groundingSources\": [\"I'm 21 years old and I need to make a decision about the next two years of my life. Within a week. I currently work for a bank that requires strict sales goals to meet. IF they aren't met three times (three months) you're canned. They pay me 10/hour and it's not unheard of to get a raise in 6ish months. The issue is, **I'm not a salesperson**. That's not my personality. I'm amazing at customer service, I have the most positive customer service \\\"reports\\\" done about me in the short time I've worked here. A coworker asked \\\"do you ask for people to fill these out? you have a ton\\\". That being said, I have a job opportunity at Chase Bank as a part time teller. What makes this decision so hard is that at my current job, I get 40 hours and Chase could only offer me 20 hours/week. Drive time to my current job is also 21 miles **one way** while Chase is literally 1.8 miles from my house, allowing me to go home for lunch. I do have an apartment and an awesome roommate that I know wont be late on his portion of rent, so paying bills with 20hours a week isn't the issue. It's the spending money and being broke all the time.\\n\\nI previously worked at Wal-Mart and took home just about 400 dollars every other week. So I know i can survive on this income. I just don't know whether I should go for Chase as I could definitely see myself having a career there. I'm a math major likely going to become an actuary, so Chase could provide excellent opportunities for me **eventually**.\"],\r\n    \"reasoning\":false\r\n    }", null, "application/json");
request.Content = content;
var response = await client.SendAsync(request);
response.EnsureSuccessStatusCode();
Console.WriteLine(await response.Content.ReadAsStringAsync());

```

### Java

Java sample request:. 

```java
OkHttpClient client = new OkHttpClient().newBuilder()
  .build();
MediaType mediaType = MediaType.parse("application/json");
RequestBody body = RequestBody.create(mediaType, "{\r\n    \"domain\": \"Generic\",\r\n    \"task\": \"QnA\",\r\n    \"qna\": {\r\n        \"query\": \"How much does she currently get paid per hour at the bank?\"\r\n    },\r\n    \"text\": \"12/hour\",\r\n    \"groundingSources\": [\"I'm 21 years old and I need to make a decision about the next two years of my life. Within a week. I currently work for a bank that requires strict sales goals to meet. IF they aren't met three times (three months) you're canned. They pay me 10/hour and it's not unheard of to get a raise in 6ish months. The issue is, **I'm not a salesperson**. That's not my personality. I'm amazing at customer service, I have the most positive customer service \\\"reports\\\" done about me in the short time I've worked here. A coworker asked \\\"do you ask for people to fill these out? you have a ton\\\". That being said, I have a job opportunity at Chase Bank as a part time teller. What makes this decision so hard is that at my current job, I get 40 hours and Chase could only offer me 20 hours/week. Drive time to my current job is also 21 miles **one way** while Chase is literally 1.8 miles from my house, allowing me to go home for lunch. I do have an apartment and an awesome roommate that I know wont be late on his portion of rent, so paying bills with 20hours a week isn't the issue. It's the spending money and being broke all the time.\\n\\nI previously worked at Wal-Mart and took home just about 400 dollars every other week. So I know i can survive on this income. I just don't know whether I should go for Chase as I could definitely see myself having a career there. I'm a math major likely going to become an actuary, so Chase could provide excellent opportunities for me **eventually**.\"],\r\n    \"reasoning\":false\r\n    }");
Request request = new Request.Builder()
  .url("<Endpoint>/contentsafety/text:detectGroundedness?api-version=2024-02-15-preview")
  .method("POST", body)
  .addHeader("Ocp-Apim-Subscription-Key", "<your_subscription_key>")
  .addHeader("Content-Type", "application/json")
  .build();
Response response = client.newCall(request).execute();
```

## Key reference 

- [Content Safety Doc](https://aka.ms/acs-doc)


## We're here to help!

If you get stuck, [shoot us an email](mailto:rai_hdms@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! 

