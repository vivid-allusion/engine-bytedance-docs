---
title: "ModifyVpnConnectionHealthChecker - Updating health check for VPN"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionHealthChecker"
---

Call ModifyVpnConnectionHealthChecker to modify the health check for an IPsec\-VPN connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpnConnectionHealthChecker&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|s-sEFO">必选</span> Example: `ModifyVpnConnectionHealthChecker`

The action that you want to perform. Value: ModifyVpnConnectionHealthChecker.



**Version ** `String` <span data-api-tag="require|XPKAzP">必选</span> Example: `2020-04-01`

The API version.



**CheckerId ** `String` <span data-api-tag="require|ICyfdo">必选</span> Example: `vhc-fsej4fhk0lw****`

The health check ID of the IPsec\-VPN connection. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the health check ID of the IPsec\-VPN connection.



**VpnConnectionId ** `String` `optional` Example: `vgc-3tex2x1cwd4c6c0v****`

The ID of the IPsec\-VPN connection whose health check you want to modify. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



**LocalIp ** `String` `optional` Example: `100.XX.XX.10`

The source IP for health check.


* Do not support IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8`.

* If you need to configure health check for multiple IPsec\-VPN connections under the same VPN gateway, use different source IPs to differentiate.

* If left blank, the current configuration remains.



**RemoteIp ** `String` `optional` Example: `100.XX.XX.10`

Destination IP for health check.


* The destination IP must not be the same as the source IP, and does not support IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8`.

* If left blank, the original configuration remains.



**CheckInterval ** `Integer` `optional` Example: `3`

The time interval for performing health checks.


* Values: 1\-300. Unit: seconds.

* If left blank, the original configuration remains.



**UpTime ** `Integer` `optional` Example: `3`

The health threshold for health check.


* Value range: 1 to 10. Unit: checks.

* If left blank, the original configuration remains.



**DownTime** `Integer` `optional` Example: `3`

The unhealthy threshold for health check.


* Value range: 1 to 10. Unit: checks.

* If left blank, the original configuration remains.



**Timeout ** `Integer` `optional` Example: `2`

The response timeout of the health check. If the IPsec\-VPN connection does not respond properly within the specified response time, the health check is declared failed.


* Value range: 1 to 300. It must be less than the value of `CheckInterval`. Unit: seconds.

* If left blank, the original configuration remains.



**ClientToken ** `String` `optional` Example: `123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyVpnConnectionHealthChecker&Version=2020-04-01&CheckerId=vhc-2fewk20sch0qo59gp674****&LocalIp=172.XX.XX.108&RemoteIp=172.XX.XX.253&VpnConnectionId=vgc-3tex2x1cwd4c6c0v****&CheckInterval=5&UpTime=1&DownTime=7&Timeout=3 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240318145124A933E01C1C38EB8****",
        "Action": "ModifyVpnConnectionHealthChecker",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20240318145124A933E01C1C38EB84****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCheckInterval.Malformed |The specified check interval is malformed. |The specified check interval is invalid. |
|400 |InvalidDownTime.Malformed |The specified check downtime is malformed. |The specified check downtime is invalid. |
|400 |InvalidHealthCheckConfig.IpPairExists |The specified local ip and remote ip is the same with that of another health checker in the same VPN connection. |The specified local IP and remote IP duplicate those of other health checks on this IPsec\-VPN connection. |
|400 |InvalidHealthCheckConfig.LocalIpConflict |The specified local ip conflicts with that of another health checker in the same VPN gateway. |The specified local IP conflicts with other health checks on this gateway. |
|400 |InvalidHealthCheckConfig.RemoteIpConflict |The specified remote ip conflicts with that of another health checker in the same VPN gateway. |The specified remote IP conflicts with other health checks on this gateway. |
|400 |InvalidHealthCheckConfig.RemoteIpInUse |The specified remote ip conflicts with the address used in the VPN gateway. |The specified remote IP conflicts with the local IP of this gateway. |
|400 |InvalidHeathCheckConfig.LocalIpInUse |The specified local ip conflicts with the address used in the VPN gateway. |The specified local IP conflicts with the local IP of this gateway. |
|400 |InvalidLocalIp.Malformed |The specified local IP is malformed. |The specified local IP is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
|400 |InvalidRemoteIp.Malformed |The specified remote ip is malformed. |The specified remote IP is invalid. |
|400 |InvalidTimeout.Malformed |The specified check timeout is malformed. |The specified check timeout is invalid. |
|400 |InvalidUpTime.Malformed |The specified check uptime is malformed. |The specified check uptime is invalid. |
|400 |InvalidVpnConnection.HealthCheckNotSupported |Health check is not supported for the specified VPN connection. |Currently, IPsec\-VPN connections do not support health check. |
|400 |InvalidVpnConnection.InvalidStatus |The specified VPN connection is not in the correct status for the request. |The specified VPN cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidHealthCheckConfig.IpPairMalformed |The specified remote ip is the same with the local ip. |The remote IP specified for the health check duplicates its local IP. |
|400 |InvalidHealthCheckConfig.IpNotInTrafficSelector |The specified local ip or remote ip is not within the configured traffic selector. |The local IP or remote IP of the health check is not within the set range of Traffic Selector. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|404 |InvalidVpnConnectionHealthChecker.NotFound |The specified VPN connection health checker does not exist. |The specified VPN health check does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
