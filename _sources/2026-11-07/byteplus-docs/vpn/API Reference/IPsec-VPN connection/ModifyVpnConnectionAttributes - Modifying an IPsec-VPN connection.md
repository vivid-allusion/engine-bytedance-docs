---
title: "ModifyVpnConnectionAttributes - Modifying an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes"
---

Call ModifyVpnConnectionAttributes to modify the information of an IPsec\-VPN connection, such as the name, description, local subnets, remote subnets, IKE configuration, and IPsec configuration.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

To enable dynamic routing for IPsec\-VPN connections via Transit Router (TR) that were created before September 30, 2024, you need to [submit a ticket](https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000249&FlowKey=NGhBLLYotsiBMSgHMvCt).

If you leave optional parameters of this API unset, their original configuration remains.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyVpnConnectionAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|4w6hWO">必选</span> Example: `ModifyVpnConnectionAttributes`

The action that you want to perform. Value: ModifyVpnConnectionAttributes.



**Version ** `String` <span data-api-tag="require|UaJ4zS">必选</span> Example: `2020-04-01`

The API version.



**VpnConnectionId ** `String` <span data-api-tag="require|3YxS5t">必选</span> Example: `vgc-3tehy13n2l4c6c0v****`

ID of the IPsec\-VPN connection. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



**VpnConnectionName ** `String` `optional` Example: `abc`

Name of the IPsec\-VPN connection.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the IPsec\-VPN connection.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.



**LocalSubnet.N ** `String` `optional` Example: `10.0.XX.0/24`

The local subnet of the IPsec\-VPN connection.


* N represents the serial number of the local subnet.

* You can set up to five CIDR blocks.

* Separate multiple CIDR blocks with ampersands (&).

* If left blank, the original configuration remains.



**RemoteSubnet.N ** `String` `optional` Example: `172.16.XX.0/24`

The remote network of the IPsec\-VPN connection.


* N is the serial number of a remote subnet.

* You can set up to five CIDR blocks.

* Separate multiple CIDR blocks with ampersands (&).



**Single\-tunnel configurations**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Parameters in this section are inapplicable when creating a dual\-tunnel IPsec\-VPN connection.</div>



**IKE Config.Psk ** `String` `optional` Example: `Test123***`

The Pre\-Shared Key of IKE in the single\-tunnel IPsec\-VPN connection. It is used for identity authentication between the VPN gateway and the customer gateway in Phase 1.


* Must not exceed 100 characters in length.

* May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**IkeConfig.Version ** `String` `optional` Example: `ikev1`

Version of the IKE protocol for the single\-tunnel IPsec\-VPN connection. Values:


* ikev1

* ikev2


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">If the IP address of the customer gateway is set to <code>0.0.0.0</code>, <code>IkeConfig.Version</code> only allows <strong><code>ikev1</code></strong><strong>.</strong></div>




**IkeConfig.Mode ** `String` `optional` Example: `main`

The negotiation mode for IKE Phase 1 in the single\-tunnel IPsec\-VPN connection. This parameter is required only if `IkeConfig.Version` is set to **ikev1**. Values:


* main

* aggressive


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">If the IP address of the customer gateway is set to <code>0.0.0.0</code>, <code>IkeConfig.Mode</code> only allows <code>aggressive</code>.</div>




**IkeConfig.EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. Values:


* aes

* aes192

* aes256

* des

* 3des

* sm4



**IkeConfig.AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for IKE Phase 1 in the single\-tunnel IPsec\-VPN connection. Values:


* sha1

* md5

* sha256

* sha384

* sha512

* sm3



**IKE Config.DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. Values:


* group1

* group2

* group5

* group14



**IkeConfig.Lifetime ** `Integer` `optional` Example: `86400`

The Security Association (SA) lifetime for IKE Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated. Value range: 900 to 86400. Unit: seconds.



**IkeConfig.LocalId** `String` `optional` Example: `IKE-VPN`

The identifier of the VPN gateway in the single\-tunnel IPsec\-VPN connection. It is used for Phase 1 negotiation, supporting IP format and fully qualified domain name (FQDN) format.


* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters in length. May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**IkeConfig.RemoteId ** `String` `optional` Example: `IKE-USER`

The identifier of the customer gateway in the single\-tunnel IPsec\-VPN connection. It is used for Phase 1 negotiation, supporting IP and FQDN formats.


* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters in length. May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**IpsecConfig.EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. Values:


* aes

* aes192

* aes256

* des

* 3des

* sm4



**IpsecConfig.AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for IKE Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. Values:


* sha1

* md5

* sha256

* sha384

* sha512

* sm3



**IpsecConfig.DhGroup ** `String` `optional` Example: `group2`

The Diffie\-Hellman (DH) key exchange algorithm for Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. Values:


* group1

* group2

* group5

* group14

* disable: Do not configure DH algorithm.


> If selecting group1, group2, group5, or group14, PFS is enabled by default. You also need to enable PFS on the peer client. If PFS is not available on the client, set to "disable" here.



**IpsecConfig.Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for IKE Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated.


* Values: 900–86400

* Unit: seconds.



**NatTraversal ** `Boolean` `optional` Example: `false`

Specify whether to enable NAT traversal.


* true: Enable.

* false: Disable.

* If left blank, the current configuration remains.



**DpdAction ** `String` `optional` Example: `clear`

Status of the DPD feature.


* none: Disable DPD.

* clear (default): Enable DPD. When DPD timeout occurs, clear IKE SA.

* hold: Enable DPD. When DPD timeout occurs, hold the current status and re\-establish the connection upon receiving new traffic.

* restart: Enable DPD. When DPD timeout occurs, re\-establish the connection instantly.



**BgpConfig.EnableBgp ** `Boolean` `optional` Example: `true`

Specify whether to enable dynamic routing propagation.


* false (default): No. Use static routing.

* true: Yes. Use BGP routing.

* If left blank, the original configuration remains.



**BgpConfig.TunnelCidr ** `String` `optional` Example: `169.254.XX.XX/30`

The tunnel CIDR block where the local IP and remote IP of the BGP session are located.


* This CIDR block must be within `169.254.0.0/16`, with a mask length of `/30`. It cannot be within `169.254.255.0/24`.

* If `BgpConfig.EnableBgp` is set to `true`, this parameter is required.

* If left blank, the original configuration remains.



**BgpConfig.LocalBgpIp ** `String` `optional` Example: `169.254.XX.XX`

The local tunnel IP is the BGP address configured on the VPN gateway


* This parameter defaults to the first host address of `BgpConfig.TunnelCidr`.

* This address must be an IP address within the IPsec tunnel CIDR block.

* If `BgpConfig.EnableBgp` is set to `true`, this parameter is required.

* If left blank, the original configuration remains.



**CustomerGatewayId ** `String` `optional` Example: `cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID. If left blank, the original configuration remains.




**Dual\-tunnel configurations**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Parameters in this section are inapplicable when creating a single\-tunnel IPsec\-VPN connection.</div>



* <div data-tips="true" data-tips-type="default">In each parameter, N represents the serial number of the tunnel. You can only add up to two tunnels (primary and secondary) for an IPsec\-VPN connection.</div>


* <div data-tips="true" data-tips-type="default">Separate the primary and secondary tunnels with an ampersand (&).</div>




**TunnelOptions.N.TunnelId ** `String` `optional` Example: `tunnel-t2eryj3hl6gc60bv****`

The ID of the dual\-tunnel connection.



**TunnelOptions.N.CustomerGatewayId ** `String` `optional` Example: `cgw-t2eryj3hl6gc60bv****`

The ID of the customer gateway associated with the dual tunnels. If the IP address of the customer gateway is 0.0.0.0, you can only set NegotiateInstantly to **false**. In IkeConfig, you can only set IkeConfig.Version to **ikev1**, and set IkeConfig.Mode to **aggressive**.

When creating a dual\-tunnel IPsec\-VPN connection, this parameter is required.



**TunnelOptions.N.IkeConfig.Psk ** `String` `optional` Example: `Test123***`

The Pre\-Shared Key of IKE in the dual\-tunnel IPsec\-VPN connection. It is used for identity authentication between the VPN gateway and the customer gateway in Phase 1. Must not exceed 100 characters in length. May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**TunnelOptions.N.IkeConfig.Version ** `String` `optional` Example: `ikev1`

Version of the IKE protocol for the dual\-tunnel IPsec\-VPN connection. Values:


* ikev1

* ikev2


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">If the IP address of the customer gateway is set to <code>0.0.0.0</code>, <code>IkeConfig.Version</code> only allows <strong><code>ikev1</code></strong><strong>.</strong></div>




**TunnelOptions.N.IkeConfig.Mode ** `String` `optional` Example: `main`

The negotiation mode for IKE Phase 1 in the dual\-tunnel IPsec\-VPN connection. This parameter is required only if `IkeConfig.Version` is set to **ikev1**. Values:


* main

* aggressive


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">If the IP address of the customer gateway is set to <code>0.0.0.0</code>, <code>IkeConfig.Mode</code> only allows <code>aggressive</code>.</div>




**TunnelOptions.N.IkeConfig.EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection. Values:


* aes

* aes192

* aes256

* des

* 3des

* sm4



**TunnelOptions.N.IkeConfig.AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for IKE Phase 1 in the dual\-tunnel IPsec\-VPN connection. Values:


* sha1

* md5

* sha256

* sha384

* sha512

* sm3



**TunnelOptions.N.IkeConfig.DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection. Values:


* group1

* group2

* group5

* group14



**TunnelOptions.N.IkeConfig.Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for IKE Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated. Value range: 900 to 86400. Unit: seconds.



**TunnelOptions.N.IkeConfig.LocalId ** `String` `optional` Example: `IKE-VPN`

The identifier of the VPN gateway in the dual\-tunnel IPsec\-VPN connection. It is used for Phase 1 negotiation, supporting IP and FQDN formats.


* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters in length. May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**TunnelOptions.N.IkeConfig.RemoteId ** `String` `optional` Example: `IKE-USER`

The identifier of the customer gateway in the dual\-tunnel IPsec\-VPN connection. It is used for Phase 1 negotiation, supporting IP and FQDN formats.


* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters in length. May include uppercase and lowercase letters, numbers and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).



**EnableTunnelsBgp ** `Boolean` `optional` Example: `false`

Specify whether to enable BGP. Values:


* false: No. Use static routing.

* true: Yes. Use BGP routing.



**TunnelOptions.N.BGPConfig.TunnelCidr ** `String` `optional` Example: `169.254.XX.XX/30`

The CIDR block where the local and remote IPs of the BGP session are located.


* This CIDR block must be within 169.254.0.0/16, with a mask length of 30.

* If EnableTunnelsBgp is set to "true", this parameter is required.



**TunnelOptions.N.BGPConfig.LocalBgpIP ** `String` `optional` Example: `169.254.XX.XX`

The BGP address on the BytePlus side.


* This address must be within the IPsec tunnel CIDR block.

* If EnableTunnelsBgp is set to "true", this parameter is required.



**TunnelOptions.N.IpsecConfig.EncAlg ** `String` `optional` Example: `aes`

The encryption algorithm for Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection. Values:


* aes

* aes192

* aes256

* des

* 3des

* sm4



**TunnelOptions.N.IpsecConfig.AuthAlg ** `String` `optional` Example: `sha1`

The authentication algorithm for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection. Values:


* sha1

* md5

* sha256

* sha384

* sha512

* sm3



**TunnelOptions.N.IpsecConfig.DhGroup ** `String` `optional` Example: `group2`

The DH key exchange algorithm for Phase 2 in the dual\-tunnel IPsec\-VPN connection. Values:


* group1

* group2

* group5

* group14

* disable: Do not configure DH algorithm.


> If selecting group1, group2, group5, or group14, PFS is enabled by default. You also need to enable PFS on the peer client. If PFS is not available on the client, set to "disable" here.



**TunnelOptions.N.IpsecConfig.Lifetime ** `Integer` `optional` Example: `86400`

The SA lifetime for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated. Valid range: 900 to 86400. Unit: seconds. Default: 86400.



**TunnelOptions.N.NatTraversal ** `Boolean` `optional` Example: `false`

Specify whether to enable NAT traversal.


* true: Enable. Enabling NAT traversal skips the verification of the UDP port number during IKE negotiation and facilitates the discovery of NAT gateway devices involved in VPN.

* false: Disable.



**TunnelOptions.N.DpdAction** `String` `optional` Example: `clear`

Status of the Dead Peer Detection (DPD) feature.


* none: Disable DPD.

* clear: Enable DPD. When DPD timeout occurs, clear IKE SA.

* hold: Enable DPD. When DPD timeout occurs, hold the current status and re\-establish the connection upon receiving new traffic.

* restart: Enable DPD. When DPD timeout occurs, re\-establish the connection instantly.




**NegotiateInstantly ** `Boolean` `optional` Example: `true`

Specify whether to initiate the negotiation instantly.


* true: The system proactively initiates the negotiation instantly upon the completion of IPsec\-VPN connection configuration.

* false: The system does not initiate negotiation after the IPsec\-VPN connection configuration completes. Negotiation is triggered passively when traffic passes through.

* If left blank, the original configuration remains.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the IP address of the customer gateway associated with the IPsec\-VPN connection is <code>0.0.0.0</code>, you can only set to <strong>false</strong> here.</div>




**LogEnabled ** `Boolean` `optional` Example: `false`

Specify whether to enable IPsec Connection Log. After enabling IPsec Connection Log, you can view and download IPsec\-VPN connection logs, and troubleshoot IPsec\-VPN connection issues by logs.


* true: Enable.

* false: Disable.

* If left blank, the original configuration remains.


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">Before enabling IPsec Connection Log, confirm that you have enabled Torch Log Service (TLS) and Torch Object Storage (TOS) for the current account and have granted cross\-service permissions to the VPN connection service for accessing TLS.</div>




**Spec ** `String` `optional` Example: `default`

The instance type of the IPsec\-VPN connection. This parameter is only effective for IPsec\-VPN connections associated with Transit Router (TR) instances, and is invalid for connections associated with VPN gateways. If left blank, the default configuration remains.


* default: Default specification with a bandwidth cap of 200 Mbps.

* large: Large specification with a bandwidth cap of 1 Gbps.

* xlarge: Extra\-large specification with a bandwidth cap of 3 Gbps.


<div data-tips="true" data-tips-type="default">Note</div>


<div data-tips="true" data-tips-type="default">The large and extra\-large specifications are currently in the beta stage, and are available only after being enabled. If you need a trial, please contact your account manager.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



**OrderId ** `String` `optional` Example: `Order7078570823273845036`

The order ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyVpnConnectionAttributes&Version=2020-04-01&VpnConnectionId=vgc-2bzvqi8kerd342dx0eg2f****&IpsecConfig.EncAlg=aes256 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
ServiceName: vpn
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ModifyVpnConnectionAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "OrderId": "Order7078570823273845036",
        "RequestId": "202203211611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidVpnConnectionLocalSubnet.Malformed |The specified LocalSubnet is malformed. |The specified local network is invalid. |
|400 |InvalidVpnConnectionRemoteSubnet.Malformed |The specified RemoteSubnet is malformed. |The specified remote network is invalid. |
|400 |InvalidVpnConnectionIKEPsk.Malformed |The specified IKE Psk is malformed. Ensure the maximum length of IKE Psk is 100. |The format of specified IKE PSK is invalid. An IKE PSK cannot be more than 100 characters. |
|400 |InvalidVpnConnectionIKEPsk.Malformed |The specified IKE Psk is malformed. |The specified IKE Psk is invalid. |
|400 |InvalidVpnConnectionIKEAuthElg.Malformed |The specified IKE AuthAlg is malformed. |The specified IKE AuthAlg is invalid. |
|400 |InvalidVpnConnectionIKEEncElg.Malformed |The specified IKE EncAlg is malformed. |The specified IKE EncAlg is invalid. |
|400 |InvalidVpnConnectionIKEDhGroup.Malformed |The specified IKE DhGroup is malformed. |The specified IKE DhGroup is invalid. |
|400 |InvalidVpnConnectionIKEMode.Malformed |The specified IKE Mode is malformed. |The specified IKE Mode is invalid. |
|400 |InvalidVpnConnectionIKEVersion.Malformed |The specified IKE Version is malformed. |The specified IKE version is invalid. |
|400 |InvalidVpnConnectionIKELocalID.Malformed |The specified IKE LocalId is malformed. Ensure the maximum length of IKE LocalId is 100. |The format of specified IKE LocalId is invalid. IKE LocalId cannot exceed 100 characters in length. |
|400 |InvalidVpnConnectionIKELocalID.Malformed |The specified IKE LocalId is malformed. |The specified IKE LocalId is invalid. |
|400 |InvalidVpnConnectionIKERemoteID.Malformed |The specified IKE RemoteId is malformed. Ensure the maximum length of IKE RemoteId is 100. |The format of specified IKE RemoteId is invalid. An IKE RemoteId cannot be more than 100 characters. |
|400 |InvalidVpnConnectionIKERemoteID.Malformed |The specified IKE RemoteId is malformed. |The specified IKE RemoteId is invalid. |
|400 |InvalidVpnConnectionIKELifetime.Malformed |The specified IKE Lifetime is malformed. |The specified IKE Lifetime is invalid. |
|400 |InvalidVpnConnectionIPSecAuthElg.Malformed |The specified IPSec AuthAlg is malformed. |The specified IPSec AuthAlg is invalid. |
|400 |InvalidVpnConnectionIPSecEncElg.Malformed |The specified IPSec EncAlg is malformed. |The specified IPSec EncAlg is invalid. |
|400 |InvalidVpnConnectionIPSecDhGroup.Malformed |The specified IPSec DhGroup is malformed. |The specified IPSec DhGroup is invalid. |
|400 |InvalidVpnConnectionIPSecLifetime.Malformed |The specified IPSec Lifetime is malformed. |The specified IPSec Lifetime is invalid. |
|400 |QuotaExceeded.LocCIDREachVpnCon |You've reached the limit on the number of local subnet per IPSec connection that you can create. |You have reached the maximum of local subnets that you can create per IPsec\-VPN connection. |
|400 |QuotaExceeded.RemCIDREachVpnCon |You've reached the limit on the number of remote subnet per IPSec connection that you can create. |You have reached the maximum of remote subnets that you can create per IPsec\-VPN connection. |
|400 |InvalidVpnConnectionDpdAction.Malformed |The specified DpdAction is malformed. |The specified DpdAction is invalid. |
|400 |InvalidVpnGateway.FirmwareNotSupported |The specified features aren't supported by the VPN gateway, please upgrade your VPN gateway. |The selected feature is unavailable for the VPN gateway. Upgrade your VPN gateway. |
|400 |IncorrectVpnConnectionAttachStatus |The operation is not supported by the current IPSec connection attach status. |This action is unsupported. Retry later. |
|400 |IncorrectVpnConnectionStatus |The operation is not supported by the current vpn connection. |This action is unsupported. Retry later. |
|400 |InvalidVpnConnectionLocalSubnet.Conflict |The specified LocalSubnet conflicts with that of another subnet. |The specified local subnet conflicts with another CIDR block. |
|400 |InvalidVpnConnectionRemoteSubnet.Conflict |The specified RemoteSubnet conflicts with that of another subnet. |The specified remote subnet conflicts with another CIDR block. |
|400 |InvalidVpnConnectionRemoteId.Conflict |The specified IKE RemoteId conflicts with that of another IPSec connection in the specified VPN gateway. |The specified IKE RemoteId conflicts with another IPsec\-VPN connection under this gateway. |
|400 |InvalidVpnConnection.LogNotSupported |IPSec connection log is not supported in this region. |IPsec Connection Log is not available in the current region. |
|400 |LimitExceeded.TLSProject |You've reached the limit on the number of TLS project per region that you can create. |You have reached the maximum TLS log projects that you can create in a single region under the current account. |
|400 |InsufficientResource.VpnConnection |The specified region does not have enough resources for IPSec connection. |The available resources for the IPsec\-VPN connection are insufficient. |
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay the order. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InvalidVpnConnectionBgpLocalIp.Malformed |The BGP local IP is invalid; it should be within BGP tunnel CIDR and must be a host IP. |The specified BGP local address is invalid. |
|400 |InvalidVpnConnectionBgpTunnelCidr.Malformed |The BGP tunnel CIDR is invalid. |The specified BGP tunnel address is invalid. |
|400 |InvalidCustomerGateWay.ASNNotConfigured |The specified Customer gateway does not have an ASN. |The specified customer gateway is not configured with an ASN, and therefore BGP is unavailable. |
|400 |InvalidCustomerGateway.InvalidStatus |The specified customer gateway is not in the correct status for the request. |The specified customer gateway cannot respond to this request due to its status. |
|400 |InvalidVpnConnectionBgpTunnelCidr.Conflict |The specified BGP tunnel CIDR has conflicts. |The specified BGP tunnel address conflicts. |
|400 |InvalidVpnGateway.ASNNotConfigured |The specified VPN gateway does not have an ASN. |The specified customer gateway is not configured with an ASN, and therefore BGP is unavailable. |
|400 |InvalidVpnGateway.CustomerGateWayASNDuplicated |The VPN gateway ASN is the same as the customer gateway ASN. |The ASN of VPN gateway is the same as the ASN of customer gateway, and therefore BGP is unavailable. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |InvalidCustomerGateWay.SameVpcWithVpnGateway |The specified customer gateway and VPN gateway are in the same VPC. |The user gateway and VPN gateway are in the same VPC. The IPsec\-VPN connection between them cannot be established. |
|400 |InvalidCustomerGateway.InvalidASN |The Customer Gateway ASN is invalid and it should be in the range of 1\-4294967294, excluding 65535, 137718 and 150436. |The specified ASN is invalid. The value must be within the range of 1\-4294967294, excluding 65535, 137718, and 150436. |
|400 |InvalidHealthCheckConfig.IpNotInTrafficSelector |The specified local ip or remote ip is not within the configured traffic selector. |The local IP or remote IP of the health check is not within the set range of Traffic Selector. |
|400 |InvalidVpnGateway.InvalidASN |The VPN Gateway ASN is invalid and it should be in the range of 64512\-65534 or 4200000000\-4294967294. |The specified ASN is invalid. An ASN must be in the ranges of 64512\-65534 and 4200000000\-4294967294. |
|400 |InvalidVpnGatewayRouteType.Malformed |The specified route type is not support. |Unsupported route type. |
|400 |InvalidVpnConnection.DualTunnelConfigNotSupported |For single\-tunnel VPN connections, parameters used for dual\-tunnel VPN connections should not be passed in. |Parameters specific to dual\-tunnel VPN are inapplicable to single\-tunnel VPN. |
|400 |InvalidVpnConnection.SingleTunnelConfigNotSupported |For dual\-tunnel VPN connections, parameters used for single\-tunnel VPN connections should not be passed in. |Parameters specific to single\-tunnel VPN are inapplicable to dual\-tunnel VPN. |
|400 |InvalidVpnTunnelRemoteId.Conflict |The specified IKE RemoteId conflicts with that of another IPSec connection tunnel with the same role under this gateway. |The specified IKE RemoteId conflicts with another IPsec\-VPN connection tunnel in the same role under this gateway. |
|403 |InvalidVpnConnection.TlsNotSupport |TLS is not supported in this region. |TLS is not supported for the current account in this region. |
|403 |Forbidden.VpnConnectionBlocked |The specified TR IPsec is blocked. |The current TR IPsec is blocked. No actions are allowed. |
|403 |Forbidden.VpnGatewayBlocked |The specified VPN gateway is blocked. |The current VPN gateway is blocked. No actions are allowed. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|404 |InvalidTunnel.NotFound |The specified tunnel not exist. |The specified tunnel does not exist. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
|412 |InvalidVpnConnection.AccountInArrears |The specified IPSec connection has been shut down due to the account in arrears status. |The specified IPsec\-VPN connection is suspended due to overdue payments. |
