---
title: "API overview"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Direct-Connect-API-overview"
---

This document introduces the APIs and their features related to using the Direct Connect.

<span id=".54mp55CG5LiT57q_"></span>
## DC Connection


|API |Functionality |
|---|---|
|[CreateDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnection) |Create a dedicated DC Connection. |
|[CreateDirectConnectConnectionOrder](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectConnectionOrder) |Create payment order. |
|[DescribeDirectConnectAccessPoints](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectAccessPoints) |Query Direct Connect access point information. |
|[DescribeDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionAttributes) |Query detailed information of a single DC Connection. |
|[DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) |Query the list of DC Connections that meet the condition. |
|[ModifyDirectConnectConnectionAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectConnectionAttributes) |Modify the name and description of the DC Connection. |
|[DeleteDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectConnection) |Delete the specified DC Connection. |
|[RenewDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/RenewDirectConnectConnection) |Renewal for the specified DC Connection. |
|[SetDirectConnectConnectionRenewal](https://docs.byteplus.com/en/docs/directconnect/SetDirectConnectConnectionRenewal) |Modify the renewal method of the DC Connection. |
|[DescribeDirectConnectConnectionBilling](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionBilling) |Query the billing information of the DC Connection. |
|[ApplyDirectConnectConnectionLoa](https://docs.byteplus.com/en/docs/directconnect/ApplyDirectConnectConnectionLoa) |Submit Direct Connect LOA application. |
|[ModifyDirectConnectConnectionLoaAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectConnectionLoaAttributes) |Modify Direct Connect LOA application. |
|[DescribeDirectConnectConnectionLoaAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionLoaAttributes) |View detailed information about the specified Direct Connect LOA. |


<span id=".5YWx5Lqr5LiT57q_"></span>
## Shared Direct Connect connection


|API |Functionality |
|---|---|
|[CreateSharedDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/CreateSharedDirectConnectConnection) |Operators Account create a shared DC connection for the specified tenant Account. |
|[ConfirmDirectConnectConnection](https://docs.byteplus.com/en/docs/directconnect/ConfirmDirectConnectConnection) |The tenant Account accepts a shared DC connection. |
|[DescribeSharedDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeSharedDirectConnectConnections) |Query detailed information about the shared DC connection based on conditions. |


<span id=".5LiT57q_572R5YWz"></span>
## Direct Connect gateway


|API |Functionality |
|---|---|
|[CreateDirectConnectGateway](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGateway) |Create a new Direct Connect Gateway. |
|[DeleteDirectConnectGateway](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGateway) |Delete the specified Direct Connect Gateway. |
|[ModifyDirectConnectGatewayAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectGatewayAttributes) |Modify the name and Description of the Direct Connect Gateway. |
|[DescribeDirectConnectGatewayAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayAttributes) |Query the detailed information of the specified Direct Connect Gateway. |
|[DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) |Query the list of Direct Connect Gateways that meet the condition. |


<span id=".6Jma5ouf5o6l5Y-j"></span>
## Direct Connect virtual interface


|API |Functionality |
|---|---|
|[CreateDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectVirtualInterface) |Create a new virtual interface. |
|[DeleteDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectVirtualInterface) |Delete the specified virtual interface. |
|[ModifyDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectVirtualInterfaceAttributes) |Modify the name and description of the virtual interface. |
|[DescribeDirectConnectVirtualInterfaceAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaceAttributes) |Query the details of a specified virtual interface. |
|[DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) |Query the list of virtual interfaces that meet the conditions. |


<span id=".5YWx5Lqr6Jma5ouf5o6l5Y-j"></span>
## Shared virtual interface

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current shared virtual interface feature is in Beta. If you need a trial, please contact your account manager. Please log in to the opened Account to view the relevant API Documentation after enabling the trial. You will not be able to view it without enabling the trial.</div>



|API |Functionality |
|---|---|
|[AllocateDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/AllocateDirectConnectVirtualInterface) |Create a new shared virtual interface. |
|[ConfirmDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/ConfirmDirectConnectVirtualInterface) |Accept the shared virtual interface. |


<span id=".QkdQ6YK75bGF"></span>
## BGP Peer


|API |Functionality |
|---|---|
|[CreateBgpPeer](https://docs.byteplus.com/en/docs/directconnect/CreateBgpPeer) |Create a BGP Peer. |
|[DeleteBgpPeer](https://docs.byteplus.com/en/docs/directconnect/DeleteBgpPeer) |Delete the specified BGP Peer. |
|[ModifyBgpPeerAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyBgpPeerAttributes) |Modify the name and Description of the BGP Peer. |
|[DescribeBgpPeerAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeerAttributes) |Query the specified BGP Peer. |
|[DescribeBgpPeers](https://docs.byteplus.com/en/docs/directconnect/DescribeBgpPeers) |Query the list of BGP Peers that meet the condition. |


<span id=".5LiT57q_572R5YWz6Lev55Sx"></span>
## Direct Connect Gateway Route


|API |Functionality |
|---|---|
|[CreateDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGatewayRoute) |Add a static route entry to the specified Direct Connect Gateway. |
|[DeleteDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGatewayRoute) |Deletes a specified static route entry. |
|[DescribeDirectConnectGatewayRouteAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRouteAttributes) |Query detailed information of a specified static route entry. |
|[DescribeDirectConnectGatewayRoutes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRoutes) |Query the list of static route entries that meet the conditions. |


<span id=".UW9T562W55Wl"></span>
## QoS policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Direct Connect QoS policy feature is in Beta. Please contact your account manager for a trial. Please log in to the activated Account after starting the trial to view the related API Documentation. You cannot view it without starting the trial.</div>



|API |Functionality |
|---|---|
|[CreateDirectConnectTrafficQosPolicy](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosPolicy) |Create a QoS policy. |
|[DeleteDirectConnectTrafficQosPolicy](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosPolicy) |Delete specified Qos policy. |
|[ModifyDirectConnectTrafficQosPolicyAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosPolicyAttributes) |Modify information of a specified Qos policy. |
|[DescribeDirectConnectTrafficQosPolicies](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies) |Query Qos policies that meet the conditions. |
|[CreateDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosQueue) |Add flow queue for specified Qos policy. |
|[DeleteDirectConnectTrafficQosQueue](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosQueue) |Delete the specified flow queue. |
|[ModifyDirectConnectTrafficQosQueueAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosQueueAttributes) |Modify the information of the specified traffic queue. |
|[DescribeDirectConnectTrafficQosQueues](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues) |Query flow queue that meets the conditions. |
|[CreateDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosRule) |Add qos queue rules for the specified flow queue. |
|[DeleteDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosRule) |Delete the specified flow queue rule. |
|[ModifyDirectConnectTrafficQosRuleAttributes](https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosRuleAttributes) |Modify the configuration information of the specified flow queue rule. |
|[DescribeDirectConnectTrafficQosRules](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosRules) |Query traffic queue rules that meet the conditions. |
