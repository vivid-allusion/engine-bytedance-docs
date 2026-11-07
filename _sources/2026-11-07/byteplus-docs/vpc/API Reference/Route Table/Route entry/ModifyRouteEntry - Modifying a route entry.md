---
title: "ModifyRouteEntry - Modifying a route entry"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry"
---

Call the ModifyRouteEntry API to modify the name and description of a custom route entry.

## Instructions

If the following optional parameters are not configured, the existing configurations will be preserved.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyRouteEntry&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifyRouteEntry`

Interface name. The current API name is `ModifyRouteEntry`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**RouteEntryId ** String必选 `Example: rte-3tj9gw2pwq3vj******`

Route entry ID.

You can call the [DescribeRouteEntryList](https://docs.byteplus.com/en/docs/vpc/DescribeRouteEntryList) API to query the route entry ID.

**RouteEntryName** String `optional` `Example: route-entry-1`

Route entry name.

* Length limit: 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: This is my first route entry`

Route entry description.

* Length limit: 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**NextHopType ** String`optional` `Example: NatGW`

* **Subnet route table**: The next hop type for custom route entries. Valid values:

   * Instance: ECS instance

   * HaVip: High\-Availability Virtual IP Address

   * NetworkInterface: Secondary network interface

   * NatGW: NAT Gateway

   * VpnGW: VPN Gateway

   * TransitRouter: Transit Router

   * GWLBEndpoint: Gateway Load Balancer Endpoint

* **Gateway route table**: The next hop type for custom route entries. Valid values:

   * NetworkInterface: Secondary network interface

   * GWLBEndpoint: Gateway Load Balancer Endpoint

> **tip**

* > The Gateway Load Balancer is currently in the invite\-only Beta stage. If you need a trial, please contact your account manager for application.

* > Only custom route tables support specifying a GWLBEndpoint. When the destination CIDR of a GWLBEndpoint matches that of a local route, the GWLBEndpoint route becomes active.

**NextHopId ** String`optional` `Example: ngw-2feq5xhimd88w59gp686****`

ID of the next hop resource.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

## Request example

```json
GET /?Action=ModifyRouteEntry&Version=2020-04-01&RouteEntryId=rte-3tj9gw2pwq3vj******&RouteEntryName=route-entry-1  HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyRouteEntry",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. A name cannot exceed 128 characters. |
|400 |InvalidRouteEntry.PublishedToCen |The specified route entry has been published to CEN. |The specified route entry has already been published to CEN and cannot be modified. |
|400 |InvalidRouteNextHop.Malformed |The specified next hop is malformed. |The specified next hop is invalid. |
|400 |InvalidVpc.InvalidStatus |The specified VPC is not in the correct status for the request. |The specified VPC is in a state that cannot respond to this request. |
|400 |InvalidVpcPeeringConnection.InvalidStatus |The specified VPC peering connection is not in the correct status for the request. The specified VPC peering connection is in freeze. |The specified Peering Connection is in a state that cannot respond to this request. The current Peering Connection is frozen. |
|403 |Forbidden.RouteNextHopType |You are not authorized to perform operations on the specified route next hop. The specified route next hop type is not allowed to modify instance. |No permission to perform actions on the route next hop type. |
|403 |Forbidden |You are not authorized to perform operations on the specified route entry. The specified route entry is a system route entry. |No sufficient permissions to perform this operation on the specified route entry. The specified route entry is a system route entry. |
|404 |InvalidRouteEntry.NotFound |The specified route entry does not exist. |The specified route entry does not exist. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another subnet in your VPC. |The specified CIDR block conflicts with another subnet's CIDR block within the same VPC. |
