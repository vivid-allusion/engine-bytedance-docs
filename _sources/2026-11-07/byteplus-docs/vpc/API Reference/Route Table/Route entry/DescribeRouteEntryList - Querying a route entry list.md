---
title: "DescribeRouteEntryList - Querying a route entry list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList"
---

Call the DescribeRouteEntryList API to query route entries that meet specified conditions within a given route table.

## Instructions

* When multiple request parameters are passed in, the system queries based on these parameters and returns route entries that match all conditions. If no matching route entries are found, an empty value is returned.

* If no optional request parameters are provided, all route entries in the specified route table are returned.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeRouteEntryList&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeRouteEntryList`

Interface name. The current API name is `DescribeRouteEntryList`.

**Version ** String必选`Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**RouteTableId ** String必选`Example: vtb-2fdzao4h726f45oxruw****`

ID of the route table to query.

You can call the [DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) API to query the route table ID.

**RouteEntryType ** String`optional` `Example: Custom`

The type of route entry, fixed as `Custom`.

> **tip**

> If any optional parameter is provided, this parameter must also be provided.

**RouteEntryId ** String`optional` `Example: rte-3tj9gw2pwq3vj0****`

The ID of the route entry.

**RouteEntryName ** String`optional` `Example: Test route entry`

Name of the route entry.

**NextHopType** String `optional` `Example: NetworkInterface`

* Subnet route table: The next hop type for custom route entries. Valid values:

   * Instance: ECS instance.

   * HaVip: High\-Availability Virtual IP Address.

   * NetworkInterface: Secondary network interface.

   * NatGW: NAT Gateway.

   * VpcPeer: Cloud Enterprise Network (same region).

   * RegionGW: Cloud Enterprise Network (cross\-region).

   * TransitRouter: Transit Router.

   * IPv6GW: IPv6 Gateway.

   * CloudConnector: Cloud Connector.

   * GWLBEndpoint: Gateway Load Balancer Endpoint.

   * InstanceGroup: Server group.

* Gateway Route Table: The next hop type for a route entry. Valid values:

   * NetworkInterface: Secondary network interface

   * GWLBEndpoint: Gateway Load Balancer Endpoint.

> **tip**

> Gateway Load Balancer, IPv6 Gateway, Cloud Connector, server group, and gateway route table are in the invite\-only Beta stage. If you need a trial, please contact your account manager.

**NextHopId ** String`optional` `Example: eni-2fdzbqxfwrt345oxruv******`

Next hop resource ID of the route entry.

Provide the correct resource ID based on the next hop type.

**DestinationCidrBlock ** String`optional` `Example: 8.XX.XX.1/22`

The destination CIDR block of the route entry.

**DestinationPrefixListId ** String`optional` `Example: route-prefixlist-1`

ID of the prefix list.

**PageNumber ** Integer`optional` `Example: 1`

The page number of the list. Default: 1.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`optional` `Example: 20`

The number of entries per page in a paginated query. Maximum: 100. Default: 20.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

**VpcId ** String`optional` `Example: vpc-2fdz8g5nruzuo5oxru****`

ID of the VPC to which the route table belongs.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**TotalCount ** Integer`Example: 2`

Total number of matching route entries.

> **tip**

> This parameter is scheduled for deprecation. It becomes meaningless when using `NextToken` and `MaxResults` for paginated queries.

**PageNumber ** Integer`Example: 1`

The current page number.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`Example: 10`

The number of rows on the current page.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**RouteEntries ** Object[]`Example: -`

Details of the route entry.

**Description ** String`Example: This is the first route`

Description of the route entry.

**DestinationCidrBlock ** String`Example: 8.XX.XX.0/16`

The destination CIDR block of the route entry.

**RouteEntryId ** String`Example: rte-3tj9gw2pwq3vj******`

Route entry ID.

**RouteEntryName ** String`Example: test-route`

Route entry name.

**RouteTableId ** String`Example: vtb-fadfgegg******`

ID of the route table to which the route entry belongs.

**Status ** String`Example: Available`

Route rule state.

* Pending: Configuring

* Available

**Type ** String`Example: Custom`

Route type.

* Custom: Custom route entry

* System: System route entry

**VpcId ** String`Example: vpc-3tj9fo0uqy3vj0******`

The ID of the VPC to which the route entry belongs.

**NextHopId ** String`Example: eni-2fdzbqxfwrt345oxru******`

ID of the next hop resource.

**NextHopType ** String`Example: NetworkInterface`

Next Hop type.

**PrefixListCidrBlocks ** String[]`Example: ["8.XX.XX.0/16"]`

CIDR block of the prefix list.

**NextHopName ** String`Example: eni-test`

Name of the next hop resource.

## Request example

```json
GET /?Action=DescribeRouteEntryList&Version=2020-04-01&RouteTableId=vtb-2fdzao4h726f45oxruw****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeRouteEntryList",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****",
        "RouteEntries": [
            {
                "Type": "Custom",
                "VpcId": "vpc-3tj9fo0uqy3vj0******",
                "Status": "Available",
                "NextHopId": "eni-2fdzbqxfwrt345oxru******",
                "Description": "This is the first route",
                "NextHopType": "NetworkInterface",
                "RouteEntryId": "rte-3tj9gw2pwq3vj******",
                "RouteTableId": "vtb-fadfgegg******",
                "RouteEntryName": "test-route",
                "DestinationCidrBlock": "8.XX.XX.0/16",
                "PrefixListCidrBlocks": [
                    ""
                ]
            }
        ]
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of queries is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.RouteEntryIds |You've reached the limit on the number of route entry ids that you can describe. |You have reached the maximum number of route entry IDs that can be queried. |
|403 |Forbidden |You are not authorized to create IPv6 only subnet. |You do not have permission to create IPv6\-only subnets. |
|404 |InvalidRouteNextHop.NotFound |The specified next hop does not exist. |The specified Next Hop does not exist. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
