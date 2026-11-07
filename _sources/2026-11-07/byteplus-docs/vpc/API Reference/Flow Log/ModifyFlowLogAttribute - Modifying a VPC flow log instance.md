---
title: "ModifyFlowLogAttribute - Modifying a VPC flow log instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/ModifyFlowLogAttribute"
---

Call the ModifyFlowLogAttribute API to modify the flow log.

## Instructions

* If the following optional parameters are not configured, the existing configurations will be preserved.

* ModifyFlowLogAttribute is an asynchronous API. When a request ID is returned, the system is still configuring in the background. You can call [DescribeFlowLogs](https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs) to check the status of flow logs. Pending indicates that the configuration is in progress, and Active indicates that the modification is complete.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyFlowLogAttribute&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: ModifyFlowLogAttribute`

The interface name. The current API name is `ModifyFlowLogAttribute`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**FlowLogId ** String必选 `Example: fl-123456****`

Flow log ID.

You can call the [DescribeFlowLogs](https://docs.byteplus.com/en/docs/vpc/DescribeFlowLogs) API to query the flow log ID.

**FlowLogName ** String`optional` `Example: FlowLog-1`

The name of the flow log.

* Must be 1 to 128 characters.

* Must start with a letter, Chinese character, or number. May include periods (.), underscores (_), and hyphens (\-).

**Description ** String`optional` `Example: FlowLog_VPC`

Flow log description.

* Must be 0 to 255 characters.

* Must start with a letter, Chinese character, or number. May include commas (,), periods (.), underscores (_), spaces ( ), equal signs (=), hyphens (\-), full\-width commas (，), and full\-width periods (。).

**AggregationInterval ** Integer`optional` `Example: 10`

Sampling interval of the flow log. Values:

* 1: 1 minute.

* 5: 5 minutes.

* 10: 10 minutes.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client token: Used to ensure request idempotency.

* You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If no ClientToken passed in, the API call does not verify idempotency.

**TrafficPath.N ** String`optional` `Example: NatGW`

Identifies the path by which traffic reaches the destination. Valid values:

* All: All traffic except the scenarios below.

* NatGW: Traffic through the NAT Gateway.

* Ipv4GW: Traffic accessing the internet through an EIP (including via IPv4 gateway).

* Ipv6GW: Traffic accessing the internet through an IPv6 gateway.

* VpnGW: Traffic through the VPN gateway.

* GWLBEndpoint: Traffic through the Gateway Load Balancer Endpoint.

* TransitRouter: Traffic through a Transit Router (TR), including traffic destined for VPCs in the same region, VPCs in cross\-regions, Direct Connect gateways, and other resources via TR.

* CEN: Traffic through Cloud Enterprise Network (CEN), including traffic destined for VPCs in the same region, VPCs in cross\-regions, Direct Connect (DC) Gateways, and other resources via CEN.

* IntraRegionVpcPeeringConnection: Traffic through a same\-region Peering Connection.

* InterRegionVpcPeeringConnection: Traffic through a cross\-region Peering Connection.

* DirectExchangeGateway: Traffic through a Direct Exchange Gateway.

**FlowLogVersion ** Integer`optional` `Example: 1`

Version of the VPC flow log.

* 1: Version 1.

* 2: Version 2.

* 3: Version 3.

* 4: Version 4.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

The request ID.

**Version ** Integer`Example: 1`

Version of the VPC flow log.

* 1: Version 1.

* 2: Version 2.

* 3: Version 3.

* 4: Version 4.

## Request example

```json
GET /?Action=ModifyFlowLogAttribute&Version=2020-04-01&FlowLogId=fl-123456****&FlowLogName=FlowLog-1&AggregationInterval=10 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyFlowLogAttribute",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "Version": 1
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The specified description format is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The specified description format is invalid. The description cannot exceed 255 characters. |
|400 |InvalidFlowLog.InvalidStatus |The specified flow log is not in the correct status for the request. |The specified flow log is in a state that cannot respond to this request. |
|400 |InvalidFlowLog.InvalidVersion |The version is not invalid. |Setting to this version is not supported. |
|400 |InvalidFlowLog.TrafficPathNotSupported |The specified flow log does not support traffic path updates. |The current version of the specified flow log does not support modifying path filter parameters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The specified name format is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The specified name format is invalid. The name cannot exceed 128 characters. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is invalid. It cannot be more than 64 ASCII characters. |
|400 |InvalidParameter.FlowLogAggregationInterval |The specified aggregation interval is invalid. |The specified flow log sampling interval parameter is invalid. |
|400 |InvalidParameter.FlowLogTrafficPath |The specified traffic path is invalid. |The specified flow log path filter parameter is invalid. |
|404 |InvalidFlowLog.NotFound |The specified flow log does not exist. |The specified flow log does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in process. |
|429 |RateLimited |Too many requests, please try again later. |Too many requests, please try again later. |
