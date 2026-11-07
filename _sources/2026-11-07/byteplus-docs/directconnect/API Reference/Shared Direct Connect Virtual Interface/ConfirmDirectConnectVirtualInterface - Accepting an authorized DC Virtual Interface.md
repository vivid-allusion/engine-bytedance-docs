---
title: "ConfirmDirectConnectVirtualInterface - Accepting an authorized DC Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ConfirmDirectConnectVirtualInterface"
---

Call ConfirmDirectConnectVirtualInterface to accept a Shared Virtual Interface created by another account.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Shared Virtual Interface is currently in the beta stage. If you need a trial, please contact your account manager.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ConfirmDirectConnectVirtualInterface&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|AG2WYe">必选</span> `Example: ConfirmDirectConnectVirtualInterface`

The interface name. The current API name is `ConfirmDirectConnectVirtualInterface`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|0KFre8">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|QbtqXp">必选</span> `Example: dcv-7qthudw0ll6jmc****`

The ID of the Shared Virtual Interface to be accepted. You can contact the creator of the Shared Virtual Interface to obtain this ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ConfirmDirectConnectVirtualInterface&Version=2020-04-01&VirtualInterfaceId=dcv-12al2no****&DirectConnectGatewayId=dcg-imh3****'
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20240510163937A73A8BC05C817200****",
        "Action": "ConfirmDirectConnectVirtualInterface",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20240510163937A73A8BC05C817200****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosPolicy.DirectConnectConnectionWithSharedVif |It is not supported to associate the qos policy for direct connect connection associated with shared direct connect virtual interfaces. |The DC Connection associated with a Shared Virtual Interface does not support associating QoS policies. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
