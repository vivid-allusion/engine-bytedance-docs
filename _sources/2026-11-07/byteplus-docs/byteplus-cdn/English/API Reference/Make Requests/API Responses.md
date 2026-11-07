---
title: "API Responses"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-api-request-reponses"
---

This document describes how the BytePlus CDN responds to API requests.

<span id="response-status-code"></span>
## Response status code

The response status codes of CDN are described as follows:


* 2xx: Indicates that the CDN has successfully responded to the API request. But a successful response does not necessarily guarantee that the API request was successful. See [Determine whether the API request is successful](https://docs.byteplus.com/en/docs/18/6814#determine-whether-the-api-request-is-successful).

* 4xx: Indicates that the content distribution network cannot return the content requested by the client. The reason is that the client request is invalid. For example:

* The requested file does not exist.

* The request method is incorrect.

* A required parameter is missing from the request. For example the `Action` parameter is missing.

* The requester does not have permission to operate the target resource.

* 5xx: Indicates that the request has failed. The failure was due to an internal error with the Content Delivery Network. For example, the Content Delivery Network service is unavailable.


<span id="determine-whether-an-api-request-is-successful"></span>
## Determine whether an API request is successful

It is not recommended that you use CDN response status codes when you determine whether an API request was successful. We recommend that you use the following criteria:


* If an API request is successful, the `ResponseMetadata` structure of the response body does not contain an `Error` field.

* The rest of the cases are considered request failures. You can find the corresponding error message in the `Error` field of the `ResponseMetadata` structure.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Your API request may encounter the following:</div>



* <div data-tips="true" data-tips-type="tip">The CDN response status code is 2xx, but the <code>ResponseMetadata</code> structure contains an <code>Error</code> field.</div>



<div data-tips="true" data-tips-type="tip">In this case, the API request is a failure. The reason is that the client request does not satisfy the configuration in the CDN. For example:</div>



* <div data-tips="true" data-tips-type="tip">The value of a request parameter is invalid.</div>


* <div data-tips="true" data-tips-type="tip">When you configure a certificate for an accelerated domain name, the certificate file does not contain the complete certificate chain.</div>



For common errors in CDN, see [API Error Codes](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-api-error-codes).

<span id="response-example"></span>
## Response example

<span id="example-response-to-a-successful-api-request"></span>
### Example response to a successful API request

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {...}
}
```


<span id="example-response-to-a-failed-api-request"></span>
### Example response to a failed API request

```json
{
    "ResponseMetadata": {
        "RequestId": "2021041510110201022510703416005FB0",
        "Action": "DescribeCdnData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore",
        "Error": {
            "Code": "ResourceNotFound",
            "Message": "resource is not found"
        }
    }
}
```
