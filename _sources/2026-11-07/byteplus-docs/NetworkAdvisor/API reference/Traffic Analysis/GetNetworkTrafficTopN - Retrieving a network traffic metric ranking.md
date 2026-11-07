---
title: "GetNetworkTrafficTopN - Retrieving a network traffic metric ranking"
product: "Network Advisor"
product_code: "NetworkAdvisor"
source: "https://docs.byteplus.com/en/docs/NetworkAdvisor/GetNetworkTrafficTopN"
---

Call the GetNetworkTrafficTopN API to retrieve the network traffic metric ranking.

## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=GetNetworkTrafficTopN&groupName=%E6%B5%81%E9%87%8F%E5%88%86%E6%9E%90&serviceCode=na&version=2020-04-01)

## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** string必选 `Example: GetNetworkTrafficTopN`

Action to execute. Set the value to GetNetworkTrafficTopN.

**Version ** string必选 `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.

**Region ** string必选 `Example: cn-beijing`

Region of the resource.

**SortBy ** string必选 `Example: ByteCount`

Sorting metric. Valid values:

* ByteCount: The byte count of the traffic.

* PacketCount: The packet count of the traffic.

**EndTime ** long`optional` `Example: 1764045943000`

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

**Value ** string必选`Example: 101.XX.XX.223`

Filter condition value.

**GroupBy ** string必选 `Example: Tuple1`

The dimension for traffic statistics sorting. Valid values:

* Internet Traffic Analysis:

   * Tuple1: Single (cloud IP).

   * Tuple2: Pair (source and destination IP).

   * Tuple5: Five\-tuple (source and destination IP, source and destination port, protocol).

   * Protocol

   * Country: Country of the client.

   * City: City of the client.

   * ISP: Line operator of the client.

   * SourcePort: Source port (supported only when Direction is out).

   * DestinationPort: Destination port (supported only when Direction is in).

* Cross Region Traffic Analysis:

   * Tuple1: Single (source IP).

   * Tuple2: Pair (source and destination IP).

   * PeerRegion: Peer region.

   * InstanceId: Cloud Enterprise Network (CEN) or Transit Router (TR) instance ID.

* Hybird Cloud Traffic Analysis:

   * Tuple1: Single (cloud IP).

   * Tuple2: Pair (source and destination IP).

   * InstanceId: Direct Connect Gateway instance ID.

**TopCount ** integer`optional` `Example: 10`

The number of top\-ranked data entries after sorting.

* Value range: 1\-100.

* Default value: 10.

**BeginTime ** long`optional` `Example: 1764042943000`

Start timestamp, in milliseconds.

Default time span is 5 minutes; maximum time span is 24 hours.

**Direction ** string必选 `Example: out`

Network traffic direction. Valid values:

* in: Inbound.

* out: Outbound.

> When ResourceType is CEN or TR, fill in "out".

**SortOrder ** string`optional` `Example: desc`

The sorting method. Valid values:

* asc: Sort in ascending order.

* desc (default): Sort in descending order.

**ResourceType ** string必选 `Example: TR`

The resource type. Valid values:

* EIP: EIP traffic.

* CEN: Cloud Enterprise Network traffic.

* TR: Transit Router traffic.

* DCG: Direct Connect Gateway traffic.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**Data ** object[]`Example: --`

Metric ranking data.

**Isp ** string`Example: China Mobile`

Line operator of the client.

**City ** string`Example: Beijing`

City of the client.

**Country ** string`Example: China`

Country of the client.

**Protocol ** string`Example: TCP`

Protocol.

* TCP

* UDP

* ICMP

* ICMPv6

**SourceIp ** string`Example: 101.XX.XX.110`

Source IP.

**ByteCount ** long`Example: 100`

Traffic bytes.

**InstanceId ** string`Example: cen-7qthudw0ll6jmc****`

Instance ID.

**PeerRegion ** string`Example: cn-beijing`

Peer region.

**SourcePort ** integer`Example: 80`

Source port.

**PacketCount ** long`Example: 1000`

Number of traffic packages.

**DestinationIp ** string`Example: 19.XX.XX.19`

Destination IP.

**TrAttachmentId ** string`Example: tr-attach-7qthudw0ll6jmc****`

Transit Router cross\-region connection instance ID.

**DestinationPort ** integer`Example: 80`

The destination port.

## Request example

```text
POST /?Action=GetNetworkTrafficTopN&Version=2020-04-01
{
    "Region": "cn-beijing",
    "SortBy": "ByteCount",
    "EndTime": 1764045943000,
    "Filters": [
        {
            "Name": "SourceIp",
            "Value": "101.126.83.223"
        }
    ],
    "GroupBy": "Tuple1",
    "TopCount": 10,
    "BeginTime": 1764042943000,
    "Direction": "out",
    "SortOrder": "desc",
    "ResourceType": "EIP"
}
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Version": "2020-04-01",
        "Service": "na",
        "Region": "cn-beijing"
    },
    "Result": {
        "Data": [
            {
                "Isp": "China Mobile",
                "City": "Beijing",
                "Country": "China",
                "Protocol": "TCP",
                "SourceIp": "101.XX.XX.110",
                "ByteCount": 100,
                "InstanceId": "tr-7qthudw0ll6jmc****",
                "PeerRegion": "cn-beijing",
                "SourcePort": 80,
                "PacketCount": 1000,
                "DestinationIp": "19.XX.XX.19",
                "TrAttachmentId": "tr-attach-7qthudw0ll6jmc****",
                "DestinationPort": 80
            }
        ]
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DuplicateFilters |Filters with same Name are not allowed. |Filter conditions cannot be duplicated. |
|400 |FiltersUnsupportedForGroupBy |The specified Filters are unsupported for the requested GroupBy |The specified filter condition is not supported under the current grouping dimension. |
|400 |GroupByUnsupportedForDirection |The specified GroupBy is unsupported for the requested Direction. |The specified grouping dimension is not supported for the requested traffic direction. |
|400 |InvalidDirection |The specified Direction is invalid. |The specified traffic direction is invalid. |
|400 |InvalidGroupBy |The specified GroupBy is invalid. |The specified grouping dimension is invalid. |
|400 |InvalidIPInFilters |There exists invalid IP address in Filters. |Filter condition contains invalid IP address. |
|400 |InvalidPortInFilters |There exists invalid port in Filters. |Filter condition contains invalid ports. |
|400 |InvalidQueryDuration |query duration invalid duration must less than 24H five tuple duration must less than 5Min. |The query time range is invalid. The query range must be less than 24 hours; for quintuple queries, the range must be less than 5 minutes. |
|400 |InvalidRegion |The specified Region is invalid. |The specified region is invalid. |
|400 |InvalidResourceType |The specified ResourceType is invalid. |The specified resource type is invalid. |
|400 |InvalidSortBy |The specified SortBy is invalid. |The specified sorting metric is invalid. |
|400 |InvalidSortOrder |The specified SortOrder is invalid. |The specified sorting method is invalid. |
|400 |MissingParameter |The request is missing a required parameter. Ensure that you have supplied all the required parameters for the request, for example, the ''. |This request does not contain required parameters. Ensure the request includes all required parameters, such as . |
|400 |RegionNotOpen |Traffic analysis is not enabled in the current region. Please enable traffic analysis first. |Traffic analysis is not enabled in the current region. Enable traffic analysis first. |
|400 |RegionNotSupported |Current region is not support. |The current region is not yet supported. Supported regions: %s |
|400 |TopCountOutOfRange |The specified TopCount is out of range (1\-100). |The specified number of data entries exceeds the allowed range (1\-100). |
|401 |ServiceRoleUnauthorized |service role is unauthorized |Role not authorized. Please visit the IAM console to grant the required permissions first |
