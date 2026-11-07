---
title: "CreateVpnConnection - Creating an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection"
---

Call CreateVpnConnection to create a new IPsec\-VPN connection.

## Instructions

* Two routing modes are available for creating an IPsec\-VPN connection: "Protected Data Flows" and "Destination Routing Mode". The default value is "Protected Data Flows". To use "Destination Routing Mode", set both request parameters LocalSubnet and RemoteSubnet to 0.0.0.0/0.

* You can create only one IPsec\-VPN connection when using the same VPN gateway and Remote ID.

* To use dynamic routing, the Autonomous System Number (ASN) of the VPN gateway must be different from that of the customer gateway associated with the same IPsec\-VPN connection. For IPsec\-VPN connections using dynamic routing, we do not recommend using 65535 as the ASN in any AS within the autonomous system. If 65535 exists in AS\-Path, the related routes may be discarded.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpnConnection&serviceCode=vpn&version=2020-04-01&groupName=)

## Request parameters

The following lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: CreateVpnConnection`

The action to perform. Value: CreateVpnConnection.

**Version ** String必选 `Example: 2020-04-01`

The API version.

**VpnConnectionName ** String`optional` `Example: IPsecVPN-10wd`

The name of the IPsec\-VPN connection.

* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, it defaults to the ID of IPsec\-VPN connection.

**Description ** String`optional` `Example: test`

The description of the IPsec\-VPN connection.

* Must start with a Chinese character, letter, or digit. May include Chinese characters, letters, digits, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.

**VpnGatewayId ** String`optional` `Example: vgw-3tex2x1cwd4c6c0v****`

The ID of the VPN gateway associated with the IPsec\-VPN connection. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the VPN gateway ID.

> Description

> This parameter is required when `AttachType` is not provided or is set to **VpnGateway**. This parameter is not required when `AttachType` is set to **TransitRouter**.

**LocalSubnet.N ** String必选 `Example: 10.0.XX.0/24`

The local CIDR block of the IPsec\-VPN connection.

* N in this parameter represents the sequence number of a local CIDR block.

* Up to five CIDR blocks are allowed.

* Separate multiple CIDR blocks with ampersands (&).

**RemoteSubnet.N ** String必选 `Example: 172.16.XX.0/24`

The remote CIDR block of the IPsec\-VPN connection.

* N in this parameter represent the sequence number of a remote CIDR block.

* Up to five CIDR blocks are allowed.

* Separate multiple CIDR blocks with ampersands (&).

**CustomerGatewayId ** String`optional` `Example: cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the single\-tunnel IPsec connection. This parameter is required when creating a single\-tunnel IPsec connection.

If the IP address of the customer gateway is `0.0.0.0`, `NegotiateInstantly` can only be set to **false**; in `IkeConfig`, `IkeConfig.Version` can only be set to **ikev1**, and `IkeConfig.Mode` can only be set to **aggressive**. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID.

**NatTraversal ** Boolean`optional` `Example: false`

Specify whether to enable NAT traversal for the single\-tunnel IPsec\-VPN connection. Values:

* true: Enable. Enabling NAT traversal skips the verification of the UDP port number during IKE negotiation and facilitates the discovery of NAT gateway devices involved in VPN.

* false (default): Disable.

**DpdAction ** String`optional` `Example: clear`

Specify whether to enable DPD for the single\-tunnel IPsec\-VPN connection. Values:

* none: Disable DPD.

* clear: Enable DPD. Clear IKE SA after timeout.

* hold: Enable DPD. Maintain the current status after timeout. Re\-establish the connection when new traffic is detected.

* restart: Enable DPD. Reconnect immediately after timeout.

**AttachType ** String`optional` `Example: VpnGateway`

The type of resource associated with the IPsec\-VPN connection. Values:

* VpnGateway (default): VPN gateway.

* TransitRouter: Transit Router.

**BgpConfig.EnableBgp ** Boolean`optional` `Example: true`

Specify whether to enable dynamic routing propagation. Values:

* false (default): No. Use static routing.

* true: Yes. Use BGP routing.

**BgpConfig.TunnelCidr** String `optional` `Example: 169.254.XX.XX/30`

The tunnel CIDR block of a single\-tunnel IPsec\-VPN connection. It is the CIDR block where the local and peer IP addresses of the BGP session reside.​

* This CIDR block must be within `169.254.0.0/16`, with a mask length of `/30`. It cannot be within 169.254.255.0/24.

* This parameter is required when `BgpConfig.EnableBgp` is set to `true`.

**BgpConfig.LocalBgpIp ** String`optional` `Example: 169.254.XX.XX`

The local tunnel IP is the BGP address configured on the VPN gateway

* This parameter defaults to the first host address of `BgpConfig.TunnelCidr`.

* This address must be within the IPsec tunnel CIDR block.

* This parameter is required when `BgpConfig.EnableBgp` is set to **true**.

**TunnelOptions.N.Role ** String`optional` `Example: TunnelOptions.1.Role=primary&TunnelOptions.2.Role=secondary`

The tunnel role of the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* primary: The current tunnel is the primary tunnel.

* secondary: The current tunnel is the secondary tunnel.

> **tip**

> This parameter is required when creating a dual\-tunnel IPsec\-VPN connection.

**TunnelOptions.N.CustomerGatewayId ** String`optional` `Example: TunnelOptions.1.CustomerGatewayId=cgw-t2eryj3hl6gc60bv****&TunnelOptions.2.CustomerGatewayId=cgw-rtvtey1nlt4yycvw****`

The ID of the customer gateway associated with the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* If the IP address of the customer gateway is 0.0.0.0, `NegotiateInstantly` can only be set to **false**, `IkeConfig.Version` can only be set to **ikev1**, and `IkeConfig.Mode` can only be set to **aggressive**.

> **tip**

> This parameter is required when creating a dual\-tunnel IPsec\-VPN connection.

**EnableTunnelsBgp ** Boolean `optional` `Example: false`

Specify whether to enable BGP. Values:

* false (default): No. Use static routing.

* true: Yes. Use BGP routing.

**TunnelOptions.N.BGPConfig.TunnelCidr** String `optional` `Example: TunnelOptions.1.BGPConfig.TunnelCidr=169.254.XX.XX/30&TunnelOptions.2.BGPConfig.TunnelCidr=169.254.XX.XX/30`

The CIDR block in the dual\-tunnel IPsec connection.​ It is the CIDR block where the local and peer IP addresses of the BGP session reside.

* N in this parameter represents the sequence number of a tunnel role.

* This address block must be within 169.254.0.0/16, with a mask length of 30.

* This parameter is required when `EnableTunnelsBgp` is set to **true**.

**TunnelOptions.N.BGPConfig.LocalBgpIP ** String`optional` `Example: TunnelOptions.1.BGPConfig.LocalBgpIP=169.254.XX.XX/30&TunnelOptions.2.BGPConfig.LocalBgpIP=169.254.XX.XX/30`

The BGP address on the BytePlus side of the IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* This parameter defaults to the first host address of `TunnelOptions.N.BGPConfig.TunnelCidr`.

* This address must be within the IPsec tunnel CIDR block.

* This parameter is required when `EnableTunnelsBgp` is set to **true**.

**TunnelOptions.N.NatTraversal ** Boolean`optional` `Example: TunnelOptions.1.NatTraversal=false&TunnelOptions.2.NatTraversal=false`

Specify whether to enable NAT traversal for the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* true: Enable. Enabling NAT traversal skips the verification of the UDP port number during IKE negotiation and facilitates the discovery of NAT gateway devices involved in VPN.

* false (default): Disable.

**TunnelOptions.N.DpdAction ** String`optional` `Example: TunnelOptions.1.DpdAction=clear&TunnelOptions.2.DpdAction=clear`

The DPD status of the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * none: Disable DPD.

   * clear: Enable DPD. Clear IKE SA after timeout.

   * hold: Enable DPD. Maintain the current status after timeout. Re\-establish the connection when new traffic is detected.

   * restart: Enable DPD. Reconnect immediately after timeout.

**ClientToken ** String`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

A client token used to ensure idempotency of requests.​

* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.

**ProjectName ** String`optional` `Example: Project_1`

The project to which the IPsec\-VPN connection belongs. If left blank, default is used. That is, the created resource belongs to the default project. You can call [ListProjects](https://docs.byteplus.com/en/docs/6649/1131880) to query project information under the current account.

**NegotiateInstantly ** Boolean`optional` `Example: true`

Specify whether to initiate negotiation instantly.

* true: The system actively initiates the negotiation instantly upon the completion of IPsec\-VPN connection configuration.

* false (default): The system does not initiate negotiation after the IPsec\-VPN connection configuration completes. Negotiation is triggered passively when traffic passes through.

> Description

> If the IP address of the customer gateway passed in is 0.0.0.0, you can only set to **false** here.

**LogEnabled ** Boolean`optional` `Example: true`

Specify whether to enable Connection Log. After enabling Connection Log, you can view and download IPsec\-VPN connection logs, and troubleshoot IPsec\-VPN connection issues by logs.

* true: Enable.

* false (default): Disable.

> Description

> Before enabling Connection Log, confirm that you have enabled TLS and TOS for the current account and have granted cross\-service permissions to the VPN Connect service for accessing TLS.

**Spec ** String `optional` `Example: default`

The instance type of the IPsec\-VPN connection. Values:

* default: Default specification with a bandwidth cap of 200 Mbps.

* large: Large specification with a bandwidth cap of 1 Gbps.

* xlarge: Extra\-large specification with a bandwidth cap of 3 Gbps.

> Description

* > This parameter takes effect only when the IPsec\-VPN connection is associated with a TR instance. It does not take effect for IPsec\-VPN connections associated with a VPN gateway instance. In other words, this parameter takes effect only when `AttachType` is set to **TransitRouter**.​

* > The large and extra\-large specifications are in the invite\-only beta stage, and are available only after being enabled. To request a trial, please contact your account manager.

**Tags.N.Key ** String`optional` `Example: key1`

The tag key of the IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with ampersands (&). Naming rules are as follows:

* Must not start with volc: or sys:, regardless of case.

* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* Must be 1 to 128 characters.

> **tip**

> Tag keys for the same resource must be unique.

**Tags.N.Value ** String`optional` `Example: value1`

The value of the IPsec\-VPN connection tag.

* N in this parameter represents the sequence number of a tag value. Valid values: 1–20.

* Separate multiple tag values with ampersands (&). Naming rules are as follows:

* May include language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* May be left blank. Must be 0 to 256 characters in length.

* Case\-sensitive. Must not start or end with a space.

> **tip**

> This parameter is required when `Tags.N.Value` is provided.

**IkeConfig.Psk ** String`optional` `Example: Test123***`

The Pre\-Shared Key of IKE in the single\-tunnel IPsec\-VPN connection. It is used for identity authentication between the VPN gateway and the customer gateway in Phase 1.

* Must not exceed 100 characters.

* May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**IkeConfig.Version ** String`optional` `Example: ikev2`

The IKE protocol version of the single\-tunnel IPsec\-VPN connection. Values:

* ikev1

* ikev2 (default)

**IkeConfig.Mode ** String`optional` `Example: main`

The negotiation mode for IKE Phase 1 in the single\-tunnel IPsec\-VPN connection. Values:

* main (default)

* aggressive

> **tip**

> This parameter is required only when `IkeConfig.Version` is set to **ikev1**.

**IkeConfig.EncAlg ** String`optional` `Example: aes`

The encryption algorithm for IKE Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. Values:

* aes (default)

* aes192

* aes256

* des

* 3des

* sm4

**IkeConfig.AuthAlg ** String`optional` `Example: sha1`

The authentication algorithm for IKE Phase 1 in the single\-tunnel IPsec\-VPN connection. Values:

* sha1 (default)

* md5

* sha256

* sha384

* sha512

* sm3

**IkeConfig.DhGroup** String `optional` `Example: group2`

The Diffie\-Hellman (DH) key exchange algorithm for Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. Values:

* group1

* group2 (default)

* group5

* group14

**IkeConfig.Lifetime ** Integer`optional` `Example: 86400`

The SA lifetime for IKE Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated.

Value range: 900 to 86400. Unit: seconds. Default: 86400.

**IkeConfig.LocalId ** String`optional` `Example: IKE-vpn`

The VPN gateway identifier of the single\-tunnel IPsec\-VPN connection. It is used for IKE Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection.​

* Supports IP and FQDN formats.

* If left unset, this parameter defaults to the egress IP address of the currently selected VPN gateway.

* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters. May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**IkeConfig.RemoteId ** String`optional` `Example: IKE-user`

The identifier of the customer gateway in the single\-tunnel IPsec\-VPN connection. It is used for IKE Phase 1 negotiation in the single\-tunnel IPsec\-VPN connection.

* Supports IP and Fully Qualified Domain Name (FQDN) formats.

* If left unset, this parameter defaults to the EIP of the currently selected customer gateway.

* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters. May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**IpsecConfig.EncAlg ** String`optional` `Example: aes`

The encryption algorithm for Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. Values:

* aes (default)

* aes192

* aes256

* des

* 3des

* sm4

**IpsecConfig.AuthAlg ** String`optional` `Example: sha1`

The authentication algorithm for IKE Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. Values:

* sha1 (default)

* md5

* sha256

* sha384

* sha512

* sm3

**IpsecConfig.DhGroup ** String`optional` `Example: group2`

The DH key exchange algorithm for Phase 2 in the single\-tunnel IPsec\-VPN connection. Values:

* group1

* group2 (default)

* group5

* group14

* disable: Do not configure DH algorithm.

> **tip**

> When this parameter is set to **group1**, **group2**, **group5**, or **group14**, PFS is enabled by default. The peer client must enable PFS as well. If the client does not support PFS, set this parameter to **disable**.​

**IpsecConfig.Lifetime ** Integer`optional` `Example: 86400`

The SA lifetime for IKE Phase 2 negotiation in the single\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated.

Value range: 900 to 86400. Unit: seconds. Default: 86400.

**TunnelOptions.N.IkeConfig.Psk ** String`optional` `Example: TunnelOptions.1.IkeConfig.Psk=Test123***&TunnelOptions.2.IkeConfig.Psk=Test678***`

The Pre\-Shared Key of IKE in the dual\-tunnel IPsec\-VPN connection. It is used for identity authentication between the VPN gateway and the customer gateway in Phase 1.

* N in this parameter represents the sequence number of a tunnel role.

* Must not exceed 100 characters.

* May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**TunnelOptions.N.IkeConfig.Version ** String`optional` `Example: TunnelOptions.1.IkeConfig.Version=ikev1&TunnelOptions.2.IkeConfig.Version=ikev1`

The version of the IKE protocol for the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * ikev1

   * ikev2 (default)

**TunnelOptions.N.IkeConfig.Mode ** String`optional` `Example: TunnelOptions.1.IkeConfig.Mode=main&TunnelOptions.2.IkeConfig.Mode=main`

The negotiation mode for IKE Phase 1 in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* This parameter is required only when `IkeConfig.Version` is set to **ikev1**.

* Values:

   * main (default)

   * aggressive

**TunnelOptions.N.IkeConfig.EncAlg ** String`optional` `Example: TunnelOptions.1.IkeConfig.EncAlg=aes&TunnelOptions.2.IkeConfig.EncAlg=aes`

The encryption algorithm for Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * aes (default)

   * aes192

   * aes256

   * des

   * 3des

   * sm4

**TunnelOptions.N.IkeConfig.AuthAlg ** String`optional` `Example: TunnelOptions.1.IkeConfig.AuthAlg=sha1&TunnelOptions.2.IkeConfig.AuthAlg=sha1`

The authentication algorithm for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * sha1 (default)

   * md5

   * sha256

   * sha384

   * sha512

   * sm3

**TunnelOptions.N.IkeConfig.DhGroup ** String`optional` `Example: TunnelOptions.1.IkeConfig.DhGroup=group2&TunnelOptions.2.IkeConfig.DhGroup=group2`

The DH key exchange algorithm for Phase 2 in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * group1

   * group2 (default)

   * group5

   * group14

   * disable: Do not configure DH algorithm.

> **tip**

> When this parameter is set to **group1**, **group2**, **group5**, or **group14**, PFS is enabled by default. The peer client must enable PFS as well. If the client does not support PFS, set this parameter to **disable**.​

**TunnelOptions.N.IkeConfig.Lifetime ** Integer`optional` `Example: TunnelOptions.1.IkeConfig.Lifetime=86400&TunnelOptions.2.IkeConfig.Lifetime=86400`

The SA lifetime for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated.

* N in this parameter represents the sequence number of a tunnel role.

* Value range: 900 to 86400. Unit: seconds. Default: 86400.

**TunnelOptions.N.IkeConfig.LocalId ** String`optional` `Example: TunnelOptions.1.IkeConfig.LocalId=IKE-vpn1&TunnelOptions.2.IkeConfig.LocalId=IKE-vpn2`

The IKE VPN gateway identifier of a dual\-tunnel IPsec\-VPN connection. It is used for IKE Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection.​

* N in this parameter represents the sequence number of a tunnel role.

* Supports IP and FQDN formats.

* If left unset, this parameter defaults to the egress IP address of the currently selected VPN gateway.

* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters. May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**TunnelOptions.N.IkeConfig.RemoteId ** String` optional` `Example: TunnelOptions.1.IkeConfig.RemoteId=IKE-user1&TunnelOptions.2.IkeConfig.RemoteId=IKE-user2`

The identifier of the customer gateway in the dual\-tunnel IPsec\-VPN connection. It is used for IKE Phase 1 negotiation in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Supports IP and FQDN formats.

* If left unset, this parameter defaults to the EIP of the currently selected customer gateway.

* We recommend setting the negotiation mode to "aggressive" if you manually set it to the FQDN format.

* Must not exceed 100 characters. May include uppercase and lowercase letters, digits and symbols (~ ` | ! @ # $ % ^ ( ) \- _ + = [ ] { } \ , . / : ;).

**TunnelOptions.N.IpsecConfig.EncAlg ** String`optional` `Example: TunnelOptions.1.IpsecConfig.EncAlg=aes&TunnelOptions.2.IpsecConfig.EncAlg=aes`

The encryption algorithm for Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * aes (default)

   * aes192

   * aes256

   * des

   * 3des

   * sm4

**TunnelOptions.N.IpsecConfig.AuthAlg ** String` optional` `Example: TunnelOptions.1.IpsecConfig.AuthAlg=sha1&TunnelOptions.2.IpsecConfig.AuthAlg=sha1`

The authentication algorithm for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * sha1 (default)

   * md5

   * sha256

   * sha384

   * sha512

   * sm3

**TunnelOptions.N.IpsecConfig.DhGroup ** String`optional` `Example: TunnelOptions.1.IpsecConfig.DhGroup=group2&TunnelOptions.2.IpsecConfig.DhGroup=group2`

The DH key exchange algorithm for Phase 2 in the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * group1

   * group2 (default)

   * group5

   * group14

   * disable: Do not configure DH algorithm.

> **tip**

> When this parameter is set to **group1**, **group2**, **group5**, or **group14**, PFS is enabled by default. The peer client must enable PFS as well. If the client does not support PFS, set this parameter to **disable**.​

**TunnelOptions.N.IpsecConfig.Lifetime ** Integer`optional` `Example: TunnelOptions.1.IpsecConfig.Lifetime=86400&TunnelOptions.2.IpsecConfig.Lifetime=86400`

The SA lifetime for IKE Phase 2 negotiation in the dual\-tunnel IPsec\-VPN connection. When the lifetime expires, a renegotiation is initiated.

* N in this parameter represents the sequence number of a tunnel role.

* Value range: 900 to 86400. Unit: seconds. Default: 86400.

**DpdMode ** String`optional` `Example: on_demand`

The DPD mode of the single\-tunnel IPsec\-VPN connection. Values:

* on_demand (default)

* periodic

**TunnelOptions.N.DpdMode ** String`optional` `Example: on_demand`

The DPD method for the dual\-tunnel IPsec\-VPN connection.

* N in this parameter represents the sequence number of a tunnel role.

* Values:

   * on_demand (default)

   * periodic

## Response parameters

The following lists only the response parameters unique to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2022032111142501022524314704AF****`

The request ID.

**VpnConnectionId ** String `Example: vgc-3tex2x1cwd4c6c0v****`

The ID of the new IPsec\-VPN connection.

**OrderId ** String`Example: Order7078570823273845036`

The order ID of the new IPsec\-VPN connection with TR.

**AsyncTaskId ** String`Example: asynctask-13f0odozfrdvk3n6nu41lt59g`

## Request example

```JSON
GET /?Action=CreateVpnConnection&Version=2020-04-01&VpnConnectionName=test&Description=test&CustomerGatewayId=cgw-274mm8eodvu9s7fap8skw****&VpnGatewayId=vgw-2752abxsju1vk7fap8sgk****&LocalSubnet=192.168.XX.XX/16&RemoteSubnet=172.16.XX.XX/16&IKEConfig.Psk=12345&IKEConfig.Version=ikev2&IKEConfig.EncAlg=aes&IPSecConfig.DhGroup=disable HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
ServiceName: vpn
Region: cn-beijing
```

## Response example

```JSON
{
    "ResponseMetadata":{
        "RequestId":"2022032111142501022524314704AF****",
        "Action":"CreateVpnConnection",
        "Version":"2020-04-01",
        "Service":"vpn",
        "Region":"cn-beijing"
    },
    "Result":{
        "RequestId":"2022032111142501022524314704AF****",
        "VpnConnectionId":"vgc-2bzvqi8kerd342dx0eg2f****"
    }
}
```

## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).
