---
title: "DescribeNLBListenerHealth - Viewing the backend server health status"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/DescribeNLBListenerHealth"
---

You can call the DescribeNLBListenerHealth API to query the health status of the backend server associated with the listener.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeNLBListenerHealth&serviceCode=clb&version=2020-04-01&groupName=)

## Request parameters

**Action ** String必选 `Example: DescribeNLBListenerHealth`

Action to execute. Set the value to DescribeNLBListenerHealth.

**Version ** String必选 `Example: 2020-04-01`

Current API version is 2020\-04\-01.

**ListenerId ** String必选 `Example: lsn-2fek3rgsxhrsw5oxruwec****`

Listener ID.

You can call the [DescribeNLBListeners](https://docs.byteplus.com/en/docs/clb/DescribeNLBListeners) API to obtain the listener ID.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that marks the position for paginated queries. Leave it empty for the initial call. For subsequent queries, set this value to the `NextToken` parameter returned by the previous API call.

**MaxResults ** Integer`optional` `Example: 10`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

**RequestId ** String`Example: 2024092952539010225146063030****`

Request ID.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The query token returned by this API call. An empty value indicates that there is no next page.

**ListenerId ** String`Example: lsn-defyhgsiy5jggkl****`

Listener ID.

**ServerGroupId ** String`Example: rsp-qwsdjekl67tgh****`

Server group ID.

**HealthyCount ** Integer`Example: 1`

Number of normal backend servers in the server group.

**UnhealthyCount ** Integer`Example: 0`

Number of exception backend servers in the server group.

**Status ** String`Example: Active`

Status of the server group.

* NoTarget: includes the following two scenarios:

   * No backend servers added to the server group

   * The server group has disabled cross\-az forwarding, and there is no backend server in the group corresponding to the availability zone of the traffic.

* Error: There are exception backend servers in the server group.

* Active: All backend servers in the server group are normal.

* Disabled: includes the following two scenarios:

   * Server group has disabled health check.

   * The NLB instance attached to the server group is in a suspended status.

**Results ** Object[]`Example: --`

Detailed information about the eligible backend servers.

**ServerId ** String`Example: rs-2fel9yaoyv75s5oxruux5****`

Backend server ID.

**ServerType ** String`Example: eni`

Type of backend server.

* ecs: Elastic Compute Service (ECS) instance (i.e., primary network interface)

* eni: Secondary network interface

* ip: IP address

**InstanceId ** String`Example: eni-e3elrfaaqverf5oedru3r****`

The instance ID or IP address of the backend server.

**ZoneId ** String`Example: cn-beijing-a`

Availability zones from which the backend server receives access traffic.

**Ip ** String`Example: 192.XX.XX.8`

The IP address of the backend server.

**Port ** Integer`Example: 443`

The port on which the backend server provides services.

**Status ** String`Example: Up`

The health status of the backend server.

* Up: Normal.

* Down: Abnormal

* Unused: Not used. NLB instance has cross\-az forwarding disabled and no access traffic from the backend server's availability zone.

## Request examples

```json
GET /?Action=DescribeNLBListenerHealth&Version=2020-04-01&ListenerId=lsn-2fek3rgsxhrsw5oxruwec****&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=10 HTTP/1.1
Host: clb.cn-beijing.byteplusapi.com.cn
Date: 20260310T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/clb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response examples

```json
{ 
    "ResponseMetadata": { 
        "RequestId": "20230604110420****100232280022D31", 
        "Action": "DescribeNLBListenerHealth", 
        "Version": "2020-04-01", 
        "Service": "clb", 
        "Region": "cn-beijing" 
    }, 
    "Result": { 
        "HealthyCount": 1, 
        "ListenerId": "lsn-defyhgsiy5jggkl****", 
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****", 
        "RequestId": "2024092952539010225146063030****", 
        "Results": [ 
            { 
                "Ip": "192.XX.XX.8", 
                "Port": 443, 
                "Status": "Up", 
                "ZoneId": "cn-beijing-a", 
                "ServerId": "rs-2fel9yaoyv75s5oxruux5****", 
                "InstanceId": "eni-e3elrfaaqverf5oedru3r****", 
                "ServerType": "eni" 
            } 
        ], 
        "ServerGroupId": "rsp-qwsdjekl67tgh****", 
        "Status": "Active", 
        "UnhealthyCount": 0 
    } 
}
```

## Error codes

This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/NLB-Common-Error-Codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken format is invalid. |
|400 |InvalidMaxResult.Malformed |The specified MaxResult is malformed. |The specified MaxResult parameter format is invalid. |
|400 |InvalidMaxResults.Malformed |The specified MaxResults is malformed. |The specified MaxResults parameter format is invalid. |
|400 |InvalidNextToken.Malformed |The specified NextToken is malformed. |The specified NextToken parameter format is invalid. |
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|404 |InvalidListener.NotFound |The specified Listener does not exist. |The specified listener does not exist. |
|409 |InvalidOperation.Conflict |The specified resource operation conflicts. |The specified resource action conflicted. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
