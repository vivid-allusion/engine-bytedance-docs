---
title: "CreateRouteEntry - Creating a route entry"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry"
---

Call the CreateRouteEntry API to add a custom route entry to the route table.

## Instructions

* A single route table can create up to 200 custom route entries by default. If the default quota cannot meet your needs, go to the [Quota Center](https://console.byteplus.com/quota/productList/coParameterList?ProviderCode=VPC) to increase the corresponding quota.

* CreateRouteEntry is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) to check the status of route entries; `Pending` means configuring, and `Available` means configuration complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateRouteEntry&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateRouteEntry`

The API name. The current API name is `CreateRouteEntry`.

**Version ** String必选 `Example: 2020-04-01`

The API version. The current API version is `2020-04-01`.

**RouteTableId ** String必选 `Example: vtb-2fdzao4h726f45oxruw******`

Route table ID.

You can call the [DescribeRouteTableList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteTableList) API to query the route table ID.

**RouteEntryName ** String`optional` `Example: route-entry-1`

Route entry name.

* The name must start with a letter, Chinese character, or number. It may contain periods (.), underscores (_), and hyphens (\-).

* Length limit: 1 to 128 characters

* If left blank, this defaults to an empty string.

**Description ** String`optional` `Example: This is first route entry`

Description of the route entry.

* Must start with a letter, Chinese character, or number. It may include half\-width commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

* Length limit: 0 to 255 characters.

* If left blank, this defaults to an empty string.

**NextHopName ** String`optional` `Example: eni-01`

Name of the next hop resource for the route entry.

**NextHopType ** String必选 `Example: NetworkInterface`

* **Subnet route table**: The next hop type for custom route entries. Valid values:

   * Instance: ECS instance.

   * HaVip: High\-Availability Virtual IP Address.

   * NetworkInterface: Secondary network interface.

   * NatGW: NAT Gateway.

   * VpnGW: VPN Gateway.

   * TransitRouter: Transit Router.

   * IPv6GW: IPv6 Gateway.

   * CloudConnector: Cloud Connector.

   * GWLBEndpoint: Gateway Load Balancer Endpoint.

* **Gateway route table**: The next hop type for custom route entries. Valid values:

   * NetworkInterface: Secondary network interface.

   * GWLBEndpoint: Gateway Load Balancer Endpoint.

> **tip**

* > Gateway Load Balancer, Cloud Connector, IPv6 Gateway, and Gateway Route Table are in the invite\-only Beta stage. For a trial, contact your account manager.

* > Custom subnet route tables support GWLBEndpoint as a valid parameter. When the destination CIDR of a GWLBEndpoint matches that of a local route, the GWLBEndpoint route takes precedence.

* > If GWLBEndpoint is specified as the NextHopType in a gateway route table, the DestinationCidrBlock can be a subset of the subnet CIDR (e.g., /32).

**NextHopId ** String`optional` `Example: eni-2fdzbqxfwrt345oxru******`

Next hop resource ID.

Provide the correct resource ID based on the next hop type.

**DestinationCidrBlock ** String`optional` `Example: 8.XX.XX.8/32`

The destination CIDR block of the route entry.

> **tip**

* > When `NextHopType` is set to "IPv6GW", this parameter can only be ::/0.

* > At least one of the parameters `DestinationCidrBlock` and `DestinationPrefixListId` must be provided.

**DestinationPrefixListId ** String`optional` `Example: pl-bp1fg655nh68xyz9****`

ID of the prefix list.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the Prefix List ID.

> **tip**

* > At least one of the parameters `DestinationCidrBlock` and `DestinationPrefixListId` must be provided.

* > Gateway route tables do not support this parameter.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RouteEntryId** String `Example: rte-3tj9gw2pwq3vj0******`

ID of the newly added route entry.

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=CreateRouteEntry&Version=2020-04-01&RouteTableId=vtb-2fdzao4h726f45oxruw******&DestinationCidrBlock=8.XX.XX.8/32&NextHopType=NetworkInterface&NextHopId=eni-2fdzbqxfwrt345oxru******&RouteEntryName=RouteEntry_1 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "CreateRouteEntry",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "RouteEntryId": "rte-3tj9gw2pwq3vj0******"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidCidrBlock.Reserved |The specified CidrBlock is reserved for system use. |This network segment has been reserved by the system, and operations on it are prohibited. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidEni.InvalidStatus |The specified elastic network interface is not in the correct status for the request. |The specified Elastic Network Interface is not in a status that can respond to this request. |
|400 |InvalidGatewayRouteTablePrefixList.Malformed |The specified gateway route table does not support prefix list. |The specified gateway route table does not support Prefix List. |
|400 |InvalidGroup.NotExist |The specified default resource not exist in current route next hop group. |The specified default resource does not exist in the next\-hop route group. |
|400 |InvalidGroupItem.MissingDefault |The specified route next hop group is missing a default item. |The specified route next hop group lacks a default entry. |
|400 |InvalidGroupResource.TypesInconsistent |The types of all resources within the RouteNextHopGroup are inconsistent. |The next hop routing group contains resources with inconsistent IP types. |
|400 |InvalidInstanceGroup.InvalidStatus |The specified instance group is not in the correct status for the request. |The specified server group is in a status that cannot respond to the request. |
|400 |InvalidIpv4Gateway.VpcMismatch |The specified IPv4 gateway is not attached to the specified VPC. |The specified IPv4 Gateway is not associated with the specified VPC. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of the specified ClientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidParameter.IpVersion |The specified IP version is not supported. |The specified IP address type is not supported. |
|400 |InvalidPrefixListAssociation.InUse |The specified prefix list is already associated with the same resource. |The specified prefix list is referenced by same resource. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidRouteCidr.UnsupportedCidr |The specified CIDR is not supported, you can change the CIDR to ::/0. |The specified CIDR block is not supported. You can change to ::/0 and try again. |
|400 |InvalidRouteCidr.UnsupportedIPv6Cidr |The specified CIDR is not supported. The specified CIDR block is not supported for IPv6. |The specified CIDR block is not supported. The specified CIDR block does not support IPv6. |
|400 |InvalidRouteNextHop.IPv6Only |The specified next hop only supports IPv6. |The specified next hop only supports IPv6. |
|400 |InvalidRouteNextHop.Inactive |The specified next hop does not contain active ECMP members. |There are no active members in the specified next‑hop ECMP group. |
|400 |InvalidRouteNextHop.Malformed |The specified next hop is malformed. |The specified next hop is invalid. |
|400 |InvalidRouteNextHop.Malformed |The specified next hop is malformed. Next hop not support IPv6. |The specified next hop does not support IPv6. |
|400 |InvalidVpc.EnableIpv6 |Operation failed because IPv6 is not enabled for the VPC. |The specified VPC does not have IPv6 enabled. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot process this request. |
|400 |QuotaExceeded.PrefixListAssociation |The number of resources a prefix list can be referenced by exceeded quota. |The number of resources associated with the prefix list has exceeded the quota limit. |
|400 |QuotaExceeded.RouteEntry |Route entry of a route table number exceeded quota. |Reached the maximum route entries that you can create. |
|403 |Forbidden.DualTunnelVpnGatewayRoute |You are not authorized to perform operations on the specified route of dual tunnel VPN gateway. |You do not have permission to create dual‑tunnel VPN gateway routes. |
|403 |Forbidden.RouteNextHopType |You are not authorized to perform operations on the specified route next hop. The specified route next hop type is not allowed to modify instance. |No sufficient permissions to perform this operation on the specified route next hop type. The specified route next hop type does not allow instance modifications. |
|403 |Forbidden |You are not authorized to perform operations on the specified route table. The specified route table is a system route table. |No sufficient permissions to perform this operation on the specified route table. The specified route table is the system route table. |
|404 |InvalidEniId.NotFound |The specified elastic network interface does not exist. |The specified ENI does not exist. |
|404 |InvalidGroup.NotFound |The specified RouteNextHopGroup does not exist. |The specified next\-hop route group does not exist. |
|404 |InvalidIpv4Gateway.NotFound |The specified Ipv4Gateway does not exist. |The specified IPv4 Gateway does not exist. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified prefix list does not exist. |
|404 |InvalidRouteNextHop.NotFound |The specified next hop does not exist. |The specified Next Hop does not exist. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the same route table. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another subnet in your VPC. |The specified CIDR block conflicts with another subnet's CIDR block within the same VPC. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
