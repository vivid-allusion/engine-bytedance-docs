---
title: "AddActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addactivityantidirtapi"
---

Call this API to add a list of sensitive words to a specified live room. This helps you moderate chat content and maintain a safe interactive environment.

<span id="6ca3ae9b"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="3e5e18b2"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01`

* Method: POST


<span id="a7e0438d"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="dc691b28"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`AddActivityAntidirtAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="e9034e45"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`178398113630****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|WordList |Array of String |Yes |`["a","b"]` |An array of sensitive words to add. There is no limit on the number of words you can add.<br><br>Note: Words cannot contain commas (,) because commas are used as separators. |


<span id="eceb3e71"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the sensitive words were added successfully.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="4cf59303"></span>
## Samples

<span id="45d8e74f"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="8e3de267"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "AddActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846
    },
    "Result": {
        "Status": true
    }
}
```


<span id="2c603933"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
