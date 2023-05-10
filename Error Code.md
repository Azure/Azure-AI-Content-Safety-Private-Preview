# Content Safety Error codes and response codes

The content APIs may return the following error codes:

| Error Code          | Possible reasons                                             | Suggestions                                                  |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| InvalidRequestBody  | One or more fields in the request body does not match the API definition. | 1. Check the API version you specified in the API call.                                                           2. Check the corresponding API definition for the API version you selected. |
| InvalidResourceName | The resource name you specified in the URL does not meet the requirements, like the blocklist name, blocklist term id, etc. | 1. Check the API version you specified in the API call.  2. Check whether the given name has invalid characters according to the API definition. |
| ResourceNotFound    | The resource you specified in the URL may not exist, like the blocklist name. | 1. Check the API version you specified in the API call.  2. Double check the existence of the resource specified in the URL. |
| InternalError       | Some unexpected situations in the server side have been triggered. | 1. You may want to retry a few times after a small period and see it the issue will happen again.               2. Contact the Azure Support if this issue persists. |
| ServerBusy          | The server side cannot process the request temporarily.      | 1. You may want to retry a few times after a small period and see it the issue will happen again.  2.Contact the Azure Support if this issue persists. |
| TooManyRequests     | The current RPS has exceeded the quota for your current SKU. | 1. Check the pricing table to understand the RPS quota.                                                                            2.Contact the Azure Support if you need more QPS. |

The content APIs may return the following HTTP response codes:

| Response code | Description                                                  |
| :------------ | :----------------------------------------------------------- |
| `200`         | OK - Standard response for successful HTTP requests.         |
| `201`         | Created - The request has been fulfilled, resulting in the creation of a new resource. |
| `204`         | No content - The server successfully processed the request, and isn't returning any content. Usually this is returned for the DELETE operation. |
| `400`         | Bad request – The server can't process the request due to a client error (for example, malformed request syntax, size too large, invalid request message framing, or deceptive request routing). |
| `401`         | Unauthorized – Authentication is required and has failed.    |
| `403`         | Forbidden – User not having the necessary permissions for a resource. |
| `404`         | Not found - The requested resource couldn't be found.        |
| `429`         | Too many requests – The user has sent too many requests in a given amount of time. Refer to "Quota Limit" section for limitations. |
| `500`         | Internal server error – An unexpected condition was encountered on the server side. |
| `503`         | Service unavailable – The server can't handle the request temporarily. Try again at a later time. |
| `504`         | Gateway time out – The server didn't receive a timely response from the upstream service. Try again at a later time. |