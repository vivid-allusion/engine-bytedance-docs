---
title: "UpdateProbe"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/UpdateProbe"
---

Updates the health check parameters of a GTM instance.

## Request

* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=UpdateProbe&Version=2023\-01\-01

## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

### Query

|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateProbe` |The name of the API. The value of this parameter is `UpdateProbe`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |

### Body

|Name |Type |Required |Example |Description |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the GTM instance. You can obtain the GtmId through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|PolicyType |String |Yes |`geo` |The policy type corresponding to the health check.<br><br><br>* geo: Basic routing.<br><br>* perf: Intelligent routing. |
|Probe |Object |Yes | |Health check parameters of the policy. |
|Disable |Boolean |No |`false` |Whether to disable the health check.<br><br><br>* true: Disable the health check.<br><br>* false: (default) Enable the health check. |
|Protocol |String |No |`ping` |The protocol used for the health check.<br><br><br>* ping: ICMP protocol.<br><br>* tcp: TCP protocol.<br><br>* http: HTTP protocol.<br><br>* https: HTTPS protocol. |
|Interval |Integer |No |`60` |The interval of the health check (seconds). The shorter the interval, the faster the cloud scheduling GTM detects unavailable addresses and triggers failover, but the higher the cost. This parameter only supports the following values:<br><br><br>* 60: (default) The interval of the health check is 60 seconds.<br><br>* 15: The interval of the health check is 15 seconds. |
|Timeout |Integer |No |`5` |The timeout period for the health check task, in seconds.<br><br><br>* ping: If the delay is greater than the value of `Timeout`, it is considered a packet loss.<br><br>* http/https: If the delay is greater than the value of `Timeout`, it is considered an abnormal result. |
|PingCount |Integer |No |`10` |The number of packets sent. If you set this parameter to 10, each ping check will send 10 packets simultaneously.<br><br> <br><br>If you set the `Protocol` parameter to `ping`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|PingLossPercent |Integer |No |`10` |Packet loss rate, in percentage. If the packet loss rate is greater than the value of this parameter, it is considered an abnormal result. For example, if this parameter is 10 and the packet loss rate during the health check is 11%, it is considered an abnormal result.<br><br> <br><br>If you set the `Protocol` parameter to `ping`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|FailedCount |Integer |No |`3` |The threshold for the number of health check failures to determine if an address is unavailable. For example, if you set this parameter to 3, an address will be determined as an unavailable address after 3 consecutive health check failures. The default value is 3. |
|SuccessCount |Integer |No |`3` |The threshold for the number of health check successes to determine if an unavailable address is available. For example, if you set this parameter to 3, an unavailable address will be determined as an available address after 3 consecutive health check successes. The default value is 0.<br><br> <br><br>If you set this parameter to 0, BytePlus GTM ignores this parameter and uses its internal logic to determine whether an unavailable address will be determined as available again. |
|TcpConnTimeout |Integer |No |`2` |The timeout period for establishing a single TCP connection. For example, if you set this parameter to 2 seconds, and a TCP connection is not successfully established within 2 seconds from the start of a health check, it is considered a connection failure. The default value is 2 seconds. |
|Host |String |No |`www.example.com` |The full domain name of the health check target address.<br><br> <br><br>This parameter is only valid when the health check protocol is set to HTTP or HTTPS. |
|Port |Integer |No |`80` |The port of the health check target address.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|Url |String |No |`/content/pages` |The path part of the health check target address, starting with `/`.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|Host |String |No |`www.example.com` |The full domain name of the health check target address.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpMethod |String |No |`get` |The HTTP request method used for the health check.<br><br><br>* get<br><br>* post<br><br>* head<br><br>* put<br><br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpHeader |Object |No |`{"Content-type": "application/json","Content-Length": "1234"}` |The HTTP request header used for the health check.<br><br> <br><br>If you set the `Protocol` parameter to `http` or `https`, this parameter is required. If you set the `Protocol` parameter to other values, this parameter is invalid. |
|HttpUsabilityCodes |Array of objects |No |`{"Operator": "interval", "Codes": [100,200]}` |Customize a range of HTTP status codes. If a probe point initiates a health check and the target address returns an HTTP status code outside the range, the health check of the probe point is considered a failure. By default, if the HTTP status code is outside the range of 200 to 399, the health check is considered a failure. |
|Operator |String |No |`interval` |Operator.<br><br><br>* interval: Match values within the interval.<br><br>* include: Match specified values.<br><br>* exclude: Match values other than the specified values. |
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
POST https://gtm.byteplusapi.com/?Action=UpdateProbe&Version=2023-01-01

{
    "GtmId": "2a8f91c4-aa07-4ae4-9ebc-68750d611822",
    "PolicyType": "perf",
    "Probe": {
        "Disable": true,
        "Protocol": "https",
        "Interval": 60,
        "Port": 80,
        "Host": "example.com",
        "Url": "/docs",
        "Timeout": 10,
        "HttpMethod": "get",
        "HttpHeader": {
            "Content-type": "application/json",
            "Content-Length": "1234"
        }
    }
}
```

### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230727111556366951A9363D5437BD44",
        "Action": "UpdateProbe",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```

## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
