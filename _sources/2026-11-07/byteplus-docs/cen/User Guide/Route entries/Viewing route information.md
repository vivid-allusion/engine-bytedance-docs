---
title: "Viewing route information"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-02"
---

Cloud Enterprise Network (CEN) and network instances can learn routes from each other. After completing operations in the CEN console (such as configuring cloud service access or attaching/detaching network instances), you can view corresponding route information. You can do this via the CEN route table, the VPC route table, or the Direct Connect Gateway Route Table.


* Routes in the CEN Route Table: Enable connectivity between network instances and the CEN.

* Routes in the VPC Route Table: Routes learned from the CEN, enabling network connectivity between this VPC and other VPCs or the Direct Connect Gateway.

* Routes in the Direct Connect Gateway Route Table: Routes learned from the CEN, enabling private network connectivity between the Direct Connect Gateway and VPCs. For specific usage of the Direct Connect Gateway, see [Direct Connect Quick start](https://docs.byteplus.com/en/docs/directconnect/Quick-start).


<span id=".5Zyo5LqR5LyB5Lia572R5o6n5Yi25Y-w5p-l55yL6Lev55Sx5L-h5oGv"></span>
## View route information via CEN console


1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. Select the **Route Table** tab to enter the route list page.

   * You can view the full set of routes in the target CEN instance or apply filters to find specific routes that meet your criteria. If there are many route entries, you can use fuzzy search by Instance ID or Destination CIDR to filter for the desired routes.

   * Click the download icon on the right side of the search box, and then click **OK** to convert the route information locally for viewing and management.

   The descriptions of each field in the route information are provided in the table below.

   
   |Field |Explanation |
   |---|---|
   |Destination CIDR |The CIDR block of the network instance or the cloud service address.<br><br><br>* VPC: Each subnet publishes one route entry. The destination CIDR block is the CIDR block of that subnet within the VPC.<br><br>* Direct Connect Gateway: The destination CIDR block is the network segment of the on\-premises IDC.<br><br>* Cloud Service Address: The destination CIDR block is the address or address range configured in the [Cloud Service access configuration](https://docs.byteplus.com/en/docs/cen/Route-entries-for-access-to-cloud-services-01). |
   |Status |Indicates the status of a route entry, which can be Available or Conflicted.<br><br><br>* Available: Indicates that the route has been published to the route table and is functioning normally.<br><br>* Conflicting: Indicates that the route has been published to the route table but conflicts with other route entries, rendering it unavailable. |
   |Source Instances |The ID of the network instance, i.e., the ID of the VPC or Direct Connect Gateway to which the destination CIDR belongs. If the instance belongs to the same account as the CEN instance, clicking the instance name will redirect to its details page. For manually configured cloud service route entries, there is no source instance involved, and this field displays as "\-". |
   |Route Type |The route entry types in CEN are classified as CEN and Custom.<br><br><br>* CEN: Indicates that the route was learned from a network instance.<br><br>* Custom: Indicates that the route is a cloud service route configured within the CEN. |
   |Route attribute |Routing property refers to the as\-path information of the Direct Connect Gateway's BGP route.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not applicable (displayed as "\-") when the source instance type is VPC, or when the source instance type is Direct Connect Gateway with a static route.</div><br> |
   |Next Hop region |The region to which the network instance or cloud service belongs. |
   


<span id=".5Zyo56eB5pyJ572R57uc6Lev55Sx6KGo5Lit5p-l55yL5LqR5LyB5Lia572R6Lev55Sx"></span>
## View CEN routes via VPC route table

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To view CEN route entries in a VPC route table, you must obtain the VPC ID from the Network instances tab of the CEN instance details page.</div>



1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Search for the route table associated with the VPC based on the VPC ID, and click the route table name.

5. On the route table details page, select the **Route Entry** tab.

6. Click the **System route** tab to view route information where the next hop Type is CEN.

   
   |Destination CIDR |Next Hop type |Next Hop |CEN Publish Status |
   |---|---|---|---|
   |The destination CIDR block can be the subnet CIDR of other VPCs attached to the CEN instance, a custom route, or the on\-premises IDC network segment connected via the Direct Connect Gateway. |All are CEN: Indicates that the route was automatically learned and published by the CEN. |Name of the CEN instance |All are "\-" |
   


<span id=".5Zyo5LiT57q_572R5YWz6Lev55Sx5L-h5oGv5Lit5p-l55yL5LqR5LyB5Lia572R6Lev55Sx"></span>
## View CEN routes via Direct Connect Gateway route information

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To view CEN route entries in on a Direct Connect gateway, you must obtain the ID of the Direct Connect gateway from the Network instances tab of the CEN instance details page.</div>



1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target Region.

3. On the Direct Connect Gateway page, search by the Direct Connect Gateway ID and click the name of the target gateway.

4. On the details page, click the Routing information tab to view the route entries.

   
   |Destination CIDR |Next Hop type |Next Hop |Route type |
   |---|---|---|---|
   |The destination CIDR block is the subnet CIDR of a VPC attached to the CEN or the cloud service address range configured in the CEN. |CEN: Indicates that the route was automatically learned and published by the CEN. |Name of the CEN instance |This is a CEN, indicating that the route is learned from the CEN. |
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DescribeCenRouteEntries](https://docs.byteplus.com/en/docs/cen/DescribeCenRouteEntries)
