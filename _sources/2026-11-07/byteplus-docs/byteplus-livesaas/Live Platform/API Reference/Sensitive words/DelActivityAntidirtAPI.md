---
title: "DelActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-delactivityantidirtapi"
---

This API is used to delete sensitive words from a specified live room.

<span id="9a06e2dd"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="3dda4933"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01`

* Method: POST


<span id="44d1b454"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="19f7773f"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DelActivityAntidirtAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="e8b5e6dd"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`178398113630****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|WordList |Array of String |Yes |`["a","b"]` |Sensitive words to be deleted.<br><br>A sensitive word cannot contain a comma (,) because commas are used to separate words in the list. |
|DeleteAll |Boolean |No |`true` |Specifies whether to delete all the sensitive words from the live room.<br><br>Default value: `false`.<br><br>Valid values:<br><br><br>* `true`: Deletes all the sensitive words.<br><br>* `false`: Does not delete all the sensitive words. |


<span id="c86c0d63"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the operation was successful.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="cae97f6d"></span>
## Samples

<span id="691dfa76"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="31e7c378"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "DelActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681971407
    },
    "Result": {
        "Status": true
    }
}
```


<span id="bd73d2c5"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
