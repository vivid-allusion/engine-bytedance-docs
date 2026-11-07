---
title: "DescribeVpnConnectionAttributes - Querying a specified IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnectionAttributes"
---

Call DescribeVpnConnectionAttributes to query a specified IPsec\-VPN connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnConnectionAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|10zNRK">必选</span> Example: `DescribeVpnConnectionAttributes`

The action that you want to perform. Value: DescribeVpnConnectionAttributes.



**Version ** `String` <span data-api-tag="require|rdJ7Jb">必选</span> Example: `2020-04-01`

The API version.



**VpnConnectionId ** `String` <span data-api-tag="require|ZTpSjN">必选</span> Example: `vgc-3tehy13n2l4c6c0v****`

ID of the IPsec\-VPN connection. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `20220322145233010225243081016A***`

Request ID.



**AccountId ** `String` `optional` Example: `2000****`

ID of the account that owns the IPsec\-VPN connection.



**VpnConnectionId ** `String` `optional` Example: `vgc-3tehy13n2l4c6c0v****`

The ID of the IPsec\-VPN connection.



**CreationTime ** `String` `optional` Example: `2021-04-09T08:36:47+08:00`

The time when the IPsec\-VPN connection is created.



**UpdateTime ** `String` `optional` Example: `2021-04-10T08:30:00+08:00`

The time when the IPsec\-VPN connection is updated.



**VpnConnectionName ** `String` `optional` Example: `abc`

Name of the IPsec\-VPN connection.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the IPsec\-VPN connection.



**Status ** `String` `optional` Example: `Available`

The status of the IPsec\-VPN connection.


* Creating

* Deleting

* Pending: Configuration in progress.

* Available



**VpnGatewayId ** `String` `optional` Example: `vgw-3tex2x1cwd4c6c0v****`

The ID of the VPN gateway associated with the IPsec\-VPN connection.



**CustomerGatewayId ** `String` `optional` Example: `cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection.



**LocalSubnet ** `String[]` `optional` Example: `10.XX.XX.1/24`

The local network of the IPsec\-VPN connection.



**RemoteSubnet ** `String[]` `optional` Example: `192.XX.XX.1/24`

The remote network of the IPsec\-VPN connection.



**DpdAction ** `String` `optional` Example: `clear`

Describes whether Dead Peer Detection (DPD) is enabled.


* none: DPD is not enabled.

* clear: DPD is enabled. Clear IKE SA after timeout.

* hold: DPD is enabled. Maintain the current status after timeout. Re\-establish the connection when new traffic is detected.

* restart: DPD is enabled. Reconnect immediately after timeout.



**DualTunnelEnabled ** `Boolean` `optional` Example: `true`

Describe whether the dual\-tunnel mode is enabled.


* true: Enabled

* false (default): Not enabled


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The values of DualTunnelEnabled and SslEnabled cannot both be true.</div>


* <div data-tips="true" data-tips-type="default">If you enable BGP, this parameter cannot be true.</div>




**TunnelOptions ** `Object[]` `optional` Example: `-`

Configurations of the dual\-tunnel IPsec\-VPN connection.


**TunnelId ** `String` `optional` Example: `tunnel-3tehy13n2l4c6c0v****`

The ID of the tunnel.



**Role ** `String` `optional` Example: `Primary`

The role of the tunnel.


* primary: The current tunnel is the primary tunnel.

* secondary: The current tunnel is the secondary tunnel.



**CustomerGatewayId ** `String` `optional` Example: `cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection.



**ConnectStatus ** `String` `optional` Example: `ike_sa_negotiation_completed`

The connection status of the tunnel.


* ike_sa_negotiation_failed: Phase 1 negotiation failed.

* ike_sa_negotiation_completed: Phase 1 negotiation is completed successfully.

* ipsec_sa_negotiation_failed: Phase 2 negotiation failed.

* ipsec_sa_negotiation_completed: Phase 2 negotiation is completed successfully.



**IkeConfig ** `Object` `optional` Example: `-`

The IKE Config of the IPsec\-VPN connection.


**Version ** `String` `optional` Example: `ikev1`

The version of the IKE protocol.



**Psk ** `String` `optional` Example: `12345***`

The Pre\-Shared Key for identity authentication between the VPN gateway and the customer gateway in Phase 1.



**DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 1 negotiation.



**Mode ** `String` `optional` Example: `main`

The negotiation mode for Phase 1. When the version of the IKE protocol is **ikev2**, an empty string is returned.



**EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 1 negotiation.



**AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for Phase 1 negotiation.



**LocalId ** `String` `optional` Example: `2.XX.XX.2`

The identifier of the VPN gateway for Phase 1 negotiation.



**RemoteId ** `String` `optional` Example: `1.XX.XX.1`

The identifier of the customer gateway for Phase 1 negotiation.



**Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for Phase 1 negotiation. When the lifetime expires, a renegotiation is initiated.




**IpsecConfig ** `Object` `optional` Example: `-`

The IPsec configuration of the IPsec\-VPN connection.


**AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for Phase 2 negotiation.



**EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 2 negotiation.



**DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 2 negotiation.



**Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for Phase 2 negotiation. When the lifetime expires, a renegotiation is initiated.




**NatTraversal ** `Boolean` `optional` Example: `false`

Describes whether NAT Traversal is enabled.


* true: Enabled

* false: Disabled.







**IkeConfig ** `Object` `optional` Example: `-`

The IKE Config of the IPsec\-VPN connection.


**Version ** `String` `optional` Example: `ikev1`

The version of the IKE protocol.



**Psk ** `String` `optional` Example: `12345***`

The Pre\-Shared Key for identity authentication between the VPN gateway and the customer gateway in Phase 1.



**DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 1 negotiation.



**Mode ** `String` `optional` Example: `main`

The negotiation mode for Phase 1. When the version of the IKE protocol is **ikev2**, an empty string is returned.



**EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 1 negotiation.



**AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for Phase 1 negotiation.



**LocalId ** `String` `optional` Example: `2.XX.XX.2`

The identifier of the VPN gateway for Phase 1 negotiation.



**RemoteId ** `String` `optional` Example: `1.XX.XX.1`

The identifier of the customer gateway for Phase 1 negotiation.



**Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for Phase 1 negotiation. When the lifetime expires, a renegotiation is initiated.




**IpsecConfig ** `Object` `optional` Example: `-`

The IPsec configuration of the IPsec\-VPN connection.


**AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for Phase 2 negotiation.



**EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 2 negotiation.



**DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 2 negotiation.



**Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for Phase 2 negotiation. When the lifetime expires, a renegotiation is initiated.




**NatTraversal ** `Boolean` `optional` Example: `false`

Describes whether NAT Traversal is enabled.


* true: Enabled

* false: Disabled.



**ProjectName ** `String` `optional` Example: `Project_1`

The project to which the IPsec\-VPN connection belongs.



**NegotiateInstantly ** `Boolean` `optional` Example: `true`

Describes whether to initiate the negotiation instantly.


* true: The system proactively initiates the negotiation instantly upon the completion of IPsec\-VPN connection configuration.

* false: The system does not initiate negotiation after the IPsec\-VPN connection configuration completes. Negotiation is triggered passively when traffic passes through.



**AttachStatus ** `String` `optional` Example: `Attached`

The status of the IPsec\-VPN connection.


* VpnGateway:

   * Attached

* TransitRouter:

   * Attached

   * Attaching

   * Detached

   * Detaching



**AttachType ** `String` `optional` Example: `VpnGateway`

The gateway type associated with the IPsec\-VPN connection.


* VpnGateway: VPN gateway

* TransitRouter: Transit Router (TR)



**IpAddress ** `String` `optional` Example: `180.XX.XX.182`

The elastic IP address (EIP) of the TR. The parameter returns a value only if `AttachType` is set to "TransitRouter".



**TransitRouterId ** `String` `optional` Example: `tr-bp1osj4c1q84p7syi****`

The TR ID. The parameter is returned only if `AttachType` is set to "TransitRouter".



**ZoneId ** `String` `optional` Example: `cn-beijing-a`

The availability zone of the TR attachment point. This parameter is returned only if `AttachType` is "TransitRouter".



**BusinessStatus ** `String` `optional` Example: `Normal`

The billing status of the IPsec\-VPN connection. This parameter is returned only if `AttachType` is set to "TransitRouter".


* Normal

* FinancialLocked: Being locked.



**DeletedTime ** `String` `optional` Example: `2022-12-07 23:23:23`

The time when the resource is scheduled to be forcibly reclaimed. The parameter is returned only if `AttachType` is set to "TransitRouter". Furthermore, it has a response value only if the resources are frozen due to overdue payments. Otherwise, it returns an empty string.



**OverdueTime ** `String` `optional` Example: `2022-12-07 23:23:23`

The time when the resource is frozen. The parameter is returned only if `AttachType` is set to "TransitRouter". Furthermore, it has a response value only if the resources are frozen due to overdue payments. Otherwise, it returns an empty string.



**LogEnabled ** `Boolean` `optional` Example: `false`

Describes whether Connection Log is enabled.


* true: Enabled.

* false: Disabled.



**Spec ** `String` `optional` Example: `default`

The instance type of the IPsec\-VPN connection. If `AttachType` is `VpnGateway`, this parameter is not returned.


* default: Default specification with a bandwidth cap of 200 Mbps.

* large: Large specification with a bandwidth cap of 1 Gbps.

* xlarge: Extra\-large specification with  a bandwidth cap of 3 Gbps.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The large and extra\-large specifications are currently in the beta stage, and are available only after being enabled. If you need a trial, please contact your account manager.</div>




**HealthCheckers ** `Object[]` `optional` Example: `-`

The health check information of the IPsec\-VPN connection.


**CheckInterval ** `Integer` `optional` Example: `3`

The time interval for performing health checks.



**CheckResult ** `String` `optional` Example: `Up`

The result of health check.


* Up: Healthy

* Down: Unhealthy



**CheckerId ** `String` `optional` Example: `vhc-abc`

The health check ID of the IPsec\-VPN connection.



**DownTime** `Integer` `optional` Example: `3`

The unhealthy threshold for health check. When consecutive health checks on an IPsec\-VPN connection fail for the specified number, the connection is declared unhealthy.



**LocalIp ** `String` `optional` Example: `100.XX.XX.10`

The source IP for health check.



**RemoteIp ** `String` `optional` Example: `100.XX.XX.10`

The target IP for health check.



**Timeout ** `Integer` `optional` Example: `2`

The response timeout of the health check. If the IPsec\-VPN connection does not respond properly within the specified response time, the health check is declared failed.



**UpTime ** `Integer` `optional` Example: `3`

The health threshold for health check. When consecutive health checks on an IPsec\-VPN connection pass for the specified number, the connection is declared healthy.




**IsBlocked ** `Boolean` `optional` Example: `false`

Describes whether the current resource is blocked.


* true: Blocked.

* false: Not blocked.



**BgpInfo ** `Object` `optional` Example: `-`

The BGP information of the IPsec connection.


**EnableBgp ** `Boolean` `optional` Example: `true`

Describes whether BGP is enabled.


* true: Yes. Enabled.

* false: No. Not enabled.



**TunnelCidr ** `String` `optional` Example: `169.254.11.0/30`

The CIDR block where the local and remote IPs of the BGP session are located.



**LocalBgpIp ** `String` `optional` Example: `169.254.XX.XX`

The local IP of the BGP session. That is, the BGP address on the BytePlus side.



**PeerBgpIp ** `String` `optional` Example: `169.254.XX.XX`

The remote IP of BGP session. That is, the BGP address on the customer gateway side.



**SessionStatus ** `String` `optional` Example: `Up`

The status of the BGP connection.


* Up: BGP connection is normal

* Down: BGP connection is unreachable.



**LocalAsn ** `Integer` `optional` Example: `65534`

The ASN of the VPN gateway.



**PeerAsn ** `Integer` `optional` Example: `42949`

The ASN of the customer gateway.




**Tags ** `Object[]` `optional` Example: `-`

Information about all tags associated with the IPsec\-VPN connection.


**Key ** `String` `optional` Example: `key1`

The tag key.



**Value ** `String` `optional` Example: `value1`

The tag value.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpnConnectionAttributes&Version=2020-04-01&VpnConnectionId=vgc-2bzvqi8kerd342dx0eg2f**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata":{
        "RequestId":"20220322145233010225243081016A****",
        "Action":"DescribeVpnConnectionAttributes",
        "Version":"2020-04-01",
        "Service":"vpn",
        "Region":"cn-beijing"
    },
    "Result": {
        "RequestId": "20220322145233010225243081016A***",
        "AccountId": "210000****",
        "VpnConnectionId": "vgc-2bzvqi8kerd342dx0eg2f****",
        "VpnConnectionName": "test",
        "CreationTime": "2022-03-13T17:50:42+08:00",
        "UpdateTime": "2022-03-18T06:31:21+08:00",
        "Description": "test",
        "Status": "Available",
        "VpnGatewayId": "vgw-2d670iixygs8w58ozfde1****",
        "CustomerGatewayId": "cgw-2d670j4napdz458ozfd8y****",
        "ProjectName":"Project_1",
        "LocalSubnet": [
            "192.XX.XX.0/16"
        ],
        "RemoteSubnet": [
            "172.XX.XX.0/16"
        ],
        "NatTraversal": false,
        "DpdAction": "clear",
        "ConnectStatus": "ike_sa_negotiation_completed",
        "NegotiateInstantly": true,
        "AttachStatus": "Attached",
        "AttachType": "VpnGateway",
        "LogEnabled": false,
        "IsBlocked": false,
        "Tags":[
            {
               "Key":"k1",
               "Value":"v1"
            },
            {
               "Key":"k2",
               "Value":"v2"
            }
        ],
        "IkeConfig": {
            "Version": "ikev2",
            "Psk": "12345***",
            "DhGroup": "group2",
            "Mode": "main",
            "EncAlg": "aes",
            "AuthAlg": "sha1",
            "Lifetime": 86400,
            "LocalId": "2.XX.XX.2",
            "RemoteId": "1.XX.XX.1"
        },
        "IpsecConfig": {
            "EncAlg": "aes",
            "AuthAlg": "sha1",
            "Lifetime": 86400,
            "DhGroup": "group2"
        },
        "HealthCheckers": [
            {
                "CheckerId": "vhc-inb9bswzfksg8gbss****",
                "LocalIp": "100.XX.XX.10",
                "RemoteIp": "100.XX.XX.10",
                "CheckInterval": 3,
                "Timeout": 1,
                "UpTime": 3,
                "DownTime": 3,
                "CheckResult": "Down"
            }
         ],
        "BgpInfo": [
            {
                "EnableBgp":"true" ,
                "LocalAsn": 65543,
                "LocalBgpIp": "169.254.XX.1",
                "PeerAsn": 42949,
                "PeerBgpIp": "169.254.XX.2",
                "SessionStatus": "Up",
                "TunnelCidr": "169.254.XX.0/30"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
