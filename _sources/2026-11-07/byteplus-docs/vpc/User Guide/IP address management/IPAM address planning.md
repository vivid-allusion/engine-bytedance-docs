---
title: "IPAM address planning"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPAM-address-planning"
---

Planning CIDR blocks not only prevents routing issues caused by overlapping CIDRs and reserves space for business expansion but also simplifies operations and enhances security control through functional partitioning.

## Planning principles

* **CIDR blocks do not overlap**

   All CIDR ranges used by any business must strictly avoid any overlap to prevent routing conflicts or access chaos.

* **Reservation of non\-assignable addresses**

   Each subnet must reserve 3 non\-assignable addresses: the Network Address (e.g., 10.1.1.0, identifying the CIDR itself), the Gateway Address (e.g., 10.1.1.1, dedicated to the CIDR gateway), and the Broadcast Address (e.g., 10.1.1.255, for broadcast communication within the CIDR).

* **VPC isolation priority**

   Divide independent VPCs by environment (Production/Test/Development), business unit, or security domain to achieve network isolation and reduce cross\-scenario risks.

* **Reserved expansion redundancy**

   It is recommended to plan the address space based on **current requirements plus projected growth over the next three years**, and reserve 50% additional CIDR blocks as a buffer to accommodate new services, capacity expansion, or architectural adjustments.

* **Full lifecycle documentation**

   Use IPAM tools for centralized management, recording each CIDR block's CIDR Range, Purpose, Owner, Associated Security Policies. Conduct regular audits and updates to ensure traceability.

## Rule content

### Role planning

It is recommended to use an enterprise organization to simplify account management and role planning.

|**Role** |Notes |**IPAM\-related operations** |
|---|---|---|
|**Enterprise organization admin account** |The account used to manage the enterprise organization (e.g., adding or removing member accounts). The account should not be used to operate IPAM resources, it is advisable to create a dedicated account for managing IPAM resources. |* Enable enterprise organization<br><br>* [Enable IPAM trusted service](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service)<br><br>* [Delegate IPAM admin](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service)<br><br>* [Disable IPAM trusted service](https://docs.byteplus.com/en/docs/vpc/Enabling-trusted-service) |
|**IPAM delegated admin** (member account) |The IPAM delegated admin account is a dedicated account for managing IPAM resources \- for example, creating IPAM address pools and sharing them with business accounts. |* [Creating an IPAM instance](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-instances)<br><br>* [Managing a scope](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-scopes)<br><br>* [Managing an address pool](https://docs.byteplus.com/en/docs/vpc/Managing-IPAM-pools)<br><br>* [Sharing address pool with business accounts](https://docs.byteplus.com/en/docs/vpc/Sharing-IPAM-Pool)<br><br>* [Managing a resource discovery](https://docs.byteplus.com/en/docs/vpc/IPAM-Viewing-resource-discovery) |
|**Business account** (member account) |Business accounts are used to deploy business resources. They can use the address pools shared by the IPAM delegated admin to create VPCs and allocate secondary CIDR blocks. |* [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC)<br><br>* [Configuring a custom-allocated CIDR](https://docs.byteplus.com/en/docs/vpc/Creating-Deleting-a-custom-allocated-CIDR) |

### Region planning

To reduce access latency and improve download speed, it is recommended that you choose the nearest region based on your business needs.

### Address planning

1. **Define top\-level address pool**

   Select a foundational address pool from the IPv4 private address ranges (RFC 1918), aligned with business scale:

   * 10.0.0.0/8: Suitable for large enterprises, cross\-region/hybrid cloud architectures.

   * 172.16.0.0/12: Suitable for medium\-sized businesses, multi\-department/multi\-scenario use.

   * 192.168.0.0/16: Suitable for small teams, simple network architectures.

2. **Define regional address pool**

   Based on your business situation, divide different address pools for different regions.

3. **Define business address pool**

   Based on your business situation, divide address pools for different businesses. These address pools will be used to create VPCs.

4. **VPC CIDR planning**

   * **VPC CIDR division**:

      * A /16 CIDR (containing 65,536 addresses) is recommended for a single VPC to meet small\-to\-medium business needs; very large businesses can split into multiple /16 VPCs.

      * **Core rule**: VPC CIDR blocks should not overlap wherever possible, in order to avoid routing conflicts.

   * **Subnet division within a VPC**: Divide subnets by business functional modules (e.g., frontend layer, application service layer, data storage layer) to achieve functional isolation and security control.

5. **Plan and reserve CIDR blocks**

Configure independent reserved address pools to prevent them from being automatically allocated to cloud resources or accidentally occupied, while reserving space for future business maintenance and expansion.

## Planning examples

A company deploys its services on BytePlus resources. To support future expansion into multi\-vendor and hybrid cloud scenarios and simplify operations, it plans a multi\-tier CIDR structure in advance. The specific plan is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_41a580411ae443184f4bf610f01a14aa.png)

|Role |Actions |
|---|---|
|Enterprise organization admin |Open the Enterprise Organization and specify an IPAM delegated admin. |
|IPAM delegated admin |* Based on the requirements for scenario isolation and reservation across Cloud \- On\-Premises \- Other Clouds, three top\-level CIDR blocks are defined:<br><br>   * **BytePlus Cloud**: Uses the 10.0.0.0/8 block as the core address pool for current and future cloud services.<br><br>   * **On\-premises IDC reserve**: Uses the 192.168.0.0/16 block to avoid conflicts with cloud addresses and reserve space for future on\-premises data center (IDC) integration.<br><br>   * **Other Cloud vendor reserve**: Uses the 172.16.0.0/12 block to accommodate future multi\-cloud deployment needs, ensuring no address overlap across vendors.<br><br>* Within the 10.0.0.0/8 block, independent address pools are allocated by business unit based on regional segments:<br><br>   * **Region A**: Uses the 10.0.0.0/11 and 10.32.0.0/11 blocks to meet its comprehensive address requirements across all scenarios.<br><br>   * **Region B**: Uses the 10.64.0.0/11 and 10.96.0.0/11 blocks to meet its comprehensive address requirements across all scenarios.<br><br>   * **Region expansion reserve**: The remaining segments outside the above ranges are reserved for new business units or expansion of existing ones.<br><br>* Within Region A's CIDR block (10.1.0.0/16 to 10.10.0.0/16), subdivide according to business requirements:<br><br>   * Business A: Use the CIDR block 10.1.0.0/16 to 10.10.0.0/16, and share Business A's address pool with Business A's account.<br><br>   * Business B: Use the CIDR block 10.11.0.0/16 to 10.20.0.0/16, and share Business B's address pool with Business B's account.<br><br>   * Business C: Use the CIDR block 10.21.0.0/16 to 10.30.0.0/16, and share Business C's address pool with Business C's account.<br><br>   * **Business expansion reserve**: 10.0.0.0/16 and 10.31.0.0/16 are reserved as independent CIDR blocks for scaling or temporary needs. |
|Business account |Different business accounts create VPCs through IPAM address pools to deploy services for their respective businesses. |

##
