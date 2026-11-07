---
title: "UpdateRule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/UpdateRule"
---

Updates a rule.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=UpdateRule&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRule` |Name of the API. The value of this parameter is `UpdateRule`. |
|Version |String |Yes |`2023-01-01` |Version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh) |
|RuleId |String |Yes |`c3f65de3-7b01-4ad5-8225-d0e42ced2e05` |The ID of the rule. You can obtain the rule ID through the [ListRules API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListRules). |
|PolicyType |String |Yes |`geo` |The policy type corresponding to the rule.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |
|Rule |Object |Yes | |The rule. |
|Name |String |Yes |`Rule` |The name of the rule. |
|Remark |String |No |`Remark` |The remark for the rule. Default is an empty string. UTF\-8 format. Maximum length is 128 UTF\-8 characters. |
|Line |String |Yes |`default` |The line to which the rule applies. You can obtain available line names by calling the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listlines). You must fill in the value of the `value` field returned by the API. |
|Weight |Integer |No |`1` |The weight of the rule. Default value is 1. |
|Disable |Boolean |No |`false` |Whether to disable this rule.<br><br><br>* true: Disable this rule.<br><br>* false: (Default) Enable this rule. |
|PoolSetMode |String |No |`auto` |The effective mode of the pool set.<br><br><br>* (Default) auto: Automatically set the effective pool set. The available pool with the highest priority automatically takes effect. If all pools are unavailable, the pool with the highest priority takes effect.<br><br>* manual: Manually set the effective pool set. In this mode, you need to set the index of the effective pool set in the `EffectivePoolSetIndex` parameter. |
|EffectivePoolSetIndex |Integer |No |`0` |The index of the effective pool set, starting from 0. Default is 0. The index corresponds to the position of the pool in the pool set array in the `PoolSets` parameter. This parameter is valid only when you set `PoolSetMode` to `manual`. |
|PoolSets |Array of Objects |Yes | |One or more pool sets. The order of the array represents the priority of the pool sets. |
|Name |String |Yes |`Pool set` |The name of the pool set. UTF\-8 format. Maximum length is 32 UTF\-8 characters. |
|ActiveAddrThr |Integer |No |`1` |The minimum number of available addresses for the pool set to be considered available. For example, if you set this parameter to 1, the pool set is available if there is 1 or more available addresses. Otherwise, the pool set is unavailable. Default value is 1. When health check is not enabled, each pool set is considered available by default. |
|Pools |Array of Objects |Yes | |One or more pools contained in the pool set. |
|PoolId |String |Yes |`cf65f46e-6a19-4d15-99b5-684a6ce4e7ff` |ID of the pool. You can get the ID of the pool from the [CreatePool API](https://docs.byteplus.com/docs/byteplus-dns-suite/CreatePool) or the [ListPools API](https://docs.byteplus.com/docs/byteplus-dns-suite/ListPools). |
|Weight |Integer |No |`1` |The weight of the pool. Default value is 1. |
|UseRuleProbeConfig |Boolean |No |`true` |Whether to use the health check basic configuration of the rule.<br><br><br>* true: Use the health check basic configuration of the rule.<br><br>* false (default): Inherit the health check basic configuration of the policy. |
|UsePolicyProbeNodes |Boolean |No |`true` |Whether to inherit the health check probes of the policy.<br><br><br>* true: Inherit the health check probes of the policy.<br><br>* false (default): Use the health check probes of the rule. |
|Probe |Object |No | |Health check parameters. |
|Disable |Boolean |No |`false` |Whether to disable health check.<br><br><br>* true: Disable health check.<br><br>* false: (Default) Enable health check. |
|Protocol |String |No |`ping` |The protocol used for health check.<br><br><br>* ping: ICMP protocol.<br><br>* tcp: TCP protocol.<br><br>* http: HTTP protocol.<br><br>* https: HTTPS protocol. |
|Interval |Integer |No |`60` |The time interval for health checks (in seconds). The shorter the interval, the faster BytePlus GTM detects unavailable addresses and triggers failover, but the higher the cost. This parameter only supports the following values:<br><br><br>* 60: (Default) The health check interval is 60 seconds.<br><br>* 15: The health check interval is 15 seconds. |
|Timeout |Integer |Yes |`5` |The timeout for health check tasks. Unit: seconds.<br><br><br>* ping: If the delay is greater than the value of `Timeout`, it is considered a packet loss.<br><br>* http/https: If the delay is greater than the value of `Timeout`, the result is considered abnormal. |
|PingCount |Integer |No |`10` |The number of packets sent. If you set this parameter to 10, each ping check will send out 10 data packets simultaneously.<br><br> <br><br>If you set the `Protocol` parameter to `ping`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|PingLossPercent |Integer |No |`10` |The packet loss rate. Unit: percentage. If the packet loss rate is greater than the value of this parameter, the result is considered abnormal. For example, if this parameter is 10 and the packet loss rate during health check is 11%, the result is considered abnormal.<br><br> <br><br>If you set the `Protocol` parameter to `ping`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|FailedCount |Integer |No |`3` |The threshold for the number of health check failures to determine if an address is unavailable. For example, if you set this parameter to 3, an address will be determined as an unavailable address after 3 consecutive health check failures. The default value is 3. |
|SuccessCount |Integer |No |`3` |The threshold for the number of health check successes to determine if an unavailable address is available. For example, if you set this parameter to 3, an unavailable address will be determined as an available address after 3 consecutive health check successes. The default value is 0.<br><br> <br><br>If you set this parameter to 0, BytePlus GTM ignores this parameter and uses its internal logic to determine whether an unavailable address will be determined as available again. |
|TcpConnTimeout |Integer |No |`2` |The timeout for establishing a single TCP connection. For example, if you set this parameter to 2 seconds, if a TCP connection is not established successfully within 2 seconds from the start of establishment during a health check, it will be considered a connection failure. The default value is 2 seconds. |
|Host |String |No |`www.example.com` |The complete domain name of the health check target address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Port |Integer |No |`80` |The port of the health check target address.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|Url |String |No |`/content/pages` |The path part of the health check target address, starting with `/`.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|Host |String |No |`www.example.com` |The complete domain name of the health check target address.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpMethod |String |No |`get` |The HTTP request method used for health check.<br><br><br>* get<br><br>* post<br><br>* head<br><br>* put<br><br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpHeader |Object |No |`{"Content-type": "application/json","Content-Length": "1234"}` |The HTTP request headers used for health check.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpUsabilityCodes |Array of objects |No |`{"Operator": "interval", "Codes": [100,200]}` |Define a custom range of HTTP status codes. After a probe point initiates a health check, if the target address returns an HTTP status code outside this range, the health check from this probe point is considered failed. If you set the `Protocol` parameter to a value other than `http` or `https`, this parameter is invalid. By default, if the HTTP status code is a number outside the range of 200 to 399, the health check is considered failed. |
|Operator |String |No |`interval` |The operator.<br><br><br>* interval: Match values within the interval.<br><br>* include: Match specified values.<br><br>* exclude: Match values other than the specified ones. |
|Codes |Array of integers |No |`[100,200]` |List of HTTP status codes. If `Operator` is `interval`, you need to fill in 2 values. If `Operator` is `include` or `exclude`, you need to fill in at least 1 value. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

## Example

### Request example

```JSON
POST https://gtm.byteplusapi.com/?Action=UpdateRule&Version=2023-01-01

{
    "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
  "RuleId": "c3f65de3-7b01-4ad5-8225-d0e42ced2e05",
    "Rule": {
        "Name": "TestRule",
        "Remark": "",
        "Disable": false,
        "Line": "default",
        "Weight": 1,
        "PoolSets": [
            {
                "Name": "PoolSet1",
                "Pools": [
                    {
                        "PoolId": "cf65f46e-6a19-4d15-99b5-684a6ce4e7ff",
                        "Weight": 1
                    }
                ]
            }
        ],
        "Probe": {
            "Disable": false
        },
        "UseRuleProbeConfig": false,
        "UsePolicyProbeNodes": false
    }
}
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023072718230548623722C3A60BA95BBE",
        "Action": "UpdateRule",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
