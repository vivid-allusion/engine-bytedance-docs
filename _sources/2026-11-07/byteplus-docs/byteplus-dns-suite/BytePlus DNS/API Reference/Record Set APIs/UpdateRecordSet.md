---
title: "UpdateRecordSet"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updaterecordset"
---

Enables or disables load balancing for a record set.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 5 calls per second.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=UpdateRecordSet&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRecordSet` |The name of the API. The value of this parameter is `UpdateRecordSet`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ID |String |Yes |`MTU0MHxpbWcubWljcm9maXNoLmxpZmUufEF8ZGVmYXVsdA` |The ID of the record set for which to enable or disable load balancing. |
|WeightEnabled |Boolean |Yes |`true` |Whether to enable load balancing. If load balancing is enabled, BytePlus DNS will return the resolution result based on the weight of the record. This parameter can have the following values:<br><br><br>* `true`: Enable load balancing.<br><br>* `false`: Disable load balancing. |


<span id="dd662fa8"></span>
## Response body

<span id="5d8f6b29"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="76418171"></span>
### Result Object


|Name |Type |Description |
|---|---|---|
|ID |String |The ID of the record set. |
|FQDN |String |The domain prefix included in the record set. The domain prefix is displayed in FQDN format. |
|Host |String |The domain prefix included in the record set. |
|Type |String |The type of the record in the record set. |
|Line |String |The line code corresponding to the record set. |
|WeightEnabled |Boolean |Whether the record set has load balancing enabled. If load balancing is enabled, BytePlus DNS will return an IP address based on the weight of the record.<br><br>This parameter can have the following values:<br><br><br>* `true`: Load balancing is enabled.<br><br>* `false`: Load balancing is not enabled. |


<span id="4f1c2d94"></span>
## Example

<span id="a3a4f532"></span>
### Request example

```HTTP
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateRecordSet
{
  "ID": "MTU0MHxpbWcubWljcm9maXNoLmxpZmUufEF8ZGVmYXVsdA==",
  "WeightEnabled": true
}
```


<span id="7c7faa38"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041215595881035184908E7F1FE4BE",
        "Action": "UpdateRecordSet",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "ID": "MzE3MDUzNDEzNzY2OTA5ODc5OHxALnlhbWFzaXRlLnRvcC58QXxkZWZhdWx0",
        "FQDN": "@.example.com",
        "PQDN": "@.example.com",
        "Host": "@",
        "Type": "A",
        "Line": "default",
        "WeightEnabled": true
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
