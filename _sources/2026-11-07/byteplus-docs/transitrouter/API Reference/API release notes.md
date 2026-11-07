---
title: "API release notes"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/API-release-notes"
---

This section describes the API updates for Transit Router (TR).

<span id="hgZ62f0r"></span>
## April 2026


|API  |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|P4Ks8s">更新</span>[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment) |Delete error code: Forbidden.EnableRouteTablePropagationGranularity. |VPC attachment |
|<span data-api-tag="update\|cynPDL">更新</span>[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation)<br><br> ||Route learning |


<span id="ZT4N49Zf"></span>
## March 2026


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="add\|VmUZCT">新增</span> [ModifyTransitRouterTrafficQosQueueEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueueEntryAttributes) |Add a new API to modify the bandwidth allocation, name and description for a traffic queue. |Flow Log |
|<span data-api-tag="update\|cwXIm9">更新</span>[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) |* Add a new request parameter: PrefixListId. It indicates the ID of the prefix list.<br><br>* Add new error codes: InvalidTransitRouterRoutePolicyEntry.IpPrefixesInvalid and InvalidPrefixList.NotFound. |Route policy |
|<span data-api-tag="update\|4xhHkj">更新</span>[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||
|<span data-api-tag="update\|q0l4P2">更新</span>[DescribeTransitRouterRoutePolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyEntries) |Add a new response parameter: DestinationPrefixListId. It indicates the ID of the destination prefix list. ||
|<span data-api-tag="update\|Gc7Ru3">更新</span>[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry) |* Add a new request parameter: DestinationPrefixListId. It indicates the ID of the destination prefix list.<br><br>* Modify a request parameter: DestinationCidrBlock, from required to optional. This parameter is required when Destination CIDR is set to CIDR.<br><br>* Add new error codes: InvalidTransitRouterRouteEntry.DestinationInvalid, InvalidPrefixList.NotFound, InvalidTransitRouterRouteEntry.DestinationPrefixListConflict, and InvalidTransitRouterRouteEntry.DestinationPrefixListCidrConflict. |Route entry |
|<span data-api-tag="update\|wM2jIy">更新</span>[DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) |Add new response parameters:<br><br><br>* DestinationPrefixListId, indicating the ID of the destination prefix list.<br><br>* TransitRouterRouteEntryNextHopVpnTunnelId, indicating the tunnel ID of the route's Next Hop. ||


<span id="pFw5J7mL"></span>
## February 2026


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|lxufQh">更新</span> [DescribeTransitRouterAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterAttachments) |Add a new response parameter: BillingAccountId. It indicates the billing account ID of the intra\-region attachment. |TR instance |
|<span data-api-tag="update\|kHhLVw">更新</span> [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) |Add a new response parameter: BillingOwnerType. It indicates the fee payer of the network instance attachment. ||
|<span data-api-tag="update\|ZzhcdE">更新</span> [ModifyTransitRouterAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterAttributes) |* Add a new request parameter: BillingOwnerType, indicating the fee payer of the network instance attachment.<br><br>* Add a new error code: InvalidTransitRouter.BillingOwnerTypeInvalid. ||


<span id="O5gcS5qi"></span>
## January 2026


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|rE4l5q">更新</span>[CreateTransitRouterTrafficQosQueueEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosQueueEntry) |* Modify a request parameter: BandwidthPercent is modified from required to optional.<br><br>* Add a new request parameter: Priority, indicating the queue priority.<br><br>* Add new error codes: InvalidTransitRouterTrafficQosQueueEntry.PriorityInvalid, InvalidTransitRouterTrafficQosQueueEntry.BandwidthPercentNotSupport, and InvalidTransitRouterTrafficQosQueueEntry.PriorityExist. |Traffic queue policy |
|<span data-api-tag="update\|nOZh2o">更新</span>[DescribeTransitRouterTrafficQosQueueEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueueEntries) |Add a new response parameter: Priority. ||
|<span data-api-tag="update\|V3TqWg">更新</span>[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |Add a new error code: InvalidTransitRouterAttachment.DirectConnectAccessPointUnsupported. |DC Gateway attachment |


<span id="rWcBAWj9"></span>
## November 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|boYrmM">更新</span>[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |Add a new error code: UnsupportedOperation.<br><br> |TR instance |
|<span data-api-tag="update\|oFeB4a">更新</span>[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment) ||VPC attachment |
|<span data-api-tag="update\|Gh8f4R">更新</span>[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) ||VPN attachment |
|<span data-api-tag="update\|rLNDD5">更新</span>[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) ||DC Gateway attachment |
|<span data-api-tag="update\|tTQcL4">更新</span>[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage) ||Bandwidth package |
|<span data-api-tag="add\|Rexz8c">新增</span>[AcceptTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/AcceptTransitRouterPeerAttachment_-_Accepting_a_cross-account_inter-region_attachment) |Add new APIs to accept or reject cross\-account inter\-region attachments. |Inter\-region attachment |
|<span data-api-tag="add\|JQbymP">新增</span>[RejectTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/RejectTransitRouterPeerAttachment_-_Rejecting_a_cross-account_inter-region_attachment) |||
|<span data-api-tag="update\|nyx6AY">更新</span>[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) |* Add a new request parameter: PeerTransitRouterOwnerId, indicating the ID of the account that owns the TR instance.<br><br>* Add a new error code: InvalidTransitRouterPeer.InvalidAccount. ||
|<span data-api-tag="update\|jnTSjP">更新</span>[DeleteTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterPeerAttachment) |Add new error codes: InvalidTransitRouterAttachment.PeerRegionWithAssociation, InvalidTransitRouterAttachment.PeerRegionWithFlowLog, InvalidTransitRouterAttachment.PeerRegionWithRouteTablePropagation, InvalidTransitRouterPeerAttachment.PeerTransitRouterWithRouteEntryToPeerAttachment, and Forbidden.NoPermissionToOperate. ||
|<span data-api-tag="update\|MbnN9W">更新</span>[DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) |Add new response parameters:<br><br><br>* PeerTransitRouterOwnerId, indicating the ID of the account that owns the peer TR instance.<br><br>* TransitRouterBandwidthPackageOwnerId, indicating the ID of the account that owns the TR bandwidth package. ||
|<span data-api-tag="update\|ZuepdG">更新</span>[ModifyTransitRouterPeerAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterPeerAttachmentAttributes) |Add a new error code: Forbidden.NoPermissionToOperate. ||
|<span data-api-tag="update\|LojNxT">更新</span>[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry) |Add a new error code: InvalidTransitRouterAttachment.InvalidStatus. |Route entry |
|<span data-api-tag="update\|Xucr1o">更新</span>[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) ||Route policy |
|<span data-api-tag="update\|6O1EDr">更新</span>[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||
|<span data-api-tag="add\|CLgflK">新增</span>6 APIs, including [CreateTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterFlowLog) |Add new APIs to manage TR flow logs. |Flow Log |
|<span data-api-tag="update\|mGQFBW">更新</span>[DescribeTransitRouterRouteTablePropagations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTablePropagations) |Add a new response parameter: PropagationGranularity. |Route learning |
|<span data-api-tag="update\|cynPDL">更新</span>[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation)<br><br> |* Add a new request parameter: PropagationGranularity, indicating the granularity of route learning.<br><br>* Add new error codes: InvalidTransitRouterAttachment.InvalidStatus, InvalidTransitRouterRouteTablePropagation.PropagationGranularityInvalid, InvalidTransitRouterRouteTablePropagation.UnsupportedPropagationGranularity, and Forbidden.EnableRouteTablePropagationGranularity.<br><br><br> ||


<span id="JRSvn6II"></span>
## September 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|WmHW0p">更新</span>[DeleteTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterDirectConnectGatewayAttachment) |Add new error codes: Forbidden.NoPermissionToOperate and InvalidTransitRouter.NotFound. |DC Gateway attachment |
|<span data-api-tag="update\|nFTg4V">更新</span>[DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) |Add a new response parameter: Bandwidth. ||
|<span data-api-tag="update\|s7Q3u3">更新</span>[ModifyTransitRouterDirectConnectGatewayAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterDirectConnectGatewayAttachmentAttributes) |Add a new error code: Forbidden.NoPermissionToOperate ||
|<span data-api-tag="update\|UlWGFy">更新</span>[CreateTransitRouterGrantRule](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterGrantRule) |Add a new error code: Forbidden.SelfShareNotSupported. |Sharing |
|<span data-api-tag="update\|QHcps0">更新</span>[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |Add a new error code: Forbidden.CreateTransitRouterWithASN. |TR instance |
|<span data-api-tag="update\|dBK8dm">更新</span>[DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) |Add new response parameters:<br><br><br>* GrantSourceType, indicating the type of the shared instance.<br><br>* bandwidth, indicating the bandwidth cap of the TR instance. ||
|<span data-api-tag="update\|b5tUoP">更新</span>[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment) |* Add a new request parameter: ApplianceModeEnabled, indicating whether the path consistent mode is enabled for the VPC attachment.<br><br>* Add new error codes: InvalidTransitRouter.ApplianceModeNotSupported and Forbidden.ApplianceModeNotSupported. |VPC attachment |
|<span data-api-tag="update\|CduUHB">更新</span>[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes) |||
|<span data-api-tag="update\|xZFXcY">更新</span>[DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) |Add new response parameters:<br><br><br>* ApplianceModeEnabled, indicating whether the path consistent mode is enabled for the attachment.<br><br>* bandwidth, indicating the bandwidth cap of the attachment. ||
|<span data-api-tag="update\|FakFMr">更新</span>[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) |Add a new error code: InvalidTransitRouterRouteTableAssociation.TransitRouterMismatch. |VPN attachment |
|<span data-api-tag="update\|VINm6x">更新</span>[DeleteTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpnAttachment) |Add new error codes: InvalidTransitRouter.NotFound and Forbidden.NoPermissionToOperate. ||
|<span data-api-tag="update\|tIyA4D">更新</span>[DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) |Add a new response parameter: HealthCheckRevokeRouteEnabled. ||
|<span data-api-tag="update\|PSmQ9L">更新</span>[ModifyTransitRouterVpnAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpnAttachmentAttributes) |* Add a new request parameter: HealthCheckRevokeRouteEnabled, indicating whether to enable health check static route convergence.<br><br>* Add new error codes: InvalidTransitRouterRouteTableAssociation.TransitRouterMismatch and Forbidden.NoPermissionToOperate. ||


<span id="pZiDpOPJ"></span>
## July 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|RO9meT">更新</span>[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry)<br><br> |* Add a new request parameter: IpPrefixMatchMode.<br><br>* Add new error codes: InvalidTransitRouterRoutePolicyEntry.IpPrefixMatchModeInvalid and InvalidTransitRouterRoutePolicyEntry.IpPrefixMatchModeMismatch. |Route policy<br><br> |
|<span data-api-tag="update\|m0f95z">更新</span>[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||
|<span data-api-tag="update\|oXvhNy">更新</span>[DescribeTransitRouterRoutePolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyEntries) |Add a new response parameter: IpPrefixMatchMode. ||


<span id="nVyReiZk"></span>
## May 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="add\|fXaoNq">新增</span>12 APIs, including [CreateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastDomain) |Add new APIs to manage TR multicast. |Multicast |
|<span data-api-tag="update\|em159K">更新</span>[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) |Add new error codes: InvalidPeerTransitRouter.InvalidBusinessStatus, InvalidTransitRouterRouteTablePropagation.ASNConflict, and QuotaExceeded.PeerTransitRouterAttachment. |Inter\-region attachment |
|<span data-api-tag="update\|PlDEBS">更新</span>[DeleteTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterPeerAttachment) |Add a new error code: InvalidTransitRouterAttachment.WithFlowLog. ||
|<span data-api-tag="update\|VqPK15">更新</span>[TagResources](https://docs.byteplus.com/en/docs/transitrouter/TagResources) |A request parameter is modified: transiroutermulticastdomain is added as a value field to ResourceType. |Tag |
|<span data-api-tag="update\|6ef6Qs">更新</span>[UntagResources](https://docs.byteplus.com/en/docs/transitrouter/UntagResources) |||
|<span data-api-tag="update\|mFw3FJ">更新</span>[ListTagsForResources](https://docs.byteplus.com/en/docs/transitrouter/ListTagsForResources) |||
|<span data-api-tag="update\|QHcps0">更新</span>[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |* Add a new request parameter: MulticastEnabled.<br><br>* Add new error codes: InvalidAccount.CreateTransitRouterWithMulticast and Forbidden.CreateTransitRouterWithMulticast. |TR instance |
|<span data-api-tag="update\|NYsItS">更新</span>[DeleteTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouter) |Add a new error code: InvalidTransitRouter.WithMulticastDomain. ||
|<span data-api-tag="update\|dBK8dm">更新</span>[DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) |Add a new response parameter: MulticastEnabled. ||
|<span data-api-tag="update\|ht5pvL">更新</span>[DeleteTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpcAttachment) |Add new error codes: InvalidTransitRouterAttachment.WithMulticastDomainAssociation and InvalidTransitRouterAttachment.WithMulticastGroup. |VPC attachment |
|<span data-api-tag="update\|4O8EDb">更新</span>[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage) |Add a new error code: Forbidden.NotVerifiedAccount. |Bandwidth package |
|<span data-api-tag="update\|gboRHv">更新</span>[DeleteTransitRouterForwardPolicyTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterForwardPolicyTable) |Add a new request parameter: Force.<br><br> |Forwarding policy |
|<span data-api-tag="update\|lTYPsO">更新</span>[DeleteTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRoutePolicyTable) ||Route policy |
|<span data-api-tag="update\|jCAkDL">更新</span>[DeleteTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingPolicy) ||Traffic marking policy |
|<span data-api-tag="update\|sWPYhC">更新</span>[DeleteTransitRouterTrafficQosQueuePolicy](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueuePolicy) ||Traffic queue policy |
|<span data-api-tag="update\|9gT1OB">更新</span>[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation) |Add new error codes: InvalidTransitRouterRouteTablePropagation.ASNConflict and InvalidTransitRouterPeerAttachment.PeerAttachmentNotFound. |Route learning |
|<span data-api-tag="update\|9IQDla">更新</span>[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry) |Add a new error code: InvalidTransitRouterRouteEntry.MulticastCidrNotSupported. |Route entry<br><br> |
|<span data-api-tag="update\|nWQa0J">更新</span>[DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries)<br><br> |* Add new request parameters: TransitRouterRouteEntryNextHopId, TransitRouterRouteEntryNextHopResourceType, and TransitRouterRouteEntryNextHopType.<br><br>* Add new response parameters: TransitRouterRouteEntryNextHopResourceId and TransitRouterRouteEntryNextHopResourceType. ||


<span id=".MjAyNOW5tDEy5pyI"></span>
## March 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|hKV4GP">更新</span>[CreateTransitRouterForwardPolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyEntry) |* Add a new request parameter: DestinationCidrBlock.<br><br>* Add new error codes: InvalidTransitRouterForwardPolicyEntry.CidrVersionMismatch and Forbidden.TransitRouterIPv6.<br><br>* An error code is deleted: InvalidTransitRouterForwardPolicyEntry.SourceCidrBlockIsIPv6. |Forwarding policy |
|<span data-api-tag="update\|rAzRi9">更新</span>[ModifyTransitRouterForwardPolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyEntryAttributes) |||
|<span data-api-tag="update\|aCg4dO">更新</span>[DescribeTransitRouterForwardPolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyEntries) |* Add a new request parameter: DestinationCidrBlock.<br><br>* Add a new response parameter: DestinationCidrBlock. ||
|<span data-api-tag="update\|UlWGFy">更新</span>[CreateTransitRouterGrantRule](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterGrantRule) |Add a new error code: InvalidTransitRouterGrantRule.AccountTypeConflict. |Sharing |
|<span data-api-tag="update\|VP5F6G">更新</span>[DescribeTransitRouterAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterAttachments)<br><br> |Add a new response parameter: Ipv6Enabled. |TR instance |
|<span data-api-tag="update\|b5tUoP">更新</span>[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment)<br><br> |* Add a new request parameter: Ipv6Enabled.<br><br>* Add new error codes: InvalidTransitRouterAttachment.SubnetWithoutIPv4Cidr, InvalidTransitRouterAttachment.SubnetWithoutIPv6Cidr, and Forbidden.TransitRouterIPv6. |VPC attachment<br><br> |
|<span data-api-tag="update\|xZFXcY">更新</span>[DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) |Add a new response parameter: Ipv6Enabled.<br><br> ||
|<span data-api-tag="update\|CduUHB">更新</span>[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes)<br><br> |* Add a new request parameter: Ipv6Enabled.<br><br>* Add new error codes: InvalidTransitRouterAttachment.SubnetWithoutIPv4Cidr, InvalidTransitRouterAttachment.SubnetWithoutIPv6Cidr, InvalidTransitRouterAttachment.VpcWithIPv4RouteEntryToTransitRouter, InvalidTransitRouterAttachment.VpcWithIPv6RouteEntryToTransitRouter, InvalidTransitRouterAttachment.VpcWithRouteEntryToTransitRouter, InvalidTransitRouterAttachment.WithIPv4StaticRouteEntry, InvalidTransitRouterAttachment.WithIPv6StaticRouteEntry, InvalidTransitRouterAttachment.WithStaticRouteEntry, and Forbidden.TransitRouterIPv6. ||
|<span data-api-tag="update\|m6zraC">更新</span>[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |Add a new error code: Forbidden.TransitRouterIPv6.<br><br> |DC Gateway attachment |
|<span data-api-tag="update\|FakFMr">更新</span>[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) ||VPN attachment |
|<span data-api-tag="update\|3vp9Iw">更新</span>[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) ||Inter\-region attachment<br><br> |
|<span data-api-tag="update\|nFTg4V">更新</span>[DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) |Add a new response parameter: Ipv6Enabled.<br><br> ||
|<span data-api-tag="update\|cIV0zc">更新</span>[DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) |||
|<span data-api-tag="update\|GenM3i">更新</span>[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry)<br><br> |* An error code is deleted: InvalidTransitRouterRouteEntry.DestinationCidrBlockIsIPv6.<br><br>* Add new error codes: InvalidTransitRouterRouteEntry.IPv4OnlyAttachment, InvalidTransitRouterRouteEntry.IPv6OnlyAttachment, and Forbidden.TransitRouterIPv6. |Route entry |
|<span data-api-tag="update\|YOvWvE">更新</span>[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) |Add a new error code: Forbidden.TransitRouterIPv6.<br><br>An error code is deleted: InvalidTransitRouterRoutePolicyEntry.IpPrefixIsIPv6. |Route policy<br><br> |
|<span data-api-tag="update\|oZzNND">更新</span>[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||


<span id="eRZLrCzT"></span>
## January 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|0LdyJi">更新</span>[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage) |* Add a new request parameter: LineOperator.<br><br>* Add new error codes: InvalidLineOperator.LineOperatorMalformed and UnsupportedOperation.CreateNonCrossBorderBandwidthPackageWithLineOperator. |Bandwidth package |
|<span data-api-tag="update\|tHRJEO">更新</span>[DescribeTransitRouterBandwidthPackages](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages) |Add a new response parameter: LineOperator. ||
|<span data-api-tag="update\|rygGhp">更新</span>[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |An error code is deleted: InvalidTransitRouterAttachment.DirectConnectGatewayHasCustomizedAsn. |DC Gateway attachment |


<span id="q9KLtVmh"></span>
## December 2024


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="add\|hbB8P3">新增</span>10 APIs, including [CreateTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingPolicy) |Add new APIs to manage traffic marking policies. |Traffic marking policy |
|<span data-api-tag="add\|ucsP58">新增</span>10 APIs, including [CreateTransitRouterTrafficQosQueuePolicy](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosQueuePolicy) |Add new APIs to manage traffic queue policies. |Traffic queue policy |


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|KYYGKs">更新</span>[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) |Value range is modified for "N" in the request parameter `IpPrefixes.N`. |Route policy |
|<span data-api-tag="update\|iodQWm">更新</span>[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||
|<span data-api-tag="update\|CzcnZX">更新</span>[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage) |An error code is deleted: `UnsupportedOperation.AutoRenewal`. |Bandwidth package |
|<span data-api-tag="update\|6yicUK">更新</span>[RenewTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/RenewTransitRouterBandwidthPackage) |Add new error codes: `InvalidTransitRouterCrossBorderBandwidthPackage.FrozenStatus` and `UnsupportedOperation.PrepaidInstanceRequired`. An error code is deleted: `UnsupportedOperation.CrossBorderBandwidthPackage`. ||
|<span data-api-tag="update\|0E5Apc">更新</span>[SetTransitRouterBandwidthPackageRenewal](https://docs.byteplus.com/en/docs/transitrouter/SetTransitRouterBandwidthPackageRenewal) |Add a new error code `UnsupportedOperation.PrepaidInstanceRequired`. An error code is deleted: `UnsupportedOperation.CrossBorderBandwidthPackage`. ||
|<span data-api-tag="update\|O0kl5u">更新</span>[ModifyTransitRouterBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterBandwidthPackageAttributes) |An error code is deleted: `UnsupportedOperation.BandwidthScaleDown`. ||
|<span data-api-tag="update\|lrkBSQ">更新</span>[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) |Add a new error code: `LimitExceeded.PhysicalLineBandwidth`. |Inter\-region attachment |
|<span data-api-tag="update\|lw3Dmd">更新</span>[ModifyTransitRouterPeerAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterPeerAttachmentAttributes) |Add a new error code: `LimitExceeded.PhysicalLineBandwidth`. ||
|<span data-api-tag="update\|EF2hf5">更新</span>[DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) |Add a new request parameter: `TransitRouterRouteEntryType`. |Route entry |


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|**API** |**Release note** |**Associated features** |
|---|---|---|
|[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) |Add request parameters: TransitRouterRouteTableId; and error codes: InvalidTransitRouterAttachment.TransitRouterLackOfAsn, InvalidTransitRouterRoutePropagation.TransitRouterMismatch, Forbidden.CreateTransitRouterBgpVpnAttachment, InvalidTransitRouterAttachment.IPSecConnectionAsnConflict, and InvalidTransitRouterAttachment.IPSecConnectionBgpTunnelCidrConflict. |VPN attachments |
|[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |Add error codes: InvalidTransitRouterAttachment.DirectConnectGatewayHasCustomizedAsn. |Direct Connect Gateway attachments |
|[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation) |Add error codes: Forbidden.CreateRouteTablePropagationWithVpnAttachment, Forbidden.CreateTransitRouterBgpVpnAttachment. |Route learning |
|[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) |Add error codes: Forbidden.CreateRoutePolicyEntryWithVpnAttachment, Forbidden.CreateTransitRouterBgpVpnAttachment. |Routing policies |
|[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |||
|[CreateTransitRouterForwardPolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyEntry) |Add error codes: InvalidTransitRouterForwardPolicyEntry.PriorityInvalid. |Forwarding policies |


<span id=".MjAyNOW5tDA35pyI"></span>
## July 2024


|**API** |**Released on** |**Release note** |**Associated features** |
|---|---|---|---|
|[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |2024\-07\-17 |Add error codes: Forbidden.PurchaseLimited. |TR instances |
|[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment) |||VPC attachments |
|[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) |||VPN attachments |
|[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |||Direct Connect Gateway attachments |


<span id=".MjAyNOW5tDA15pyI"></span>
## May 2024


|**API** |**Released on** |**Release note** |**Associated features** |
|---|---|---|---|
|[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |2024\-05\-28 |Add request parameters: Asn; Add error codes: InvalidTransitRouter.ASNInvalid, Forbidden.CreateTransitRouterWithASN. |TR instances |
|[DeleteTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouter) ||Add error codes: InvalidTransitRouter.WithForwardPolicyTable, InvalidTransitRouter.WithRoutePolicy. ||
|[DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) ||Add response parameters: Asn. ||
|[DescribeTransitRouterAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterAttachments) ||Add request parameters: TransitRouterForwardPolicyTableId; and response parameters: TransitRouterForwardPolicyTableId. ||
|[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) ||Add error codes: Forbidden.VpnConnectionBlocked. |Intra\-region attachments |
|[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes) ||Add error codes: InvalidTransitRouterAttachment.InvalidStatus. ||
|[ModifyTransitRouterVpnAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpnAttachmentAttributes) ||||
|[ModifyTransitRouterDirectConnectGatewayAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterDirectConnectGatewayAttachmentAttributes) ||||
|[ModifyTransitRouterPeerAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterPeerAttachmentAttributes) |||Inter\-Region attachments |
|[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) ||Add error codes: Forbidden.EnablePeerTransitRouterRouteTablePropagation. ||
|[DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) ||Add response parameters: TransitRouterForwardPolicyTableId. ||
|[AssociateTransitRouterAttachmentToRouteTable](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterAttachmentToRouteTable) ||Add error codes: InvalidTransitRouterAttachment.InvalidStatus. |Associated forwarding |
|[DissociateTransitRouterAttachmentFromRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterAttachmentFromRouteTable) ||||
|[ModifyTransitRouterRouteTableAssociationAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteTableAssociationAttributes) ||Add error codes: InvalidTransitRouterAttachment.InvalidStatus, InvalidTransitRouter.InvalidBusinessStatus. ||
|[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation) ||A request parameter is modified: TransitRouterAttachmentId supports inter\-region attachments. Add error codes: Forbidden.EnablePeerTransitRouterRouteTablePropagation. |Route learning |
|[DisableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/DisableTransitRouterRouteTablePropagation) ||A request parameters is modified: TransitRouterAttachmentId supports inter\-region attachments. ||
|[DescribeTransitRouterRouteTablePropagations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTablePropagations) ||||
|[DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) ||Add response parameters: InRoutePolicyTableId, OutRoutePolicyTableId. |Route tables |
|[DeleteTransitRouterRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteTable) ||Add error codes: InvalidTransitRouterRouteTable.WithForwardPolicyEntry. ||
|[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry) ||A request parameters is modified: TransitRouterRouteEntryNextHopType supports inter\-region attachments. |Route entries |
|[CreateTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyTable) and other 10 interfaces ||New interface, used for managing routing policy. |Routing policies |
|[CreateTransitRouterForwardPolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyTable) and other 10 interfaces ||A new interface for managing forwarding policies. |Forwarding policies |


<span id=".MjAyNOW5tDA05pyI"></span>
## April 2024


|**API** |**Released on** |**Release note** |**Associated features** |
|---|---|---|---|
|All actions |2024\-04\-10 |TR APIs are released for the first time. |\-\- |
