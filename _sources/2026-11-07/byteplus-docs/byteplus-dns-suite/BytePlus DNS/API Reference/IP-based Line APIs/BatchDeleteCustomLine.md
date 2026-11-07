---
title: "BatchDeleteCustomLine"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-batchdeletecustomline"
---

Batch deletes the specified IP\-based lines.

If the IP\-based lines you want to delete are used by one or more DNS records, the deletion will fail. You can use the [ListRecordDigestByLine API](https://docs.byteplus.com/byteplus-dns-suite/reference/listrecorddigestbyline) to query all DNS records that use the IP\-based lines.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=BatchDeleteCustomLine&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request Parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`BatchDeleteCustomLine` |The name of the API. The value of this parameter is `BatchDeleteCustomLine`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Lines |String |Yes |`["custom-101"]` |One or more IDs of the IP\-based lines. You can obtain the IDs of the IP\-based lines from the `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/byteplus-dns-suite/reference/listcustomlines). |


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


<span id="result-object"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|TotalCount |Integer |The total number of IP\-based lines deleted. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=BatchDeleteCustomLine

{
  "Lines": [
       "custom-101"
                ]
}
```


<span id="376e2525"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230412182556F74F757E0A95003D4FF8",
        "Action": "BatchDeleteCustomLine",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalCount": 1
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
