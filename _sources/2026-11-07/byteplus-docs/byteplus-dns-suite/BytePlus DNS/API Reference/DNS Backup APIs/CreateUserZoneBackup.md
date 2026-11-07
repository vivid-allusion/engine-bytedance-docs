---
title: "CreateUserZoneBackup"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-createuserzonebackup"
---

Manually creates a backup of DNS records for a domain.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.

* The DNS record backup feature is only supported for domains with ultimate edition or premium edition.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=CreateUserZoneBackup&Version=2018\-08\-01


<span id="9f7164b6"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CreateUserZoneBackup` |The name of the API. The value of this parameter is `CreateUserZoneBackup`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to get the backup schedule. You can call the [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones) to get the domain ID. |


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


<span id="29cf5c83"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|BackupTime |String |Time when the backup was created. Timezone is UTC. |


<span id="29b47bd6"></span>
## Example

<span id="58b5c6ee"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=CreateUserZoneBackup&Version=2018-08-01&ZID=33279
{
  "ZID": 123
}
```


<span id="9f6f28e1"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230413120434E55296E4B4D8B711A68F",
        "Action": "CreateUserZoneBackup",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "BackupTime": "2023-04-13 12:04:34_2"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
