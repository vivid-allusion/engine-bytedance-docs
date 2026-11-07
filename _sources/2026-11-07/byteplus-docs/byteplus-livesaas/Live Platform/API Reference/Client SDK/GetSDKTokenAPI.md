---
title: "GetSDKTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi"
---

Call this API to get the authorization token that is required to allow viewers to enter a live room through web pages or apps integrated with the Viewer SDK.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To prevent malicious attacks, ensure that you validate all request parameters before calling this API operation.</div>


<span id="61e03047"></span>
## Requirement

Quota: 5,000 queries per minute per account

<span id="8fc08545"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01`

* Method: POST


<span id="06d777a9"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="513dbfbc"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSDKTokenAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="Body parameters"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`179758233282****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Mode |Integer |Yes |`2` |The authentication mode of the live room.<br><br>Valid values:<br><br><br>* `1`: Public mode. Viewers can enter the live room without logging in. However, in scenarios where user information is needed, such as when clicking the comment text box or liking comments, viewers must enter their nicknames first.<br><br>* `2`: Custom mode. You must pass viewers' nicknames and user IDs to this API operation after they log in to your own account system. Viewers enter the live room using the credentials from your account system. Therefore, viewers can directly perform operations such as sending and liking comments. |
|Nickname |String |No |`Viewer A` |The nickname of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>Mode</code> is <code>2</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To prevent personal information leakage, we recommend that you do not use information such as phone numbers as the viewer's nickname.</div><br> |
|UserIdStr |String |No |`57584` |The user ID of the viewer.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>Mode</code> is <code>2</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To prevent personal information leakage, we recommend that you do not use information such as phone numbers as the viewer's user ID.</div><br> |
|InviteToken |String |No |`abcd` |If a viewer shares the live room from a page that is integrated with the Web Viewer SDK, this value is the `inviter_token` from the shared URL. For example, if the path is `https://test.live.com/123/456?inviter_token=abcd`, the parameter value is `abcd`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect if the value of <code>Mode</code> is <code>2</code>.</div><br> |
|AvatarUrl |String |No |`http://xxx.example` |The URL of the viewer's avatar. This avatar is displayed only on viewing pages integrated with the Viewer SDK for iOS or Android. |
|CustomComment |String |No |`Singapore` |Specifies custom information (such as the winner's location) to display to the right of the viewer's nickname in the winner list. The value can be up to 50 characters long.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only takes effect if the value of <code>Mode</code> is <code>2</code>.</div><br> |


<span id="f9131aea"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Token |String |`ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D` |The authorization token that is required to allow viewers to enter a live room through web pages or apps integrated with the Viewer SDK.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the value of <code>Mode</code> is <code>2</code>, a URL\-encoded token is generated and you must URL\-decode it before passing it to the Viewer SDK. Otherwise, the Viewer SDK will fail to authenticate the token.</div><br> |


<span id="eebe5d33"></span>
## Samples

<span id="5e5b0957"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01
{
     "ActivityId": 179758233282****,
     "Mode": 2,
     "Nickname": "Viewer A",
     "UserIdStr": "57584"
}
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetSDKTokenAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714572349
    },
    "Result": {
        "Token": "ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D"
    }
}
```


<span id="6e0e0a4d"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
