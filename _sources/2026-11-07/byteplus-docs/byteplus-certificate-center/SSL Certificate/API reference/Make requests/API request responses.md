---
title: "API request responses"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/reference-api-request-responses"
---

This document describes how the BytePlus Certificate Center responds to API requests.

## Response status code

The response status codes of BytePlus Certificate Center are described as follows:

* 2xx: Indicates that BytePlus Certificate Center has successfully responded to the API request. But a successful response does not necessarily guarantee that the API request was successful.

* 4xx: Indicates that BytePlus Certificate Center cannot return the content requested by the client. The reason is that the client request is invalid. For example:

   * The requested file does not exist.

   * The request method is incorrect.

   * A required parameter is missing from the request. For example, the `Action` parameter is missing.

   * The requester does not have permission to operate the target resource.

* 5xx: Indicates that the request has failed. The failure was due to an internal error with BytePlus Certificate Center. For example, the BytePlus Certificate Center service is unavailable.

## Determine whether the API request is successful

It is not recommended that you use BytePlus Certificate Center response status codes when you determine whether an API request was successful. We recommend that you use the following criteria:

* If an API request is successful, the `ResponseMetadata` structure of the response body does not contain an `Error` field.

* The rest of the cases are considered request failures. You can find the corresponding error message in the `Error` field of the `ResponseMetadata` structure.

> **tip**

> Your API request may encounter the following:

> The BytePlus Certificate Center response status code is 2xx, but the `ResponseMetadata` structure contains an `Error` field.

> In this case, the API request is a failure. The reason is that the client request does not satisfy the configuration in BytePlus Certificate Center. For example, the value of a request parameter is invalid.

> For common errors in BytePlus Certificate Center, see [API Error Codes](https://docs.byteplus.com/byteplus-certificate-center/reference/api-error-codes).

## Response example

### Example response to a successful API request

```json
{
        "ResponseMetadata": {
                "RequestId": "2021041510110201022510703416005FB0",
                "Action": "CertificateGetInstance",
                "Version": "2024-10-01",
                "Service": "certificate_service",
                "Region": "ap-singapore-1"
        },
        "Result": {...}
}
```

### Example response to a failed API request

```json
{
        "ResponseMetadata": {
                "RequestId": "2021041510110201022510703416005FB0",
                "Action": "CertificateGetInstance",
                "Version": "2024-10-01",
                "Service": "certificate_service",
                "Region": "ap-singapore-1",
                "Error": {
                        "Code": "2000",
                        "Message": "System busy, please try again later."
                }
        }
}
```
