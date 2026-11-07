---
title: "DescribeVpnConnections - Querying IPsec-VPN connections"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections"
---

Call DescribeVpnConnections to query IPsec\-VPN connections that meet the specified conditions.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnConnections&serviceCode=vpn&version=2020-04-01&groupName=)

## Request parameters

The following lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribeVpnConnections`

The action to perform. Value: DescribeVpnConnections.

**Version ** String必选 `Example: 2020-04-01`

The API version.

**PageSize ** Integer`optional` `Example: 20`

The number of entries per page in a pagination query. Valid values: 1–100. Default: 20.

**PageNumber ** Integer`optional` `Example: 1`

The page number of the list.

* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.

**VpnConnectionIds.N ** String`optional` `Example: vgc-273zkshb2qayo7fap8t21****`

The ID of the IPsec\-VPN connection.

* N in this parameter represents the sequence number of an IPsec\-VPN connection ID.

* Separate multiple IDs with ampersands (&).

**VpnConnectionName ** String`optional` `Example: test-001`

The name of the IPsec\-VPN connection.

**VpnGatewayId ** String`optional` `Example: vgw-3tex2x1cwd4c6c0v****`

The ID of the VPN gateway associated with the IPsec\-VPN connection. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.

**CustomerGatewayId ** String`optional` `Example: cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID.

**ProjectName ** String `optional` `Example: Project_1`

The name of the project to which the IPsec\-VPN connection belongs.

* If you provide this field, the system queries IPsec\-VPN connections under the specified project.

* If you omit this field, the system queries IPsec\-VPN connections across all projects.

**AttachType ** String`optional` `Example: VpnGateway`

The status of the resources attached to the IPsec\-VPN connection. That is, whether the IPsec\-VPN connection has attached resources.

* VpnGateway: VPN gateway

* TransitRouter: Transit Router

**AttachStatus ** String`optional` `Example: Attached`

The status of the IPsec\-VPN connection.

* The IPsec\-VPN connection is associated with a VPN gateway:

   * Attached

* The IPsec\-VPN connection is associated with a TR:

   * Attached

   * Attaching: The association is in process.

   * Detached

   * Detaching: The disassociation is in process.

**TransitRouterId ** String`optional` `Example: tr-bp1osj4c1q84p7syi****`

The TR ID. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to query the TR ID.

> **tip**

> When the value of `AttachType` is `TransitRouter`, provide this parameter for exact search. When the value of `AttachType` is `VpnGateway`, leave this field blank.

**Spec ** String`optional` `Example: default`

The instance type of the IPsec\-VPN connection.

* default: Default specification with a bandwidth cap of 200 Mbps.

* large: Large specification with a bandwidth cap of 1 Gbps.

* xlarge: Extra\-large specification with a bandwidth cap of 3Gbps.

> **tip**

> The large and extra\-large specifications are in the invite\-only beta stage, and are available only after being enabled. To request a trial, please contact your account manager.

**Status ** String`optional` `Example: Available`

The status of the IPsec\-VPN connection.

* Creating

* Deleting

* Pending: Configuration in progress.

* Available

**TagFilters.N.Key ** String`optional` `Example: key1`

The specified tag key when querying resources based on tags.

* N in this parameter represents the sequence number of a tag key. Valid values: 1\-10.

* Separate multiple tag keys with (`&`).

* The tag key must be unique.

**TagFilters.N.Values.M ** String`optional` `Example: value1`

The specified tag value when querying resources by tag.

* The first N represents the sequence number of a tag key. Valid values: 1–10.

* The second N represents the sequence number of a tag value. Valid values: 1–3. That is, you can query up to three tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide TagFilters.N.Key.

* If you only provide TagFilters.N.Key without this parameter, the system queries all tag values of the same tag key.

* If you provide an empty string, the system queries tags with an empty tag value.

* If you set multiple TagFilters.N.Values.M values for the same TagFilters.N.Key, these TagFilters.N.Values.M values are combined with a logical OR.

## Response parameters

The following lists only the response parameters unique to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 20220322145233010225243081016A****`

The request ID.

**PageSize ** Integer`Example: 20`

The number of entries on the current page.

**PageNumber ** Integer`Example: 1`

The current page number.

**TotalCount ** Integer`Example: 33`

Total number of IPsec\-VPN connections meeting the query conditions.

**VpnConnections ** Object[]`Example: -`

The description of the IPsec\-VPN connection.

**AccountId ** String`Example: 2000****`

The ID of the account that owns the IPsec\-VPN connection.

**VpnConnectionId ** String`Example: vgc-3tehy13n2l4c6c0v****`

The ID of the IPsec\-VPN connection.

**CreationTime ** String`Example: 2021-04-09T08:36:47+08:00`

The time when the IPsec\-VPN connection is created.

**UpdateTime ** String`Example: 2021-04-010T08:36:47+08:00`

The time when the IPsec\-VPN connection is updated.

**VpnConnectionName ** String`Example: abc`

The name of the IPsec\-VPN connection.

**Description ** String`Example: This is a sample description`

The description of the IPsec\-VPN connection.

**Status ** String`Example: Available`

The status of the IPsec\-VPN connection.

* Creating

* Deleting

* Pending: Configuration in progress.

* Available

**VpnGatewayId ** String`Example: vgw-3tex2x1cwd4c6c0v****`

The ID of the VPN gateway associated with the IPsec\-VPN connection.

**CustomerGatewayId ** String`Example: cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection.

**LocalSubnet** String[] `Example: 10.0.XX.XX/24`

The local subnet of the IPsec\-VPN connection.

**RemoteSubnet ** String[]`Example: 192.168.XX.XX/24`

The remote subnet of the IPsec\-VPN connection.

**DpdAction ** String`Example: clear`

Describes whether Dead Peer Detection (DPD) is enabled.

* none: DPD is not enabled.

* clear: DPD is enabled. Clear IKE SA after timeout.

* hold: DPD is enabled. Maintain the current status after timeout. Re\-establish the connection when new traffic is detected.

* restart: DPD is enabled. Reconnect immediately after timeout.

**ConnectStatus ** String`Example: ike_sa_negotiation_completed`

The status of the IPsec\-VPN connection.

* ike_sa_negotiation_failed: Phase 1 negotiation failed

* ike_sa_negotiation_completed: Phase 1 negotiation succeeded

* ipsec_sa_negotiation_failed: Phase 2 negotiation failed

* ipsec_sa_negotiation_completed: Phase 2 negotiation succeeded

**IkeConfig ** Object`Example: -`

The IKE Config of the IPsec\-VPN connection.

**Version ** String`Example: ikev1`

The version of the IKE protocol.

**Psk ** String`Example: 12345***`

The Pre\-Shared Key for identity authentication between the VPN gateway and the customer gateway in Phase 1.

**DhGroup ** String`Example: group2`

The DH key exchange algorithm for Phase 1 negotiation.

**Mode ** String`Example: main`

The negotiation mode for Phase 1. When the version of the IKE protocol is **ikev2**, an empty string is returned.

**EncAlg ** String`Example: aes`

The encryption algorithm for Phase 1 negotiation.

**AuthAlg ** String`Example: sha1`

The authentication algorithm for Phase 1 negotiation.

**LocalId** String `Example: 2.XX.XX.2`

The identifier of the VPN gateway for Phase 1 negotiation.

**RemoteId ** String`Example: 1.XX.XX.1`

The identifier of the customer gateway for Phase 1 negotiation.

**Lifetime ** Integer`Example: 86400`

The SA lifetime for Phase 1 negotiation. When the lifetime expires, a renegotiation is initiated.

**IpsecConfig ** Object`Example: -`

Information about the IPsec configuration of the IPsec\-VPN connection.

**AuthAlg ** String`Example: sha1`

The authentication algorithm for Phase 2 negotiation.

**EncAlg ** String`Example: aes`

The encryption algorithm for Phase 2 negotiation.

**DhGroup ** String`Example: group2`

The DH key exchange algorithm for Phase 2 negotiation.

**Lifetime ** Integer`Example: 86400`

The SA lifetime for Phase 2 negotiation. When the lifetime expires, a renegotiation is initiated.

**NatTraversal ** Boolean`Example: false`

Describes whether NAT Traversal is enabled.

* true: Enabled.

* false: Disabled.

**DualTunnelEnabled ** Boolean`Example: true`

Describe whether the dual\-tunnel mode is enabled.

* true: Enabled

* false (default): Disabled

**TunnelOptions ** Object[]`Example: -`

Configurations of the dual\-tunnel IPsec\-VPN connection.

**TunnelId ** String`Example: tunnel-3tehy13n2l4c6c0v****`

The ID of the tunnel connection.

**Role ** String`Example: Primary`

The role of the tunnel.

* primary: The current tunnel is the primary tunnel.

* secondary: The current tunnel is the secondary tunnel.

**CustomerGatewayId ** String`Example: cgw-3tehy13n2l4c6c0v****`

The ID of the customer gateway associated with the IPsec\-VPN connection.

**ConnectStatus ** String`Example: ike_sa_negotiation_completed`

The connection status of the tunnel.

* ike_sa_negotiation_failed: Phase 1 negotiation failed

* ike_sa_negotiation_completed: Phase 1 negotiation succeeded

* ipsec_sa_negotiation_failed: Phase 2 negotiation failed

* ipsec_sa_negotiation_completed: Phase 2 negotiation succeeded

**IkeConfig ** Object`Example: -`

The IKE Config of the IPsec\-VPN connection.

**Version ** String`Example: ikev1`

The version of the IKE protocol.

**Psk ** String`Example: 12345***`

The Pre\-Shared Key for identity authentication between the VPN gateway and the customer gateway in Phase 1.

**DhGroup ** String`Example: group2`

The DH key exchange algorithm for Phase 1 negotiation.

**Mode ** String`Example: main`

The negotiation mode for Phase 1. When the version of the IKE protocol is **ikev2**, an empty string is returned.

**EncAlg ** String`Example: aes`

The encryption algorithm for Phase 1 negotiation.

**AuthAlg ** String`Example: sha1`

The authentication algorithm for Phase 1 negotiation.

**LocalId** String `Example: 2.XX.XX.2`

The identifier of the VPN gateway for Phase 1 negotiation.

**RemoteId ** String`Example: 1.XX.XX.1`

The identifier of the customer gateway for Phase 1 negotiation.

**Lifetime ** Integer`Example: 86400`

The SA lifetime for Phase 1 negotiation. When the lifetime expires, a renegotiation is initiated.

**IpsecConfig ** Object`Example: -`

Information about the IPsec configuration of the IPsec\-VPN connection.

**AuthAlg ** String`Example: sha1`

The authentication algorithm for Phase 2 negotiation.

**EncAlg ** String`Example: aes`

The encryption algorithm for Phase 2 negotiation.

**DhGroup ** String`Example: group2`

The DH key exchange algorithm for Phase 2 negotiation.

**Lifetime ** Integer`Example: 86400`

The SA lifetime for Phase 2 negotiation. When the lifetime expires, a renegotiation is initiated.

**NatTraversal ** Boolean`Example: false`

Describes whether NAT Traversal is enabled.

* true: Enabled.

* false: Disabled.

**DpdMode ** String`Example: on_demand`

The DPD method of the IPsec\-VPN connection.

* on_demand

* periodic

**NegotiateInstantly ** Boolean`Example: true`

Specify whether to initiate the negotiation instantly.

* true: The system proactively initiates the negotiation instantly upon the completion of IPsec\-VPN connection configuration.

* false: The system does not initiate negotiation after the IPsec\-VPN connection configuration completes. Negotiation is triggered passively when traffic passes through.

**AttachStatus ** String`Example: Attached`

The status of the IPsec\-VPN connection.

* VpnGateway:

   * Attached

* TransitRouter:

   * Attached

   * Attaching: The association is in process.

   * Detached

   * Detaching: The disassociation is in process.

**AttachType ** String`Example: VpnGateway`

The gateway type associated with the IPsec\-VPN connection.

* VpnGateway: VPN gateway

* TransitRouter: Transit Router

**IpAddress ** String`Example: 180.XX.XX.182`

The Elastic IP Address (EIP) of the TR. The parameter returns a value only when `AttachType` is set to "TransitRouter".

**TransitRouterId ** String`Example: tr-bp1osj4c1q84p7syi****`

The TR ID. The parameter is returned only if `AttachType` is set to "TransitRouter".

**BusinessStatus ** String`Example: Normal`

The billing status of the IPsec\-VPN connection. This parameter is returned only when `AttachType` is "TransitRouter".

* Normal

* FinancialLocked: Being locked.

**DeletedTime ** String`Example: 2022-12-07 23:23:23`

The scheduled time when the resource is reclaimed forcibly. The parameter is returned only if `AttachType` is set to "TransitRouter". Furthermore, it has a response value only if the resources are frozen due to arrears. Otherwise, it returns an empty string.

**OverdueTime ** String`Example: 2022-12-07 23:23:23`

The time when the resource is frozen. The parameter is returned only if `AttachType` is set to "TransitRouter". Furthermore, it has a response value only if the resources are frozen due to arrears. Otherwise, it returns an empty string.

**LogEnabled ** Boolean`Example: false`

Describes whether Connection Log is enabled.

* true: Enabled.

* false: Disabled.

**Spec ** String`Example: default`

The instance type of the IPsec\-VPN connection. When `AttachType` is `VpnGateway`, this parameter is not returned.

* default: Default specification with a bandwidth cap of 200 Mbps.

* large: Large specification with a bandwidth cap of 1 Gbps.

* xlarge: Extra\-large specification with a bandwidth cap of 3Gbps.

**HealthCheckers ** Object[]`Example: -`

The health check information of the IPsec\-VPN connection.

**CheckInterval** Integer `Example: 3`

The time interval for performing health checks.

**CheckResult ** String`Example: Up`

The result of health check.

* Up: Healthy

* Down: Unhealthy

**CheckerId ** String`Example: vhc-abc`

The health check ID of the IPsec\-VPN connection.

**DownTime ** Integer`Example: 3`

The unhealthy threshold for health check. When consecutive health checks on an IPsec\-VPN connection fail for the specified number, the connection is declared unhealthy.

**LocalIp ** String`Example: 100.XX.XX.10`

The source IP for health check.

**RemoteIp ** String`Example: 100.XX.XX.10`

The target IP for health check.

**Timeout ** Integer`Example: 2`

The response timeout of the health check. If the IPsec\-VPN connection does not respond properly within the specified response time, the health check is declared failed.

**UpTime ** Integer`Example: 3`

The health threshold for health check. When consecutive health checks on an IPsec\-VPN connection pass for the specified number, the connection is declared healthy.

**IsBlocked ** Boolean`Example: false`

Describes whether the current resource is blocked.

* true: Blocked.

* false: Not blocked.

**BgpInfo ** Object`Example: -`

The BGP information of the IPsec\-VPN connection.

**EnableBgp ** Boolean`Example: true`

Describes whether BGP is enabled.

* true: Yes. Enabled.

* false: No. Disabled.

**TunnelCidr ** String`Example: 169.254.11.0/30`

The CIDR block where the local and remote IPs of the BGP session are located.

**LocalBgpIp ** String`Example: 169.254.XX.XX`

The local IP of the BGP session. That is, the BGP address on the BytePlus side.

**PeerBgpIp ** String`Example: 169.254.XX.XX`

The peer IP of the BGP session. That is, the BGP address on the customer gateway side.

**SessionStatus ** String`Example: Up`

The status of the BGP connection.

* Up: BGP connection is normal

* Down: BGP connection is unreachable.

**LocalAsn ** Integer`Example: 65534`

The ASN of the VPN gateway.

**PeerAsn ** Integer`Example: 42949`

The ASN of the customer gateway.

**Tags ** Object[]`Example: -`

Information about all tags associated with the IPsec\-VPN connection.

**Key ** String`Example: key1`

The tag key.

**Value ** String`Example: value1`

The tag value.

**ProjectName ** String`Example: default`

The project name of the IPsec\-VPN connection.

**ExpectedOverdueTime ** String`Example: 2024-05-18T14:00:00+08:00`

The time when the resource is frozen. This parameter returns a value only when the resource is frozen due to arrears.

## Request example

```JSON
GET /?Action=DescribeVpnConnections&Version=2020-04-01&PageSize=20&PageNumber=1&VpnConnectionIds.1=vgc-273zkshb2qayo7fap8t21****&VpnConnectionName=test-001&VpnGatewayId=vgw-3tex2x1cwd4c6c0v****&CustomerGatewayId=cgw-3tehy13n2l4c6c0v****&ProjectName=Project_1&AttachType=VpnGateway&AttachStatus=Attached&TransitRouterId=tr-bp1osj4c1q84p7syi****&Spec=default&Status=Available&TagFilters.1.Key=key1&TagFilters.1.Values.M=value1 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeVpnConnections",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "RequestId": "20220322145233010225243081016A****",
        "TotalCount": 33,
        "VpnConnections": [
            {
                "Spec": "default",
                "Tags": [
                    {
                        "Key": "key1",
                        "Value": "value1"
                    }
                ],
                "Status": "Available",
                "BgpInfo": {
                    "PeerAsn": 42949,
                    "LocalAsn": 65534,
                    "EnableBgp": true,
                    "PeerBgpIp": "169.254.XX.XX",
                    "LocalBgpIp": "169.254.XX.XX",
                    "TunnelCidr": "169.254.11.0/30",
                    "SessionStatus": "Up"
                },
                "AccountId": "2000****",
                "DpdAction": "clear",
                "IkeConfig": {
                    "Psk": "12345***",
                    "Mode": "main",
                    "EncAlg": "aes",
                    "AuthAlg": "sha1",
                    "DhGroup": "group2",
                    "LocalId": "2.XX.XX.2",
                    "Version": "ikev1",
                    "Lifetime": 86400,
                    "RemoteId": "1.XX.XX.1"
                },
                "IpAddress": "180.XX.XX.182",
                "IsBlocked": true,
                "AttachType": "VpnGateway",
                "LogEnabled": true,
                "UpdateTime": "2021-04-010T08:36:47+08:00",
                "DeletedTime": "2022-12-07 23:23:23",
                "Description": "This is a sample description",
                "IpsecConfig": {
                    "EncAlg": "aes",
                    "AuthAlg": "sha1",
                    "DhGroup": "group2",
                    "Lifetime": 86400
                },
                "LocalSubnet": [
                    ""
                ],
                "OverdueTime": "2022-12-07 23:23:23",
                "ProjectName": "default",
                "AttachStatus": "Attached",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "NatTraversal": false,
                "RemoteSubnet": [
                    ""
                ],
                "VpnGatewayId": "vgw-3tex2x1cwd4c6c0v****",
                "ConnectStatus": "ike_sa_negotiation_completed",
                "TunnelOptions": [
                    {
                        "Role": "Primary",
                        "DpdMode": "on_demand",
                        "TunnelId": "tunnel-3tehy13n2l4c6c0v****",
                        "IkeConfig": {
                            "Psk": "12345***",
                            "Mode": "main",
                            "EncAlg": "aes",
                            "AuthAlg": "sha1",
                            "DhGroup": "group2",
                            "LocalId": "2.XX.XX.2",
                            "Version": "ikev1",
                            "Lifetime": 86400,
                            "RemoteId": "1.XX.XX.1"
                        },
                        "IpsecConfig": {
                            "EncAlg": "aes",
                            "AuthAlg": "sha1",
                            "DhGroup": "group2",
                            "Lifetime": 86400
                        },
                        "NatTraversal": false,
                        "ConnectStatus": "ike_sa_negotiation_completed",
                        "CustomerGatewayId": "cgw-3tehy13n2l4c6c0v****"
                    }
                ],
                "BusinessStatus": "Normal",
                "HealthCheckers": [
                    {
                        "UpTime": 3,
                        "LocalIp": "100.XX.XX.10",
                        "Timeout": 2,
                        "DownTime": 3,
                        "RemoteIp": "100.XX.XX.10",
                        "CheckerId": "vhc-abc",
                        "CheckResult": "Up",
                        "CheckInterval": 3
                    }
                ],
                "TransitRouterId": "tr-bp1osj4c1q84p7syi****",
                "VpnConnectionId": "vgc-3tehy13n2l4c6c0v****",
                "CustomerGatewayId": "cgw-3tehy13n2l4c6c0v****",
                "DualTunnelEnabled": true,
                "VpnConnectionName": "abc",
                "NegotiateInstantly": true,
                "ExpectedOverdueTime": "2024-05-18T14:00:00+08:00"
            }
        ]
    }
}
```

## Error codes

The table below lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).

|**Status code** |**Error code** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.VpnConnectionId |You've reached the limit on the number of IPSec connection IDs that you can describe. |You have reached the maximum IDs of IPsec\-VPN connections that you can query. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
