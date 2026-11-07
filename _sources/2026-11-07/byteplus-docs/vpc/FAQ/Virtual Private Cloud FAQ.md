---
title: "Virtual Private Cloud FAQ"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/VPC-FAQ"
---

|Issue category |Issue |
|---|---|
|**Limit** |* [How many VPCs can be created per account?](https://docs.byteplus.com/en/docs/47/4636#.5LiA5Liq6LSm5Y-35pSv5oyB5Yib5bu65aSa5bCR5Liq56eB5pyJ572R57uc77yf)<br><br>* [Can multiple route tables be created within a single VPC?](https://docs.byteplus.com/en/docs/47/4636#.5q-P5Liq56eB5pyJ572R57uc5Y-v5Lul5Yib5bu65aSa5Liq6Lev55Sx6KGo5ZCX77yf)<br><br>* [Can each subnet be associated with multiple route tables?](https://docs.byteplus.com/en/docs/47/4636#.5q-P5Liq5a2Q572R5Y-v5Lul5YWz6IGU5aSa5Liq6Lev55Sx6KGo5ZCX77yf)<br><br>* [What CIDR blocks are supported for VPCs? How many usable IPs per block?​​](https://docs.byteplus.com/en/docs/47/4636#.56eB5pyJ572R57uc5pSv5oyB5L2_55So5ZOq5Lqb572R5q6177yIQ0lEUu-8ie-8n-WQhOe9keauteacieWkmuWwkeWPr-eUqElQ77yf)<br><br>* [Can ECSs be migrated from their current VPC to another VPC?​​](https://docs.byteplus.com/en/docs/47/4636#.5piv5ZCm5pSv5oyB5LqR5pyN5Yqh5Zmo5LuO5b2T5YmNVlBD5YiH5o2i6Iez5YW25LuWVlBD77yf) |
|**Feature** |* [Is it possible to modify the CIDR blocks of existing VPCs or subnets?](https://docs.byteplus.com/en/docs/47/4636#.56eB5pyJ572R57uc5ZKM5a2Q572R55qE572R5q615piv5ZCm5pSv5oyB5L-u5pS577yf)<br><br>* [Is there a charge for VPC?](https://docs.byteplus.com/en/docs/47/4636#.56eB5pyJ572R57uc5piv5ZCm5pS26LS577yf)<br><br>* [Can VPC access internet services?](https://docs.byteplus.com/en/docs/47/4636#.56eB5pyJ572R57uc5Y-v5Lul6K6_6Zeu5YWs572R5pyN5Yqh5ZCX77yf)<br><br>* [How do VPCs ensure ECS security?​​](https://docs.byteplus.com/en/docs/47/4636#.56eB5pyJ572R57uc5aaC5L2V5L-d6K-B5LqR5pyN5Yqh5Zmo55qE5a6J5YWo77yf)<br><br>* [How to modify private DNS?](https://docs.byteplus.com/en/docs/47/4636#.54Gr5bGx5byV5pOORE5T55qESVDlnLDlnYDmmK_lpJrlsJHvvJ_lpoLkvZXkv67mlLlETlPvvJ8=)[How to modify private DNS?](https://docs.byteplus.com/en/docs/47/4636#.54Gr5bGx5byV5pOORE5T55qESVDlnLDlnYDmmK_lpJrlsJHvvJ_lpoLkvZXkv67mlLlETlPvvJ8=)<br><br>* [Why haven't DNS modifications taken effect in my VPC?](https://docs.byteplus.com/en/docs/47/4636#.5L-u5pS556eB5pyJ572R57ucRE5T5ZCO77yM6YWN572u5pyq55Sf5pWI77yf)<br><br>* [Can different VPCs communicate with each other?](https://docs.byteplus.com/en/docs/47/4636#.5LiN5ZCM56eB5pyJ572R57uc5LmL6Ze06IO95ZCm5LqS6YCa77yf)<br><br>* [Why does the transit router field display "-" in the VPC details page despite the VPC being associated with a transit router?​​](https://docs.byteplus.com/en/docs/47/4636#.VlBD5bey5YWz6IGU5Yiw5Lit6L2s6Lev55Sx5Zmo5a6e5L6L77yM5Li65LuA5LmIVlBD6K-m5oOF6aG15Lit6L2s6Lev55Sx5Zmo5LuN5pi-56S65Li64oCcLeKAne-8nw==) |

## Limit

### How many VPCs can be created per account?

A single account in one region can create up to 10 Virtual Private Clouds (VPCs) by default, including the default VPC. If the default quota does not meet your needs, go to the Quota Center to apply for a quota increase.

### Can multiple route tables be created within a single VPC?

Yes. A single VPC supports up to 1 system route table and 9 custom route tables. The system route table is automatically created with the VPC and shares its lifecycle.

### Can each subnet be associated with multiple route tables?

No. Each subnet must be associated with exactly one subnet route table, and each subnet route table can be linked to multiple subnets.

### What CIDR blocks are supported for VPCs? How many usable IPs per block?​​

* IPv4: Supported CIDR blocks for VPCs and their usable IPv4 address counts are listed in the table below:

   |**CIDR block** |**Total available IP addresses in a VPC (excluding platform\-reserved IPs).**  |
   |---|---|
   |10.0.0.0/8~28 |16777213 |
   |172.16.0.0/12~28 |1048573 |
   |192.168.0.0/16~28 |65533 |

* ​​IPv6: ​​BytePlus automatically assigns an IPv6 CIDR block with a `/56` mask to your VPC. Subnets within this VPC receive a fixed `/64` mask.

### Can ECSs be migrated from their current VPC to another VPC?​​

Yes, supported. For actions, see [Changing Virtual Private Cloud or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance).

## Feature

### Is it possible to modify the CIDR blocks of existing VPCs or subnets?

Unsupported. After creation, the CIDR blocks of both VPCs and subnets cannot be modified.​​

### Is there a charge for VPC?

For VPC billing details, see [Billing documentation](https://docs.byteplus.com/en/docs/vpc/Billing).

### Can VPC access internet services?

ECS instances within a VPC can leverage the following products to access the internet or expose services publicly.

* Elastic IP Address (EIP)​​: By binding an EIP to the ECS, it gains bidirectional internet connectivity.

* Public NAT Gateway​​: SNAT function enables secure outbound public access for ECSs. DNAT function allows exposing services to the internet.

* Classic Load Balancer (CLB): Distributes incoming public client requests to backend ECSs according to predefined CLB policies.

### How do VPCs ensure ECS security?​​

* A VPC is a logically isolated network environment where ECSs cannot communicate externally by default.

* Configure security group rules for ECSs to enforce access control. Any traffic not explicitly allowed to enter or exit the instance is automatically denied.

### What is the private DNS IP address? How to modify private DNS?

The default DNS server addresses are `100.96.0.2` and `100.96.0.3`. ECS instances within the VPC use private DNS for internal resolution by default. This means ECSs can be accessed directly via private DNS without traversing the internet. If you need to resolve domain names using a custom private DNS service, you can modify the default DNS server addresses. For detailed steps, see [customize private DNS](https://docs.byteplus.com/en/docs/vpc/Customizing-the-private-DNS).

### Why haven't DNS modifications taken effect in my VPC?

After modifying the DNS settings of a VPC, new ECS instances will automatically inherit the updated configuration. Existing instances require DHCP service renewal to apply the changes. For specific operations, refer to [allocating a private domain name](https://docs.byteplus.com/en/docs/vpc/Customizing-the-private-DNS).

### Can different VPCs communicate with each other?

Yes. By default, VPCs are fully isolated. However, you can enable interconnectivity using dedicated cloud services.

|Product |Description |Same account, same region |Cross\-account, same region |Same account, cross\-region |Cross\-account, cross\-region |
|---|---|---|---|---|---|
|Cloud Enterprise Network (CEN) |Achieve full private network connectivity among multiple cloud Virtual Private Clouds |Yes, see [Same account, same region VPC Interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-within-the-same-account-and-Region-01) |Yes, see [Cross-account, same-region VPC Interconnection](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-accounts-within-the-same-Region) |Supported, see [Same account cross-region private network connectivity](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-within-the-same-account-01) |Supported, see [Cross-account and across regions private network communication](https://docs.byteplus.com/en/docs/cen/Inter-VPC-communication-across-Regions-and-accounts) |
|Transit Router |Flexibly define connectivity and isolation between multiple VPCs |Yes, see [Implementing private connectivity and isolation between different VPCs (same account, same region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-02) |Yes, see [Cross-account, same region VPC interconnection and isolation](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-04) |Yes, see [Implementing private connectivity and isolation between different VPCs (same account, cross-region)](https://docs.byteplus.com/en/docs/transitrouter/Quick-start-03) ||
|PrivateLink (PL) |Resources within a VPC can securely and simply access services shared by other VPCs. |Yes, see [Implementing private access between VPCs within the same account](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-02) |Supported, see [Enabling private network access between VPCs across accounts](https://docs.byteplus.com/en/docs/privatelink/Getting-Started-03) |Not natively supported, but cross\-region access can be achieved by integrating with other products/services. ||
|VPN |Achieve bidirectional private connectivity between two VPCs without public exposure. |Supported, see [Establishing network connectivity between VPCs](https://docs.byteplus.com/en/docs/vpn/Connecting-virtual-private-clouds) ||||

### Why does the transit router field display "\-" in the VPC details page despite the VPC being associated with a transit router?​​

This occurs because you're using an IAM user lacking query permissions for transit routers. To display it properly, add query permissions for the transit router to this account.
