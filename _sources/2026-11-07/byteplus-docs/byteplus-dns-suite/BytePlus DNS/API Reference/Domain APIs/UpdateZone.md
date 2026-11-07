---
title: "UpdateZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updatezone"
---

Updates the remark of a domain.

<span id="usage"></span>
## Usage


* Rate limit: 5 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=UpdateZone?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateZone` |The name of the API. The value of this parameter is `UpdateZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain for which the comments need to be updated. You can get the domain ID by [CreateZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createzone) or [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones). |
|Remark |String |No |`Remark` |The new domain remark. |


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


<span id="5b77d5bb"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|CreatedAt |String |The creation time of the domain. |
|UpdatedAt |String |The most recent update time of the domain. Update operations include:<br><br><br>* Updating domain comments<br><br>* Adding DNS records to the domain |
|ZID |Integer |The ID of the domain. |
|ZoneName |String |The domain name. |
|InstanceID |String |The ID of the instance. For free edition, the value of this field is `null`. |
|Remark |String |The new comments of the domain. |
|ConfigurationCode |String |This parameter is deprecated. |
|RecordCount |Integer |The total number of DNS records under the domain. |
|ExpiredTime |Integer |The expiration time of the domain. For BytePlus DNS Free Edition, the value of this field is `0`, indicating that the domain does not expire. |
|LastOperator |String |The BytePlus account ID of the user that last updated this domain. Update operations include:<br><br><br>* Updating domain comments<br><br>* Adding DNS records under the domain |
|CacheStage |Integer |The status of domain ownership. This parameter can have the following values:<br><br><br>* `0`: Indicates that you are the owner of the domain.<br><br>* `1`: Indicates that you are not the owner of the domain. |
|TradeCode |String |The edition of the domain. This parameter can have the following values:<br><br><br>* `free_edition_global`: Free Edition.<br><br>* `professional_edition_global`: Professional Edition.<br><br>* `enterprise_edition_global`: Enterprise Edition.<br><br>* `ultimate_edition_global`: Ultimate Edition.<br><br>* `exclusive_edition_global`: Exclusive Edition. |
|DnsSecurity |String |This parameter is not used. Please ignore this parameter. |
|IsSubDomain |Boolean |Whether the domain is a subdomain.<br><br><br>* `true`: Subdomain.<br><br>* `false`: Root domain. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateZone
{
  "Remark": "update a domain2",
  "ZID": 2652
}
```


<span id="08f8ae8a"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202406270911544FE1CFFEA1818402E16D",
        "Action": "UpdateZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "CreatedAt": "2024-06-27T08:22:09Z",
        "UpdatedAt": "2024-06-27T09:11:55Z",
        "ZID": 454465,
        "ZoneName": "test123.com",
        "InstanceID": null,
        "Remark": "create a domain2",
        "ConfigurationCode": null,
        "RecordCount": 0,
        "ExpiredTime": 0,
        "LastOperator": "3000000832",
        "CacheStage": 0,
        "TradeCode": "free_edition_global",
        "DnsSecurity": "",
        "IsSubDomain": false
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
