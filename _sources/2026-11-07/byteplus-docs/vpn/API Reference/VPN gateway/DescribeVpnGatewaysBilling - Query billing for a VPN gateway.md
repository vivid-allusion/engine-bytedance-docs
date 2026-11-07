---
title: "DescribeVpnGatewaysBilling - Query billing for a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewaysBilling"
---

Call DescribeVpnGatewaysBilling to query the billing information of a specified VPN gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnGatewaysBilling&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|vOc23a">必选</span> Example: `DescribeVpnGatewaysBilling`

The action that you want to perform. Value: DescribeVpnGatewaysBilling.



**Version ** `String` <span data-api-tag="require|W6pA84">必选</span> Example: `2020-04-01`

The API version.



**PageSize ** `Integer` `optional` Example: `20`

The number of rows per page for paginated queries. Value range: 1–100. Default: 20.



**PageNumber ** `Integer` `optional` Example: `1`

Page number for pagination query.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**VpnGatewayIds.N ** `String` `optional` Example: `vgw-273zkshb2qayo7fap8t2****`

ID of the VPN gateway. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.


* N represents the sequence number of a VPN gateway ID.

* Separate multiple IDs with ampersands (&).



**ProjectName ** `String` `optional` Example: `project01`

The project to which the VPN gateway belongs.


* If you provide this field, the system will query VPN gateways under the specified project.

* If you omit this field, the system will query VPN gateways across all projects.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `2022032416142901022524308102CF****`

Request ID



**PageSize ** `Integer` `optional` Example: `10`

The number of rows on the current page.



**PageNumber ** `Integer` `optional` Example: `1`

Current page number.



**TotalCount ** `Integer` `optional` Example: `1`

The number of VPN gateways that meet the query conditions.



**VpnGateways ** `Object[]` `optional` Example: `-`

Detailed billing information list of the VPN gateway.


**VpnGatewayId ** `String` `optional` Example: `vgw-2zeerraiwb7uj****`

ID of the VPN gateway.



**BillingStatus ** `Integer` `optional` Example: `1`

Billing status.


* 1: Running

* 3: Unsubscribed and reclaimed

* 4: Suspended due to expiration



**BillingType ** `Integer` `optional` Example: `1`

The billing method for the VPN gateway.


* 1: Subscription

* 2: Pay\-as\-you\-go (specification\-based)



**ExpiredTime ** `String` `optional` Example: `2021-03-11 23:59:59`

The time when the VPN gateway expires.



**ReclaimTime ** `String` `optional` Example: `2021-03-18 23:59:59`

The time when the VPN gateway is reclaimed.



**RemainRenewTimes ** `Integer` `optional` Example: `1`

The number of remaining automatic renewals available.


* 1 to 100: The number of remaining automatic renewals.

* \-1: Unlimited renewals.



**RenewType ** `Integer` `optional` Example: `1`

Type of automatic renewal.


* 1: Manual renewal.

* 2: Automatic renewal.

* 3: Non\-renewal upon expiration.


> Note: If `3` is specified, the platform will not send expiration notifications before the VPN gateway expires.



**OverdueTime ** `String` `optional` Example: `2023-08-07T23:23:23+08:00`

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.



**OverdueReclaimTime ** `String` `optional` Example: `2019-04-29T01:37:38+08:00`

The time when the system forcibly reclaims the resource that is already suspended due to overdue payments. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpnGatewaysBilling&Version=2020-04-01 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata":{
        "RequestId":"2022032416142901022524308102CF****",
        "Action":"DescribeVpnGatewaysBilling",
        "Version":"2020-04-01",
        "Service":"vpn",
        "Region":"cn-beijing"
    },
    "Result":{
        "RequestId":"2022032416142901022524308102CF****",
        "PageNumber":1,
        "PageSize":20,
        "TotalCount":1,
        "VpnGateways":[
            {
                "VpnGatewayId":"vgw-2fe7zjsz13ksg5oxruwed****",
                "BillingType":1,
                "BillingStatus":1,
                "RenewType":1,
                "RemainRenewTimes":-1,
                "ExpiredTime":"2022-05-21 23:59:59",
                "ReclaimTime":"2022-06-05 23:59:59",
                "OverdueTime":"",
                "OverdueReclaimTime":""
            }           
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.VpnGatewayId |You've reached the limit on the number of VPN gateway IDs that you can describe. |You have reached the maximum IDs of VPN gateways that you can query. |
