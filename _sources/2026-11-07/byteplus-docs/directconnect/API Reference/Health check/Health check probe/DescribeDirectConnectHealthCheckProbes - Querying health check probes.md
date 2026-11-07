---
title: "DescribeDirectConnectHealthCheckProbes - Querying health check probes"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthCheckProbes"
---

Call the DescribeDirectConnectHealthCheckProbes API to query the details of health check probes that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectHealthCheckProbes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DY8LOs">必选</span> `Example: DescribeDirectConnectHealthCheckProbes`

The interface name. The current API name is `DescribeDirectConnectHealthCheckProbes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Ppz0oI">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckProbeIds.N ** <span data-label="purple">String </span>`optional` `Example: dhp-2752hz4****`

The ID of the health check probe.


* N represents the sequence number of a health check instance. You can call a maximum of 100 instances in a single request.

* Separate multiple health check instances with ampersands (&).



**DirectConnectHealthCheckProbeName ** <span data-label="purple">String </span>`optional` `Example: CheckProbes-01`

The name of the health check probe.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If you omit it or set it to 0, the value defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span>`optional` `Example: dhc-2752hz4tek****`

The ID of the health check instance where the health check probe is located.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

Total number of health check probes that meet the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**DirectConnectHealthCheckProbes ** <span data-label="purple">Object[] </span>`Example: -`

Details of the health check instance


**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the account to which the resource belongs.



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



**ProbeThreshold ** <span data-label="purple">Integer </span>`Example: 5`

Specify the number of health check packets to send.



**ProbePacketProtocol ** <span data-label="purple">String </span>`Example: ICMP`

The protocol of the health check packet.



**ProbePort ** <span data-label="purple">Integer </span>`Example: 10000`

The port of the health check packet.



**ProbePacketSize ** <span data-label="purple">Integer </span>`Example: 100`

The size of the health check packet. Unit: Byte.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the health check probe.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check probe is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check probe is updated.




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
        "Action": "DescribeDirectConnectHealthCheckProbes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectHealthCheckProbes": [
            {
                "Status": "Available",
                "AccountId": "20******57",
                "ProbePort": 10000,
                "UpdateTime": "2021-12-07T15:57:22+08:00",
                "Description": "This is a checkprobes",
                "CreationTime": "2021-12-07T15:57:22+08:00",
                "ProbeInterval": 2,
                "ProbeTargetIp": "10.XX.XX.1",
                "ProbeThreshold": 5,
                "ProbePacketSize": 100,
                "ProbePacketProtocol": "ICMP",
                "DirectConnectHealthCheckId": "dhc-2752hz4tek****",
                "DirectConnectHealthCheckProbeId": "dhp-2752hz4****",
                "DirectConnectHealthCheckProbeName": "CheckProbes-01"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectHealthCheckProbeId |You've reached the limit on the number of direct connect health check IDs that you can describe. |You have reached the maximum number of health check probes that can be queried. |
