---
title: "CheckRetrieveZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-checkretrievezone"
---

Verifies the ownership of your domain.

<span id="usage"></span>
## Usage


* Rate limit: 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=CheckRetrieveZone?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CheckRetrieveZone` |The name of the API. The value of this parameter is `CheckRetrieveZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZoneName |String |Yes |`example.com` |The domain to be verified. The domain must be a second\-level domain and cannot be a wildcard domain. |


<span id="613b33f1"></span>
## Response body

<span id="cb4a2f87"></span>
### ResponseMetadata object


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="0fe40a3f"></span>
### Result object

If the domain ownership verification is successful, this API returns `"Success": "true"`. If the verification fails, this API does not return a Result object. Instead, it returns an error message `type TXT record not found` through the `ResponseMetadata` object.

<span id="58662018"></span>
## Example

<span id="f99ad33b"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=CheckRetrieveZone
{
  "ZoneName": "example.com"
}
```


<span id="aa7f0dce"></span>
### Response example

The domain ownership verification is successful.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221101155301010225243125056CA34D",
        "Action": "CheckRetrieveZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Success": "true"
    }
}
```


The domain ownership verification fails.

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20211215202125010225243125052DB635",
        "Action": "CheckRetrieveZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore",
        "Error": {
            "CodeN": 600104,
            "Code": "CheckRetrieveZone",
            "Message": "type TXT record not found"
        }
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
