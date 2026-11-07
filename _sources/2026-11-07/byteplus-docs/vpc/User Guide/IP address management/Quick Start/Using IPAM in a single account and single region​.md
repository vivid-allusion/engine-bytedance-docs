---
title: "Using IPAM in a single account and single region​"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/IPAM-Getting-started"
---

## Scenarios

Company X has two core businesses deployed on BytePlus, involving multiple Virtual Private Cloud (VPCs). To prevent IP address conflicts, simplify maintenance, and support future expansion, all their IP addresses are centrally managed via the IPAM tool. This enables standardized management of address allocation, documentation, and reservation, reducing operational complexity across VPCs.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed5e004cd6224f94333105420a8b8b53.png)

## Before you begin

For CIDR planning, see [IPAM address planning](https://docs.byteplus.com/en/docs/vpc/IPAM-address-planning) first.

## Procedure

### Step 1: Create IPAM instance

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the region.

3. In the left navigation pane, select **IPAM**.

4. Click **Create IPAM**.

5. Configure parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Effective region |By default, the region currently selected in the top navigation bar is used as the primary region. |China (Beijing) |
   |Name |Enter the IPAM name. |IPAM\-A |

6. Click **OK** to complete the action.

### Step 2: Create IPAM scope

1. In the left navigation pane, select **IPAM Scope**.

2. Click **Create scope**.

3. Configure parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of scope. |IpamScope\-A |
   |IPAM |Fixed as the IPAM instance of that specific region. |IPAM\-A |
   |Type |Currently, only VPCs are supported. |VPC |

4. Click **OK** to complete the action.

### Step 3: Create address pool

1. In the left navigation pane, select **IPAM Address Pool**.

2. Click **Create Address Pool**.

3. Configure parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of pool. |IpamPool\-A |
   |IPAM scope |Select the IPAM scope from the dropdown list. |IpamScope\-A |
   |Address pool source |This topic selects **IPAM Scope.**  |IPAM Scope |
   |Automatic resource import |Enable resource auto\-import.<br><br><br>* When enabled, the system will continuously discover resources within the CIDR range of this pool and automatically import them as allocations into your IPAM instance.<br><br>   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.<br><br>   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.<br><br>* If this option is not enabled now, you can edit the address pool later and enable automatic resource import as needed. |Enable |
   |CIDR |Enter CIDR. |10.0.0.0/8 |
   |Allocation rule settings |Enable the allocation rule settings as needed. |Enable |
   |Allocate mask |Enter the **Minimum netmask length**, **Default netmask length**, and **Maximum netmask length** for resources allocated within the address pool. |8 16 24 |

4. Click **Create** to complete the action.

### Step 4: Create sub\-pool

See the steps below to sequentially create address pools for Business A and Business B.

1. In the left navigation pane, select **IPAM Address Pool**.

2. Click **Create Address Pool**.

3. Configure parameters based on the table below.

   |Parameter |Description |Example A |Example B |
   |---|---|---|---|
   |Name |Enter the name of pool. |IpamPool\-APP\-A |IpamPool\-APP\-B |
   |IPAM scope |Select the IPAM scope from the dropdown list. |IpamScope\-A |IpamScope\-A |
   |Address pool source |Select the **IPAM Address Pool** configuration item, and choose an address pool **IpamPool\-A** within the belonging scope to act as the parent pool for this pool. |**IPAM Pool**<br><br>IpamPool\-A |**IPAM Pool**<br><br>IpamPool\-A |
   |Automatic resource import |Enable resource auto\-import.<br><br><br>* When enabled, the system will continuously discover resources within the CIDR range of this pool and automatically import them as allocations into your IPAM instance.<br><br>   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.<br><br>   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.<br><br>* If this option is not enabled now, you can edit the address pool later and enable automatic resource import as needed. |Enable |Enable |
   |CIDR |Enter CIDR. |10.1.0.0/16<br><br>10.2.0.0/16<br><br>10.3.0.0/16 |10.11.0.0/16<br><br>10.12.0.0/16<br><br>10.13.0.0/16 |
   |Allocation rule settings |Enable the allocation rule settings as needed. |Enable |Enable |
   |Allocate mask |Enter the **Minimum netmask length**, **Default netmask length**, and **Maximum netmask length** for resources allocated within the address pool. |8 16 24 |8 16 24 |

4. Click **Create** to complete the action.

### Step 5: Create VPC

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the top menu bar, select the target region.

3. Click **Create VPC**.

4. Configure parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |**Basic information** |||
   |Region |Select the region of the VPC. |China (Beijing) |
   |Name |Enter the name of the VPC. |VPC\-A1 |
   |**CIDR block** |||
   |IPv4 CIDR |Configure the IPv4 CIDR assignment method.<br><br><br>* Manual Assignment: Enter the IPv4 CIDR directly.<br><br>* IPAM Assignment: Select an address pool from the dropdown and choose the netmask length. |Assigned by IPAM<br><br>/16 |
   |**Subnet** |||
   |Availability zone |Select an availability zone. |Availability Zone A |
   |Name |Enter the subnet name. |Subnet\-A |
   |IPv4 CIDR |Configure the subnet CIDR block, which must fall within the VPC's address range. |10.1.1.0/24 |

5. Click **Create** to complete the action.

Repeat this process to create multiple VPCs.
