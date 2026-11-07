---
title: "QueryBackupSchedule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-querybackupschedule"
---

Get the automatic backup schedule for DNS records of a domain.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.

* The DNS record backup feature is only supported for domains with ultimate edition or premium edition.


<span id="request"></span>
## Request


* Method: GET

* URL: https://dns.byteplusapi.com/?Action=QueryBackupSchedule&Version=2018\-08\-01


<span id="6741192a"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`QueryBackupSchedule` |The name of the API. The value of this parameter is `QueryBackupSchedule`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to get the backup schedule. You can get the domain ID by [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones). |


<span id="4b8b8b19"></span>
## Response body

<span id="96d7f914"></span>
### ResponseMetadata object


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="b4c9dcc4"></span>
### Result object


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|CountLimit |Integer |Maximum number of backups per domain. |
|Schedule |Integer |Backup schedule.<br><br><br>* 0: Disable automatic backup.<br><br>* 1: Backup every hour.<br><br>* 2: Backup once a day.<br><br>* 3: Backup once a month. |


<span id="da731d19"></span>
## Example

<span id="9c22ef34"></span>
### Request example

```HTTP
GET https://dns.byteplusapi.com/?Version=2018-08-01&Action=QueryBackupSchedule&Version=2018-08-01&ZID=33279
```


<span id="79d8f760"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041311234169E7FF817131DB061A27",
        "Action": "QueryBackupSchedule",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "CountLimit": 10,
        "Schedule": 1
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
