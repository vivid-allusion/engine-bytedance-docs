---
title: "GetActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityantidirtapi"
---

To manage content moderation in your live room, you can call this API to get the list of configured sensitive words. This API allows you to retrieve either all sensitive words or only those containing specific keywords.

<span id="6012f85b"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="9ee8c1eb"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01`

* Method: GET


<span id="7ad60001"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="7ccae2e4"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityAntidirtAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`178398113630****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|PageNo |Integer |Yes |`1` |The page number to return. |
|PageItemCount |Integer |Yes |`10` |The number of results to return on each page. |
|Content |String |No |`a` |Keyword. The API returns only the sensitive words that contain this keyword. |


<span id="c45a43ea"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|EnablePhoneNumberFilter |Integer |`1` |Specifies whether to block comments and nicknames that contain phone numbers.<br><br><br>* `1`: Enabled. Comments containing phone numbers are visible to the sender only.<br><br>* Other values: Disabled.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, this feature supports phone numbers from Singapore, Japan, South Korea, Indonesia, Thailand, and mainland China.</div><br> |
|EnableSensitiveForLetter |Integer |`1` |Indicates whether case sensitivity is enabled.<br><br><br>* `1`: Enabled.<br><br>* Other values: Disabled. |
|TotalItemCount |Integer |`2` |The total number of sensitive words returned. |
|WordList |Array of String |`["a","ab"]` |List of sensitive words returned. |


<span id="cd1e512b"></span>
## Samples

<span id="af8ea841"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01&ActivityId=178398113630****&PageNo=1&PageItemCount=10&Content=a
```


<span id="2ea02c1c"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846
    },
    "Result": {
        "WordList": ["a","ab"],
        "TotalItemCount": 2,
        "EnablePhoneNumberFilter": 1,
        "EnableSensitiveForLetter": 1
    }
}
```


<span id="21a1266f"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
