---
title: "UpdateActivityHostAccount"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/updateactivityhostaccount"
---

Updates the host account associated with a specific live room and configures whether to enable the account settings feature in the live room.

<span id="requirements"></span>
## Requirements


* Rate limit: 120 requests per minute per account

* Prerequisite: A BytePlus account or an IAM user with the Marketing toolkits \> Edit permission. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=UpdateActivityHostAccount&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityHostAccount` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|HostAccountId |Long |No |`13144` |The ID of the host account to be associated with the live room. You can get the ID by calling [ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter is required if the value of <code>IsBusinessAccountEnable</code> is <code>1</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To allow viewers to follow the host, you must set the viewing restrictions of the live room to custom. For more information, see <a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions">Custom authentication login</a>.</div><br> |
|IsBusinessAccountEnable |Integer |No |`1` |Specifies whether to enable the account settings feature. Default value: `0`. Valid values:<br><br><br>* `0`: Disables the feature.<br><br>* `1`: Enables the feature. Then, the host account information is displayed on the viewing page. |
|ActivityId |Long |Yes |`17****616` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the update is successful. The value is `true` if successful. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityHostAccount&Version=2023-08-01
{
    "HostAccountId": 13144,
    "IsBusinessAccountEnable": 1,
    "ActivityId": 17****616
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateActivityHostAccount",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1716273238
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|403 |OperationDenied.WatchPermission |Operation is denied because watch permission must be custom when isFollowEnable is true. |If the host account has the account following feature enabled, allowing viewers to follow the host on the viewing page, the authentication type or comment restriction must be set to custom on the **Producer** \> **Viewing restrictions** page of the live room. For more information, see [Custom authentication login](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions). |


&nbsp;
