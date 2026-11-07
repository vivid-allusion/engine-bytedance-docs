---
title: "DeleteRecord"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-deleterecord"
---

Deletes a DNS record.

<span id="usage"></span>
## Usage


* Rate limit: 10 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=DeleteRecord?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeleteRecord` |The name of the API. The value of this parameter is `DeleteRecord`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|RecordID |String |Yes |`3170534137672596377` |The ID of the DNS record to be deleted. You can call the [ListRecords API](https://docs.byteplus.com/byteplus-dns-suite/reference/listrecords) to get the list of DNS records. |


<span id="response-body"></span>
## Response body

<span id="responsemetadata-object"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=DeleteRecord
{
  "RecordID": "3170534137672596377"
}
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202112152043280102251100110543A7C3",
        "Action": "DeleteRecord",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
