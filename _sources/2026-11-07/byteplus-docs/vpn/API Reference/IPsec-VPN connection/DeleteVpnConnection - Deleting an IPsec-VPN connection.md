---
title: "DeleteVpnConnection - Deleting an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnection"
---

Call DeleteVpnConnection to delete a specified IPsec\-VPN connection.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Deleting an IPsec\-VPN connection also removes all route entries in the VPN gateway whose next hop is this IPsec\-VPN connection.

* An IPsec\-VPN connection associated with a Transit Router (TR) cannot be deleted directly. To delete, first call [DeleteTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpnAttachment) to remove the IPsec\-VPN connection instance from the TR side.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once deleted, the IPsec\-VPN connection becomes immediately invalid. This may affect your ongoing services. Proceed with caution.</div>


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpnConnection&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|tF60YR">必选</span> Example: `DeleteVpnConnection`

The action that you want to perform. Value: DeleteVpnConnection.



**Version ** `String` <span data-api-tag="require|I2qQZ2">必选</span> Example: `2020-04-01`

The API version.



**VpnConnectionId ** `String` <span data-api-tag="require|cn4JWc">必选</span> Example: `vgc-3tex2x1cwd4c6c0v****`

ID of the IPsec\-VPN connection to be deleted. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



**OrderId ** `String` `optional` Example: `Order7078570823273845036`

Order ID for deleting an IPsec\-VPN connection associated with a TR instance. This parameter is not returned when deleting an IPsec\-VPN connection associated with a VPN gateway.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteVpnConnection&Version=2020-04-01&VpnConnectionId=vgc-2bzvqi8kerd342dx0eg2f**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202203211611080102121461940900****",
        "Action": "DeleteVpnConnection",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202203211611080102121461940900****",
        "OrderId": "Order7078570823273845036"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidCustomerGateway.InvalidStatus |The specified customer gateway is not in the correct status for the request. |The specified customer gateway cannot respond to this request due to its status. |
|400 |IncorrectVpnConnectionAttachStatus |The operation is not supported by the current IPSec connection attach status. |This action is unsupported. Retry later. |
|400 |IncorrectVpnConnectionStatus |The operation is not supported by the current vpn connection. |This action is unsupported. Retry later. |
|400 |InvalidVpnConnection.InvalidAttachStatus |The specified IPSec has been attached to a Transit Router. |The current action is not supported. The IPsec\-VPN connection is associated with the TR. Disassociate it first. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
