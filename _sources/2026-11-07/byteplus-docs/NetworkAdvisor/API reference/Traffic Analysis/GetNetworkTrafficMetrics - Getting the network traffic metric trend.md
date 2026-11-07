---
title: "GetNetworkTrafficMetrics - Getting the network traffic metric trend"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/GetNetworkTrafficMetrics"
---

Call the GetNetworkTrafficMetrics API to get network traffic metric trends.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=GetNetworkTrafficMetrics&groupName=%E6%B5%81%E9%87%8F%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: GetNetworkTrafficMetrics`

Action to execute. Set the value to GetNetworkTrafficMetrics.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Region ** string必选 `Example: cn-beijing`

Region of the resource.

**EndTime ** long`optional` `Example: 1764042945000`

End timestamp, in milliseconds.

**Filters ** object[]`optional` `Example: --`

Filter condition.

**Name ** string必选 `Example: SourceIp`

Filter condition names, with values as follows:

* Internet Traffic Analysis:

   * InstanceId: EIP instance ID.

   * BandwidthPackageId: The instance ID of the bandwidth package.

   * SourceIp: Source IP.

   * DestinationIp: Destination IP.

   * SourcePort: Source port.

   * DestinationPort: Destination port.

   * Protocol: Protocol (supports TCP, UDP, ICMP, ICMPv6).

   * Country: Country of the client.

   * City: City of the client.

   * ISP: Line operator of the client.

* Cross Region Traffic Analysis:

   * InstanceId: CEN or TR instance ID.

   * SourceIp: Source IP.

   * DestinationIp: Destination IP.

   * PeerRegion: Peer Region.

* Hybird Cloud Traffic Analysis:

   * InstanceId: Direct Connect Gateway instance ID.

   * SourceIp: Source IP.

   * DestinationIp: Destination IP.

> * The **SourcePort**, **DestinationPort**, and **Protocol** filter conditions can be specified only when the **GroupBy** parameter is **Tuple5**, **Protocol**, **SourcePort**, or **DestinationPort**.

> * Duplicate filter conditions are not allowed.

**Value ** string必选 `Example: 101.XX.XX.223`

Filter condition value.

**BeginTime ** long`optional` `Example: 1764042943000`

Start timestamp, in milliseconds

Default time span is 5 minutes; maximum time span is 24 hours

**Direction ** string必选 `Example: out`

Network traffic direction. Valid values:

* in: Inbound.

* out: Outbound.

> When ResourceType is CEN or TR, fill in "out".

**MetricName ** string必选 `Example: bps`

Metric name. Valid values:

* bps: Bits per second.

* pps: Packets per second.

**ResourceType ** string必选 `Example: EIP`

The resource type. Valid values:

* EIP: EIP traffic.

* CEN: Cloud Enterprise Network traffic.

* TR: Transit Router traffic.

* DCG: Direct Connect Gateway traffic.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**Data ** object`Example: --`

Metric trend data.

**Metrics ** object[]`Example: --`

Set of metric trend data.

**Time ** string`Example: 2025-11-25 03:55:44`

Data timestamp.

**Value ** float`Example: 130.6666717529297`

Metric value.

## Request example

```text
POST /?Action=GetNetworkTrafficMetrics&Version=2020-04-01
{
    "Region": "cn-beijing",
    "EndTime": 1764042944000,
    "Filters": [
        {
            "Name": "InstanceId",
            "Value": "eip-12345678"
        }
    ],
    "BeginTime": 1764042943000,
    "Direction": "out",
    "MetricName": "bps",
    "ResourceType": "EIP"
}
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetNetworkTrafficMetrics",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": {
            "Metrics": [
                {
                    "Time": "2025-12-23 18:27:00",
                    "Value": 130.6666717529297
                }
            ]
        }
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DuplicateFilters |Filters with same Name are not allowed. |Filter conditions cannot be duplicated. |
|400 |InvalidDirection |The specified Direction is invalid. |The specified traffic direction is invalid. |
|400 |InvalidIPInFilters |There exists invalid IP address in Filters. |Filter condition contains invalid IP address. |
|400 |InvalidMetricName |The specified MetricName is invalid. |The specified metric name is invalid. |
|400 |InvalidPortInFilters |There exists invalid port in Filters. |Filter condition contains invalid ports. |
|400 |InvalidQueryDuration |query duration invalid duration must less than 24H five tuple duration must less than 5Min. |The query time range is invalid. The query range must be less than 24 hours; for quintuple queries, the range must be less than 5 minutes. |
|400 |InvalidRegion |The specified Region is invalid. |The specified region is invalid. |
|400 |InvalidResourceType |The specified ResourceType is invalid. |The specified resource type is invalid. |
|400 |RegionNotOpen |Traffic analysis is not enabled in the current region. Please enable traffic analysis first. |Traffic analysis is not enabled in the current region. Please enable traffic analysis first. |
|400 |RegionNotSupported |Current region is not support. |The current region is not yet supported. Supported regions: %s |
