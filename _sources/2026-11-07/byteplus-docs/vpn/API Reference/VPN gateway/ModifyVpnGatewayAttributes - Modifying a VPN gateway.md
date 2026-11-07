---
title: "ModifyVpnGatewayAttributes - Modifying a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes"
---

Call ModifyVpnGatewayAttributes to modify the basic information of a Virtual Private Network (VPN) gateway, such as the name, bandwidth size, and description.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* For an expired Subscription VPN gateway or a Pay\-as\-you\-go VPN gateway that is suspended due to overdue payments, modifying bandwidth is unsupported.

* After the bandwidth of a Subscription VPN gateway is modified successfully, the new specification takes effect immediately. The expiration time remains unchanged. The amount displayed on the interface during specification modification is the difference between the new specification fee and the fee already paid. For more about the modification fees, see [Changing Annual or Monthly Subscription Resource Specifications](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8).

* After the bandwidth of a Pay\-as\-you\-go VPN gateway is modified successfully, the new specification takes effect immediately. Billing is calculated based on the new specification's price. When modifying the bandwidth of a VPN gateway within a billing cycle, the fee calculation for that billing cycle is: **Old spec unit price × Old usage duration + New spec unit price × New usage duration**.

* If the current VPN gateway version is outdated, you can neither upgrade the specification of the VPN gateway from 200 Mbps and lower specifications to 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps, nor downgrade from 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps to 200 Mbps and lower. If necessary, go to the console to update the VPN gateway to the latest version. For specific procedure, see [Upgrading a VPN Gateway](https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway).

* **The following actions may cause connection interruption. Perform them during off\-peak hours**:

   * Modify SSL Max Connections: `SslMaxConnections`.

   * Modify the bandwidth between the lower (5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, and 200 Mbps) and the higher (300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, and 3 Gbps).


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpnGatewayAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|TQWRo6">必选</span>Example: `ModifyVpnGatewayAttributes`

The action that you want to perform. Value: ModifyVpnGatewayAttributes.



**Version ** `String` <span data-api-tag="require|U5yh6x">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` <span data-api-tag="require|V0_i6j">必选</span> Example: `vgw-12bfa2du7fojk17q7y1rk****`

The ID of the VPN gateway instance. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



**VpnGatewayName ** `String` `optional` Example: `VpnGateway-test`

The name of the VPN gateway instance.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, the original configuration remains.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the VPN gateway instance.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



**Bandwidth ** `Integer` `optional` Example: `20`

The bandwidth unit of the VPN gateway instance: Mbps.


* If left blank, the original configuration remains.

* Values: 5, 10, 20, 50, 100, 200, 300, 400, 500, 1000, and 3000.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VPN gateways with bandwidths of 1000 Mbps and 3000 Mbps are in the beta stage. These specifications are only available to users who have this feature enabled. If not enabled, do not set <code>Bandwidth</code> to these values. If you need a trial, please contact your account manager.</div>




**IpsecEnabled** `Boolean` `optional` Example: `true`

Describes whether to enable IPsec.


* true: Enable

* false: Disable


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The values of <code>IpsecEnabled</code> and <code>SslEnabled</code> cannot both be <code>false</code>.</div>




**SslEnabled ** `Boolean` `optional` Example: `false`

Specify whether to enable SSL\-VPN.


* true: Enable

* false: Disable


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The values of <code>IpsecEnabled</code> and <code>SslEnabled</code> cannot both be <code>false</code>.</div>




**SslMaxConnections ** `Integer` `optional` Example: `10`

The maximum number of SSL\-VPN connections. Provide this parameter only if `SslEnabled` is set to `true`.


* 5

* 10

* 20

* 50

* 100

* 200



**Asn ** `Integer` `optional` Example: `64512`

The ASN of the VPN gateway. Only supports configuring ASN for the first time. That is, if the original VPN gateway has no ASN configured, you can set the ASN using this parameter. Once configured, the ASN cannot be modified.


* The value ranges for VPN gateway ASN are 64512\-65534, and 4200000000\-4294967294.

* If left blank, the original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



**OrderId ** `String` `optional` Example: `BO702327073660581****`

The order ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyVpnGatewayAttributes&Version=2020-04-01&VpnGatewayId=vgw-12bfa2du7fojk17q7y1rk****&VpnGatewayName=test&Description=test&Bandwidth=10 HTTP/1.1
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
        "Action": "ModifyVpnGatewayAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202203211611080102121461940900****",
        "OrderId":"BO702327073660581****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidVpnGatewayBandwidth.Malformed |The specified VPN gateway bandwidth is malformed. |The specified VPN gateway bandwidth is unsupported. |
|400 |InsufficientResource.VpnGateway |The specified region does not have enough resources for VPN gateway. |The available resources of the VPN gateway are insufficient. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay the order. |
|400 |PreOrderError |Failed to create pre order. |The creation of the configuration order failed. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InvalidIpsecEnabled.InUse |The specified VPN gateway has dependent resource of VPN connection. |The IPsec feature cannot be disabled because the VPN gateway contains IPsec\-VPN connections. |
|400 |InvalidSslEnabled.InUse |The specified VPN gateway has dependent resource of SSL server. |The VPN gateway contains an SSL VPN server, and therefore SSL cannot be disabled. |
|400 |InvalidSslMaxConnections.Malformed |The specified SSL max connection of VPN Gateway is malformed. |The specified SSL Max Connections for the VPN gateway is invalid. |
|400 |InvalidVpnEnabled.Malformed |IpsecEnabled and SslEnabled can not be set to false at the same time. |The IPSec and SSL features cannot both be disabled. |
|400 |InvalidVpnGateway.FirmwareNotSupported |The specified features aren't supported by the VPN gateway, please upgrade your VPN gateway. |The selected feature is unavailable for the VPN gateway. Upgrade your VPN gateway. |
|400 |InvalidVpnGateway.SslNotEnabled |SSL of the specified VPN gateway is not enabled. |The current VPN gateway does not have SSL enabled. |
|400 |InvalidSslMaxConnections.ClientIpPoolNotEnough |The specified SslMaxConnections is larger than the support ip numbers of ssl server. |The SSL Max Connections is greater than the IP count supported by the current SSL VPN server. |
|400 |InvalidVpnGateway.InvalidASN |The VPN Gateway ASN is invalid and it should be in the range of 64512\-65534 or 4200000000\-4294967294. |The specified ASN is invalid. An ASN must be in the ranges of 64512\-65534 and 4200000000\-4294967294. |
|400 |InvalidVpnGatewayAsn.ASNAlreadyConfigured |The specified VPN gateway already has an ASN, which cannot be modified. |The specified VPN gateway instance is configured with an ASN. |
|400 |InvalidVpnGateway.BGPSupport |The dual\-tunnel VPN gateway does not support BGP. |Dual\-tunnel VPN gateways do not support Border Gateway Protocol (BGP). |
|400 |InvalidVpnGateway.SslNotSupport |The dual\-tunnel VPN gateway does not support Ssl. |Dual\-tunnel VPN gateways do not support SSL features. |
|403 |Forbidden |The specified service is temporarily unavailable. Please try again later. |The specified service is unavailable. Retry later. |
|403 |Forbidden.VpnGatewayBlocked |The specified VPN gateway is blocked. |The current VPN gateway is blocked. No actions are allowed. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidVpnGateway.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
