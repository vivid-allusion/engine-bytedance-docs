---
title: "Network Instance FAQ"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Network-instances-faq"
---

* [What types of network instances can be loaded into Cloud Enterprise Network (CEN)?](https://docs.byteplus.com/en/docs/44/16682#.5LqR5LyB5Lia572R5pSv5oyB5Yqg6L295ZOq5Lqb57G75Z6L55qE572R57uc5a6e5L6L77yf)

* [After configuring CEN, how can I test connectivity between network instances?](https://docs.byteplus.com/en/docs/44/16682#.5LqR5LyB5Lia572R6YWN572u5a6M5oiQ5ZCO77yM5aaC5L2V5rWL6K-V572R57uc5a6e5L6L6Ze06L-e6YCa5oCn77yf)

* [After configuring CEN, what might be the reasons if cross-region VPCs cannot communicate?](https://docs.byteplus.com/en/docs/44/16682#.5LqR5LyB5Lia572R6YWN572u5a6M5oiQ5ZCO77yM6Leo5Zyw5Z-fVlBD5peg5rOV6YCa5L-h5Y-v6IO95piv5LuA5LmI5Y6f5Zug77yf)

## What types of network instances can be loaded into Cloud Enterprise Network (CEN)?

The CEN currently supports loading the following types of network instances: Virtual Private Cloud (VPC) and Direct Connect Gateway. If a Direct Connect Gateway is selected, it must be used in conjunction with the Direct Connect service to enable network connectivity. For detailed instructions, see the [Direct Connect Quick start](https://docs.byteplus.com/en/docs/directconnect/Quick-start).

## After configuring CEN, how can I test connectivity between network instances?

Once CEN is configured, you can test connectivity between network instances using methods such as `ping` or `telnet`.

Testing connectivity varies depending on the types of loaded network instances:

* Testing connectivity between VPCs: Verify by testing whether the ECSs in two different VPCs can communicate with each other.

* Testing connectivity between a VPC and a Direct Connect Gateway: Verify by testing whether an ECS within the VPC can communicate with a server in an on\-premises IDC that is connected via the Direct Connect service.

* Testing connectivity between Direct Connect Gateways: Verify by testing whether servers in two on\-premises IDCs, each connected via their respective Direct Connect services, can communicate with each other.

> **tip**

> The Direct Connect Gateway is a component of the Direct Connect service and must be used in conjunction with it.

## After configuring CEN, what might be the reasons if cross\-region VPCs cannot communicate?

After configuring CEN, you can log in to an ECS within a VPC and execute the `ping <IP address of the ECS in the peer VPC, e.g., 192.168.1.11>` command to verify cross\-region VPC connectivity.

* If the `ping` is successful but normal communication still fails, the issue may lie in an incorrect CEN configuration. Please verify the relevant settings.

   Cross\-region VPC communication requires not only a configured bandwidth package but also the allocation of corresponding inter\-region bandwidth. If a bandwidth package is configured but inter\-region bandwidth is not allocated, only the default 10 Kbps bandwidth will be available between regions. This is sufficient only for small\-scale testing and cannot support normal communication involving large data volumes.

* Troubleshooting steps if `Ping` fails:

   * Check the security group rules configured in the target VPC to see if they are restricting access from the source VPC.

      If the target VPC has an inbound security group policy that denies access from the source VPC, data packets will be filtered and blocked, preventing communication.

   * Check whether the VPCs that need to communicate have conflicting or overlapping subnets.

      If conflicting or overlapping subnets exist, packets originally intended for the target subnet may be routed within the source VPC itself and never forwarded to the correct destination subnet.
