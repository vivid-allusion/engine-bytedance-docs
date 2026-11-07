---
title: "GetProbe"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/GetProbe"
---

Gets the health check information of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=GetProbe&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetProbe` |The name of the API. The value of this parameter is `GetProbe`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PolicyType |String |Yes |`geo` |The policy type corresponding to the health check.<br><br><br>* geo: Basic routing policy.<br><br>* perf: Intelligent routing policy. |

## Response parameters

### ResponseMetadata object

|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |

### Result Object

|Name |Type |Description |
|---|---|---|
|Nodes |String[] |Health check probes. |
|IsManualNodes |Boolean |Whether the health check probes are manually configured.<br><br><br>* true: Health check probes are manually configured.<br><br>* false: Recommended health check probes are used. |
|AdvisedNodeCount |Integer |The recommended number of health check probes. |
|Protocol |String |The protocol used for health checks.<br><br><br>* ping: ICMP protocol.<br><br>* tcp: TCP protocol.<br><br>* http: HTTP protocol.<br><br>* https: HTTPS protocol. |
|Interval |Integer |The time interval between each health check. Unit: seconds. |
|Timeout |Integer |The timeout period for a health check task. Unit: seconds. |
|PingLossRate |Integer |Packet loss rate. Unit: percentage. If the packet loss rate is greater than the value of this parameter, the result is considered failed. For example, if this parameter is 10 and the packet loss rate during the health check is greater than 10, the result is considered failed.<br><br> <br><br>This parameter is only valid when the health check protocol is set to ping. |
|PingCount |Integer |The number of packets sent. If you set this parameter to 10, 10 data packets will be sent simultaneously for each ping check.<br><br> <br><br>This parameter is only valid when the health check protocol is set to ping. |
|FailedCount |Integer |The threshold for the number of health check failures to determine if an address is unavailable. For example, if you set this parameter to 3, an address will be determined as an unavailable address after 3 consecutive health check failures. The default value is 3. |
|SuccessCount |Integer |The threshold for the number of health check successes to determine if an unavailable address is available. For example, if you set this parameter to 3, an unavailable address will be determined as an available address after 3 consecutive health check successes. The default value is 0.<br><br> <br><br>If you set this parameter to 0, BytePlus GTM ignores this parameter and uses its internal logic to determine whether an unavailable address will be determined as available again. |
|TcpConnTimeout |Integer |The timeout period for establishing a single TCP connection. For example, if you set this parameter to 2 seconds, and if a TCP connection is not successfully established within 2 seconds from the start of establishment during a health check, it will be considered a connection failure.<br><br> <br><br>This parameter is only valid when the health check protocol is set to tcp. |
|Host |String |The complete domain name of the health check target address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Port |Integer |The port of the health check target address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Url |String |The path part of the health check target address, starting with /.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|HttpMethod |String |The HTTP request method.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|HttpHeader |Object |The HTTP request headers used for health checks.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. If you have not set HTTP request headers, this parameter will not appear. |
|HttpUsabilityCodes |Array of objects |Define a custom range of HTTP status codes. After a probe initiates a health check, if the target address returns an HTTP status code outside this range, the health check for that probe is considered failed. If you have not set the `HttpUsabilityCodes` parameter for the policy, this parameter will not be returned. |
|Operator |String |Operator.<br><br><br>* interval: Match values within the interval.<br><br>* include: Match specified values.<br><br>* exclude: Match values other than the specified ones. |
|Codes |Array of integers |List of HTTP status codes. |
|Disable |Boolean |Whether the health check is disabled.<br><br><br>* true: Disabled.<br><br>* false: Enabled. |

## Example

### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=GetProbe&Version=2023-01-01&GtmId=2a8f91c4-aa07-4ae4-9ebc-68750d611822&PolicyType=geo
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20240725065447537AE6037350750A8004",
        "Action": "GetProbe",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Nodes": [
            "Mexico, North America",
            "Germany, Europe",
            "Singapore, Asia",
            "Pakistan, Asia",
            "Chile, South America",
            "Vietnam, Asia",
            "Peru, South America",
            "Netherlands, Europe"
        ],
        "IsManualNodes": false,
        "AdvisedNodeCount": 8,
        "Protocol": "ping",
        "Interval": 60,
        "Timeout": 5,
        "PingLossPercent": 10,
        "PingCount": 20,
        "FailedCount": 3,
        "SuccessCount": 3,
        "TcpConnTimeout": 2,
        "Host": "",
        "Port": 80,
        "Url": "",
        "HttpMethod": "GET",
        "Disable": false
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
