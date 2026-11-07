---
title: "Step 2: Plan and allocate IPAM pools as the delegated admin"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Step-2-plans-and-allocates-IPAM-address-pools"
---

## Scenarios

The IPAM delegated admin uses the IPAM feature to plan the IP address space within the organization and allocates IPAM address pools to various business accounts for their use.

## Procedures

### Step 1: Create IPAM instance

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the top menu bar, select the Region.

3. In the left navigation pane, select **IPAM**.

4. Click **Create IPAM**.

5. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Effective region |By default, the region currently selected in the top navigation bar is used as the primary region. |China (Beijing) |
   |Name |Enter the IPAM name. |IPAM\-A |

6. Click **OK** to complete the action.

### Step 2: Create IPAM scope

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left navigation pane, select **IPAM Scope**.

3. Click **Create scope**.

4. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of scope. |IpamScope\-A |
   |IPAM |Fixed as the IPAM instance of that specific region.<br><br>Because only one IPAM instance is supported per region. |IPAM\-A |
   |Type |Currently, only VPCs are supported. |VPC |

5. Click **OK** to complete the action.

### Step 3: Create IPAM parent pool

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left navigation pane, select **IPAM Address Pool**.

3. Click **Create Address Pool**.

4. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example |
   |---|---|---|
   |Name |Enter the name of pool. |IpamPool\-A |
   |IPAM scope |Select the IPAM scope from the dropdown list. |IpamScope\-A |
   |Address pool source |Based on the IPAM pool plan, select either a top\-level pool or a sub pool.<br><br><br>* Top\-level pool: Choose **IPAM Scope** as the pool source.<br><br>* Sub\-pool: Choose **IPAM Address Pool** as the source, and choose an address pool within the corresponding scope as the parent address pool for this pool. |IPAM Scope |
   |Automatic resource import |Enable resource auto\-import.<br><br><br>* When enabled, the system will continuously discover resources within the CIDR range of this pool and automatically import them as allocations into your IPAM instance.<br><br>   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.<br><br>   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.<br><br>* If this option is not enabled now, you can edit the address pool later and enable automatic resource import as needed. |Do not enable |
   |CIDR |Enter the CIDR as needed.<br><br><br>* You can click Add CIDR to add pre‑provisioned CIDR blocks. Up to 50 CIDR blocks can be added.<br><br>* If the address pool is a sub\-pool, the entered CIDR must be a subset of its parent address pool. |10.0.0.0/8 |
   |Allocation rule settings |Enable the allocation rule settings as needed. |Enable |
   |Allocate mask |Configure the allocation mask. This parameter is only configurable after enabling the Allocation Rule Settings.<br><br>Enter the **Minimum netmask length**, **Default netmask length**, and **Maximum netmask length** for resources allocated within the address pool. |8 16 24 |

5. Click **Create** to complete the action.

### Step 4: Create IPAM sub\-pool

See the steps below to sequentially create address pools for Business A and Business B.

1. Log in to the [IPAM console](https://console.byteplus.com/ipam/ipam).

2. In the left navigation pane, select **IPAM Address Pool**.

3. Click **Create Address Pool**.

4. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example A |Example B |
   |---|---|---|---|
   |Name |Enter the name of pool. |IpamPool\-APP\-A |IpamPool\-APP\-B |
   |IPAM scope |Select the IPAM scope from the dropdown list. |IpamScope\-A |IpamScope\-A |
   |Address pool source |Select the **IPAM pool** configuration option, and choose **IpamPool\-A** within the corresponding scope as the parent pool for this pool. |**IPAM address pool**<br><br>IpamPool\-A |**IPAM address pool**<br><br>IpamPool\-A |
   |Automatic resource import |Enable resource auto\-import.<br><br><br>* When enabled, the system will continuously discover resources within the CIDR range of this pool and automatically import them as allocations into your IPAM instance.<br><br>   * If multiple CIDRs discovered by IPAM overlap, IPAM will only automatically import the CIDR with the largest address block.<br><br>   * If IPAM discovers multiple identical CIDRs, IPAM instance will randomly import one of them.<br><br>* If this option is not enabled now, you can edit the address pool later and enable automatic resource import as needed. |Enable |Enable |
   |CIDR |Enter CIDR. |10.1.0.0/16<br><br>10.2.0.0/16<br><br>10.3.0.0/16 |10.11.0.0/16<br><br>10.12.0.0/16<br><br>10.13.0.0/16 |
   |Allocation rule settings |Enable the allocation rule settings as needed. |Enable |Enable |
   |Allocate mask |Enter the **Minimum netmask length**, **Default netmask length**, and **Maximum netmask length** for resources allocated within the address pool. |8 16 24 |8 16 24 |

5. Click **Create** to complete the action.

### Step 5: Share IPAM sub\-pool

1. Log in to the [Resource Sharing console](https://console.byteplus.com/resourcemanager/region:resource-manager+cn-beijing/resource_share/owned).

2. In the left navigation pane, select **Resource sharing \> Shared by me**.

3. In the top menu bar, select the Region.

4. On the **Shared unit** tab, click **Create shared unit**.

5. Configure the relevant parameters based on the table below.

   |Parameter |Description |Example A |
   |---|---|---|
   |Shared unit name |Enter the name of shared unit. |Shared address pool\-A |
   |Region |Select the region where the pool resides. |China (Beijing) |
   |Product |Select VPC \- IPAM pool. |VPC \- IPAM Pool |
   |Resource ID |Select (check) the IDs of the IPAM pools to be shared. |Select the ID of the IPAM pool |
   |Shared policy name |Defaults to and only supports IPAMPoolDefaultPermission. |IPAMPoolDefaultPermission |
   |Add via enterprise organization |Enable the **Add via enterprise organization** feature and select the member accounts from the enterprise organization. Note that this feature can only be enabled by an enterprise organization admin. |Do not enable |
   |User type and user ID |Select root user as the type and enter the Account ID of the consumer. |Root user 210005\*\*\*\* |

6. Click **Next**, confirm everything is correct, then click **Confirm** to complete the actions.

   Repeat the above steps to share Pool B with Business Account B.

   > **tip**

   * > Within the same enterprise organization, resource sharing invitations are accepted by default. However, across different enterprise organizations, the recipient account must manually accept the share.

   * > If the IPAM pool consumer and owner are not in the same enterprise organization, the following two\-way sharing operations must be completed before the consumer can use the pool.

      * > The IPAM pool owner shares the pool with the consumer.

      * > The IPAM pool consumer shares its own Resource Discovery with the IPAM pool owner.

###
