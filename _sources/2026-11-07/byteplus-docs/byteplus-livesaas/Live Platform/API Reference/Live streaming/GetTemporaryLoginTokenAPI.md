---
title: "GetTemporaryLoginTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-gettemporarylogintokenapi"
---

Call this API to get the secret key of a live room, which is used to start a live stream.

<span id="bac9c171"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="b63c37e0"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01`

* Method: GET


<span id="576d363d"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="64a0bda3"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetTemporaryLoginTokenAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="a8e81e5f"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|SecretKey |String |`0UmdWrZKAVWJJTxzCOJ****` |The secret key of the live room, which is used to start a live stream. |
|ActivityId |Long |`17218312****` |The activity ID of the live room. |


<span id="bf977fee"></span>
## Samples

<span id="875465ab"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetTemporaryLoginTokenAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="8d037a06"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "GetTemporaryLoginTokenAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
      "SecretKey": "0UmdWrZKAVWJJTxzCOJ****",
      "ActivityId": 17218312****
  }
}
```


<span id="53f720b3"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
