---
title: "ListRules"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ListRules"
---

Gets a list of rules of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=ListRules&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ListRules` |Name of the API. The value of this parameter is `ListRules`. |
|Version |String |Yes |`2023-01-01` |Version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`8234cb50-f957-4be9-b515-55c5d419ea9e` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PolicyType |String |Yes |`geo` |Policy type corresponding to the rule.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |
|Name |String |No |`rule` |Name of the rule.<br><br>The default is an empty value, meaning this parameter is not used as a query condition. |
|Line |String |No |`os_euro_fr` |Line applicable to the rule. You can get the available line names by calling the [ListLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listlines). You must fill in the value of the `value` field returned by the API.<br><br>The default is an empty value, meaning this parameter is not used as a query condition. |
|Address |String |No |`1.1.1.1` |Address of the rule.<br><br>The default is an empty value, meaning this parameter is not used as a query condition. |
|SearchMode |String |No |`like` |Query mode. Includes the following modes:<br><br><br>* like (default): Fuzzy query.<br><br>* exact: Exact query. |
|PoolName |String |No |`pool` |Name of the pool in the rule.<br><br>The default is an empty value, meaning this parameter is not used as a query condition. |
|SortBy |String |No |`UpdateTime` |Key for sorting the returned results.<br><br><br>* Name: Sort the returned results by the value of the `Name` parameter.<br><br>* Line: Sort the returned results by the value of the `Line` parameter.<br><br>* UpdateTime: Sort the returned results by the value of the `UpdateTime` parameter. |
|SortOrder |String |No |`Desc` |Sorting direction of the returned results.<br><br><br>* Asc: Ascending order.<br><br>* Desc (default): Descending order. |
|PageSize |Integer |No |`50` |Number of pools included per page. The default is 50. BytePlus GTM will paginate the retrieved pools. The number of pages is determined by the total number of pools retrieved and `PageSize`. |
|PageNumber |Integer |No |`1` |Page number. The default is 1. The number of pages is determined by the total number of rules retrieved and `PageSize`. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result

|Name |Type |Description |
|---|---|---|
|TotalCount |Integer |Total number of pools. |
|PageNumber |Integer |Page number of the pagination. |
|PageSize |Integer |Number of pools per page. |
|Data |Array of Objects |Information about the rules. |
|CreateTime |String |Creation time of the rule. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|UpdateTime |String |Most recent modification time of the rule. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|RuleId |String |ID of the rule. |
|Name |String |Name of the rule. |
|Remark |String |Remark of the rule. |
|Disable |Boolean |Whether the rule is disabled.<br><br><br>* true: The rule is disabled.<br><br>* false: The rule is enabled. |
|Line |String |Line applicable to the rule. |
|Weight |Integer |Weight of the rule. |
|EffectivePoolSetIndex |Integer |Index of the effective pool set. |
|PoolSetMode |String |Effective mode of the pool set.<br><br><br>* auto: Automatically set the effective pool set. The highest priority available pool is automatically effective. If all pools are unavailable, the highest priority pool is effective.<br><br>* manual: Manually set the effective pool set. In this mode, you need to set the index of the effective pool set in the `EffectivePoolSetIndex` parameter. |
|PoolSets |Array of Objects |Pool sets associated with the rule. |
|PoolSetId |String |ID of the pool set. |
|Name |String |Name of the pool set. |
|Weight |Integer |Weight of the pool set. |
|ActiveCount |Integer |Minimum number of available addresses to determine if the pool set is available. For example, if you set this parameter to 10 and there are 10 available addresses in the pool, the pool set is considered available. |
|AddrType |String |Type of address.<br><br><br>* ip4: IPv4 address.<br><br>* ip6: IPv6 address.<br><br>* host: Domain name, such as www.example.com. |
|Pools |Array of Objects |Address pools. |
|PoolId |String |ID of the pool. |
|Weight |Integer |Weight of the pool. |
|PoolName |String |Name of the pool. |
|ActiveAddrThr |Integer |Minimum number of available addresses for the pool set to be considered available. For example, if you set this parameter to 1, the pool set is available if there is 1 or more available addresses. Otherwise, the pool set is unavailable. When health check is not enabled, each pool set is considered available by default. |
|Addresses |Array of Objects |Addresses in the pool. |
|Value |String |Address. |
|Weight |Integer |Weight of the address.<br><br> <br><br>For addresses without a set weight value, this parameter returns the default weight value of 1. |
|Capacity |Integer |Capacity of the address.<br><br> <br><br>For addresses without a set capacity value, this parameter returns the default capacity value of 1000. |
|Mode |String |Mechanism for determining whether the address is available.<br><br><br>* auto: Automatic mode. BytePlus GTM determines whether the address is available based on the health check results.<br><br>* always_on: The address is always available.<br><br>* always_off: The address is always unavailable. |
|Active |Boolean |Whether the pool is available.<br><br><br>* true: The address is available.<br><br>* false: The address is unavailable. |
|Latency |Integer |Latency (ms) for the health check probe to access the address. |
|PlatId |Integer |This parameter is invalid. You can ignore this parameter. |
|Area |String |This parameter is invalid. You can ignore this parameter. |
|InactiveAddrNumber |Integer |Number of unavailable addresses in the pool. |
|Active |Boolean |Whether the pool set is available.<br><br><br>* true: The pool set is available.<br><br>* false: The pool set is unavailable. |
|Disable |Boolean |Whether the pool set is disabled.<br><br><br>* true: The pool set is disabled.<br><br>* false: The pool set is not disabled. |
|Addresses |Array of objects |This parameter is invalid. You can ignore this parameter. |
|AddrType |String |Address type. |
|Probe |Object |Health check parameters of the rule. |
|Nodes |String[] |Health check probes. |
|IsManualNodes |Boolean |Whether to manually configure health check probes.<br><br><br>* true: Manually configure health check probes.<br><br>* false: Use recommended health check probes. |
|AdvisedNodeCount |Integer |Number of recommended health check probes. |
|Protocol |String |Protocol used for health check.<br><br><br>* ping: ICMP protocol.<br><br>* tcp: TCP protocol.<br><br>* http: HTTP protocol.<br><br>* https: HTTPS protocol. |
|Interval |Integer |Interval for each health check. Unit is seconds. |
|Timeout |Integer |Timeout for the health check task. Unit is seconds.<br><br><br>* ping: If the latency is greater than the value of `Timeout`, it is considered a packet loss.<br><br>* http/https: If the latency is greater than the value of `Timeout`, the result is considered abnormal. |
|PingLossPercent |Integer |Packet loss rate. Unit is percentage. If the packet loss rate is greater than the value of this parameter, the result is considered abnormal. For example, if this parameter is 10 and the packet loss rate during the health check is 11%, the result is considered abnormal.<br><br> <br><br>This parameter is only valid when the health check protocol is set to ping. |
|PingCount |Integer |Number of packets sent. If you set this parameter to 10, each ping check will send 10 packets simultaneously.<br><br> <br><br>This parameter is only valid when the health check protocol is set to ping. |
|FailedCount |Integer |The threshold for the number of health check failures to determine if an address is unavailable. For example, if you set this parameter to 3, an address will be determined as an unavailable address after 3 consecutive health check failures. The default value is 3. |
|SuccessCount |Integer |The threshold for the number of health check successes to determine if an unavailable address is available. For example, if you set this parameter to 3, an unavailable address will be determined as an available address after 3 consecutive health check successes The default value is 0.<br><br> <br><br>If you set this parameter to 0, BytePlus GTM ignores this parameter and uses its internal logic to determine whether an unavailable address will be determined as available again. |
|TcpConnTimeout |Integer |Timeout for establishing a single TCP connection. For example, if you set this parameter to 2 seconds, and the TCP connection is not successfully established within 2 seconds from the start of the health check, it is considered a connection failure.<br><br> <br><br>This parameter is only valid when the health check protocol is set to TCP. |
|Host |String |Domain name of the health check address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Port |Integer |Port of the health check address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Url |String |Path part of the health check address, starting with /.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|HttpMethod |String |HTTP request method.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|HttpHeader |Object |HTTP request headers used for health check.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. If you do not set the HTTP request headers, this parameter will not appear. |
|HttpUsabilityCodes |Array of objects |Custom range of HTTP status codes. If a probe point initiates a health check and the address returns an HTTP status code outside the range, the health check of that probe point is considered a failure. If you do not set the `HttpUsabilityCodes` parameter for the rule, this parameter will not be returned. |
|Operator |String |Operator.<br><br><br>* interval: Match values within the interval.<br><br>* include: Match specified values.<br><br>* exclude: Match values other than the specified values. |
|Codes |Array of integers |List of HTTP status codes. |
|Disable |Boolean |Whether the health check is disabled.<br><br><br>* true: Disabled.<br><br>* false: Not disabled. |
|UseRuleProbeConfig |Boolean |Whether to use the health check basic configuration of the rule.<br><br><br>* true: Use the health check basic configuration of the rule.<br><br>* false: Inherit the health check basic configuration of the policy. |
|UsePolicyProbeNodes |Boolean |Whether to inherit the health check probes of the policy.<br><br><br>* true: Inherit the health check probes of the policy.<br><br>* false: Use the health check probes of the rule. |
|ProbeMode |String |This parameter is invalid. Please ignore this parameter. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=ListRules&Version=2023-01-01&GtmId=b46cf3dc-10e5-4847-8e32-e5c7696eebd0&PolicyType=geo
```

### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2024073003190513AB2DD919B87B3EEDA1",
        "Action": "ListRules",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 100,
        "Data": [
            {
                "RuleId": "cbdb7e70-3258-41c6-899a-2f18ca5dfe54",
                "Name": "test",
                "Remark": "",
                "Disable": false,
                "Line": "default",
                "Weight": 1,
                "EffectivePoolSetIndex": 0,
                "PoolSetMode": "auto",
                "PoolSets": [
                    {
                        "PoolSetId": "34789f8c-1aa8-4c90-8e52-bb42727cac50",
                        "Name": "pool_set_1",
                        "Weight": 1,
                        "ActiveAddrThr": 1,
                        "Pools": [
                            {
                                "PoolId": "e2697a96-2cd9-4507-8499-837e30493b26",
                                "Weight": 1,
                                "PoolName": "test",
                                "Addresses": [
                                    {
                                        "Value": "1.1.1.1",
                                        "Weight": 1,
                                        "Capacity": 1000,
                                        "Mode": "auto",
                                        "Active": true,
                                        "Latency": 0,
                                        "PlatId": 0,
                                        "Area": ""
                                    }
                                ],
                                "InactiveAddrNumber": 0
                            }
                        ],
                        "Active": true,
                        "Disable": false,
                        "Addresses": [
                            {
                                "Value": "1.1.1.1",
                                "Weight": 1,
                                "Capacity": 1000,
                                "Mode": "auto",
                                "AddrId": "9f6281bc-0b0e-44b4-8dc2-52f9151ef8ef",
                                "Active": false,
                                "Latency": 0,
                                "PlatId": 0,
                                "Area": ""
                            }
                        ],
                        "AddrType": "ipv4"
                    }
                ],
                "Probe": {
                    "Nodes": [
                        "Germany, Europe",
                        "Mexico, North America",
                        "Vietnam, Asia",
                        "Chile, South America",
                        "Netherlands, Europe",
                        "Singapore, Asia",
                        "Pakistan, Asia",
                        "Peru, South America"
                    ],
                    "IsManualNodes": false,
                    "AdvisedNodeCount": 8,
                    "Protocol": "",
                    "Interval": 60,
                    "Timeout": 5,
                    "PingLossPercent": 10,
                    "PingCount": 20,
                    "FailedCount": 3,
                    "SuccessCount": 0,
                    "TcpConnTimeout": 2,
                    "Host": "",
                    "Port": 80,
                    "Url": "",
                    "HttpMethod": "GET",
                    "Disable": false
                },
                "UseRuleProbeConfig": true,
                "UsePolicyProbeNodes": false,
                "ProbeMode": "customized_base_config",
                "CreateTime": "2024-07-30T03:06:52.829Z",
                "UpdateTime": "2024-07-30T03:19:02.88Z"
            }
        ]
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
