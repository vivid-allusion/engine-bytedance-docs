---
title: "Route overview"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Route-entries-01"
---

## Concept introduction

|Term |Notes |
|---|---|
|LPM principle |Longest Prefix Match (LPM) principle. When multiple routes in the route table match the destination IP address, the route with the longest subnet mask (most specific prefix) is matched first. |
|BGP route |Direct Connect supports real\-time awareness of route changes on the IDC side through the automatic convergence capability of the BGP routing protocol, and updates the IDC routes learned on the cloud side. CEN instance learns the updated IDC routes from the DC instance by attaching the DC gateway. |
|ECMP route |Equal\-cost multi\-path (ECMP) route. In the following two scenarios, when a DC gateway is attached to CEN the CEN route table will form ECMP routes:<br><br><br>* BGP routes from multiple DC Gateways in the same region have the same CIDR block and the same as\-path length.<br><br>* Static routes with the same destination CIDR block are configured on multiple DC Gateways in the same region. |

## Route type

Cloud Enterprise Network (CEN) can automatically learn route entries from network instances. The sources, application scenarios, and publishing status of route entries in CEN are shown in the table below.

|Route source |Route information |Scenarios |Auto publish |Support manual publication/withdrawal |
|---|---|---|---|---|
|VPC |System route entries in the VPC system route table where the destination CIDR is a subnet CIDR |Different VPCs attached to the CEN can achieve private network connectivity via this route |Yes |Yes |
||Custom route entries in the VPC system route table where the next hop type is ECS |Applications deployed on an ECS instance can be accessed by other VPCs or DC Gateways attached to the CEN for connecting to the Internet or other services |No |Yes |
||Custom route entries in the VPC system route table where the next hop type is HaVip |Traffic from other VPCs or DC Gateways attached to the CEN, destined for this CIDR block, can be forwarded to this High Availability Virtual IP (HaVip) |No |Yes |
||Custom route entries in the VPC system route table where the next hop type is NAT Gateway |Other VPCs or DC Gateways attached to the CEN can connect to the Internet via the NAT Gateway |No |Yes |
|DC Gateway |DC Gateway route entries (including both static and BGP route entries) |The on\-premises network connected via a DC Gateway attached to the CEN can achieve private network connectivity with the cloud network via this route |Yes |No |
|CEN |Manually configured route entries for accessing cloud services |The on\-premises network connected via a DC Gateway attached to the CEN can access cloud public services via this route |Yes |No |

> **tip**

* > For route entries in the above table that support manual publishing/withdrawal, if they need to be synchronized to the CEN route table, they must be manually published in the Virtual Private Cloud (VPC) console. The CEN console only supports withdrawal. For detailed publishing steps, see [Publish route entries to CEN](https://docs.byteplus.com/en/docs/vpc/Publishing-or-canceling-a-route-for-a-CEN#.5Y-R5biD6Lev55Sx5p2h55uu5Yiw5LqR5LyB5Lia572R).

* > The table above lists the routes that can be manually published or withdrawn. The destination CIDR blocks of these routes must not fall within the following ranges:​

   * > IPv4 CIDR block

      * > Loopback address `127.0.0.0/8~32`

      * > Multicast address `224.0.0.0/4~32`

      * > Reserved address `240.0.0.0/4~32`

   * > IPv6 CIDR block

      * > Loopback address `::1/128`

      * > Multicast address `FF00::/8~128`

      * > Link\-local address `FE80::/10~128`

## Route limits

* Different VPCs that are already attached to CEN cannot communicate with each other if their subnet CIDR blocks are the same or overlapping.

* If the number of route entries reaches the upper limit when loading a VPC, some system routes (e.g., routes for subnets created later) may not be automatically published to the CEN route table. Later, if the number of route entries falls below the limit (due to route withdrawal or instance detachment), any previously unpublished system routes will not be automatically published. You must manually publish them in the VPC console.

* If the route entry limit is reached when attaching a Direct Connect (DC) Gateway, some added routes may not be automatically published to the CEN route table. Routes added later are discarded. Plan your routing information carefully before attachment.

## Conflict and matching description

After a network instance is attached to the CEN, bidirectional route synchronization occurs: CEN automatically learns the instance's routes. The instance learns routes from other attached network instances via the CEN.

### CEN route

In the CEN route table, a newly learned route from a VPC is marked as Conflicting only if its destination CIDR block exactly matches that of an existing route also learned from a VPC. In all other cases, newly learned routes are marked as Available. Conflicting route entries are not used for matching.

### Matching description

When traffic is matched against CEN route entries, it follows the LPM principle. If multiple routes have the same destination CIDR during the matching process, the matching sequence is as follows:

1. Match routes learned from a VPC.

2. Match static routes learned from a DC Gateway. If multiple static routes exist, first determine if the DC Gateways from which the routes were learned are in different regions:

   * If they are in the same region, the learned static routes form ECMP routes within the CEN.

   * If they are in different regions, identify the region of the DC Gateway whose route was learned first.

      * If only one BGP route learned from a DC Gateway in that region meets the condition, match that route.

      * If multiple routes learned from DC gateways in the region meet the conditions, these routes will form ECMP routes within the CEN.

3. Match BGP routes learned from a DC Gateway. If multiple BGP routes exist:

   1. Priority is determined by the as\-path length – the shorter the as\-path, the higher the priority.

   2. If the as\-path length is the same, then determine if the DC Gateways from which the routes were learned are in different regions:

      * If they are in the same region, the learned BGP routes form ECMP routes within the CEN.

      * If they are in different regions, identify the region of the DC Gateway whose route was learned first.

         * If only one BGP route learned from a DC Gateway in that region meets the condition, match that route.

         * If multiple routes learned from DC gateways in the region meet the conditions, these routes will form ECMP routes within the CEN.

4. Summary routes do not participate in route selection. When a summary route conflicts with an instance route, the instance route takes precedence.

### Network instance route

When CEN synchronizes routes to network instances, the specific synchronization behavior is as follows:

1. **Synchronize routes to VPC**: If the destination CIDR block of the route entry to be synchronized is completely consistent with the subnet segment of the VPC, or the mask of the destination CIDR block is longer than the mask of the VPC subnet, the route entry will conflict and will not be synchronized to the route table of the VPC.

2. **Synchronize routes to DC Gateway**:

   * If multiple ECMP routes exist in the CEN route table, the system filters them based on the source DC gateway instance ID, selecting only the ECMP route with the smallest source DC gateway instance ID for synchronization.

   * When a summary route CIDR block exactly matches a route CIDR block learned by CEN from a network instance, CEN synchronizes the route learned from the network instance to the DC gateway. If that CEN\-learned route with the same CIDR block as the summary route is deleted, the summary route is automatically re\-synchronized to the DC gateway.

> **tip**

> By default, when accessing resources inside a VPC through CEN, CEN uses the routes published by the destination VPC to route traffic to the destination resources.

> When accessing VPC resources through CEN, if you need traffic coming from CEN to match the route table inside the VPC again, you can contact your account manager to enable this allowlist feature.
