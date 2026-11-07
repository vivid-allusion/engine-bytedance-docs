---
title: "ListUserZoneBackups"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-listuserzonebackups"
---

Gets the backup list of DNS records for a domain.

## Usage

* Rate limit: Maximum 1 call per second.

* The DNS record backup feature is only supported for domains with ultimate edition or premium edition.

## Request

* Method: GET

* URL: https://dns.byteplusapi.com/?Action=ListUserZoneBackups&Version=2018\-08\-01

## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListUserZoneBackups` |The name of the API. The value of this parameter is `ListUserZoneBackups`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to get the backup schedule. You can call the [ListZones API](https://docs.byteplus.com/byteplus-dns-suite/reference/listzones) to get the domain ID. |

## Response body

### ResponseMetadata object

|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |

### Result object

|Name |Type |Description |
|---|---|---|
|BackupInfos |Array of Objects |Backup information. |
|BackupID |String |The ID of the backup. |
|BackupTime |String |The time when the backup was created. The time zone is UTC + 8. |
|RecordCount |Integer |The number of DNS records in the backup. |

## Example

### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=ListUserZoneBackups&Version=2018-08-01&ZID=33279
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202304131141558042281C24CCE20B216C",
        "Action": "ListUserZoneBackups",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "BackupInfos": [
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0Nzo1Ml8x",
                "BackupTime": "2023-04-01 03:47:52",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0Nzo0OV8x",
                "BackupTime": "2023-04-01 03:47:49",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0Nzo0Nl8x",
                "BackupTime": "2023-04-01 03:47:46",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyN18x",
                "BackupTime": "2023-04-01 03:47:27",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyNl8x",
                "BackupTime": "2023-04-01 03:47:26",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyNV8x",
                "BackupTime": "2023-04-01 03:47:25",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyNF8x",
                "BackupTime": "2023-04-01 03:47:24",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyM18x",
                "BackupTime": "2023-04-01 03:47:23",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoyMl8x",
                "BackupTime": "2023-04-01 03:47:22",
                "RecordCount": 1
            },
            {
                "BackupID": "MjAyMy0wNC0wMSAwMzo0NzoxNl8x",
                "BackupTime": "2023-04-01 03:47:16",
                "RecordCount": 1
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
