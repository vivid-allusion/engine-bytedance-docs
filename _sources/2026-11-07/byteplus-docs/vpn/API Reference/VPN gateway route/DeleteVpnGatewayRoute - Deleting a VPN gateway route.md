---
title: "DeleteVpnGatewayRoute - Deleting a VPN gateway route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteVpnGatewayRoute"
---

Call DeleteVpnGatewayRoute to delete a specified destination route of the VPN gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Confirm that the route to be deleted is no longer needed. If the route to be deleted is still in use, deleting it may cause network disruption.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpnGatewayRoute&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|D_2Ga8">必选</span> Example: `DeleteVpnGatewayRoute`

The action that you want to perform. Value: DeleteVpnGatewayRoute.



**Version ** `String` <span data-api-tag="require|rOLdy_">必选</span> Example: `2020-04-01`

The API version.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `20220322145233010225243081016A****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteVpnGatewayRoute&Version=2020-04-01&VpnGatewayRouteId=vgr-7qthudw0ll6jmc**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20220322145233010225243081016A****",
        "Action": "DeleteVpnGatewayRoute",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220322145233010225243081016A****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidVpnGatewayRoute.SslVpnClientIpPoolConflict |The specified vpn gateway route conflicts with that of existing SSL server client ip pool. |The specified VPN gateway route conflicts with the remote CIDR of the existing SSL VPN server. |
|404 |InvalidVpnGatewayRoute.NotFound |The specified VPN gateway route does not exist. |The specified VPN gateway route does not exist. |
