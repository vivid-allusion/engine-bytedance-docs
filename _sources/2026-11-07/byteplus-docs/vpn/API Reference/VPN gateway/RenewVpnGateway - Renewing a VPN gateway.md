---
title: "RenewVpnGateway - Renewing a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/RenewVpnGateway"
---

Call RenewVpnGateway to renew a Subscription VPN gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RenewVpnGateway&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|CZV03S">必选</span> Example: `RenewVpnGateway`

The action that you want to perform. Value: RenewVpnGateway.



**Version ** `String` <span data-api-tag="require|rjheuW">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` <span data-api-tag="require|_H-OuH">必选</span> Example: `vgw-273zkshb2qayo7fap8t2****`

The ID of the VPN gateway to be renewed. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



**PeriodUnit ** `String` `optional` Example: `Month`

The purchase duration unit for the Subscription VPN gateway. Default: Month.


* Month

* Year



**Period ** `Integer` `optional` Example: `1`

The purchase duration for the Subscription VPN gateway. Default: 1.


* When `PeriodUnit` is set to "Month", the valid values of `Period` are 1–9, 12, 24, and 36.

* When `PeriodUnit` is set to "Year", the valid values of `Period` are 1–3.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203241614290567524308102CF****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=RenewVpnGateway&Version=2020-04-01&VpnGatewayId=vgw-2fe7zjsz13ksg5oxruwed**** HTTP/1.1
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
        "Action":"RenewVpnGateway",
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
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidMonthPeriod.Malformed |The specified monthly period is malformed.Monthly period only supports 1~9, 12, 24, 36. |The specified prepaid purchase duration in months is invalid. The valid prepaid purchase durations in months are 1 to 9, 12, 24, and 36. |
|400 |InvalidYearPeriod.Malformed |The specified yearly period is malformed.Yearly period only supports 1~3. |The specified purchase duration in years is invalid. The purchase duration can only be 1 to 3 years. |
|400 |InvalidPeriodUnit.Malformed |The specified period unit is malformed. Pre billing period unit can only be Month or Year. |The unit specified for the subscription duration is invalid. The subscription duration unit must be Month or Year. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidVpnGateway.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
