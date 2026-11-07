---
title: "GetBusinessAccountInfoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi"
---

Call this API to get the host account information for a specific live room.

Quota: 120 queries per minute per account

<span id="106bf19e"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01`

* Method: GET


<span id="44564612"></span>
## Request parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="1d297938"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetBusinessAccountInfoAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="19c0a580"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|IsBusinessAccountEnable |Integer |`1` |Indicates whether the host account feature is enabled.<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|BusinessAccountInfo |Object of [BusinessAccountInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi#1d108f6f) |`-` |Information about the host account. |


<span id="1d108f6f"></span>
### BusinessAccountInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountName |String |`Host A` |The name of the host account. |
|HostAccountId |Integer |`112038` |The ID of the host account. |
|AccountHeadImage |String |`https://example-image.image` |The URL of the account avatar. |
|AccountHeadRedirectUrl |String |`https://example.com` |The embedded link of the host account. Viewers can be redirected to this link after they click the account avatar. |
|ExternalPlatformId |String |`abc123` |The external platform ID, which only contains uppercase and lowercase letters and numbers, and does not exceed 128 characters in length. |
|ExtraInfo |String |`abc` |The additional information associated with the host account. |


<span id="e5a3129b"></span>
## Samples

<span id="78aee2a5"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01&ActivityId=17218346****
```


<span id="e4dbc391"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetBusinessAccountInfoAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1702896398
    },
    "Result": {
        "IsBusinessAccountEnable": 1,
        "BusinessAccountInfo": {
            "AccountName": "Host A",
            "HostAccountId": 112038,
            "AccountHeadImage": "https://example-image.image",
            "AccountHeadRedirectUrl": "https://example.com",
            "ExternalPlatformId": "abc123",
            "ExtraInfo": "abc"
        }
    }
}
```


<span id="55b7cc9a"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
