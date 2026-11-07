---
title: "CreateVpnGateway - Creating a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway"
---

Call CreateVpnGateway to create a VPN gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpnGateway&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|0V8b1E">必选</span> `Example: CreateVpnGateway`

The action that you want to perform. Value: CreateVpnGateway.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|myVMq6">必选</span> `Example: 2020-04-01`

The API version.



**VpcId ** <span data-label="purple"> String  </span><span data-api-tag="require|nqCVe8">必选</span> `Example: vpc-5fn4gia8n2t****`

The ID of the Virtual Private Cloud (VPC) where the VPN gateway is deployed. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query the VPC ID.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VPN Connect does not support shared VPCs. Do not provide shared VPC IDs here.</div>




**SubnetId ** <span data-label="purple"> String  </span><span data-api-tag="require|fW6JMU">必选</span> `Example: subnet-3thgqai7my4e8i****`

The ID of the subnet used by the VPN gateway. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) to query the subnet ID.



**Bandwidth ** <span data-label="purple"> Integer  </span><span data-api-tag="require|CvLG1D">必选</span> `Example: 5`

The outbound bandwidth specification of the VPN gateway. Unit: Mbps. Values: 5, 10, 20, 50, 100, 200, 300, 400, 500, 1000, and 3000.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">VPN gateways with bandwidths of 1,000 Mbps and 3,000 Mbps are in the beta stage. These specifications are only available to users who have this feature enabled. If not enabled, do not set <code>Bandwidth</code> to these values. If needed, please contact your account manager.</div>




**VpnGatewayName ** <span data-label="purple"> String  </span>`Optional` `Example: VpnGateway`

The name of the VPN gateway.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left empty, this parameter defaults to the VPN gateway ID.



**Description ** <span data-label="purple"> String </span>`optional` `Example: This is a sample description`

The description of the VPN gateway.


* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**BillingType ** <span data-label="purple"> Integer  </span>`Optional` `Example: 1`

The billing method for the VPN gateway. Default: 1.


* 1 (default): Subscription.

* 2: Pay\-as\-you\-go (specification\-based).



**PeriodUnit ** <span data-label="purple"> String  </span>`optional` `Example: Month`

The purchase duration unit for the Subscription VPN gateway. Default: Month.


* Month

* Year



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The purchase duration for the Subscription VPN gateway. Default: 1.


* When `PeriodUnit` is set to `Month`, the valid values of `Period` are 1–9, 12, 24, and 36.

* When `PeriodUnit` is set to `Year`, the valid values of `Period` are 1–3.



**ProjectName ** <span data-label="purple"> String </span>`optional` `Example: Project_1`

The project to which the VPN gateway belongs. If left blank, the `default` is used. That is, the created resource belongs to the default project. You can call [ListProjects](https://docs.byteplus.com/en/docs/6649/1131880) to query project information under the current account.



**Tags.N.Key ** <span data-label="purple"> String </span>`optional` `Example: key1`

The tag key of the VPN gateway.


* N represents the sequence number of a tag key. Valid range: 1\-20.

* Separate multiple tag keys with ampersands (&).

   The naming rules are as follows:

* Must not start with `volc:` or `sys:`, regardless of case.

* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* Must be 1 to 128 characters.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Tag keys of the same resource must be unique.​</div>




**Tags.N.Value** <span data-label="purple">String</span> `optional` `Example: value1`

The tag value of the VPN gateway.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).

   The naming rules are as follows:

* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* May be left blank. Must be 0 to 256 characters in length.

* Case\-sensitive. Cannot start or end with a space.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To provide <code>Tags.N.Value</code>, you must provide <code>Tags.N.Key</code>.</div>




**ClientToken ** <span data-label="purple">String</span> `optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**IpsecEnabled ** <span data-label="purple"> Boolean  </span>`optional` `Example: true`

Specify whether to enable IPsec features.


* true (default): Enable

* false: Disable


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The values of <code>IpsecEnabled</code> and <code>SslEnabled</code> cannot both be <code>false</code>.</div>




**DualTunnelEnabled ** <span data-label="purple"> Boolean </span>`Optional` `Example: true`

Specify whether to enable dual\-tunnel.


* true: Enable

* false (default): Disable


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The dual\-tunnel mode is in the beta stage. To request a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="default">The values of <code>DualTunnelEnabled</code> and <code>SslEnabled</code> cannot both be "true".</div>


* <div data-tips="true" data-tips-type="default">If you enable BGP, this parameter cannot be true.</div>




**SecondarySubnetId** <span data-label="purple">String</span> `optional` `Example: subnet-1b2f52ju7fojk17q7y1rk****`

The ID of the second subnet that is associated with the VPN gateway instance.

This parameter is required when enabling the dual\-tunnel mode.



**SslMaxConnections ** <span data-label="purple"> Integer  </span>`Optional` `Example: 10`

The maximum number of SSL\-VPN connections. Provide this parameter only if `SslEnabled` is set to `true`.


* 5 (default)

* 10

* 20

* 50

* 100

* 200



**Asn ** <span data-label="purple">Integer</span> `optional` `Example: 64512`

The ASN of the VPN gateway.


* To use BGP, this parameter is required.

* The value ranges for VPN gateway ASN are 64512\-65534 and 4200000000\-4294967294.



**SslEnabled ** <span data-label="purple"> Boolean </span>`optional` `Example: false`

Specify whether to enable SSL\-VPN connectivity. Values:


* true: Enable.

* false (default): Disable.


<div data-tips="true" data-tips-type="default">Description</div>


<div data-tips="true" data-tips-type="default">The values of <code>DualTunnelEnabled</code> and <code>SslEnabled</code> cannot both be "true".</div>




**IpVersion ** <span data-label="purple"> String </span>`optional` `Example: ipv4`

The IP address type of the VPN gateway. Values:


* `ipv4`: IPv4 address.

* `ipv6`: IPv6 address.


When `DualTunnelEnabled` is `false`, only `ipv4` is supported.



**IpStackType ** <span data-label="purple"> String </span>`Optional` `Example: ipv4_only`

The protocol type of the VPN gateway. Values:


* `ipv4_only`: Internet Protocol version 4 (IPv4)

* `ipv6_only`: Internet Protocol version 6 (IPv6)

* `ipv4_ipv6`: Dual\-stack (IPv4 and IPv6)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The <code>IpStackType</code> value must match the <code>IpVersion</code> value. For example, when <code>IpVersion</code> is <code>ipv4</code>, <code>IpStackType</code> supports <code>ipv4_only</code> and <code>ipv4_ipv6</code>.</div>


* <div data-tips="true" data-tips-type="default">If <code>DualTunnelEnabled</code> is set to <code>false</code>, <code>ipv6_only</code> is not supported.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example: 2022032111142501022524314704AF****`

The request ID.



**VpnGatewayId** <span data-label="purple"> String </span> `Example: vgw-12bfa2du7fojk17q7y1rk****`

The ID of the newly created VPN gateway.



**OrderId ** <span data-label="purple"> String  </span>`Example: Order7078570823273845****`

The order ID of the newly created VPN gateway.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=CreateVpnGateway&Version=2020-04-01&VpnGatewayName=test&Description=test&VpcId=vpc-12bhs1ivo6p6o17q7y2x3****&SubnetId=subnet-2fewbgn7jbk0059gp67ap****&Bandwidth=5&BillingType=1&PeriodUnit=Month&Period=1 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata":{
        "RequestId":"2022032111142501022524314704AF****",
        "Action":"CreateVpnGateway",
        "Version":"2020-04-01",
        "Service":"vpn",
        "Region":"cn-beijing"
    },
    "Result":{
        "RequestId":"2022032111142501022524314704AF****",
        "OrderId":"Order7078570823273845****",
        "VpnGatewayId":"vgw-12bfa2du7fojk17q7y1rk****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidSubnet.VpcMismatch |The specified subnet is not in the specified VPC. |The specified subnet is not within the specified VPC. |
|400 |InsufficientIpInSubnet |The specified subnet does not contain enough free private IP addresses to fulfill your request. |The available IPs under the specified subnet are insufficient. |
|400 |InsufficientResource.VpnGatewayEip |The specified region does not have enough EIP resources for VPN gateway. |The available elastic IP addresses (EIPs) of the VPN gateway are insufficient. |
|400 |QuotaExceeded.Eni |ENI number exceeded quota. |You have reached the maximum of network interfaces that can be created. |
|400 |QuotaExceeded.SecurityGroup |Security group number exceeded quota. |You have reached the maximum of security groups that you can create in a region under the current account. |
|400 |InvalidVpnGatewayBandwidth.Malformed |The specified VPN gateway bandwidth is malformed. |The specified VPN gateway bandwidth is not supported. |
|400 |InvalidBillingType.Malformed |The specified billing type is malformed. |The specified billing method is invalid. |
|400 |InvalidMonthPeriod.Malformed |The specified monthly period is malformed. Monthly period only supports 1~9, 12, 24, 36. |The specified prepaid purchase duration in months is invalid. The valid values for purchase duration in months are 1 to 9, 12, 24, and 36. |
|400 |InvalidYearPeriod.Malformed |The specified yearly period is malformed. Yearly period only supports 1~3. |The specified purchase duration in years is invalid. The purchase duration can only be 1 to 3 years. |
|400 |InvalidPeriodUnit.Malformed |The specified period unit is malformed. Pre billing period unit can only be Month or Year. |The unit specified for the subscription duration is invalid. The subscription duration unit must be Month or Year. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |PreOrderError |Failed to create pre order. |Failed to create configuration order. |
|400 |QuotaExceeded.VPNGateway |You've reached the limit on the number of VPN gateway per region that you can create. |You have reached the maximum of VPN gateways that you can create in a single region under the current account. |
|400 |QuotaExceeded.VPNGatewayEachVPC |You've reached the limit on the number of VPN gateway per VPC that you can create. |You have reached the maximum of VPN gateways that you can create in a single region under the current account. |
|400 |InsufficientResource.VpnGateway |The specified region does not have enough resources for VPN gateway. |The available resources of the VPN gateway are insufficient. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format specified for the tag is invalid. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidSslMaxConnections.Malformed |The specified SSL max connection of VPN Gateway is malformed. |The specified SSL Max Connections for the VPN gateway is invalid. |
|400 |InvalidVpnEnabled.Malformed |IpsecEnabled and SslEnabled can not be set to false at the same time. |The IPSec and SSL features cannot both be disabled. |
|400 |InvalidVpnGateway.InvalidASN |The VPN Gateway ASN is invalid and it should be in the range of 64512\-65534 or 4200000000\-4294967294. |The specified ASN is invalid. An ASN must be in the ranges of 64512\-65534 and 4200000000\-4294967294. |
|400 |InvalidSecondarySubnet.Conflict |The specified second subnet conflicts with the first subnet. |The specified second subnet conflicts with the first subnet. |
|400 |InvalidSubnet.ZoneShouldDifferent |The two subnets for creating a dual\-tunnel VPN gateway must belong to different availability zones when creating it. |The specified subnet is within the same availability zone. |
|400 |InvalidVpnGateway.BGPSupport |The dual\-tunnel VPN gateway does not support BGP. |Dual\-tunnel VPN gateways do not support Border Gateway Protocol (BGP). |
|400 |InvalidVpnGateway.SslNotSupport |The dual\-tunnel VPN gateway does not support Ssl. |Dual\-tunnel VPN gateways do not support SSL features. |
|403 |Forbidden |The specified service is temporarily unavailable. Please try again later. |The specified service is unavailable. Retry later. |
|403 |Forbidden.SharedVpc |You are not authorized to perform operations on the specified shared VPC. |No permission to perform actions on the specified shared VPC. |
|403 |Forbidden.DualTunnelVpnPermissionNotGranted |This account has no permission to create a dual\-tunnel VPN gateway. |This account does not have permission to create dual\-tunnel VPN gateways. |
|404 |InvalidSecondarySubnet.NotFound |The specified secondary subnet does not exist. |The specified second subnet does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified Virtual Private Cloud (VPC) does not exist. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidZoneId.NotFound |The specified zone does not exist. |The specified availability zone does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
