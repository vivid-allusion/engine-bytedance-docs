---
title: "Line operator guide"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Operator-operation-guide"
---

This topic guides line operators on how to create a Shared Line for a tenant and how to manage created Shared Lines.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* The line operator must complete the line construction from the operator access point to the BytePlus access point in advance.

* The line operator must submit a ticket to BytePlus in advance to apply for the feature of creating Shared Line.

* After the line operator creates a Shared Line for a tenant, the line belongs to the tenant account. The line operator account can only create Shared Line for tenants and cannot create DC gateways or use related features for itself.

* In Shared Line mode, the port fee for the Direct Connect (DC) Connection is not paid by the line operator, but by the tenant who accepts and uses the Shared Line.

* The line operator pre\-assigns VLAN IDs for the tenant to isolate resources and ensures unique VLAN IDs for multiple Shared Lines under the same DC Connection.

* The line operator should reasonably allocate bandwidth for the tenant, ensuring the total bandwidth of multiple Shared Lines under the same DC Connection does not exceed the connection's bandwidth.

* The line operator must specify the bandwidth specification and VLAN ID when creating a Shared Line.

   * If a tenant requires modifying the bandwidth, it must apply to its line operator. After the line operator initiates the bandwidth modification, the tenant can modify the bandwidth in the console.

   * If a tenant requires modifying the VLAN ID, creating and configuring a new Shared Line is the only solution.

* In a scenario where the line operator only has one tenant to use a Shared Line, if the tenant needs to use the QoS policy feature, the operator must contact the account manager to apply for activation. After activation, only the marking feature is available, while the queue feature does not take effect.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the Shared Line created for the tenant shares bandwidth with the operator’s DC Virtual Interface, allocate bandwidth in advance to avoid contention.</div>


<span id=".5Li656ef5oi35Yib5bu65YWx5Lqr5LiT57q_"></span>
## Create a Shared Line for a tenant

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* You have created an exclusive DC Connection, and enabled the capability to create a Shared Line. For details, see [Creating a Dedicated Line](https://docs.byteplus.com/en/docs/directconnect/Accessing-a-Direct-Connect-connection-1).

* You have completed the networking and construction from the tenant's data center to your Direct Connect location.

* You have obtained the BytePlus account ID and required bandwidth of the tenant who will accept the Shared Line.

* You have confirmed that the VLAN ID planned for the tenant’s Shared Line is not occupied.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Use a line operator account to log in to the BytePlus [Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target project and region.

3. Click the name of the DC connection to be shared.

4. Click the **Shared Line** tab, and then click **Create Shared Line**.

5. In the pop\-up **Create Shared Line** dialog box, configure the shared DC connection.

   
   |Parameter |Explanation |Value |
   |---|---|---|
   |Name |Set the name of the Shared Line. |DCC\-tenants05 |
   |Owner account ID |The BytePlus account ID of the tenant who will accept the Shared Line. |210\*\*\*\*400 |
   |VLAN ID |The VLAN ID assigned to the Shared Line.<br><br><br>* You must assign a unique VLAN ID to each Shared Line under the same DC Connection. Ensure this VLAN ID is not occupied.<br><br>* The VLAN ID range for the Shared Line is **1–2999**. This means the DC Connection's switch port operates in Layer 3 sub\-interface mode. Each sub\-interface has a unique VLAN ID mapped to a separate DC Virtual Interface. This mode supports multiple DC Virtual Interfaces per DC Connection. |28 |
   |Bandwidth cap |select the maximum bandwidth for the Shared Line.<br><br>The total bandwidth of all shared DC connections under the same DC Connection cannot exceed the bandwidth of the DC Connection. |100 Mbps |
   

6. Click **Create** to complete creation.

   * Line operator account: In the **Shared Line** tab of the DC Connection details page, display a new Shared Line whose status is **Pending acceptance**, and contact the tenant to accept the Shared Line.

   * Tenant account: In the list on the **Direct Connect Connection** page, display a new Shared Line whose status is **Pending acceptance**.


<span id=".5Li656ef5oi35Y-Y6YWN5YWx5Lqr5LiT57q_"></span>
## Modify line specification for a tenant

You can modify the port bandwidth of a Shared Line for a tenant based on its requirements. For procedure, see [Modifying specifications](https://docs.byteplus.com/en/docs/directconnect/Modification-of-instance-specification).

<span id=".5Yig6Zmk5YWx5Lqr5LiT57q_"></span>
## Delete a Shared Line

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

As a line operator, you can delete Shared Lines that are created but not yet accepted by tenants, or Shared Lines that are accepted but subsequently released by tenant​s. Deletion is irreversible. Proceed with caution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Only a main account can delete Shared Lines created for tenants. IAM users (including IAM users with global permissions) cannot delete them.</div>


* <div data-tips="true" data-tips-type="tip">After deleting a Shared Line, dependent configurations will be deleted accordingly and are unrecoverable.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Use a line operator account to log in to the BytePlus [Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target project and region.

3. In the DC Connection list, click the name of the Dedicated Line to which the target Shared Line belongs.

4. Click the **Shared Line** tab, and click **Delete** in the **Actions** column of the target Shared Line in the Shared Line list.

5. In the pop\-up dialog box, confirm the information is correct, and click **Delete** to complete the action.


<span id=".5Yig6Zmk54mp55CG5LiT57q_"></span>
## Delete a DC Connection

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


* You can directly delete DC Connections whose port occupancy fees are unpaid.

* For DC Connections whose port occupancy fees are paid, you can delete expired ones. Currently, you cannot delete unexpired DC Connections.

* The DC Connection to be deleted must not have any attached DC Virtual Interfaces. If have, delete the attached DC Virtual Interfaces first. For procedure, see [Deleting a Direct Connect Virtual Interface](https://docs.byteplus.com/en/docs/directconnect/Deleting-the-virtual-interface).

* The Dedicated Line to be deleted does not have any created Shared Lines. If have, delete all Shared Lines first, and then delete the Dedicated Line.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After deleting a DC Connection, dependent configurations will be deleted accordingly and are unrecoverable. Proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Use a line operator account to log in to the BytePlus [Direct Connect Connection console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select the target project and region.

3. In the DC Connection list, click **Delete** in the **Actions** column of the target Dedicated Line.

4. In the pop\-up dialog box, confirm the information is correct, and click **Delete** to complete the action.
