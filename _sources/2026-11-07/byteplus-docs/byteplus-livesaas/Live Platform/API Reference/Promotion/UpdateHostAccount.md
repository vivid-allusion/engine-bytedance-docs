---
title: "UpdateHostAccount"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/updatehostaccount"
---

Adds a host account or updates the information of an existing host account under your account.

<span id="usage-scenario"></span>
## Usage scenario

You can add and update a host account by using the `Id` parameter.


* To add a host account, either omit the `Id` (host account ID) or set the `Id` to `0` in the request parameters.

* To update the information of a host account, set the `Id` to the ID of the host account to be updated in the request parameters. You can get the ID by calling [ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts).


<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with the Marketing toolkits \> Edit permission. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateHostAccount` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|HostAccount |Object of [HostAccount](https://docs.byteplus.com/en/docs/11/35110#hostaccount) |No |`-` |The list of host account information. |
|GetFollowDataUrl |String |No |`https://example.com` |The query request URL. You must develop the OpenAPI by yourself to query whether a viewer is following the host. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live). |
|UpdateFollowDataUrl |String |No |`https://example.com` |The update request URL. You must develop the OpenAPI by yourself to update a viewer's following status for the host. For more information, see [Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live). |


<span id="hostaccount"></span>
### HostAccount


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Id |Long |No |`114333` |The host account ID.<br><br><br>* Add a host account: Either omit the parameter or set `0` as the parameter value.<br><br>* Update the information of a host account: Set the ID of the host account to be updated as the parameter value. You can get the ID by calling [ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts). |
|Name |String |Yes |`Host A` |The host account name.<br><br>The value must be 1\-260 characters in length. |
|AvatarUrl |String |Yes |`https://example.com/a.png` |The URL of the host account avatar, which must start with https. |
|IsFollowEnable |Integer |No |`1` |Specifies whether to allow viewers to follow the host on the viewing page. Default value: `0`. Valid values:<br><br><br>* `0`: Does not allow viewers to follow the host.<br><br>* `1`: Allows viewers to follow the host.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are updating the information of a host account, viewers can only follow the host when the live room associated with the host account has the authentication type or comment restriction set to custom on the <strong>Producer</strong> \> <strong>Viewing restrictions</strong> page. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions">Custom authentication login</a>.   </div><br>    |
|HomeUrl |String |No |`https://example.com` |The homepage URL of the host account. When viewers click the host avatar or name on the viewing page, they will be redirected to the URL. |
|ExternalPlatformId |String |No |`abc123` |The external platform ID, which can only contain uppercase and lowercase letters and numbers, and cannot exceed 128 characters in length. |
|ExtraInfo |String |No |`abc` |The extra information associated with the host account. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|HostAccountId |Long |`114333` |The ID of the added or updated host account. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023-08-01
{
    "HostAccount": {
        "Id": 114333,
        "Name": "Host A",
        "AvatarUrl": "https://example.com/a.png",
        "IsFollowEnable": 1,
        "HomeUrl": "https://example.com",
        "ExternalPlatformId": "abc123",
        "ExtraInfo": "abc"
    },
    "GetFollowDataUrl": "https://example.com",
    "UpdateFollowDataUrl": "https://example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateHostAccount",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1715326286
    },
    "Result": {
        "HostAccountId": 114333
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
