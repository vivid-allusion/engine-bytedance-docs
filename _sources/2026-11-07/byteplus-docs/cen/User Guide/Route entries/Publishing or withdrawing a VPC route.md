---
title: "Publishing or withdrawing a VPC route"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-04"
---

<span id=".6Lev55Sx57G75Z6L"></span>
## Route type

After a VPC is attached to the Cloud Enterprise Network (CEN), it can publish routes from its system route table to the CEN. This informs other network instances (such as VPCs) already attached to the CEN that they can use these routes to access resources within this VPC. The details of VPC route publication are shown in the table below:


|VPC system route table |Route entry |Publish by default |Support Manual Publication/Withdrawal |Explanation |
|---|---|---|---|---|
|System route |The destination CIDR is a subnet segment |Yes |Yes |For other network instances attached to the CEN, traffic matching this route will be routed to the current VPC's subnet, enabling access to resources within that subnet |
|Custom route |Next hop is ECS |No |Yes |For other network instances, traffic matching this route will be routed to that ECS to access the application deployed on it |
||Next Hop is HAVIP |||For other network instances, traffic matching this route will be routed to that High\-Availability Virtual IP (HAVIP) to access the application deployed on the associated ECS(s) |
||Next Hop is public NAT gateway |||For other network instances, traffic matching this route will be routed to the public NAT gateway, leveraging it to share access to the internet or to provide services to the internet. |


<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

<span id=".5aSE55CG572R57uc5Yay56qB"></span>
#### Handle network conflicts

If multiple VPC subnet CIDR blocks loaded to the CEN have conflicts, the route added first to the CEN by default becomes effective. When you need a later\-added route to take effect, you can withdraw the route entry previously added for the conflicting subnet in the VPC.

For example, in the scenario below, Subnet\-A1 and Subnet\-B1 have conflicting CIDR blocks. When resources in Subnet\-C need to communicate with resources in Subnet\-B1, you can withdraw the route entry published by VPC\-A with the destination CIDR of Subnet\-A1. After withdrawal, the route entry published by VPC\-B with the destination CIDR of Subnet\-B1 will take effect.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If resources in Subnet\-C later need to communicate with resources in Subnet\-A1, you can withdraw the route entry with the destination CIDR of Subnet\-B1 and re\-publish the route entry with the destination CIDR of Subnet\-A1.</div>


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e186ad30094a959456478041f0633798.png) </span>

<span id=".5aSa5LiqVlBD5YWx5Lqr6LWE5rqQ"></span>
#### Multiple VPCs Share Resources

You can publish the route entry with the next hop being the Elastic Compute Service (ECS), HAVIP, or Internet NAT gateway to the CEN to enable multiple VPCs to share the next hop resource.

For example, as shown below, publish the route entry in VPC\-B's route table with the destination CIDR block set to 0.0.0.0/0 and the next hop as the Internet NAT gateway to the CEN. A route with a destination CIDR block of 0.0.0.0/0 and the next hop as the CEN is automatically added to VPC\-A's route table. In this scenario, ECSs in VPC\-A can leverage the public NAT gateway in VPC\-B to access the internet. For more details, see [Using the CEN to enable multiple VPCs to share the Internet NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-VPCs-to-share-an-Internet-NAT-Gateway-using-CEN).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3e38063ff7bf60c3c4c025ceaed97f26.png) </span>

<span id=".5Y-R5biD6Lev55Sx5p2h55uu5Yiw5LqR5LyB5Lia572R"></span>
## Publish Route Entries to CEN

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limitations

When the number of routes in the CEN reaches its quota limit, VPC routes will no longer be published to the CEN. Please redesign your network architecture. For more routing publication limits, see [Route overview](https://docs.byteplus.com/en/docs/cen/Route-entries-01).

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click the name of target system route table.

5. Select the **Route Entry \> Custom route** tab, or the **Route Entry \> System route** tab.

6. Click **Publish** in the **CEN Publish Status** column of the target route entry.

7. Click **Publish** to complete the publication.


<span id=".5LuO5LqR5LyB5Lia572R5pKk5Zue6Lev55Sx5p2h55uu"></span>
## Withdraw route entry from CEN


<Tabs>
<Tab zoneid="oOEJJ2Kx2H" title="CEN console">
<TabTitle>CEN console</TabTitle>

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the top navigation bar, select the target project.

3. Click the target CEN instance name.

4. In the **Route Table** tab, click **Withdraw** on the right side of the target route.

5. Click **Withdraw** to complete the actions.


</Tab>
<Tab zoneid="JGhuVWjNDY" title="VPC console">
<TabTitle>VPC console</TabTitle>

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click the name of target system route table.

5. Select the **Route Entry \> Custom route** tab, or the **Route Entry \> System route** tab.

6. Click **Withdraw** in the **CEN Publish Status** column of the target route entry.

7. Click **Withdraw** to complete the withdrawal.


</Tab>
</Tabs>
