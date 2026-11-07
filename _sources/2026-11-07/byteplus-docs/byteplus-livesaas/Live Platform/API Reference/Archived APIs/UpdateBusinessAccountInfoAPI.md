---
title: "UpdateBusinessAccountInfoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatebusinessaccountinfoapi"
---

This API updates the host account information within a live room.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Note that this operation does not apply to the host account library feature. To update the host account that is associated with a specific live room, we recommend calling <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount">UpdateActivityHostAccount</a>.</div>


<span id="41c7640a"></span>
## Requirements

Quota: 120 queries per minute per account

<span id="8852fa5c"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=UpdateBusinessAccountInfoAPI&Version=2023-08-01`

* Method: POST


<span id="b858aaad"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="81fe5762"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateBusinessAccountInfoAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="c2390329"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|IsBusinessAccountEnable |Integer |Yes |`1` |Specifies whether to enable the host account feature.<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. |
|BusinessAccountInfo |Object of [BusinessAccountInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatebusinessaccountinfoapi#437dc9eb) |No |`-` |Information about the host account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>IsBusinessAccountEnable</code> is <code>1</code>.</div><br> |


<span id="437dc9eb"></span>
#### BusinessAccountInfo


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AccountName |String |No |`Host A` |The name of the host account, which cannot exceed 260 characters in length.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>IsBusinessAccountEnable</code> is <code>1</code>.</div><br> |
|AccountHeadImage |String |No |`https://example-image.image` |The URL of the account avatar. Make sure the URL is an image URL.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>IsBusinessAccountEnable</code> is <code>1</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Make sure the URL includes a protocol header.</div><br> |
|AccountHeadRedirectUrl |String |No |`https://example.com` |The embedded link of the host account. Viewers can be redirected to this link after they click the account avatar.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Make sure the URL includes a protocol header.</div><br> |
|ExternalPlatformId |String |No |`abc123` |The external platform ID. It can only contain uppercase and lowercase letters and numbers, and its length cannot exceed 128 characters. |
|ExtraInfo |String |No |`abc` |The extra information associated with the host account. |


<span id="264494db"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the information update was successful. Returns `true` for a successful update. If an error occurs, the response contains a specific error message. |


<span id="0f894047"></span>
## Samples

<span id="4b1ce486"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateBusinessAccountInfoAPI&Version=2023-08-01
{
    "ActivityId":17218346****,
    "IsBusinessAccountEnable":1,
    "BusinessAccountInfo":{
        "AccountName": "Host A",
        "AccountHeadImage":"https://example-image.image",
        "AccountHeadRedirectUrl":"https://example.com",
        "ExtraInfo":"abc",
        "ExternalPlatformId":"abc123"
    }
}
```


<span id="535cae61"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateBusinessAccountInfoAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1702891523
    },
    "Result": {
        "Status": true
    }
}
```


<span id="4155d5f5"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Name |Message |Solution |
|---|---|---|
|100005 |The request is missing BusinessAccountInfo parameter. |Check the parameter. |
|100005 |The request is missing AccountName parameter. |Check the parameter. |
|100005 |The request is missing AccountHeadImage parameter. |Check the parameter. |
|200022 |The URL for the account avatar is not an image URL. |Change the value of the `AccountHeadImage` parameter. |
|200023 |Failed to download the image. |Change the value of the `AccountHeadImage` parameter. |
|100005 |The length of the account name exceeds the maximum limit of 260 characters. |Change the value of the `AccountName` parameter. |
|100005 |The length of the external platform ID exceeds the maximum limit of 128 characters. |Change the value of the `ExternalPlatformId` parameter. |
|100005 |The external platform ID can only contain numbers and letters. |Change the value of the `ExternalPlatformId` parameter. |
