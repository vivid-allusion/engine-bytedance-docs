---
title: "Publishing/withdrawing routes in CEN"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Publishing-or-canceling-a-route-for-a-CEN"
---

## Scenarios

### Handle network conflicts

If multiple VPC subnet CIDR blocks loaded to the CEN have conflicts, the route added first to the CEN by default becomes effective. When you need a later\-added route to take effect, you can withdraw the route entry previously added for the conflicting subnet in the VPC.

As shown below, the CIDR blocks of Subnet\-A1 and Subnet\-B1 conflict. When resources in Subnet\-C need to communicate with resources in Subnet\-B1, you can withdraw the route entry published by VPC\-A with the destination CIDR of Subnet\-A1. After withdrawal, the route entry published by VPC\-B with the destination CIDR of Subnet\-B1 takes effect.

> **tip**

> If resources in Subnet\-C later need to communicate with resources in Subnet\-A1, you can withdraw the route entry with the destination CIDR of Subnet\-B1 and re\-publish the route entry with the destination CIDR of Subnet\-A1.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ef1045645ac847ae3175657170f44aa.png)

### Multiple VPCs Share Resources

You can publish the route entry with the next hop being the Elastic Compute Service (ECS), HAVip, or Internet NAT gateway to the CEN to enable multiple VPCs to share the next hop resource.

As shown below, publish the route entry with the destination CIDR block 0.0.0.0/0 and the next hop as the Internet NAT Gateway from VPC\-B’s route table to the CEN. A route with the destination CIDR block 0.0.0.0/0 and the next hop as the CEN is automatically added to VPC\-A's route table. In this scenario, ECSs in VPC\-A can leverage the public NAT gateway in VPC\-B to access the internet. For more details, see [Using CEN to enable multiple VPCs to share a Public NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-VPCs-to-share-an-Internet-NAT-Gateway-using-CEN).

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4ead5d46b285a0fb7d201ece54fe635d.png)

## Action description

After a VPC is attached to the Cloud Enterprise Network (CEN), it can publish routes from its system route table to the CEN. This informs other network instances (such as VPCs) already attached to the CEN that they can use these routes to access resources within this VPC. The details of VPC route publication are shown in the table below:

|VPC system route table |Route entry |Publish by default |Support Manual Publication/Withdrawal |Explanation |
|---|---|---|---|---|
|System route |The destination CIDR is a subnet segment |Yes |Yes |For other network instances attached to the CEN, traffic matching this route will be routed to the current VPC's subnet, enabling access to resources within that subnet |
|Custom route |Next hop is ECS |No |Yes |For other network instances, traffic matching this route will be routed to that ECS to access the application deployed on it |
||Next Hop is HAVIP |||For other network instances, traffic matching this route will be routed to that High\-Availability Virtual IP (HAVIP) to access the application deployed on the associated ECS(s) |
||Next Hop is public NAT gateway |||For other network instances, traffic matching this route will be routed to the public NAT gateway, leveraging it to share access to the internet or to provide services to the internet. |

## Publish Route Entries to CEN

### Limitations

When the number of routes in the CEN reaches its quota limit, VPC routes will no longer be advertised to the CEN. Please redesign your network architecture. For more route publishing limits, see [Route overview](https://docs.byteplus.com/en/docs/cen/Route-entries-01).

> **warning**

> After the route is published, it will be added to the route table of the joined network instance.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click the name of target system route table.

5. Select the **Route Entry \> Custom route** tab, or the **Route Entry \> System route** tab.

6. Click **Publish** in the **CEN Publish Status** column of the target route entry.

7. Click **Publish** to complete the action.

## Withdraw route entry from CEN

You can also manually withdraw routes in the CEN console. For specific operations, see [Withdrawing a route](https://docs.byteplus.com/en/docs/cen/Route-entries-04).

> **warning**

> Please note that after withdrawal, existing connections forwarded by this route will be terminated immediately. Proceed with caution.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click the name of target system route table.

5. Select the **Route Entry \> Custom route** tab, or the **Route Entry \> System route** tab.

6. Click **Withdraw** in the **CEN Publish Status** column of the target route entry.

7. Click **Withdraw** to complete the actions.

## Related documents

* [PublishCenRouteEntry](https://docs.byteplus.com/en/docs/cen/PublishCenRouteEntry)

* [WithdrawCenRouteEntry](https://docs.byteplus.com/en/docs/cen/WithdrawCenRouteEntry)
