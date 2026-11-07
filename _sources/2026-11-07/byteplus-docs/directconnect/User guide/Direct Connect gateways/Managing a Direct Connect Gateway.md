---
title: "Managing a Direct Connect Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Managing_Direct_Connect_Gateways"
---

<span id=".5p-l55yL5L-h5oGv"></span>
## View information


<Tabs>
<Tab zoneid="zMtSHzogUq" title="Associated DC Virtual Interface of DC Gateway">
<TabTitle>Associated DC Virtual Interface of DC Gateway</TabTitle>

1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target Region.

3. Click the name of the DC Gateway that you want to view.

4. Click the **DC Virtual Interface** tab to view the list of virtual interfaces associated with the current DC Gateway.

5. In the virtual interface list, click the name of the target Virtual Interface to view its details. This includes the name, status, account, VLAN ID, and other information of the Virtual Interface.


</Tab>
<Tab zoneid="rQVj9FOKOv" title="BGP Peer of DC Gateway">
<TabTitle>BGP Peer of DC Gateway</TabTitle>

1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. Click the name of the DC Gateway that you want to view.

4. Click the **BGP Peer** tab to view detailed information about the BGP Peer of the Virtual Interface currently associated with the DC Gateway. This includes BGP Peer IP, Local IP, Session state, Peer ASN, BGP key, and other information.


</Tab>
<Tab zoneid="PfwkKTcO4y" title="DC Gateway route">
<TabTitle>DC Gateway route</TabTitle>

1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. Click the name of the DC Gateway that you want to view.

4. Click the **Route information** tab to view routes of the current DC Gateway.

   
   |Destination CIDR |Next Hop type |Next Hop |Route type |
   |---|---|---|---|
   |* CIDR blocks of the on\-premises data center to be accessed<br><br>* Subnets of the Virtual Private Cloud (VPC)<br><br>* CIDR blocks of the Elastic Compute Service (ECS) |* Direct Connect Virtual Interface<br><br>* Cloud Enterprise Network<br><br>* Edge Interconnect (EIC)<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The Edge Interconnect (EIC) feature is in the beta stage. If you need a trial, please contact your account manager.</div><br> |Instance name for Next Hop |Route types:<br><br><br>* Static: Manually added static route entries<br><br>* BGP: BGP route entries automatically learned from the on\-premises BGP Peer<br><br>* CEN: Route entries that are automatically learned from the Cloud Enterprise Network (CEN) associated with the DC Gateway<br><br>* EIC: Route entries that are automatically learned from Edge Interconnect (EIC) associated with the DC Gateway<br><br>* TR: Route entries learned from the Transit Router (TR) associated with the DC Gateway |
   

5. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7d405b9f63f348db8b636e68594c475c.png) </span>icom to the right of the interface.

6. Specify the content and scope to export.

7. Click **OK** to download the route information of this DC Gateway in CSV format.


</Tab>
<Tab zoneid="yC5vNUKlXG" title="Monitoring information">
<TabTitle>Monitoring information</TabTitle>

The DC Gateway has integrated with CloudMonitor, supporting real\-time monitoring of all business metrics for the DC Gateway.


* For more about monitoring metrics, see [Direct Connect Gateway monitoring metrics](https://console.byteplus.com/cloud_monitor/docs?namespace=VCM_DirectConnectGateway).

* For methods to view monitoring data, see [Viewing monitoring data](https://docs.byteplus.com/en/docs/directconnect/Viewing-the-indicator-monitoring-data).


</Tab>
</Tabs>


<span id=".5Yig6Zmk6YWN572u"></span>
## Delete a configuration


<Tabs>
<Tab zoneid="d8XgSXhsHH" title="Delete BGP peer">
<TabTitle>Delete BGP peer</TabTitle>

You can delete BGP Peers that are no longer required.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting a BGP Peer may interrupt traffic on the Virtual Interface where that BGP Peer exists. Fully assess the potential impact on your services before proceeding.</div>



1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target Region.

3. Click the name of the target DC Gateway.

4. Click the **BGP Peer** tab. In the BGP Peer list, find the BGP Peer to be deleted.

5. Click **Delete** in the **Actions** column of the target BGP Peer.

6. Click **Delete** to complete the action.


</Tab>
<Tab zoneid="Z13RdBO5QG" title="Delete static route">
<TabTitle>Delete static route</TabTitle>

You can delete static route entries that are no longer in use. Entries of **System routes** and **BGP** routes cannot be deleted.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting static routes will disrupt network connectivity between the on\-premises data center and the DC Gateway, which may affect running services. Proceed with caution.</div>



1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target Region.

3. Click the name of the target DC Gateway.

4. Click the **Route Information** tab. In the route list, find the static route to be deleted.

5. Click **Delete** in the **Actions** column of the target static route.

6. Click **Delete** to complete the action.


</Tab>
<Tab zoneid="q5MiZ5Zkbk" title="Delete DC Gateway">
<TabTitle>Delete DC Gateway</TabTitle>

<span id="1cYps48h"></span>
### Prerequisites

Before deleting a DC Gateway, ensure the gateway meets the following conditions:


|Association |Procedure |
|---|---|
|Not belong to any CEN |[Revoke cross-account authorization for CEN](https://docs.byteplus.com/en/docs/directconnect/Cross-account-authorization#.6Kej6Zmk6Leo6LSm5Y-35o6I5p2D) |
|No associated EIC |[Revoke cross-account authorization for EIC](https://docs.byteplus.com/en/docs/6407/1847916#0SoUgsR3) |
|No static routes |[Delete static route](https://docs.byteplus.com/en/docs/53/44862#.5Yig6Zmk6YWN572u) |
|No BGP Peer |[Delete BGP peer](https://docs.byteplus.com/en/docs/53/44862#.5Yig6Zmk6YWN572u) |
|No associated Virtual Interfaces |[Delete a Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Deleting-the-virtual-interface) |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once deleted, the DC Gateway cannot be restored. Confirm that this action will not affect your business operations and proceed with caution.</div>



1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. In the DC Gateway list, click **Delete** to the right of the DC Gateway to be deleted.

4. Click **Delete** to complete the action.


</Tab>
</Tabs>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [DescribeDirectConnectGatewayAttributes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayAttributes): Query the details of a specified DC Gateway.

* [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways): Query the details of DC Gateways that meet the conditions.

* [DeleteBgpPeer](https://docs.byteplus.com/en/docs/directconnect/DeleteBgpPeer): Delete a specified BGP Peer.

* [DeleteDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGatewayRoute): Delete a specified static route of a DC Gateway.

* [DeleteDirectConnectGateway](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGateway): Delete a specified DC Gateway.
