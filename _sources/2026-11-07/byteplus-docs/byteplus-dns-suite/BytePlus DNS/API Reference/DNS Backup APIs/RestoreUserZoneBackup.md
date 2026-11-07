---
title: "RestoreUserZoneBackup"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-restoreuserzonebackup"
---

Rolls back the DNS records of a domain to a backup version.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Due to the differences between the DNS records in the backup and the DNS records before the rollback, the accessibility of the domain may be affected after the rollback. This operation cannot be undone. Please proceed with caution.</div>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If the IP\-based lines or line groups used in the backup have been deleted, the rollback will fail.</div>


* <div data-tips="true" data-tips-type="tip">If the backup uses features that exceed the specifications of your domain's current edition, the DNS records that exceed the current edition specifications cannot be modified. For example, if your domain's current edition is ultimate edition, and the DNS records in the backup use parameters that comply with premium edition specifications but exceed ultimate edition specifications. In this case, the rollback will succeed. However, you cannot modify the DNS records that exceed the specifications of the current edition.</div>


* <div data-tips="true" data-tips-type="tip">If the DNSSEC status in the backup is different from the current DNSSEC status, the current DNSSEC status will remain unchanged after the rollback.</div>



<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.

* The DNS record backup feature is only supported for domains with ultimate edition or premium edition.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=RestoreUserZoneBackup&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`RestoreUserZoneBackup` |The name of the API. The value of this parameter is `RestoreUserZoneBackup`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to update the backup schedule. You can call the [ListZones API](https://docs.byteplus.com/byteplus-dns-suite/reference/listzones) to get the domain ID. |
|BackupID |String |Yes |`MjAyMy0wNC0xMyAxMjowNDozNF8y` |The ID of the backup to which you want to roll back. You can call the [ListUserZoneBackups API](https://docs.byteplus.com/byteplus-dns-suite/reference/listuserzonebackups) to get the backup ID. |


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
|TotalRecord |Integer |The total number of DNS records in the backup. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=RestoreUserZoneBackup&Version=2018-08-01

{
  "ZID": 33279,
  "BackupID": "MjAyMy0wNC0xMyAxMjowNDozNF8y"
}
```


<span id="94bba645"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202304131450057EC1C26718C36F4985EC",
        "Action": "RestoreUserZoneBackup",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "TotalRecord": 2
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
