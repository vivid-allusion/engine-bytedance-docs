---
title: "SetVpnGatewayRenewal - Modifying renewal for a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/SetVpnGatewayRenewal"
---

Call SetVpnGatewayRenewal to modify the renewal method of a specified VPN gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SetVpnGatewayRenewal&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|_RXYRd">必选</span> Example: `SetVpnGatewayRenewal`

The action that you want to perform. Value: SetVpnGatewayRenewal.



**Version ** `String` <span data-api-tag="require|Q-7Cm-">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` <span data-api-tag="require|JKkHPu">必选</span> Example: `vgw-2fe7zjsz13ksg5oxruwed****`

ID of the VPN gateway whose renewal method you want to modify. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



**RenewType ** `Integer` <span data-api-tag="require|7eGqI3">必选</span> Example: `1`

Renewal method. This parameter defaults to "1" (Manual renewal).


* 1: Manual renewal.

* 2: Automatic renewal.

* 3: Non\-renewal upon expiration.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If 3 is specified, the platform will not send expiration notifications before the VPN gateway expires.</div>




**RenewPeriod ** `Integer` `optional` Example: `1`

The length for automatic renewal, with valid values of 1, 2, 3, 6, and 12 month(s).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If <code>RenewType</code> is set to “1” or “3”, <code>RemainRenewTimes</code> has no practical meaning.</div>




**RemainRenewTimes ** `Integer` `optional` Example: `1`

The number of automatic renewals available.


* 1–100: The number of remaining automatic renewals.

* \-1: Unlimited renewals.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If <code>RenewType</code> is set to “1” or “3”, <code>RemainRenewTimes</code> has no practical meaning.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203241614290567524308102CF****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=SetVpnGatewayRenewal&Version=2020-04-01&VpnGatewayId=vgw-2fe7zjsz13ksg5oxruwed****&RenewType=3 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202203241614290567524308102CF****",
        "Action":"SetVpnGatewayRenewal",
        "Version":"2020-04-01",
        "Service":"vpn",
        "Region":"cn-beijing"
    },
    "Result":{
        "RequestId":"202203241614290567524308102CF****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidRenewType.Malformed |The specified renew type is malformed.Renew type must be 1, 2, or 3. |The specified renewal type is invalid. The value of renewal type must be 1, 2, or 3. |
|400 |InvalidRenewPeriodTimes.Malformed |The specified renew period times is malformed.Renew period times only support 1, 2, 3, 6, 12. |The specified automatic renewal cycle is invalid. The value for the automatic renewal cycle must be 1, 2, 3, 6, or 12 months. |
|400 |InvalidRemainRenewTimes.Malformed |The specified remain renew times is malformed.Remain renew times only support \-1, 1~100. |The specified number of automatic renewals is invalid. The value for the number of automatic renewals must be \-1 or 1\-100. |
|400 |InvalidVpnGateway.InvalidBillingType |The specified VPN gateway is not in the correct BillingStatus for the request. |The specified VPN gateway instance does not support this request due to its billing method. |
|400 |InvalidVpnGateway.ModifyRenewalSettings |Modify renewal settings failed. |Failed to modify automatic renewal settings. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
