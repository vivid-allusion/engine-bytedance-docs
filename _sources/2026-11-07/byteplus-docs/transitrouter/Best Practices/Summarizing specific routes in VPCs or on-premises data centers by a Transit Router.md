---
title: "Summarizing specific routes in VPCs or on-premises data centers by a Transit Router"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Summarizing-specific-routes-in-VPCs-or-on-premises-data-centers-by-a-Transit-Router"
---

This topic describes how to configure a Transit Router (TR) to summarize specific routes between Virtual Private Clouds (VPCs) and an on\-premises data center (IDC).

<span id="cXJ3wfdI"></span>
## Scenarios

The TR learns routes at the VPC subnet granularity by default. If the VPC contains many subnet CIDR blocks, the route entries propagated to the on\-premises IDC through the TR will be excessive, potentially causing the following issues:


* A Direct Connect (DC) can receive up to 100 routes from the TR by default. If the number of CIDR blocks exceeds this limit, extra routes will be discarded, affecting traffic forwarding.

* The on\-premises IDC receives many specific routes, complicating route management and maintenance.

* Excessive specific routes may increase route convergence time.


To resolve the above issues, you can summarize specific routes (both cloud and on\-premises) by "TR route table + static route" or "route policy + static route".


|Solution |Summarize by TR route table and static route |Summarize by route policy and static route |
|---|---|---|
|Solution overview |Add a TR route table. Associate the target network instance for forwarding to this new table. Disable route learning on it, and configure a static summary route.​<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c7c7371469dab295293f90e639bcd828.png) </span> |Apply a route policy to deny specific routes, and add the static summary route to the original TR route table.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3af72a35a7acde6ce02d695870005ee2.png) </span> |
|Precautions |* You can summarize only specific routes of the same network instance into one summary route, but not routes of multiple network instances.<br><br>* If your IDC needs to scan unassigned IP addresses in a subnet, to avoid route loops, see [Manage static routes](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05) to configure blackhole routes for all unassigned IP addresses. |\-\- |
|Possible impact |False interruption may occur when switching service traffic from specific routes to a summary route. ||
|Maintenance note |When creating or deleting a subnet, you must manually update the TR route table to add static summary routes. ||


<span id="ScO1ZvqF"></span>
## Prerequisites

You have connected VPCs to the on\-premises IDC through a TR and a DC.

<span id="VCDg3DQx"></span>
## Configuration procedures


<Tabs>
<Tab zoneid="Z0iHG86wAi" title="Summarize by TR route table and static route">
<TabTitle>Summarize by TR route table and static route</TabTitle>

1. [Create a TR route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03): Create a custom TR route table.

2. [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx): Consolidate multiple specific routes into a summary route, and add the static summary route to the new route table.

3. [Modify an association forwarding route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07#.5L-u5pS55YWz6IGU6L2s5Y-R6Lev55Sx6KGo): Modify the association forwarding route table for the DC Gateway attachment to the new route table, propagating the summary route to the on\-premises IDC via the TR.

4. View cloud and on\-premises routes: Verify that routes of the TR, DC Gateway and on\-premises IDC match the expected configuration.


</Tab>
<Tab zoneid="TrjDyyIWIP" title="Summarize by route policy and static route">
<TabTitle>Summarize by route policy and static route</TabTitle>

1. Summarize routes: Identify specific routes to summarize, and consolidate them into a single summary route.

2. [Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx): Add the static summary route to the association forwarding route table for the DC Gateway attachment.

3. [Create a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy): Create an outbound route policy to deny specific VPC routes from being propagated to the DC Gateway.

4. [Associate the route policy with the TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table): To propagate the summary route to the on\-premises IDC via the TR, associate the route policy with the association forwarding route table for the DC Gateway attachment.

5. View cloud and on\-premises routes: Verify that routes of the TR, DC Gateway and on\-premises IDC match the expected configuration.


</Tab>
</Tabs>


<span id="e3da38Xl"></span>
## Summarize by TR route table and static route


1. Create a TR route table named tr01\-rtb\-set. For procedure, see [Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03).

2. Identify specific routes to summarize, and consolidate them into a single summary route. The following example demonstrates this process by summarizing specific VPC routes.

   
   |Route entry of network instance |||Summary route entry |
   |---|---|---|---|
   |Destination CIDR |Next Hop |Network Instances |Destination CIDR |
   |192.168.1.0/24 |attach\-vpc01 |vpc01 |192.168.0.0/20 |
   |192.168.2.0/24 |attach\-vpc01 |vpc01 ||
   |192.168.16.0/24 |attach\-vpc02 |vpc02 |192.168.16.0/20 |
   |192.168.17.0/24 |attach\-vpc02 |vpc02 ||
   

3. Add the summary route to the TR route table (tr01\-rtb\-set). For procedure, see [Creating a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx).

   
   |Destination CIDR |Black hole routing |Next Hop type |Next Hop |
   |---|---|---|---|
   |192.168.0.0/20 |No |Intra\-region attachment |attach\-vpc01 |
   |192.168.16.0/20 |No |Intra\-region attachment |attach\-vpc02 |
   

4. Modify association forwarding route table of the attachment to accept only summary routes. For procedure, see [Modify an association forwarding route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07#.5L-u5pS55YWz6IGU6L2s5Y-R6Lev55Sx6KGo).

   **Using the summarization of specific VPC routes as an example**: Modify the association forwarding route table for the attachment (attach\-dcg01) to the TR route table (tr01\-rtb\-set).

5. Verify that both cloud and on\-premises routes match the expected configuration.

   * **TR routes**: The association forwarding route table for the DC Gateway attachment (attach\-dcg01) contains only static summary routes.

   * **DC Gateway routes**: Learn static summary routes from the TR.

   * **IDC route**: Learn static summary routes of VPCs.


<span id="xS63WFuV"></span>
## Summarize by route policy and static route


1. Identify specific routes to summarize, and consolidate them into a single summary route. The following example demonstrates this process by summarizing specific VPC routes.

   
   |Route entry of network instance |||Summary route |
   |---|---|---|---|
   |Destination CIDR |Next Hop |Network Instances |Destination CIDR |
   |192.168.1.0/24 |attach\-vpc01 |vpc01 |192.168.0.0/20 |
   |192.168.2.0/24 |attach\-vpc01 |vpc01 ||
   |192.168.16.0/24 |attach\-vpc02 |vpc02 |192.168.16.0/20 |
   |192.168.17.0/24 |attach\-vpc02 |vpc02 ||
   

2. Add the static summary route to the association forwarding route table for the DC Gateway attachment. For procedure, see [Creating a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05#.5Yib5bu66Z2Z5oCB6Lev55Sx).

   
   |Destination CIDR |Black hole routing |Next Hop type |Next Hop |
   |---|---|---|---|
   |192.168.0.0/20 |No |Intra\-region attachment |attach\-vpc01 |
   |192.168.16.0/20 |No |Intra\-region attachment |attach\-vpc02 |
   

3. Create an outbound route policy to deny specific VPC routes from being propagated to the DC Gateway. For procedure, see [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When a summary route does not match any route policy, it is allowed by default. Therefore, no new route policy entry is required to allow summary routes to propagate to the DC Gateway.   </div>
   

   
   |Priority |Match conditions |Policy action |
   |---|---|---|
   |100 |Source instance type = VPC<br><br>Destination instance ID = *ID of the DC Gateway instance* |Deny |
   

4. To propagate the summary route to the on\-premises IDC via the TR, associate the route policy with the association forwarding route table for the DC Gateway attachment. For procedure, see [Associating a route policy with a TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table).

5. Verify that both cloud and on\-premises routes match the expected configuration.

   * **TR routes**: The association forwarding route table for the DC Gateway attachment (attach\-dcg01) contains both specific VPC routes and static summary routes.

   * **DC Gateway routes**: Learn static summary routes from the TR.

   * **IDC routes**: Learn static summary routes of VPCs.


&nbsp;
