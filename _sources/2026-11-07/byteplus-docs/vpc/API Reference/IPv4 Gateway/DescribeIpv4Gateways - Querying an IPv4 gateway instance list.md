---
title: "DescribeIpv4Gateways - Querying an IPv4 gateway instance list"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribeIpv4Gateways"
---

Call the DescribeIpv4Gateways API to query IPv4 gateways that meet specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeIpv4Gateways&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeIpv4Gateways`

The interface name. The current API name is `DescribeIpv4Gateways`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.

**Ipv4GatewayName ** String`optional` `Example: ipv4-gw-1`

IPv4 gateway name.

**Ipv4GatewayIds.N ** String`optional` `Example: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

* Parameter \- N: Represents the serial number of the gateway ID. The maximum number of entries per request is 100.

* Separate multiple IPv4 gateway IDs with ampersands ( & ).

**VpcIds.N ** String`optional` `Example: vpc-123456****`

VPC ID.

You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to query the VPC ID.

* Parameter \- N: Represents the serial number of the VPC ID. The maximum number of entries per request is 100.

* Separate multiple VPC IDs with ampersands ( & ).

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.

* If left blank, the query starts from the beginning.

* Provide the NextToken returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 10`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**Ipv4Gateways ** Object[]`Example: -`

Details of the IPv4 gateway.

**AccountId ** String`Example: 2000****`

The ID of the account to which the IPv4 gateway belongs.

**Enabled ** Boolean`Example: true`

Is IPv4 Gateway enabled

* true

* false

**Ipv4GatewayName ** String`Example: ipv4-gw-1`

IPv4 Gateway name.

**Description ** String`Example: ipv4-gw-master`

Description of the IPv4 Gateway.

**Ipv4GatewayId ** String`Example: ipv4gw-bp1fgnh68xyz9****`

IPv4 gateway ID.

**RouteTableId ** String`Example: rt-3tbe3o0tn849ovie****`

The route table ID associated with the IPv4 gateway.

**VpcId ** String`Example: vpc-bp15zkdt37pq72zv****`

VPC ID.

**Status ** String`Example: Available`

Status of the IPv4 gateway.

* Available

* Creating

* Pending

* Deleting

**CreationTime ** String`Example: 2024-12-28T22:57:32+08:00`

Creation time of the IPv4 Gateway.

## Request examples

```json
GET /?Action=DescribeIpv4Gateways&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeIpv4Gateways",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "Ipv4Gateways": [
            {
                "VpcId": "vpc-bp15zkdt37pq72zv****",
                "Status": "Available",
                "Enabled": true,
                "AccountId": "2000****",
                "Description": "ipv4-gw-master",
                "CreationTime": "2024-12-28T22:57:32+08:00",
                "RouteTableId": "rt-3tbe3o0tn849ovie****",
                "Ipv4GatewayId": "ipv4gw-bp1fgnh68xyz9****",
                "Ipv4GatewayName": "ipv4-gw-1"
            }
        ],
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```

## Error codes

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |Queried NextToken is invalid. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |LimitExceeded.Ipv4GatewayId |You've reached the limit on the number of Ipv4Gateway IDs that you can describe. |You have reached the maximum number of IPv4 gateway IDs that can be queried. |
|400 |LimitExceeded.VpcId |You've reached the limit on the number of VPC IDs that you can describe. |You have reached the maximum number of VPC IDs that can be queried. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
