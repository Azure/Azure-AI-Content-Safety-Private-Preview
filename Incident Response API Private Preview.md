# Incident Response API Private Preview Documentation ![informational](https://shields.io/badge/-PrivatePreview-PrivatePreview)

Incident response in content moderation scenario is the process of identifying, analyzing, containing, eradicating, and recovering from cyber incidents that involve inappropriate or harmful content on online platforms. For any new incidents, users could use the incident response features from Azure AI Content Safety to mitigate the new incidents quickly.

Incident response provides a set of APIs to help users mitigate incidents within short time, [Blocklist](https://learn.microsoft.com/azure/ai-services/content-safety/how-to/use-blocklist) as one solution of that but only provides with exact match, this new release we are bringing in advanced capabilities for text semantic match, and image matching capability.

For this advanced text and image incident response, you could easily define an incident with few samples which are under one specific topic, and similar content will be detected in analyze API. 

Note: This new feature is only available in East US and Sweden Central

## ⚠️ Disclaimer

The sample code could have offensive content, user discretion is advised.

## 📒 Overview

- **How It Works** contains instructions for using the service in more general ways.
- **Sample Code** shows sample requests using the cURL, Python.
- **Limitations** goes over the limitations of this feature.


## How it works
[place_hodler]

### Text incident response

#### Step 1. Create an incident

```shell
curl --location --request PATCH 'https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "incidentName": "text-incident-name",
  "description": "string"
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentName": "text-incident-name",
  "description": "string"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)

print(response.text)
```

#### Step 2. Add samples to the incident

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents/text-incident-name:addIncidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data-raw '{
  "incidentSamples": [
    { "text":      "COCKSUCKER BEFORE YOU PISS AROUND ON MY WORK"},
    { "text":"@: nobody cares about the Fucking Shit like you, fucking bitch........................ 5.9.97.199"},
    { "text":      "FUCK \nYou little bitch the cowboys have no testes"},
    { "text":"And your a dick sucker dabomb you want a big juicy jizzBOMB in your mouth."},
    { "text":"Whatever, dumbass. \n\nGo eat Jimbo'\''s pussy."},
    { "text":"you are a senile old homosexual==\n\nyou need to go to Oz to get a fucking brain \n\n=="},
    { "text":"STANDAHL ARE YOU A MAN OR A MOUSESTACHE?\n\nWHY DON'\''T YOU RESPOND.\n\nARE YOU SCARED OF THE APPROPRIATE FEDERAL AGENCIES WHO ARE ACTIVELY WATCHING YOUR ACTS?"},
    { "text":", I hope you'\''re on the next plane just so we can erase all record of what they did to you the way you are trying to revise this history.  Asshole."},
    { "text":"I very much doubt that you can describe an undoubted POV vandal such as User:Vintagekits as '\''editing in good faith'\''. Just ignore these stupid Admins"},
    { "text":"Hey, Halcy.Seems like you get mad alot. Want me to call the WAAAAAMBULANCE for you? Want some dick (extra small) with that too, bitch? U mad? butthurt? I bet you'\''re having an orgy with MeetTheMedic and MeepTheSheep, aren'\''t you? You three would make a good threesome. You'\''re all reject 4-Chan trolls that became admins on another website to have Unwarranted Self Importance while you spam faggot and dick all day. Seems like you enjoy that kind of stuff. I had no idea, really.\n \nTL;DR: U mad?"},
    { "text":"Better late then ever. \n\nGood riddance, militant freak."}
  ]
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name:addIncidentSamples?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentSamples": [
    {
      "text": "COCKSUCKER BEFORE YOU PISS AROUND ON MY WORK"
    },
    {
      "text": "@: nobody cares about the Fucking Shit like you, fucking bitch........................ 5.9.97.199"
    },
    {
      "text": "FUCK \nYou little bitch the cowboys have no testes"
    },
    {
      "text": "And your a dick sucker dabomb you want a big juicy jizzBOMB in your mouth."
    },
    {
      "text": "Whatever, dumbass. \n\nGo eat Jimbo's pussy."
    },
    {
      "text": "you are a senile old homosexual==\n\nyou need to go to Oz to get a fucking brain \n\n=="
    },
    {
      "text": "STANDAHL ARE YOU A MAN OR A MOUSESTACHE?\n\nWHY DON'T YOU RESPOND.\n\nARE YOU SCARED OF THE APPROPRIATE FEDERAL AGENCIES WHO ARE ACTIVELY WATCHING YOUR ACTS?"
    },
    {
      "text": ", I hope you're on the next plane just so we can erase all record of what they did to you the way you are trying to revise this history.  Asshole."
    },
    {
      "text": "I very much doubt that you can describe an undoubted POV vandal such as User:Vintagekits as 'editing in good faith'. Just ignore these stupid Admins"
    },
    {
      "text": "Hey, Halcy.Seems like you get mad alot. Want me to call the WAAAAAMBULANCE for you? Want some dick (extra small) with that too, bitch? U mad? butthurt? I bet you're having an orgy with MeetTheMedic and MeepTheSheep, aren't you? You three would make a good threesome. You're all reject 4-Chan trolls that became admins on another website to have Unwarranted Self Importance while you spam faggot and dick all day. Seems like you enjoy that kind of stuff. I had no idea, really.\n \nTL;DR: U mad?"
    },
    {
      "text": "Better late then ever. \n\nGood riddance, militant freak."
    }
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

#### Step 3. Analyze text with incident response

```shell
curl --location 'https://<endpoint>/contentsafety/text:analyze?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "text":  "COCKSUCKER BEFORE YOU PISS AROUND ON MY WORK",
  "incidents": {
    "incidentNames": [
      "text-incident-name"
    ],
    "haltOnIncidentHit": true
  }
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/text:analyze?api-version=2023-10-30-preview"

payload = json.dumps({
  "text": "COCKSUCKER BEFORE YOU PISS AROUND ON MY WORK",
  "incidents": {
    "incidentNames": [
      "text-incident-name"
    ],
    "haltOnIncidentHit": True
  }
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

### Image incident response

#### Step 1. Create an incident

```shell
curl --location --request PATCH 'https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "incidentName": "image-incident-name",
  "description": "string"
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentName": "image-incident-name",
  "description": "string"
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("PATCH", url, headers=headers, data=payload)

print(response.text)

```

#### Step 2. Add samples to the incident

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents/image-incident-name:addIncidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "incidentSamples": [
    {
      "image": {
        "content": "",
        "blobUrl": "https://cmbugbashsampledata.blob.core.windows.net/image-sample/cm_bugbash/safe/safe-incident-sample-image.png"
      }
    }
  ]
}'
```

```python
import requests
import json

url = "https:/<endpoint>/contentsafety/image/incidents/image-incident-name:addIncidentSamples?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentSamples": [
    {
      "image": {
        "content": "",
        "blobUrl": "https://cmbugbashsampledata.blob.core.windows.net/image-sample/cm_bugbash/safe/safe-incident-sample-image.png"
      }
    }
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

#### Step 3. Analyze image with incident response

```shell
curl --location 'https://<endpoint>/contentsafety/image:analyze?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
    "image":
        {
        "blobUrl": "https://cmbugbashsampledata.blob.core.windows.net/image-sample/cm_bugbash/safe/safe-incident-sample-image.png"
        },
    "categories": [
        "SelfHarm",
        "Sexual"
    ],
   "outputType": "FourSeverityLevels",
  "incidents": {
    "incidentNames": [
      "image-incident-name"
    ],
    "haltOnIncidentHit": true
  }
}'
```


```python
import requests
import json

url = "https://<endpoint>/contentsafety/image:analyze?api-version=2023-10-30-preview"

payload = json.dumps({
  "image": {
    "blobUrl": "https://cmbugbashsampledata.blob.core.windows.net/image-sample/cm_bugbash/safe/safe-incident-sample-image.png"
  },
  "categories": [
    "SelfHarm",
    "Sexual"
  ],
  "outputType": "FourSeverityLevels",
  "incidents": {
    "incidentNames": [
      "image-incident-name"
    ],
    "haltOnIncidentHit": True
  }
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)

```

## Sample Code 

### Other Text Incident API

#### Get the incidents list

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/text/incidents?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident details

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Delete the incident

```shell
curl --location --request DELETE 'https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident sample list

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents/text-incident-name/incidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name/incidentSamples?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident sample details

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents/text-incident-name/incidentSamples/00e63d3f-54a6-4495-8191-6020923ca789?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name/incidentSamples/00e63d3f-54a6-4495-8191-6020923ca789?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Delete the incident sample

```shell
curl --location 'https://<endpoint>/contentsafety/text/incidents/text-incident-name:removeIncidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "incidentSampleIds": [
    "00e63d3f-54a6-4495-8191-6020923ca789"
  ]
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/text/incidents/text-incident-name:removeIncidentSamples?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentSampleIds": [
    "00e63d3f-54a6-4495-8191-6020923ca789"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

### Other Image Incident API

#### Get the incidents list

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/image/incidents?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident details

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Delete the incident

```shell
curl --location --request DELETE 'https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("DELETE", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident sample list

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents/image-incident-name/incidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name/incidentSamples?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Get the incident sample details

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents/image-incident-name/incidentSamples/00e63d3f-54a6-4495-8191-6020923ca789?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>'
```

```python
import requests

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name/incidentSamples/00e63d3f-54a6-4495-8191-6020923ca789?api-version=2023-10-30-preview"

payload = {}
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>'
}

response = requests.request("GET", url, headers=headers, data=payload)

print(response.text)
```

#### Delete the incident sample

```shell
curl --location 'https://<endpoint>/contentsafety/image/incidents/image-incident-name:removeIncidentSamples?api-version=2023-10-30-preview' \
--header 'Ocp-Apim-Subscription-Key: <api_key>' \
--header 'Content-Type: application/json' \
--data '{
  "incidentSampleIds": [
    "00e63d3f-54a6-4495-8191-6020923ca789"
  ]
}'
```

```python
import requests
import json

url = "https://<endpoint>/contentsafety/image/incidents/image-incident-name:removeIncidentSamples?api-version=2023-10-30-preview"

payload = json.dumps({
  "incidentSampleIds": [
    "00e63d3f-54a6-4495-8191-6020923ca789"
  ]
})
headers = {
  'Ocp-Apim-Subscription-Key': '<api_key>',
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data=payload)

print(response.text)
```

## Limitations
[place_hodler]