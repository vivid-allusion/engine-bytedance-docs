---
title: "DeleteUserZoneBackup"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-deleteuserzonebackup"
---

Deletes a backup by ID.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=DeleteUserZoneBackup&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeleteUserZoneBackup` |The name of the API. The value of this parameter is `DeleteUserZoneBackup`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to delete the backup. You can call the [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones) to get the domain ID. |
|BackupID |String |Yes |`MjAyMy0wNC0wMSAwMzo0Nzo0OV8x` |The ID of the backup that you want to delete. You can call the [ListUserZoneBackups API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listuserzonebackups) to get the backup ID. |


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
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=DeleteUserZoneBackup&Version=2018-08-01

{
  "ZID": 33279,
  "BackupID": "MjAyMy0wNC0wMSAwMzo0Nzo0OV8x"
}
```


<span id="b9f96887"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230413135111D9C4CE1C7D20C13C5865",
        "Action": "DeleteUserZoneBackup",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
