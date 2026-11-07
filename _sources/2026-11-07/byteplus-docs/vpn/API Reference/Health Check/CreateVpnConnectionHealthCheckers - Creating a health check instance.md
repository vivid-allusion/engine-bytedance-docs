---
title: "CreateVpnConnectionHealthCheckers - Creating a health check instance"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateVpnConnectionHealthCheckers"
---

Call CreateVpnConnectionHealthCheckers to create a health check for an IPsec\-VPN connection.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If the associated resource for the IPsec\-VPN connection to be configured with a health check is a "VPN gateway", ensure the VPN gateway is updated to the latest version. If not, update VPN gateway first. For procedure, see [Upgrading a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway).

* Currently, IPsec\-VPN connections with associated resources as "Transit Router (TR)" do not support health check configuration. If needed, create a new IPsec\-VPN connection.

* If a health check is configured for an IPsec\-VPN connection, you need to configure a remote IP that can respond to ICMP packets for the health check probe.

* Ensure that you have pre\-planned the IP addresses for the health check. **The source IP for the health check cannot be any IP address within the VPC that communicates over this IPsec connection and is scheduled to be occupied**. Otherwise, traffic through the VPN gateway may become unreachable.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpnConnectionHealthCheckers&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|WrrGR2">必选</span> Example: `CreateVpnConnectionHealthCheckers`

The action that you want to perform. Value: CreateVpnConnectionHealthCheckers.



**Version ** `String` <span data-api-tag="require|CW1llm">必选</span> Example: `2020-04-01`

The API version.



**VpnConnectionId ** `String` <span data-api-tag="require|19Pvvx">必选</span> Example: `vgc-273zkshb2qayo7fap8t21`

The ID of the IPsec\-VPN connection.



**HealthCheckConfigs.N.LocalIp ** `String` <span data-api-tag="require|WjP9Gz">必选</span> Example: `100.XX.XX.10`

The source IP of the health check. It refers to the IP address on the local Virtual Private Cloud (VPC). It can be accessed by the on\-premises data center or peer VPC via IPsec\-VPN connection.


* N represents the serial number of the source IP in the health check.

* Separate multiple source IPs with the ampersand (`&`).

* Do not support IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8`.

* If you need to configure health check for multiple IPsec\-VPN connections under the same VPN gateway, use different source IPs to differentiate.



**HealthCheckConfigs.N.RemoteIp ** `String` <span data-api-tag="require|D0WNkv">必选</span> Example: `192.XX.XX.12`

The destination IP address for the health check. It refers to the IP address of the remote data center or remote VPC. It can be accessed by the local VPC via IPsec\-VPN connection.


* N represents the serial number of the destination IP in the health check.

* Separate multiple destination IPs with the ampersand (`&`).

* The destination IP must not be the same as the source IP, and does not support IPs within `169.254.0.0/16`, `224.0.0.0/3`, and `127.0.0.0/8`.



**HealthCheckConfigs.N.CheckInterval ** `Integer` `optional` Example: `3`

The time interval for performing health checks.


* N represents the serial number of the interval in the health check.

* Separate multiple intervals with the ampersands (`&`).

* Values: 1\-300. Default: 3. Unit: seconds.



**HealthCheckConfigs.N.UpTime ** `Integer` `optional` Example: `3`

The health threshold for health check.


* N represents the serial number of the healthy threshold in the health check.

* Separate multiple healthy thresholds with the ampersand (`&`).

* Values: 1\-10. Default: 3. Unit: checks.



**HealthCheckConfigs.N.DownTime ** `Integer` `optional` Example: `3`

The unhealthy threshold for health check.


* N represents the serial number of the unhealthy threshold in the health check.

* Separate multiple unhealthy thresholds with the ampersand (`&`).

* Values: 1\-10. Default: 3. Unit: checks.



**HealthCheckConfigs.N.Timeout ** `Integer` `optional` Example: `2`

The response timeout of the health check.


* N represents the serial number of the response timeout in the health check.

* Separate multiple response timeouts with the ampersands (`&`).

* Value range: 1 to 300. It must be less than the value of `CheckInterval`. Default: 1. Unit: seconds.

* The response timeout must not be longer than the probe interval.



**ClientToken ** `String` `optional` Example: `123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



**CheckerIds ** `String[]` `optional` Example: `vhc-fejkfjkrg3ef0****`

The ID list of new health checks.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=Action=CreateVpnConnectionHealthCheckers&Version=2020-04-01&VpnConnectionId=vgc-imj14gcqbbpc8gbss****&HealthCheckConfigs.1.LocalIp=172.XX.XX.134&HealthCheckConfigs.1.RemoteIp=172.XX.XX.253&HealthCheckConfigs.1.CheckInterval=5&HealthCheckConfigs.1.UpTime=3&HealthCheckConfigs.1.DownTime=3&HealthCheckConfigs.1.Timeout=3  HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240318143303A529B2D8F6C6E2****",
        "Action": "CreateVpnConnectionHealthCheckers",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20240318143303A529B2D8F6C6E2****",
        "CheckerIds": [
            "vhc-12b9ncfrstuyo17q7y1dn****"
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidCheckInterval.Malformed |The specified check interval is malformed. |The specified check interval is invalid. |
|400 |InvalidDownTime.Malformed |The specified check downtime is malformed. |The specified check downtime is invalid. |
|400 |InvalidHealthCheckConfig.Empty |Health check configuration is empty. |The specified health check configuration is empty. |
|400 |InvalidHealthCheckConfig.IpPairExists |The specified local ip and remote ip is the same with that of another health checker in the same VPN connection. |The specified local IP and remote IP duplicate those of other health checks on this IPsec\-VPN connection. |
|400 |InvalidHealthCheckConfig.LocalIpConflict |The specified local ip conflicts with that of another health checker in the same VPN gateway. |The specified local IP conflicts with other health checks on this gateway. |
|400 |InvalidHealthCheckConfig.RemoteIpConflict |The specified remote ip conflicts with that of another health checker in the same VPN gateway. |The specified remote IP conflicts with other health checks on this gateway. |
|400 |InvalidHealthCheckConfig.RemoteIpInUse |The specified remote ip conflicts with the address used in the VPN gateway. |The specified remote IP conflicts with the local IP of this gateway. |
|400 |InvalidHeathCheckConfig.LocalIpInUse |The specified local ip conflicts with the address used in the VPN gateway. |The specified local IP conflicts with the local IP of this gateway. |
|400 |InvalidLocalIp.Malformed |The specified local IP is malformed. |The specified local IP is invalid. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified ClientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidRemoteIp.Malformed |The specified remote ip is malformed. |The specified remote ip is invalid. |
|400 |InvalidTimeout.Malformed |The specified check timeout is malformed. |The specified check timeout is invalid. |
|400 |InvalidUpTime.Malformed |The specified check uptime is malformed. |The specified check uptime is invalid. |
|400 |InvalidVpnConnection.InvalidStatus |The specified VPN connection is not in the correct status for the request. |The specified VPN cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.FirmwareNotSupported |The specified features aren't supported by the VPN gateway, please upgrade your VPN gateway. |The selected feature is unavailable for the VPN gateway. Upgrade your VPN gateway. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |QuotaExceeded.VpnGatewayHealthCheckers |You've reached the limit on the number of health checkers per VPN gateway that you can create. |You have reached the maximum of health checks that you can create per VPN gateway. |
|400 |InvalidHealthCheckConfig.IpPairMalformed |The specified remote ip is the same with the local ip. |The remote IP specified for the health check duplicates its local IP. |
|400 |InvalidHealthCheckConfig.IpNotInTrafficSelector |The specified local ip or remote ip is not within the configured traffic selector. |The local IP or remote IP of the health check is not within the set range of Traffic Selector. |
|400 |QuotaExceeded.TRIPsecHealthCheckers |You've reached the limit on the number of health checkers per TR IPsec that you can create. |You have reached the maximum of health checks that you can create per VPN gateway. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
