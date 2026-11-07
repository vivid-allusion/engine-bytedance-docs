---
title: "DescribeVpnGatewayAttributes - Querying a specified VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayAttributes"
---

Call DescribeVpnGatewayAttributes to view the information of a specified VPN gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnGatewayAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|a5HXIt">必选</span> `Example: DescribeVpnGatewayAttributes`

The action that you want to perform. Value: DescribeVpnGatewayAttributes.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|rSNs5Q">必选</span> `Example: 2020-04-01`

The API version.



**VpnGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|4mki21">必选</span> `Example: vgw-3tehy13n2l4c6c0v****`

ID of the VPN gateway to be viewed. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 20220322145233010225243081016A****`

Request ID.



**AccountId ** <span data-label="purple">String </span>`Example: 20005****`

ID of the account to which the VPN gateway belongs.



**VpnGatewayId ** <span data-label="purple">String </span>`Example: vgw-3tehy13n2l4c6c0v****`

ID of the VPN gateway.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-1234567****`

The ID of the VPC where the VPN gateway is deployed.



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-3thgqai7my4e8i4****`

The ID of the subnet to which the port used by the VPN gateway belongs.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the VPN gateway is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T08:36:47+08:00`

The time when the VPN gateway is updated.



**VpnGatewayName ** <span data-label="purple">String </span>`Example: VpnGateway-test`

Name of the VPN gateway.



**IpAddress ** <span data-label="purple">String </span>`Example: 202.XX.XX.19`

The elastic IP address (EIP) of the VPN gateway.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

Description of the VPN gateway.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the VPN gateway.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 20`

The bandwidth of the VPN gateway.



**ConnectionCount ** <span data-label="purple">Integer </span>`Example: 10`

The number of IPsec\-VPN connections associated with the VPN gateway.



**RouteCount ** <span data-label="purple">Integer </span>`Example: 20`

The number of routes in the VPN gateway.



**BillingType ** <span data-label="purple">Integer </span>`Example: 1`

The billing method for the VPN gateway.


* 1: Subscription.

* 2. Pay\-as\-you\-go (specification\-based)



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

The billing status of the VPN gateway.


* Normal

* FinancialLocked: Being locked.



**LockReason ** <span data-label="purple">String </span>`Example: unlock`

The cause of the VPN gateway being locked.


* financial: Being locked due to arrears.

* security: Being locked due to security.

* unlock: Not locked.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2022-04-21 23:59:59`

The time when the VPN gateway expires.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2022-05-06 23:59:59`

The time when the resource is scheduled to be forcibly reclaimed.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Information about all tags associated with the VPN gateway.


**Key ** <span data-label="purple">String </span>`Example: key1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: value1`

The tag value.




**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The project to which the VPN gateway belongs.



**IpsecEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Describes whether the IPsec feature is enabled.


* true: Enabled

* false: Disabled



**SslEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether the SSL\-VPN feature is enabled.


* true: Enabled

* false: Disabled



**SslMaxConnections ** <span data-label="purple">Integer </span>`Example: 10`

The specification of SSL connections.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2023-08-07T23:23:23+08:00`

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.



**IsBlocked ** <span data-label="purple">Boolean </span>`Example: false`

Describes whether the current resource is blocked.


* true: Blocked.

* false: Not blocked.



**Asn ** <span data-label="purple">Integer </span>`Example: 65534`

The ASN of the VPN gateway.



**DualTunnelEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Describe whether the dual\-tunnel mode is enabled for the VPN gateway.


* true: Enabled

* false: Disabled



**SecondarySubnetId ** <span data-label="purple">String </span>`Example: subnet-1b2f52ju7fojk17q7y1rk****`

The ID of the second subnet that is associated with the VPN gateway instance.

This parameter returns a value only for VPN gateway instances in the dual\-tunnel mode, and does not return any value for single\-tunnel VPN gateway instances.



**SecondaryIpAddress ** <span data-label="purple">String </span>`Example: 47.XX.XX.22`

The second EIP of the VPN gateway.

This parameter returns a value only for VPN gateway instances in the dual\-tunnel mode, and does not return any value for single\-tunnel VPN gateway instances.



**IpStackType ** <span data-label="purple">String </span>`Example: ipv4_only`

The protocol stack type of the VPN gateway.


* ipv4_only: IPsec tunnel supports only IPv4 traffic.

* ipv6_only: IPsec tunnel supports only IPv6 traffic.

* ipv4_ipv6: (Dual\-stack) IPsec tunnel supports both IPv4 and IPv6 traffic.



**IpVersion ** <span data-label="purple">String </span>`Example: ipv4`

IP protocol type of the VPN gateway.


* ipv4

* ipv6



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpnGatewayAttributes&Version=2020-04-01&VpnGatewayId=vgw-12bfa2du7fojk17q7y1rk**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpnGatewayAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "AccountId": "20005****",
        "Asn": 65534,
        "Bandwidth": 20,
        "BillingType": 1,
        "BusinessStatus": "Normal",
        "ConnectionCount": 10,
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "DeletedTime": "2022-05-06 23:59:59",
        "Description": "This is a sample description",
        "DualTunnelEnabled": true,
        "ExpiredTime": "2022-04-21 23:59:59",
        "IpAddress": "202.XX.XX.19",
        "IpStackType": "ipv4_only",
        "IpVersion": "ipv4",
        "IpsecEnabled": true,
        "IsBlocked": true,
        "LockReason": "unlock",
        "OverdueTime": "2023-08-07T23:23:23+08:00",
        "ProjectName": "Project_1",
        "RequestId": "20220322145233010225243081016A****",
        "RouteCount": 20,
        "SecondaryIpAddress": "47.XX.XX.22",
        "SecondarySubnetId": "subnet-1b2f52ju7fojk17q7y1rk****",
        "SslEnabled": true,
        "SslMaxConnections": 10,
        "Status": "Available",
        "SubnetId": "subnet-3thgqai7my4e8i4****",
        "Tags": [
            {
                "Key": "key1",
                "Value": "value1"
            }
        ],
        "UpdateTime": "2021-04-10T08:36:47+08:00",
        "VpcId": "vpc-1234567****",
        "VpnGatewayId": "vgw-3tehy13n2l4c6c0v****",
        "VpnGatewayName": "VpnGateway-test"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
