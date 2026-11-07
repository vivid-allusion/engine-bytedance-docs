---
title: "API overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/API-overview"
---

This topic introduces the API actions available for Transit Router (TR).

<span id=".5Lit6L2s6Lev55Sx5Zmo5a6e5L6L"></span>
## TR instances


|API |Description |
|---|---|
|[CreateTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouter) |Create an instance. |
|[DeleteTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouter) |Delete an instance. |
|[DescribeTransitRouterAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterAttachments) |Query TR attachments that meet specified conditions, including VPC, VPN, DC Gateway attachments, and Inter\-region attachments. |
|[DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) |Query TR instances that meet specified conditions. |
|[ModifyTransitRouterAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterAttributes) |Modify the name or description of the TR instance. |


<span id=".5a6e5L6L5YWx5Lqr"></span>
## Instance sharing


|API |Description |
|---|---|
|[CreateTransitRouterGrantRule](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterGrantRule) |Create instance sharing to share a specified TR instance with another account. |
|[DescribeTransitRouterGrantRules](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterGrantRules) |Query instance sharing that meets specified conditions. |
|[ModifyTransitRouterGrantRuleAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterGrantRuleAttributes) |Modify the description of the instance sharing. |
|[AcceptSharedTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/AcceptSharedTransitRouter) |Accept the TR instance shared by other accounts to this account. |
|[RejectSharedTransitRouter](https://docs.byteplus.com/en/docs/transitrouter/RejectSharedTransitRouter) |Reject TR instances shared with your account by other accounts. |
|[DeleteTransitRouterGrantRule](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterGrantRule) |Delete instance sharing. |


<span id=".VlBD57G75Z6L572R57uc5a6e5L6L6L-e5o6l"></span>
## VPC attachment


|API |Description |
|---|---|
|[CreateTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpcAttachment) |Creates a VPC attachment. |
|[DeleteTransitRouterVpcAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpcAttachment) |Deletes a specified VPC attachment. |
|[DescribeTransitRouterVpcAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments) |Query VPC attachments that meet specified conditions. |
|[ModifyTransitRouterVpcAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpcAttachmentAttributes) |Modify the name, description, or attachment point of VPC attachments, enable or disable route synchronization. |


<span id=".VlBO57G75Z6L572R57uc5a6e5L6L6L-e5o6l"></span>
## Virtual Private Network (VPN)\-type attachment


|API |Description |
|---|---|
|[CreateTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterVpnAttachment) |Create a Virtual Private Network (VPN) attachment. |
|[DeleteTransitRouterVpnAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterVpnAttachment) |Delete a VPN attachment. |
|[DescribeTransitRouterVpnAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments) |Query VPN attachments that meet specified conditions. |
|[ModifyTransitRouterVpnAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterVpnAttachmentAttributes) |Modify the name or description of the VPN attachment. |


<span id=".5LiT57q_572R5YWz57G75Z6L572R57uc5a6e5L6L6L-e5o6l"></span>
## DC gateway\-type attachment


|API |Description |
|---|---|
|[CreateTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterDirectConnectGatewayAttachment) |Create a Direct Connect (DC) Gateway attachment. |
|[DeleteTransitRouterDirectConnectGatewayAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterDirectConnectGatewayAttachment) |Delete a DC Gateway attachment. |
|[DescribeTransitRouterDirectConnectGatewayAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments) |Query DC Gateway attachments that meet specified conditions. |
|[ModifyTransitRouterDirectConnectGatewayAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterDirectConnectGatewayAttachmentAttributes) |Modify the name or description of the DC Gateway attachment. |


<span id=".5bim5a695YyF"></span>
## TR bandwidth packages


|API |Description |
|---|---|
|[CreateTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterBandwidthPackage) |Create a bandwidth package. |
|[ModifyTransitRouterBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterBandwidthPackageAttributes) |Modifies the bandwidth of a specified TR bandwidth package. |
|[DeleteTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterBandwidthPackage) |Delete a bandwidth package. |
|[DescribeTransitRouterBandwidthPackages](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages) |Query TR bandwidth packages that meet specified conditions. |
|[DescribeTransitRouterRegions](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRegions) |Query the geographic region sets and regions supported for the current account. |
|[DescribeTransitRouterBandwidthPackagesBilling](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackagesBilling) |Query the billing information about a bandwidth package. |
|[RenewTransitRouterBandwidthPackage](https://docs.byteplus.com/en/docs/transitrouter/RenewTransitRouterBandwidthPackage) |Renew a bandwidth package. |
|[SetTransitRouterBandwidthPackageRenewal](https://docs.byteplus.com/en/docs/transitrouter/SetTransitRouterBandwidthPackageRenewal) |Set renewal type for a bandwidth package. |


<span id=".6Leo5Zyw5Z-f6L-e5o6l"></span>
## Inter\-region attachment


|API |Description |
|---|---|
|[CreateTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterPeerAttachment) |Creates an inter\-region peering attachment. |
|[ModifyTransitRouterPeerAttachmentAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterPeerAttachmentAttributes) |Modify the name, description, bandwidth, and the associated bandwidth package of the Inter\-region attachment. |
|[DeleteTransitRouterPeerAttachment](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterPeerAttachment) |Delete an Inter\-region attachment. |
|[DescribeTransitRouterPeerAttachments](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments) |Query inter\-region attachments that meet specified conditions. |


<span id=".6Lev55Sx6KGo"></span>
## Route tables


|API |Description |
|---|---|
|[CreateTransitRouterRouteTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteTable) |Create a custom route table. |
|[DeleteTransitRouterRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteTable) |Delete a custom route table. |
|[DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) |Query TR route tables that meet specified conditions. |
|[ModifyTransitRouterRouteTableAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteTableAttributes) |Modify the name or description of the route table. |


<span id=".6Lev55Sx5p2h55uu"></span>
## Route entry


|API |Description |
|---|---|
|[CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry) |Add static route entries to a specified TR route table. |
|[DeleteTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteEntry) |Delete a static route entry. |
|[DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries) |Query static route entries that meet specified conditions. |
|[ModifyTransitRouterRouteEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteEntryAttributes) |Modifies the name or description of a route entry. |


<span id=".5YWz6IGU6L2s5Y-R"></span>
## Association forwarding


|API |Description |
|---|---|
|[AssociateTransitRouterAttachmentToRouteTable](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterAttachmentToRouteTable) |Attach a route table for TR attachments (including VPC, VPN, DC Gateway network instance attachments and Inter\-region attachments). |
|[DescribeTransitRouterRouteTableAssociations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTableAssociations) |Query the route table attached to the TR attachment. |
|[DissociateTransitRouterAttachmentFromRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterAttachmentFromRouteTable) |Detach the route table from the TR attachment. |
|[ModifyTransitRouterRouteTableAssociationAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRouteTableAssociationAttributes) |Modify the route table associated with TR attachments. |


<span id=".6Lev55Sx5a2m5Lmg"></span>
## Route learning


|API |Description |
|---|---|
|[DescribeTransitRouterRouteTablePropagations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTablePropagations) |Query route learning that meets specified conditions. |
|[DisableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/DisableTransitRouterRouteTablePropagation) |Delete route learning. |
|[EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation) |Create a route learning rule. |


<span id=".6Lev55Sx562W55Wl"></span>
## Routing policy


|API |Description |
|---|---|
|[CreateTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyTable) |Create a route policy (excluding route policy entries). |
|[CreateTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRoutePolicyEntry) |Add a route policy entry. |
|[DescribeTransitRouterRoutePolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyEntries) |Query route policy entries that meet specified conditions. |
|[DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) |Query route policies that meets the specified condition. |
|[ModifyTransitRouterRoutePolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyEntryAttributes) |Modify a route policy entry. |
|[ModifyTransitRouterRoutePolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyAssociation) |Modifies the attachment relationship of a route policy. |
|[ModifyTransitRouterRoutePolicyTableAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterRoutePolicyTableAttributes) |Modify the name or description of the route policy. |
|[AssociateTransitRouterRoutePolicyToRouteTable](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterRoutePolicyToRouteTable) |Associate the route policy to the TR route table. |
|[DeleteTransitRouterRoutePolicyTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRoutePolicyTable) |Delete a route policy. |
|[DeleteTransitRouterRoutePolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRoutePolicyEntry) |Deleting a route policy entry. |
|[DissociateTransitRouterRoutePolicyTableFromRouteTable](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterRoutePolicyFromRouteTable) |Disassociate the route policy from the TR route table. |


<span id=".6L2s5Y-R562W55Wl"></span>
## Forwarding policy


|API |Description |
|---|---|
|[CreateTransitRouterForwardPolicyTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyTable) |Create a forwarding policy (excluding forwarding policy entries). |
|[CreateTransitRouterForwardPolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterForwardPolicyEntry) |Add a forwarding policy entries to the forwarding policy. |
|[DescribeTransitRouterForwardPolicyEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyEntries) |Query forwarding policy entries that meet specified conditions. |
|[DescribeTransitRouterForwardPolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables) |Query the forwarding policy that meets specified conditions. |
|[ModifyTransitRouterForwardPolicyEntryAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyEntryAttributes) |Modify forwarding policy entries. |
|[ModifyTransitRouterForwardPolicyTableAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyTableAssociation) |Modify the attachment relationship of the forwarding policy. |
|[ModifyTransitRouterForwardPolicyTableAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterForwardPolicyTableAttributes) |Modify the name or description of the forwarding policy. |
|[AssociateTransitRouterForwardPolicyTableToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterForwardPolicyTableToAttachment) |Associate the forwarding policy with the TR attachment (including VPC, VPN, DC Gateway network instance attachments, and Inter\-region attachment). |
|[DeleteTransitRouterForwardPolicyEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterForwardPolicyEntry) |Delete a forwarding policy entry. |
|[DeleteTransitRouterForwardPolicyTable](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterForwardPolicyTable) |Delete a forwarding policy. |
|[DissociateTransitRouterForwardPolicyTableFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterForwardPolicyTableFromAttachment) |Disassociate the forwarding policy from the TR attachment. |


<span id=".5rWB5qCH6K6w562W55Wl"></span>
## Traffic marking policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Traffic marking policy is in Beta. If you need to call the following interface, please contact the account manager.</div>



|API |Description |
|---|---|
|[CreateTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingPolicy) |Create a Traffic marking policy. |
|[DeleteTransitRouterTrafficQosMarkingPolicy](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingPolicy) |Delete Traffic marking policy. |
|[ModifyTransitRouterTrafficQosMarkingPolicyAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosMarkingPolicyAttributes) |Modify the name or description of the Traffic marking policy. |
|[DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) |Query Traffic marking policy that meets specified conditions. |
|[CreateTransitRouterTrafficQosMarkingEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosMarkingEntry) |Add marking rules to a Traffic marking policy. |
|[DeleteTransitRouterTrafficQosMarkingEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosMarkingEntry) |Delete the marking rules in the Traffic marking policy. |
|[DescribeTransitRouterTrafficQosMarkingEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingEntries) |Query the marking rules that meet the specified condition in the Traffic marking policy. |
|[AssociateTransitRouterTrafficQosMarkingPolicyToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterTrafficQosMarkingPolicyToAttachment) |Enable the Traffic marking feature for the TR attachment. |
|[DissociateTransitRouterTrafficQosMarkingPolicyFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterTrafficQosMarkingPolicyFromAttachment) |Disable the stream tagging feature for the TR attachment. |
|[ModifyTransitRouterTrafficQosMarkingPolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosMarkingPolicyAssociation) |Modify the Traffic marking policy associated with the TR attachment. |


<span id=".5rWB6Zif5YiX562W55Wl"></span>
## Traffic queue policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Traffic queue policy is in Beta; if you need to call the following interface, please contact your account manager.</div>



|API |Description |
|---|---|
|[CreateTransitRouterTrafficQosQueuePolicy](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosQueuePolicy) |Create Traffic queue policy. |
|[DeleteTransitRouterTrafficQosQueuePolicy](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueuePolicy) |Delete the Traffic queue policy. |
|[ModifyTransitRouterTrafficQosQueuePolicyAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueuePolicyAttributes) |Modify the name or description of the Traffic queue policy. |
|[DescribeTransitRouterTrafficQosQueuePolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueuePolicies) |Query the traffic queue policies that meets specified conditions. |
|[CreateTransitRouterTrafficQosQueueEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterTrafficQosQueueEntry) |Add queues to the Traffic queue policy. |
|[DeleteTransitRouterTrafficQosQueueEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterTrafficQosQueueEntry) |Delete the queue in the Traffic queue policy. |
|[DescribeTransitRouterTrafficQosQueueEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueueEntries) |Query queues in the Traffic queue policy that meet the specified condition. |
|[AssociateTransitRouterTrafficQosQueuePolicyToAttachment](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterTrafficQosQueuePolicyToAttachment) |Enable the flow queue feature for TR attachments. |
|[DissociateTransitRouterTrafficQosQueuePolicyFromAttachment](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterTrafficQosQueuePolicyFromAttachment) |Disable the flow queue feature for a TR attachment. |
|[ModifyTransitRouterTrafficQosQueuePolicyAssociation](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterTrafficQosQueuePolicyAssociation) |Modify the Traffic queue policy attached to the TR attachment. |


<span id="ivDscTz2"></span>
## Flow logs


|API |Description |
|---|---|
|[CreateTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterFlowLog) |Create a TR flow log. |
|[DescribeTransitRouterFlowLogs](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterFlowLogs) |Query the TR flow log list that meets the specified condition. |
|[ModifyTransitRouterFlowLogAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterFlowLogAttributes) |Modify the name, description, or collection cycle of the TR flow log. |
|[StartTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/StartTransitRouterFlowLog) |Enable TR flow log. |
|[StopTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/StopTransitRouterFlowLog) |Stop TR flow log. |
|[DeleteTransitRouterFlowLog](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterFlowLog) |Delete TR flow log. |


<span id="rpfsmUr9"></span>
## Multicast

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The multicast feature is in Beta. If you need to call the following interface, please contact your account manager.</div>



|API |Description |
|---|---|
|[CreateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastDomain) |Create a multicast domain. |
|[ModifyTransitRouterMulticastDomainAttributes](https://docs.byteplus.com/en/docs/transitrouter/ModifyTransitRouterMulticastDomainAttributes) |Modify the name and description of the multicast domain. |
|[DeleteTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastDomain) |Delete the multicast domain. |
|[DescribeTransitRouterMulticastDomains](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains) |Query multicast domain lists that meet specified conditions. |
|[DescribeTransitRouterMulticastDomainAssociations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomainAssociations) |Query the attachment information of the multicast domain that meets the specified conditions. |
|[AssociateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/AssociateTransitRouterMulticastDomain) |Attach the multicast domain to the specified subnet. |
|[DissociateTransitRouterMulticastDomain](https://docs.byteplus.com/en/docs/transitrouter/DissociateTransitRouterMulticastDomain) |Detach the multicast domain from the specified subnet. |
|[DescribeTransitRouterMulticastGroups](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastGroups) |Query multicast sources and multicast members in the specified multicast domain. |
|[CreateTransitRouterMulticastGroupSource](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastGroupSource) |Add multicast sources to the specified multicast domain. |
|[DeleteTransitRouterMulticastGroupSource](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastGroupSource) |Delete the specified multicast source. |
|[CreateTransitRouterMulticastGroupMember](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterMulticastGroupMember) |Add multicast members to the specified multicast domain. |
|[DeleteTransitRouterMulticastGroupMember](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterMulticastGroupMember) |Delete the specified multicast member. |


<span id=".5qCH562-"></span>
## Tag


|API |Description |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/transitrouter/TagResources) |Adds user tags to TR resources. |
|[UntagResources](https://docs.byteplus.com/en/docs/transitrouter/UntagResources) |Deletes user tags from TR resources. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/transitrouter/ListTagsForResources) |Query tags that meet specified criteria. |
