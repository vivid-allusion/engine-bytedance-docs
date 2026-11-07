---
title: "CreateZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-createzone"
---

Creates a domain.

The domain cannot be a wildcard domain. Before creating a domain, we recommend calling the [CheckZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-checkzone) to check if the domain you want to add meets the requirements.

<span id="usage"></span>
## Usage


* Rate limit: 5 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=CreateZone?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CreateZone` |The name of the API. The value of this parameter is `CreateZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZoneName |String |Yes |`example.com` |The domain to be created. The domain must be a second\-level domain and cannot be a wildcard domain. |
|Remark |String |No |`Remark` |The remark for this domain. |


<span id="response-parameters"></span>
## Response parameters

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
|CreatedAt |String |The creation time of the domain. |
|UpdatedAt |String |The update time of the domain. |
|ZID |Integer |The ID of the domain. |
|ZoneName |String |The domain name. |
|InstanceID |String |The ID of the instance. For free edition, the value of this field is `null`. |
|Remark |String |The remark for the domain. |
|ConfigurationCode |String |This parameter is deprecated. |
|RecordCount |Integer |The total number of DNS records under the domain. Since the domain has no records yet, the value of this parameter is `0`. |
|ExpiredTime |Integer |The expiration time of the domain. For free edition, the value of this field is `0`, indicating that the domain does not expire. |
|LastOperator |String |The BytePlus account ID of the user who added this domain. |
|CacheStage |Integer |The status of domain ownership. This parameter can have the following values:<br><br><br>* `0`: Indicates that you are the owner of the domain. After adding the domain, you can manage the DNS resolution for it.<br><br>* `1`: Indicates that you are not the owner of the domain. After adding the domain, the status of the domain is "DNS is managed by another account". To manage the DNS resolution for the domain, you need to verify your ownership of the domain. |
|TradeCode |String |The edition of the domain. This parameter has the following values:<br><br><br>* `free_edition_global`: Free edition.<br><br>* `professional_edition_global`: Professional edition.<br><br>* `enterprise_edition_global`: Enterprise edition.<br><br>* `ultimate_edition_global`: Ultimate edition.<br><br>* `exclusive_edition_global`: Exclusive edition. |
|DnsSecurity |String |This parameter is not used. Please ignore this parameter. |
|IsSubDomain |Boolean |Whether the domain is a subdomain.<br><br><br>* `true`: Subdomain.<br><br>* `false`: Root domain. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=CreateZone
{
  "Remark": "create a domain",
  "ZoneName": "test.com"
}
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202406270822031A522CE03AB2FA004460",
        "Action": "CreateZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "CreatedAt": "2024-06-27T08:22:09Z",
        "UpdatedAt": "2024-06-27T08:22:09Z",
        "ZID": 454465,
        "ZoneName": "xxxxx.com",
        "InstanceID": null,
        "Remark": "create a domain",
        "ConfigurationCode": null,
        "RecordCount": 0,
        "ExpiredTime": 0,
        "LastOperator": "30xxxxx32",
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
