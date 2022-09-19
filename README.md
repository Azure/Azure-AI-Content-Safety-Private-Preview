# 📝 Content Moderator Documentation
Content moderation is a process that involves simple steps. Reviewing, monitoring, and interpretation of content before it is displayed or released for general consumption is a form of moderation. Having a large amount of content to moderate can be time consuming. Using a service, such as Content Moderator, you can automate much of this process and set up the need for human review as appropriate.

The Content Moderator service is an API that is powered by artificial intelligence, and runs on Azure. The service is capable of scanning text, image for potential risky, offensive, or undesirable aspects. It will apply content flags automatically.

## Overview 

This documentation contains the following article types:

- [**Quickstarts**](https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/client-libraries) are getting-started instructions to guide you through making requests to the service.
- [**How-to guides**](https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/try-text-api) contain instructions for using the service in more specific or customized ways.
- [**Concepts**](https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/text-moderation-api) provide in-depth explanations of the service functionality and features.
- [**Tutorials**](https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/ecommerce-retail-catalog-moderation) are longer guides that show you how to use the service as a component in broader business solutions.

## 🚦When to use Content Moderator

There may be many scenarios where content moderation is required. We present a few considerations here that offer insight into some application of Content Moderator. Using these scenarios, you may come up with other ideas on how you might integrate the Content Moderator API into your applications.

### Community support forums

Your company may sell products and/or services that require support options. Perhaps you host support forums online, you may want to ensure that the content, posted on these forums, is family-friendly and doesn't contain objectionable content. You could use content moderator to scan the text of posts before you publish them. If you allow uploading of images, Content Moderator can also scan the images to ensure they are appropriate.

You might even decide to create a custom list of terms that could help identify online bullying. Use of moderation here, can help you maintain a friendly and supportive forum for your products and services, and increase customer satisfaction with your company.

### Chat rooms

Perhaps you operate online chat rooms for your gaming platforms. You may want to moderate the content that is posted in these rooms to ensure it meets your acceptable use policies. These policies can dictate acceptable content that is not rude, not racist, doesn't contain sexually explicit material, etc.

### Online company review sites

You may host an independent review site that permits posts that review companies, organizations, and products. Review sites that are not moderated, could contain objectionable material that is not appropriate for all audiences but even more so, could result in your company being held liable for the material that is posted there.





### 🚦Who to build with Content Moderator

Publishers, platforms, and individuals can use content moderator to power a variety of text-based conversations. Developers integrate our API for many different audiences.

Moderators use Content Moderator to quickly prioritize and review comments that have been reported.

Developers create tools so readers can control which comments they see, like hiding comments.





# 📈How Content Moderator works

Using the Content Moderator service requires an Azure subscription and a Content Moderator resource. The resource is required for accessing the service and provides the endpoint and access key for the service.

Microsoft provides a free pricing tier that you can use to test the service. Using the free tier, you can determine if the Content Moderator service is the right choice for your organization.

The Content Moderator service can be accessed through REST. 

## The APIs

There are different types of APIs available in Content Moderator. The following table describes the current available API.

| API             | Functionality                                                |
| :-------------- | :----------------------------------------------------------- |
| Text Moderation | Scans text for offensive, sexually explicit or suggestive, profanity, and personal data aspect |

Type a sentence into the box to see its  categories' score. Perspective returns a percentage that represents the likelihood that someone will perceive the text as toxic.

### Input

When submitting a moderation task, you’ll need to provide **raw text** sourced from your content as an input to the Content Moderator API. Externally hosted content such as links to comments and posts are not readable by the text moderation API.

> ### 🚧NOTE:
>
> The default maximum length for text submissions is 1024 characters. If you need to analyze longer blocks of text, you can split the input text (e.g., using punctuation or spacing) across multiple related submissions.

## Submission

You can submit tasks to Content Moderator API endpoints in two ways: **synchronously** or **asynchronously**. This section will focus on synchronous submission, which is preferable for most text moderation users.

Synchronous submission is optimized for real-time moderation needs. If you have a constant stream of tasks and need responses quickly, you’ll want to use synchronous submission - the Content Moderator API will return model outputs directly in the response message.

Once you’ve extracted raw text from your content, you can use the following code template to populate requests to the Content Moderator text moderation API with text strings programmatically and access model responses for analysis.

Python

```json
# Imports:
import requests # Used to call most Content Moderater APIs

# Inputs:
API_Key = 'your_textAPI_key' # The unique API Key for your text project 

def get_Content Moderater_response(input_text): 
    headers = {'Authorization': f'Token {API_Key}'} 
    data = {'text_data': input_text} # Must be a string. This is also where you would insert metadata if desired.
    # Submit request to the synchronous API endpoint. 
    response = requests.post('https://api.theContent Moderater.ai/api/v2/task/sync', headers=headers, data=data) 
    response_dict = response.json()
    return response_dict

def handle_Content Moderater_classifications(response_dict):
    # Parse model response JSON for model classifications and use for moderation.
    # See a basic example implementation in the last section. 
    pass

def handle_Content Moderater_patternmatch(response_dict):
    # Parse model response JSON for pattern matches/text filters and use for moderation.
    # See a basic example implementation in the last section
    pass
```



For synchronous requests, the Content Moderator API will generally return a response within **100 ms** for a typical short message string and within **500 ms** for a max length (1024 character) submission.

> ### 🚧NOTE:
>
> If you are planning to submit large numbers of tasks concurrently, asynchronous submission may be more suitable. In this case, you’ll also need to provide a callback URL (e.g., webhook) to which the API can send a POST request once results have finished processing. Syntax for submitting tasks asynchronously and more info is available on our [API reference](https://docs.theContent Moderator.ai/reference/submit-a-task-asynchronously). If you need help determining the best way to submit your volume, please feel free to contact [support@theContent Moderator.ai](mailto:support@theContent Moderator.ai).

### Response

Content Moderator APIs do not remove your content or ban users itself. Rather, the Content Moderator API will return classification metrics from our models as a **JSON object** that details the type(s) of sensitive subject matter in the submitted text and a score indicating severity. You can use this to take appropriate actions based on your content policies.

To see what this might look like for your moderation needs, it may be helpful to walk through an example model response.

### Model Response Format & Severity Classifications

For moderation purposes, you’ll want to focus on the classifications and severity scores for input text given in the model response object. Our text model can identify speech in five main ***classes\***:

- ***sexual\*** - explicit sexual descriptions, suggestive or flirtatious language, sexual insults
- ***hate\*** - slurs, negative stereotypes or jokes about protected groups, hateful ideology
- ***violence\*** - descriptions of violence, threats, incitement
- ***spam\*** - text such as links or phone numbers intended to redirect to another platform
- ***bullying\*** - threats or insults against specific individuals, encouraging self-harm, exclusion

We also offer a ***promotions\*** class upon request, which captures asking for donations, advertising products or services, soliciting for likes, follows, or shares etc.

Our model predictions will include a **severity score** for each class ranging from 0 to 1. 

Here’s what the response portion of the object returned by the Content Moderator API actually looks like - some fields have been truncated for clarity:

JSON

```json
"response": {
      .
      .
      .

      "language": "EN",
      "moderated_classes": [
        "sexual",
        "hate",
        "violence",
        "bullying",
        "spam"
      ],
      "output": [
        {
          "time": 0,
          "start_char_index": 0,
          "end_char_index": 110,
          "classes": [
            {
              "class": "spam",
              "score": 3
            },
            {
              "class": "sexual",
              "score": 2
            },
            {
              "class": "hate",
              "score": 0
            },
            {
              "class": "violence",
              "score": 0
            },
            {
              "class": "bullying",
              "score": 0
            }
          ]
        }
      ]
    }
```

Our model assigns severity scores based on an interpretation of full phrases and sentences in context. As an example, the model would score text that includes a slur as 1 for hate, but text that references a negative stereotype without overtly offensive language as a 0.

Text moderation supports many commonly used languages, but the supported moderation classes for each language varies. If model classifications are not supported for a language detected in the text, the score for that class will be -1. You can find a full description of our current language support [here](https://docs.theContent Moderator.ai/docs/classification-text#supported-languages).



## Profanity and Personal Identifiable Information (PII)

Content Moderator models also include a **pattern-matching** feature that will search input text for pre-defined words, phrases, or formats and return any exact matches. This can complement model classifications to provide additional insights into your text content. Currently, **profanity** and **personal information (PII)** such as email addresses, phone numbers and addresses are flagged by default.

> ### 📘NOTE:
>
> You can also add custom rules for other words and phrases you’d like to monitor within the project dashboard, though some (e.g., slurs) will be picked up by classification results. Additionally, the project dashboard allows you to whitelist words or phrases that Content Moderator flags by default. More information on setting up custom pattern-matching rules is available [here](https://docs.theContent Moderator.ai/docs/classification-text#pattern-matching-algorithms).

Here’s what pattern-matching results will look like within the model response object (classification section truncated for clarity):

JSON

```json
"response": {
      "input": "..."
      "custom_classes": [],
      "text_filters": [
        {
          "value": "ASS",
          "start_index": 107,
          "end_index": 110,
          "type": "profanity"
        }
      ],
      "pii_entities": [
        {
          "value": "JON.SMITH@GMAIL.COM",
          "start_index": 38,
          "end_index": 57,
          "type": "Email Address"
        },
        {
          "value": " 617-768-2274.",
          "start_index": 80,
          "end_index": 94,
          "type": "U.S. Phone Number"
        }
      ],
      .
      .
      .
```

Pattern-matching results include indices representing the location of the match within the input string. You can use these indices to modify or filter your text content as desired.



### What To Do With Our Results

Once you have decided on a content policy and what enforcement actions you want to take, you can design custom moderation logic that implements your policy based on severity scores pulled from the model response object.

Here’s a simple example of moderation logic that defines restricted classes and then flags text that scores at the highest severity in any of those classes. This might reflect a content policy that allows controversial text content (e.g., score 2) but moderates the most harmful content in each class.

Python

```python
# Inputs 
severity_threshold = 3 # Severity score at which text is flagged or moderated, configurable.
restricted_classes = ['sexual','hate','violence','bullying','spam'] # Select classes to monitor

def handle_Content Moderater_classifications(response_dict):
    # Create a dictionary where the classes are keys and the scores their respective values. 
    scores_dict = {x['class']:x['score'] for x in response_dict['status'][0]['response']['output'][0]['classes']}
    for ea_class in restricted_classes:
        if scores_dict[ea_class] >= severity_threshold:
            print('We should ban this guy!')
            # This is where you would call your real moderation actions to tag or delete posts, ban users etc. 
            print(str(ea_class) + ': ' + str(scores_dict[ea_class]))
            break
```

When designing your enforcement logic, you will need to decide whether to moderate each class at level 1, level 2, or level 3 depending on your community guidelines and risk sensitivity.

> ### 🚧IMPORTANT:
>
> Because all platforms have different needs, we ***strongly\*** encourage you to consult our [text model description](https://docs.theContent Moderator.ai/docs/classification-text#multilevel-model) as you consider which classes to moderate and at what severity. Here you’ll find descriptive examples of each severity level for each class. We’re happy to provide more guidance or real examples if you need them.

You can experiment with defining different thresholds for different classes, or build in different moderation actions for different classes depending on severity. For example, a dating platform with messaging capabilities might choose to allow sexual content scoring a 2 but moderate text that scores a 2 in other classes.

Here’s another simple function you can use to parse the response object for pattern-matching results and take action on any matches.

Python

```python
def handle_Content Moderater_patternmatch(response_dict):
    pm_dict = {x['type']:x['value'] for x in response_dict['status'][0]['response']
    if pm_dict = False
        pass # Do nothing if text filters, PII entities, and custom classes are all empty
    else
        print('Filter match') # Insert your moderation logic here
        for type_i in pm_dict
            print(str(type_i) + ': ' + str(pm_dict[type_i]))
```

This will do nothing if no text filters are triggered but can flag any exact matches, which you can use to take any desired moderation actions. In real moderation contexts, you may wish to combine pattern-matching results with additional insights about the user. For example, profanity can be moderated based on age, while certain PII entities can be moderated based on a number of similar messages posted.





## Language availability

The API is free and available to use in English. The team is constantly developing models to support new languages.

## Moderating text

You can call a single method in the API, **Moderate/Text/Detect**, to scan text in a file. You specify the input file and an output file in the method call. The service will scan the text in the file and return the results in the output file. The API will return a JSON formatted result back to the calling application. Using a sample text input of:

"Is this a crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052"

The service will identify some personal data (email, phone, IP, and address). It will also classify the text with a review recommendation.

```json
{
  "OriginalText": "Is this a crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052",
  "NormalizedText": "   crap email abcdef@abcd.com, phone: 6657789887, IP: 255.255.255.255, 1 Microsoft Way, Redmond, WA 98052",
  "Misrepresentation": null,
  "PII": {
    "Email": [{
      "Detected": "abcdef@abcd.com",
      "SubType": "Regular",
      "Text": "abcdef@abcd.com",
      "Index": 21
    }],
    "IPA": [{
      "SubType": "IPV4",
      "Text": "255.255.255.255",
      "Index": 61
    }],
    "Phone": [{
      "CountryCode": "US",
      "Text": "6657789887",
      "Index": 45
    }],
    "Address": [{
      "Text": "1 Microsoft Way, Redmond, WA 98052",
      "Index": 78
    }],
    "SSN": []
  },
  "Classification": {
    "ReviewRecommended": true,
    "Category1": {
      "Score": 0.00040505084325559437
    },
    "Category2": {
      "Score": 0.22345089912414551
    },
    "Category3": {
      "Score": 0.98799997568130493
    }
  },
  "Language": "eng",
  "Terms": [{
    "Index": 3,
    "OriginalIndex": 10,
    "ListId": 0,
    "Term": "crap"
  }],
  "Status": {
    "Code": 3000,
    "Description": "OK",
    "Exception": null
  },
  "TrackingId": "7a6e3717-1382-4b63-a8f4-24922e041f82"
}
```

# Concepts

## 1. Text category

This feature of the API provide scores for several different categories. Here are some of the categories our API can provide scores for:

- **Category 1:** Sexual - Sexual describes language related to anatomical organs and genitals, romantic relationship, acts portrayed in erotic or affectionate terms, pregnancy, physical sexual acts, including those portrayed as an assault or a forced sexual violent act against one’s will, prostitution, pornography and Child Sexual Abuse Material (CSAM).
- **Category 1:** Violence - Violence describes language related to physical actions intended to hurt, injure, damage, or kill someone or something; describes weapons, guns and related entities, such as manufactures, associations, legislation, etc. 
- **Category 2:** Hate - Hate speech is defined as any speech that attacks or uses pejorative or discriminatory language with reference to a person or Identity Group on the basis of certain differentiating attributes of these groups including but not limited to race, ethnicity, nationality, gender identity and expression, sexual orientation, religion, immigration status, ability status, personal appearance and body size.
- **Category 3:** Self-harm- Self-harm describes language related to physical actions intended to purposely hurt, injure, damage one’s body or kill oneself.

To learn more about our ongoing research and experimental models, visit our site.

[LEARN MORE ](https://developers.perspectiveapi.com/s/about-the-api)

When the JSON response is returned, it provides a Boolean value for a recommended review of the text. If `true`, you should review the content manually to determine the potential for any issues.

Each category is also returned with a score between 0 and 1 to indicate the predicted category for the evaluated text. The higher the score, the more likely it is that the category might apply. Here's a sample JSON response:

JSONCopy

```json
"Classification": {
    "ReviewRecommended": true,
    "Category1": {
        "Score": 0.99756889843889822
        },
    "Category2": {
        "Score": 0.12747249007225037
        },
    "Category3": {
        "Score": 0.98799997568130493
    }
}
```

## 2. Personally identifiable information

Personally identifiable information (PII) is of critical importance in many applications. This feature of the API can help you detect if any values in the text might be considered PII before you release it publicly. Key aspects that are detected include:

- Email addresses
- US mailing addresses
- IP addresses
- US phone numbers
- UK phone numbers
- Social Security numbers

If possible PII values are found, the JSON response includes relevant information about the text and the index location within the text. A sample JSON response is shown here:

When designing your enforcement logic, you will need to decide whether to moderate each class at level 1, level 2, or level 3 depending on your community guidelines and risk sensitivity.



JSONCopy

```json
"PII": {
    "Email": [{
        "Detected": "abcdef@abcd.com",
        "SubType": "Regular",
        "Text": "abcdef@abcd.com",
        "Index": 32
        }],
    "IPA": [{
        "SubType": "IPV4",
        "Text": "255.255.255.255",
        "Index": 72
        }],
    "Phone": [{
        "CountryCode": "US",
        "Text": "5557789887",
        "Index": 56
        }, {
        "CountryCode": "UK",
        "Text": "+44 123 456 7890",
        "Index": 208
        }],
    "Address": [{
        "Text": "1 Microsoft Way, Redmond, WA 98052",
        "Index": 89
        }],
    "SSN": [{
        "Text": "999-99-9999",
        "Index": 267
        }]
    }
```





# QuickStart - Test text moderation by using the API 

Before you can begin to test content moderation or integrate it into your custom applications, you need to create and subscribe to a Content Moderator resource and get the subscription key for accessing the resource.

## 1. Create and subscribe to a Content Moderator resource

1. Sign in to the [Azure portal](https://portal.azure.com/).

2. In the left pane, select **Create a resource**.

3. In the search box, enter **Content Moderator**, and then press Enter.

4. From the search results, select **Content Moderator**.

5. Select **Create**.

6. Enter a unique name for your resource, select a subscription, and select a location close to you.

7. Select the pricing tier for this resource, and then select **F0**.

    Note

   If your current subscription is already using a free tier, you will need to choose **S0** for the pricing tier or remove the existing **F0** option.

8. Create a new resource group.

9. Select **Create**.

The resource will take a few minutes to deploy. After it does, go to the new resource.

## 2. Copy the subscription key

To access your Content Moderator resource, you'll need a subscription key:

1. In the left pane, under **RESOURCE MANAGEMENT**, select **Keys and Endpoints**.
2. Copy one of the subscription key values for later use.

## 3. Sample Requests

Now that you have a resource available in Azure for content moderation, and you have a subscription key for that resource, let's run some tests by using the API web-based testing console.

1. Go to the [Content Moderator API Reference page](https://westus.dev.cognitive.microsoft.com/docs/services/57cf753a3f9b070c105bd2c1/operations/57cf753a3f9b070868a1f66f). This page is available in a number of regions for testing in the API console.

2. For the geographic region closest to you, select the appropriate location button to open the console.

3. Note the query parameters that you can select for your test. For the first test run, ensure that the classify option is set to false. Leave the remaining values at their default.Choose the combination of attributes you’d like to use

4. Paste your subscription key into the **Ocp-Apim-Subscription-Key** box.

   ![Paste subscription key into Ocp-Apim-Subscription-Key box.](https://learn.microsoft.com/en-us/training/data-ai-cert/classify-and-moderate-text-with-azure-content-moderator/media/4-exercise-paste-key.png)

5. Leave the sample text in place, and then select **Send**.

## Evaluate the response

This is an example of the returned API response.



**Response Format Reference**

Content Moderator serves three response formats to support its main groups of models:

- [Classification](https://docs.theContent Moderator.ai/reference/classification) — For [Visual](https://docs.theContent Moderator.ai/docs/detection-1) and [Text](https://docs.theContent Moderator.ai/docs/classification-text) classification models.
- [Detection](https://docs.theContent Moderator.ai/reference/detection) — For [Visual Detection](https://docs.theContent Moderator.ai/docs/detection-1) models.
- [Audio](https://docs.theContent Moderator.ai/reference/audio) — For [Speech interpretation](https://docs.theContent Moderator.ai/docs/audiovideotext) models.

The API returns model results in the output object of the JSON response. Within each model type, the output object shares the same format.

A classifier classifies an input (an entire sentence of text) into different categories. It assigns a confidence score for categories.

Classification models can be multi-headed, where each group of mutually exclusive model classes belong to a single model head. For example, when an text is run through text moderation model, one head might classify sexual content while another head might classify the violence.

This concept is illustrated below. This text model has two heads:

- NSFW classification: general_nsfw, general_suggestive, general_not_nsfw_not_suggestive
- Gun classification: gun_in_hand, animated_gun, gun_not_in_hand, no_gun

The confidence scores for each model head sum to 1.

| Name        | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| **time**    | Timestamp in seconds of video or audio frame extracted from the original media. Always 0 for images |
| **classes** | List of objects for each output class that the API predicts. |
| **class**   | Name of predicted class.                                     |
| **score**   | Confidence score of predicted class.                         |

PII



**Pattern-matching algorithm response:**
The pattern-matching algorithm results for profanity are returned in the ***text_filter\*** object. Similarly, pattern-matching algorithm results for PII are returned in the pii_entities object. Each pattern match will return an object describing matched substring in the ***value\*** field, the start and end index of the pattern match in the ***start_index\*** and ***end_index\*** field, respectively, and the ***type\*** (profanity, email, phone number, etc.).

**Deep Learning model classifications:**
The classified language is returned in the ***language\*** object. Based on the classified language, and depending on the currently [supported text moderation model classes](https://docs.theContent Moderator.ai/docs/classification-text#supported-languages), the ***moderated_classes\*** field will indicate which classes have been moderated. If the classified ***language\*** is "UNSUPPORTED", the ***moderated_classes\*** array will be empty. The ***output\*** array will contain the deep learning model results for each supported class.

**Note:** We are aware of an issue where ***start_index\*** and ***end_index\*** may be offset or misaligned relative to the text input in some cases. This can occur if the text input is significantly distorted with non-alphabetic characters, if pattern matching occurs on a subword, or if many characters are repeated on both ends of the text input. We are working to optimize our solution to this issue.











| Name             | Description                                                  |
| :--------------- | :----------------------------------------------------------- |
| classes          | List of dictionaries of all output classes. Each dictionary contains the class name and the score. The scores range from 0 to 3 with 3 being the most severe. |
| class            | Name of predicted class.                                     |
| score            | Score of predicted class.                                    |
| start_char_index | First character processed.                                   |
| end_char_index   | Last character processed.                                    |



You'll see that the email, IP address, phone, and address values are under a JSON array value of PII. You didn't have to set the PII value to true for this result.

## Run additional tests

1. To run the second test, scroll to the top of the page, and set the `classify` parameter to `true`.

2. Select **Send**.

   Note that there is now a new JSON array section title **Classification**. It indicates that a review is recommended and displays three categories with score values. The categories are pertaining to the text content that may be undesirable.

   - Category 1 - content could be sexually explicit or adult related
   - Category 2 - language may be considered sexually suggestive or mature in certain situations
   - Category 3 - potentially offensive language

3. To run additional tests, enter some of your own text values from an existing document, and run the tests again to see the results returned.

4. Study the JSON response and the Request URL syntax to see how your custom applications can call this API.

 Tip

To test this API by using a C# application, see [Quickstart: Analyze text content for objectionable material in C#](https://learn.microsoft.com/en-us/azure/cognitive-services/content-moderator/text-moderation-quickstart-dotnet).

Learn more about attribute scores in [Key Concepts](https://developers.perspectiveapi.com/s/about-the-api-key-concepts).



# Error Codes

## General Error Codes

| HTML Status | Meaning                                                      |
| :---------- | :----------------------------------------------------------- |
| 200         | Ok – everything worked!                                      |
| 400         | Bad request – the request could not be accepted.             |
| 403         | Unauthorized – there is an issue with the API key.           |
| 404         | Not found – the page could not be found.                     |
| 405         | You have insufficient balance in your Hive account.          |
| 429         | Too many requests – you’ve made too many requests to our API, please try again in a few minutes. |
| 500         | Internal service error – we had a problem with our server. Please try again later. |
| 503         | Service unavailable – we are temporarily offline for maintenance. Please try again later. |
| 504         | Gateway timeout – we are not able to fulfil your request at this time. Please try again later. |





#  💬 We're here to help!

If you get stuck, [shoot us an email](mailto:jinruishao@microsoft.com) or use the feedback widget on the upper right of any page.

We're excited you're here! ![:blue-heart:](https://content-moderator.readme.io/img/emojis/blue-heart.png)
