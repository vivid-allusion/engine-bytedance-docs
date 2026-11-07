---
title: "DescribeVpnGateways - Querying VPN gateways"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways"
---

Call DescribeVpnGateways to query VPN gateways that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnGateways&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|EwucMX">必选</span> `Example: DescribeVpnGateways`

The action that you want to perform. Value: DescribeVpnGateways.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|SDDOun">必选</span> `Example: 2020-04-01`

The API version.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

Page size of the query results. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of query results


* Set this parameter to a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**VpnGatewayIds.N ** <span data-label="purple">String </span>`optional` `Example: vgw-3tehy14c6c0v****`

ID of the VPN gateway.


* N represents the sequence number of a VPN gateway ID.

* Separate multiple IDs with ampersands (&).



**VpnGatewayName ** <span data-label="purple">String </span>`optional` `Example: VpnGateway-test`

Name of the VPN gateway.



**VpcId ** <span data-label="purple">String </span>`optional` `Example: vpc-3tijjfd0ul4bwbhc****`

The ID of the Virtual Private Cloud (VPC) where the VPN gateway is deployed. You can call [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) to query the VPC ID.



**SubnetId ** <span data-label="purple">String </span>`optional` `Example: subnet-3tijjfftzh4bwbhc****`

ID of the subnet where the VPN gateway is located. You can call [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) to query the subnet ID.



**IpAddress ** <span data-label="purple">String </span>`optional` `Example: 22.XX.XX.18`

The egress IP address of the VPN gateway.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The project to which the VPN gateway belongs.


* If you provide this field, the system will query VPN gateway instances under the specified project.

* If you omit this field, the system will query VPN gateway instances across all projects.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The specified tag key when querying resources by tag.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with `&`.

* Duplicate values are not allowed.



**TagFilters.N.Values.M ** <span data-label="purple">String </span>`optional` `Example: v1`

The specified tag value when querying resources by tag.


* The first N represents the sequence number of a tag key. Valid range: 1–10.

* The second N represents the sequence number of a tag value. Valid range: 1–3. You can query up to three tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide TagFilters.N.Key.

* If you only provide TagFilters.N.Key without this parameter, the system will query all tag values of the same tag key.

* If you provide an empty string, the system will query tags with an empty tag value.

* If you set multiple TagFilters.N.Values.M values for the same TagFilters.N.Key, these TagFilters.N.Values.M values are combined with a logical OR.



**IpsecEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Describes whether IPsec connectivity is enabled.


* true: Enabled

* false: Disabled.



**SslEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Describe whether SSL connectivity is enabled.


* true: Enabled

* false: Disabled.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

The status of the VPN gateway.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**DualTunnelEnabled ** <span data-label="purple">Boolean </span>`optional` `Example: true`

Describe whether the dual\-tunnel mode is enabled for the VPN gateway. Values:


* true: Enabled

* false: Disabled



**IpVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

The IP protocol type of the VPN gateway. Values:


* ipv4

* ipv6



**IpStackType ** <span data-label="purple">String </span>`optional` `Example: ipv4_only`

The protocol stack type of the VPN gateway. Values:


* ipv4_only: IPsec tunnel supports only IPv4 traffic.

* ipv6_only: IPsec tunnel supports only IPv6 traffic.

* ipv4_ipv6: (Dual\-stack) IPsec tunnel supports both IPv4 and IPv6 traffic.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 20220322145233010225243081016A****`

Request ID.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 33`

Total number of VPN gateways meeting the query conditions.



**VpnGateways ** <span data-label="purple">Object[] </span>`Example: -`

Collection of VPN gateway information.


**AccountId ** <span data-label="purple">String </span>`Example: 20005****`

ID of the account to which the VPN gateway belongs.



**VpnGatewayId ** <span data-label="purple">String </span>`Example: vgw-3tehy13n2l4c6c0v****`

ID of the VPN gateway.



**VpcId ** <span data-label="purple">String </span>`Example: vpc-1234567****`

The ID of the VPC where the VPN gateway is deployed.



**SubnetId** <span data-label="purple">String</span> `Example: subnet-3thgqai7my4e8i4****`

The ID of the subnet to which the port used by the VPN gateway belongs.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the VPN gateway is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T08:36:47+08:00`

The time when the VPN gateway is updated.



**VpnGatewayName ** <span data-label="purple">String </span>`Example: VpnGateway-test`

Name of the VPN gateway.



**IpAddress ** <span data-label="purple">String </span>`Example: 202.XX.XX.19`

IP address of the VPN gateway.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

Description of the VPN gateway.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the VPN gateway.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

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


* financial: Being locked due to overdue payments.

* security: Being locked due to security.

* unlock: Not locked.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2022-04-21 23:59:59`

The time when the VPN gateway expires.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2022-05-06 23:59:59`

The time when the VPN gateway is deleted due to expiration.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Information about all tags associated with the VPN gateway.


**Key ** <span data-label="purple">String </span>`Example: key1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: value1`

The tag value.




**ProjectName ** <span data-label="purple">String </span>`Example: Project_1`

The project to which the VPN gateway belongs.



**IpsecEnabled ** <span data-label="purple">Boolean </span>`Example: true`

Describes whether IPsec connectivity is enabled.


* true: Enabled

* false: Disabled



**SslEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describes whether SSL connectivity is enabled.


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



**DualTunnelEnabled** <span data-label="purple">Boolean</span> `Example: true`

Describe whether the dual\-tunnel mode is enabled for the VPN gateway.


* true: Enabled

* false: Disabled



**SecondarySubnetId** <span data-label="purple">String</span> `Example: subnet-1b2f52ju7fojk17q7y1rk****`

The ID of the second subnet that is associated with the VPN gateway instance.

This parameter returns a value only for VPN gateway instances in the dual\-tunnel mode, and does not return any value for single\-tunnel VPN gateway instances.



**SecondaryIpAddress ** <span data-label="purple">String </span>`Example: 47.XX.XX.22`

The second EIP of the VPN gateway.

This parameter returns a value only for VPN gateway instances in the dual\-tunnel mode, and does not return any value for single\-tunnel VPN gateway instances.



**IpVersion ** <span data-label="purple">String </span>`Example: ipv4`

The IP protocol type of the VPN gateway.


* ipv4

* ipv6



**IpStackType ** <span data-label="purple">String </span>`Example: ipv4_only`

The protocol stack type of the VPN gateway.


* ipv4_only: IPsec tunnel supports only IPv4 traffic.

* ipv6_only: IPsec tunnel supports only IPv6 traffic.

* ipv4_ipv6: (Dual\-stack) IPsec tunnel supports both IPv4 and IPv6 traffic.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeVpnGateways&Version=2020-04-01&VpnGatewayIds.1=vgw-12bfa2du7fojk17q7y1rk****&PageNumber=1&PageSize=20 HTTP/1.1
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
        "Action": "DescribeVpnGateways",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "20220322145233010225243081016A****",
        "TotalCount": 33,
        "VpnGateways": [
            {
                "Asn": 65534,
                "Tags": [
                    {
                        "Key": "key1",
                        "Value": "value1"
                    }
                ],
                "VpcId": "vpc-1234567****",
                "Status": "Available",
                "SubnetId": "subnet-3thgqai7my4e8i4****",
                "AccountId": "20005****",
                "Bandwidth": 20,
                "IpAddress": "202.XX.XX.19",
                "IpVersion": "ipv4",
                "IsBlocked": true,
                "LockReason": "unlock",
                "RouteCount": 20,
                "SslEnabled": false,
                "UpdateTime": "2021-04-10T08:36:47+08:00",
                "BillingType": 1,
                "DeletedTime": "2022-05-06 23:59:59",
                "Description": "This is a sample description",
                "ExpiredTime": "2022-04-21 23:59:59",
                "IpStackType": "ipv4_only",
                "OverdueTime": "2023-08-07T23:23:23+08:00",
                "ProjectName": "Project_1",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "IpsecEnabled": true,
                "VpnGatewayId": "vgw-3tehy13n2l4c6c0v****",
                "BusinessStatus": "Normal",
                "VpnGatewayName": "VpnGateway-test",
                "ConnectionCount": 10,
                "DualTunnelEnabled": true,
                "SecondarySubnetId": "subnet-1b2f52ju7fojk17q7y1rk****",
                "SslMaxConnections": 10,
                "SecondaryIpAddress": "47.XX.XX.22"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.VpnGatewayId |You've reached the limit on the number of VPN gateway IDs that you can describe. |You have reached the maximum IDs of VPN gateways that you can query. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of filter tag values that can be specified in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
