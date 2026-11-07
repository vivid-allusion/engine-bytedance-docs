---
title: "UpdateBackupSchedule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updatebackupschedule"
---

Update the automatic backup schedule for DNS records of a domain.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.

* The DNS record backup feature is only supported for domains with ultimate edition or premium edition.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=UpdateBackupSchedule&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateBackupSchedule` |The name of the API. The value of this parameter is `UpdateBackupSchedule`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain for which you want to update the backup schedule. You can get the domain ID by [CreateZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createzone) or [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones). |
|Schedule |Integer |Yes |`0` |The backup schedule.<br><br><br>* 0: Turn off automatic backup.<br><br>* 1: Automatic backup once per hour.<br><br>* 2: Automatic backup once per day.<br><br>* 3: Automatic backup once per month. |


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
|CountLimit |Integer |Limit on the number of backups. |
|Schedule |Integer |Backup schedule.<br><br><br>* 0: Disable automatic backup.<br><br>* 1: Backup every hour.<br><br>* 2: Backup once a day.<br><br>* 3: Backup once a month. |


<span id="4784ab57"></span>
## Example

<span id="dde675d6"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateBackupSchedule

{
  "ZID": 123,
  "Schedule": 1
}
```


<span id="34df133f"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230413111745A38FED8A08FE09038771",
        "Action": "UpdateBackupSchedule",
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
