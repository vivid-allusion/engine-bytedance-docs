---
title: "ResetVpnConnection - Resetting an IPsec-VPN tunnel"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ResetVpnConnection"
---

Call ResetVpnConnection to reset an IPsec\-VPN tunnel.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* You can reset IPsec\-VPN tunnels only for existing connections. This action is unsupported for connections without being associated with a Transit Router (TR).

* Resetting the IPsec\-VPN connection may interrupt the current data transmission through the tunnel. To avoid impacting business operations, perform this action at off\-peak hours.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ResetVpnConnection&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|aMZBjs">必选</span> Example: `ResetVpnConnection`

The action that you want to perform. Value: ResetVpnConnection.



**Version ** `String` <span data-api-tag="require|E9xQPm">必选</span> Example: `2020-04-01`

The API version.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ResetVpnConnection&Version=2020-04-01&VpnConnectionIds=vgc-2bzvqi8kerd342dx0eg2f**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202403211611080102121461940900****",
        "Action": "ResetVpnConnection",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202403211611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpnConnection.AttachStatus |The operation is not supported by the current VPN connection attach status. |This action is unsupported. Retry later. |
|400 |InvalidVpnConnection.InvalidStatus |The specified VPN connection is not in the correct status for the request. |The specified VPN cannot respond to this request due to its status. |
|403 |Forbidden.VpnConnectionBlocked |The specified TR IPsec is blocked. |The current TR IPsec is currently blocked. No actions are allowed. |
|403 |Forbidden.VpnGatewayBlocked |The specified VPN gateway is blocked. |The current VPN gateway is currently blocked. No actions are allowed. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidTunnel.NotFound |The specified tunnel not exist. |The specified tunnel does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidVpnConnection.AccountInArrears |The specified IPSec connection has been shut down due to the account in arrears status. |The specified IPsec\-VPN connection is suspended due to overdue payments. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
