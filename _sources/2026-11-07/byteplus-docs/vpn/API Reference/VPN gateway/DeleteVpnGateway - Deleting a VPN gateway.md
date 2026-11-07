---
title: "DeleteVpnGateway - Deleting a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteVpnGateway"
---

Call DeleteVpnGateway to delete a specified VPN gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* For a **Pay\-as\-you\-go** VPN gateway, you can delete it directly.

* For a **Subscription** VPN gateway, you can delete it only after it expires or its subscription is cancelled.

* The VPN gateway to be deleted cannot contain any IPsec\-VPN connections or SSL\-VPN servers. First call [DeleteVpnConnection](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnection) to delete all IPsec\-VPN connections under this VPN gateway and call [DeleteSslVpnServer](https://docs.byteplus.com/en/docs/vpn/DeleteSslVpnServer) to delete the SSL\-VPN server before deleting the VPN gateway.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpnGateway&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|SXaCrv">必选</span> Example: `DeleteVpnGateway`

The action that you want to perform. Value: DeleteVpnGateway.



**Version ** `String` <span data-api-tag="require|qNVJz9">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` <span data-api-tag="require|6lmpCR">必选</span> Example: `vgw-12bfa2du7fojk17q7y1rk****`

ID of the VPN gateway to be deleted. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



**OrderId ** `String` `optional` Example: `BO7023270736605810****`

The order ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteVpnGateway&Version=2020-04-01&VpnGatewayId=vgw-12bfa2du7fojk17q7y1rk**** HTTP/1.1
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
        "Action": "DeleteVpnGateway",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202203211611080102121461940900****",
        "OrderId": "BO7023270736605810****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.InUse |The specified VPN gateway has dependent resource of connection. |The specified VPN gateway cannot be deleted because it is used by an IPsec\-VPN connection. |
|400 |InvalidVpnGateway.InvalidBillingType |The specified VPN gateway is not in the correct billing type for the request. |The specified VPN gateway does not support this request due to its billing method. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |InvalidVpnGateway.InUse |The specified VPN gateway has related SSL server. |The specified VPN gateway cannot be deleted because it has an associated SSL\-VPN server. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidVpnGateway.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
