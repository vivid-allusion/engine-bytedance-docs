---
title: "DescribeNetworkInterfaces - Querying a network interface list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeNetworkInterfaces"
---

Call the DescribeNetworkInterfaces API to query network interfaces (ENI) that meet the specified conditions.

## Instructions

* If multiple request parameters are provided, the query will return ENI entries that match all the specified conditions. If no matching entry is found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all ENIs belonging to this account.

* When using a tag to filter resources, you can query up to 1,000 instances associated with the specified tag. If a specified tag is associated with more than 1000 resources, only the first 1000 instances will be returned. At this point, use the [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources) API to query.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNetworkInterfaces&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选`Example: DescribeNetworkInterfaces`

Interface name. The current API name is `DescribeNetworkInterfaces`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**NetworkInterfaceName ** String`optional` `Example: eni-1`

Name of the ENI.

**NetworkInterfaceIds.N ** String`optional` `Example: eni-bp1fg6nh****`

ENI ID.

* N represents the serial number of the ENI ID. The maximum number of entries per request is 100.

* Separate multiple ENI IDs with ampersands (&).

**Type ** String`optional` `Example: secondary`

ENI type. Valid values:

* primary: Primary network interface.

* secondary: Secondary network interface.

**InstanceId ** String`optional` `Example: i-qodj57nvnc****`

ID of the ECS instance to which the ENI is attached.

You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) API to query the ECS instance ID.

**VpcId ** String`optional` `Example: vpc-bp15zckdt37pq72zv****`

ID of the VPC to which the ENI belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

**SubnetId ** String`optional` `Example: subnet-bp15zckdt37pq72zv****`

The ID of the subnet to which the ENI belongs.

You can call the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) API to query the subnet ID.

**PrimaryIpAddresses.N ** String`optional` `Example: 192.XX.XX.10`

The primary private IPv4 address of the ENI.

* N represents the sequence number of the ENI's primary private IPv4 address. A maximum of 100 addresses can be specified per single API call.

* Separate multiple primary private IPv4 addresses with ampersands (&).

**PrivateIpAddresses.N ** String`optional` `Example: 192.168.XX.10`

Secondary private IPv4 address of the ENI.

* N represents the serial number of a secondary private IPv4 address. A maximum of 100 addresses can be specified per single API call.

* Separate multiple private IPv4 addresses with ampersands (&).

> **tip**

> This parameter must be provided together with `VpcId`.

**Ipv6Addresses.N ** String`optional` `Example: 2408::153:3921:XX:XX:7b12:1c5f`

Private IPv6 address of the ENI.

* N represents the serial number of the private IPv6 address for the network interface. The maximum number of entries per request is 100.

* Separate multiple private IPv6 addresses with ampersands ( & ).

> **tip**

> The assignment of IPv6 addresses to ENIs is currently in Beta stage and temporarily only supports accounts that have completed [enterprise certification](https://docs.byteplus.com/en/docs/6261/64937) to apply for trial. If you need a trial, please contact your account manager.

**ZoneId ** String`optional` `Example: cn-beijing-a`

ID of the availability zone to which the ENI belongs. Currently supported availability zones are listed in [Regions and Availability Zones](https://docs.byteplus.com/en/docs/vpc/Regions-and-Availability-Zones).

**SecurityGroupId ** String`optional` `Example: sg-123edfgt8hhvj***`

The ID of the security group associated with the ENI.

You can call the [DescribeSecurityGroups](https://docs.byteplus.com/en/docs/vpc/DescribeSecurityGroups) API to query the security group IDs.

**Status ** String`optional` `Example: InUse`

ENI status. Valid values:

* Creating

* Available: Unattached.

* Attaching

* InUse: Attached.

* Detaching

* Deleting

**ProjectName ** String`optional` `Example: default`

The project to which the ENI belongs.

**TagFilters.N.Key ** String`optional` `Example: k1`

The tag key.

* N represents the serial number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands ( & ). Multiple tag keys have a logical AND relationship. The query returns ENIs tagged with all the specified keys.

* Duplicate values are not allowed.

**TagFilters.N.Values.N ** String`optional` `Example: v1`

The tag value.

* The first N represents the serial number of the tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns ENIs that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).

> **tip**

* > If you pass in this parameter, you must pass in `TagFilters.N.Key` first.

* > Passing an empty string queries for ENIs with an empty tag value.

**PageNumber ** Integer`optional` `Example: 1`

The page number of the list. Default: 1.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`optional` `Example: 20`

The number of rows per page for paginated queries. Maximum: 100. Default: 20.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**TotalCount ** Integer`Example: 2`

Total number of ENIs that match the conditions.

> **tip**

> This parameter is scheduled for deprecation. It becomes meaningless when using `NextToken` and `MaxResults` for paginated queries.

**PageNumber ** Integer`Example: 1`

Current page number.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`Example: 10`

The number of rows on the current page.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty result indicates no more pages.

**NetworkInterfaceSets ** Object[]`Example: -`

Collection of ENI information.

**AccountId ** String`Example: 200015`

ID of the ENI owner.

**NetworkInterfaceId ** String`Example: eni-bpacfmxazb4p****`

ENI ID.

**NetworkInterfaceName ** String`Example: eniTestName`

Name of the ENI.

**Description ** String`Example: TestDescription`

Description of the ENI.

**VpcId ** String`Example: vpc-bpacfmxazb4p****`

ID of the VPC to which the ENI belongs.

**ZoneId ** String`Example: cn-beijing-a`

ID of the availability zone to which the ENI belongs.

**VpcName ** String`Example: vpc-name`

The name of the VPC to which the ENI belongs.

**SubnetId ** String`Example: subnet-128fhnvjjgg****`

The ID of the subnet to which the ENI belongs.

**MacAddress ** String`Example: XX.XX.XX.XX.XX.XX`

MAC address of the ENI.

**DeviceId ** String`Example: i-xfgf***x`

ID of the instance to which the ENI is bound. If the ENI is not attached or the parameter `ServiceManaged` is `true`, the returned value for `DeviceId` is empty.

**Type ** String`Example: primary`

ENI type.

**PrimaryIpAddress ** String`Example: 192.XX.XX.10`

The primary private IPv4 address of the ENI.

**AssociatedElasticIp ** Object`Example: -`

Information about the EIP bound to the ENI's primary private IPv4 address.

**AllocationId ** String`Example: eip-3tc6w4446mctiq****`

The ID of the EIP.

**EipAddress ** String`Example: 101.XX.XX.199`

The address of the EIP.

**ReleaseWithInstance ** Boolean`Example: true`

Whether the EIP is deleted along with the ECS instance. Only the pay\-as\-you\-go EIP bound to the primary private IP address of the primary ENI is valid. When enabled, the EIP will be automatically released when the ECS instance is reclaimed by the system (in 24 hours after unsubscription, due to expiration, or due to arrears) or when the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API is called.

* true: Yes.

* false: No.

**PrivateIpSets ** Object`Example: -`

List of the ENI's private IPv4 addresses.

**PrivateIpSet ** Object[]`Example: -`

List of the ENI's private IPv4 addresses.

**PrivateIpAddress ** String`Example: 192.XX.XX.10`

Private IP address of the ENI.

**Primary ** Boolean`Example: true`

Whether it is the primary private IPv4 address.

* true: Primary private IPv4 address

* false: Secondary private IPv4 address

**AssociatedElasticIp ** Object`Example: -`

EIP associated with the ENI's private IPv4 address.

**AllocationId ** String`Example: eip-3tc6w4446mctiq****`

The ID of the EIP.

**EipAddress ** String`Example: 101.XX.XX.199`

The address of the EIP.

**ReleaseWithInstance ** Boolean`Example: true`

Whether the EIP is deleted along with the ECS instance. Only the pay\-as\-you\-go EIP bound to the primary private IP address of the primary ENI is valid. When enabled, the EIP will be automatically released when the ECS instance is reclaimed by the system (in 24 hours after unsubscription, due to expiration, or due to arrears) or when the [DeleteInstances](https://docs.byteplus.com/en/docs/ecs/DeleteInstances) API is called.

* true: Yes.

* false: No.

**Status ** String`Example: InUse`

Binding state of the ENI.

**PortSecurityEnabled ** Boolean`Example: true`

Enable source/destination check for the ENI. When enabled, the system will automatically block traffic whose source or destination address is not the current ENI.

* true: Yes.

* false: No.

**Attachment ** Object`Example: -`

Specify whether to delete with the Elastic Compute Service (ECS) instance.

**DeleteOnTermination ** Boolean`Example: false`

Enable delete with ECS instance.

* true: Enabled.

* false: Disabled.

**InstanceId ** String`Example: i-wijfn35c****`

ID of the ECS instance.

**ServiceManaged ** Boolean`Example: false`

Whether it is an official BytePlus service ENI. This refers to an ENI automatically created by the system when services like Transit Router, PrivateLink, or VPN Connection are established, providing VPC for the respective backend services.

* true: Yes.

* false: No.

**SecurityGroupIds ** String[]`Example: sg-9tczdi****mctjb`

The ID of the security group associated with the ENI.

**ProjectName ** String`Example: default`

The name of the project to which the ENI belongs.

**Tags ** Object[]`Example: -`

Tag information of the ENI.

**Key ** String`Example: k1`

The tag key.

**Value ** String`Example: v1`

The tag value.

**CreatedAt ** String`Example: 2021-04-09T08:36:47+08:00`

Creation time of the ENI.

**UpdatedAt ** String`Example: 2021-04-09T08:36:47+08:00`

Update time of the ENI.

**UdpTimeout ** Integer`Example: 32`

UDP flow timeout period. This specifies the maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. When the timeout is reached, the session is automatically deleted and resources are released.

**Ipv4PrefixSets ** String[]`Example: ["192.168.1.32/28"]`

IPv4 prefix delegation added to the ENI.

> **tip**

> This parameter is currently in the invite\-only Beta stage. For trial requests, contact your account manager.

**Ipv6PrefixSets ** String[]`Example: ["2001:db8:1234:XX::/80"]`

IPv6 prefix delegation added to the ENI.

> **tip**

> This parameter is currently in the invite\-only Beta stage. For trial requests, contact your account manager.

**TcpEstablishedTimeout ** Integer`Example: 910`

TCP connection idle timeout. This specifies the maximum length of time a TCP connection can be retained without data transmission. When the timeout is reached, the connection is automatically disconnected and session resources are released.

**TcpClosedAndTimeWaitTimeout ** Integer`Example: 3`

TCP connection close timeout. This specifies the maximum length of time to wait for responses during the TCP four\-way handshake termination process. If the handshake is not completed before the timeout, the connection is forcibly disconnected and session resources are released.

## Request example

```json
GET /?Action=DescribeNetworkInterfaces&Version=2020-04-01&NetworkInterfaceName=eni-1&VpcId=vpc-bp15zckdt37pq72zv****&SubnetId=subnet-bp15zckdt37pq72zv****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeNetworkInterfaces",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NetworkInterfaceSets": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Type": "primary",
                "VpcId": "vpc-bpacfmxazb4p****",
                "Status": "InUse",
                "ZoneId": "cn-beijing-a",
                "VpcName": "vpc-name",
                "DeviceId": "i-xfgf***x",
                "SubnetId": "subnet-128fhnvjjgg****",
                "AccountId": "200015",
                "CreatedAt": "2021-04-09T08:36:47+08:00",
                "UpdatedAt": "2021-04-09T08:36:47+08:00",
                "Attachment": {
                    "InstanceId": "i-wijfn35c****",
                    "DeleteOnTermination": false
                },
                "MacAddress": "XX.XX.XX.XX.XX.XX",
                "Description": "TestDescription",
                "ProjectName": "default",
                "PrivateIpSets": {
                    "PrivateIpSet": [
                        {
                            "Primary": true,
                            "PrivateIpAddress": "192.XX.XX.10",
                            "AssociatedElasticIp": {
                                "title": "网卡私网IPv4地址关联的公网IP。"
                            }
                        }
                    ]
                },
                "Ipv4PrefixSets": [
                    "192.168.1.32/28"
                ],
                "Ipv6PrefixSets": [
                    "2001:db8:1234:XX::/80"
                ],
                "ServiceManaged": false,
                "PrimaryIpAddress": "192.XX.XX.10",
                "SecurityGroupIds": [
                    ""
                ],
                "NetworkInterfaceId": "eni-bpacfmxazb4p****",
                "AssociatedElasticIp": {
                    "EipAddress": "101.XX.XX.199",
                    "AllocationId": "eip-3tc6w4446mctiq****",
                    "ReleaseWithInstance": true
                },
                "PortSecurityEnabled": true,
                "NetworkInterfaceName": "eniTestName"
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |Forbidden.TrafficMode |You are not authorized to perform operations on the specified network interface. |You do not have permission to perform operations on the specified ENI. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of queries is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |The queried NextToken is invalid. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidSecurityGroup.NotAuthorized |You are not authorized to operate invisible security group. |Hidden security groups cannot be operated without permissions. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.IPv6Addresses |You've reached the limit on the number of IPv6 addresses that you can describe. |The maximum allowed number of IPv6 addresses for a single query has been reached. |
|400 |LimitExceeded.NetworkInterfaceIDs |You've reached the limit on the number of eni IDs that you can describe. |The maximum allowed number of ENI IDs for a single query has been reached. |
|400 |LimitExceeded.PrimaryIPAddresses |You've reached the limit on the number of primary IPs that you can describe. |The maximum allowed number of primary ENI IPs for a single query has been reached. |
|400 |LimitExceeded.PrivateIPAddresses |You've reached the limit on the number of private IPs that you can describe. |The maximum allowed number of private IPs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |The maximum number of filter tag keys that can be specified in a single request has been reached. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |The maximum number of filter tag values that can be specified in a single request has been reached. |
|404 |InvalidSubnet.NotFound |The specified subnet does not exist. |The specified subnet does not exist. |
|404 |InvalidVpc.NotFound |The specified VPC does not exist. |The specified VPC does not exist. |
