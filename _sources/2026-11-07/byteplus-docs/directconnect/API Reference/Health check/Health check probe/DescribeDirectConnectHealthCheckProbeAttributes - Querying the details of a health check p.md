---
title: "DescribeDirectConnectHealthCheckProbeAttributes - Querying the details of a health check probe"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthCheckProbeAttributes"
---

Call the DescribeDirectConnectHealthCheckProbeAttributes API to query the details of a health check probe that meets the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectHealthCheckProbeAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|XvxZ0G">必选</span>`Example: DescribeDirectConnectHealthCheckProbeAttributes`

The interface name. The current API name is `DescribeDirectConnectHealthCheckProbeAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|6SXOTa">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckProbeId ** <span data-label="purple">String </span><span data-api-tag="require|YgGPcw">必选</span> `Example: dhp-2752hz4****`

The ID of the health check probe.

You can call [DescribeDirectConnectHealthCheckProbes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthCheckProbes) to query the health check probe ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectHealthCheckProbeId ** <span data-label="purple">String </span>`Example: dhp-2752hz4****`

The ID of the health check probe.



**DirectConnectHealthCheckProbeName ** <span data-label="purple">String </span>`Example: CheckProbes-01`

The name of the health check probe.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span>`Example: dhc-2752hz4tek****`

The ID of the health check instance.



**Description ** <span data-label="purple">String </span>`Example: This is a checkprobes`

The description of the health check probe.



**ProbeTargetIp ** <span data-label="purple">String </span>`Example: 10.XX.XX.1`

Target IP address for the health check.



**ProbeInterval ** <span data-label="purple">Integer </span>`Example: 2`

The interval between consecutive health check packets. Unit: seconds.



**ProbeThreshold ** <span data-label="purple">Integer </span>`Example: 8`

Specify the number of health check packets to send.



**ProbePacketProtocol ** <span data-label="purple">String </span>`Example: ICMP`

The protocol of the health check packet.



**ProbePort ** <span data-label="purple">Integer </span>`Example: 88`

The port of the health check packet.



**ProbePacketSize ** <span data-label="purple">Integer </span>`Example: 56`

The size of the health check packet. Unit: Byte.



**Status ** <span data-label="purple">String </span>`Example: Pending`

The status of the health check probe.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check probe is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check probe is updated.



**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the account to which the resource belongs.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectHealthCheckProbes&Version=2020-04-01&DirectConnectHealthCheckIds=dhc-2752hz4tek****&DirectConnectHealthCheckProbeIds.1=dhp-2752hz4**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectHealthCheckProbeAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "20******57",
        "CreationTime": "2021-12-07T15:57:22+08:00",
        "Description": "This is a checkprobes",
        "DirectConnectHealthCheckId": "dhc-2752hz4tek****",
        "DirectConnectHealthCheckProbeId": "dhp-2752hz4****",
        "DirectConnectHealthCheckProbeName": "CheckProbes-01",
        "ProbeInterval": 2,
        "ProbePacketProtocol": "ICMP",
        "ProbePacketSize": 56,
        "ProbePort": 88,
        "ProbeTargetIp": "10.XX.XX.1",
        "ProbeThreshold": 8,
        "Status": "Pending",
        "UpdateTime": "2021-12-07T15:57:22+08:00"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectHealthCheckProbe.NotFound |The specified direct connect health check probe does not exist. |The specified health check probe does not exist. |
