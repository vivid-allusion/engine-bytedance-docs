---
title: "Modifying a bandwidth package"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-03"
---

## Modify bandwidth

When the allocatable bandwidth of a bandwidth package falls short of actual requirements, you can adjust the package's bandwidth as needed.

**Upgrade**: Increase bandwidth. Upgrading​ does not affect running services but increases costs.

**Downgrade**: Decrease bandwidth. Downgrading​ may affect running services if the reduced bandwidth is lower than current service requirements. Proceed with caution.

### Action description

* The modified bandwidth of the package must not be less than the total bandwidth already allocated to inter\-region connections.

* For BytePlus accounts blocked by the line operator due to illegal use of cross\-border services, modifying the bandwidth of the cross\-border Bandwidth Package is not supported.

### Procedures

**Bandwidth Package console**

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. In the left navigation tree, select **Bandwidth Package**.

3. In the top navigation bar, select the target project.

4. Click **Modify bandwidth** on the right side of the target Bandwidth Package.

5. On the Modify Bandwidth page, adjust the bandwidth of the target bandwidth package.

6. Follow the console guidance to review and accept Legal, and click **Buy now**.

7. Click **Next** and complete the payment according to the interface prompts.

**CEN console**

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click the target CEN instance name.

3. Select the **Inter\-region bandwidth** tab, then click **Modify bandwidth** on the right side of the target Bandwidth Package.

4. On the Modify Bandwidth page, adjust the bandwidth of the target bandwidth package.

5. Follow the console guidance to review and accept Legal, and click **Buy now**.

6. Click **Next** and complete the payment according to the interface prompts.

## Modify bandwidth package

### Prerequisites

* The new bandwidth package has the same interconnection regions as the original bandwidth package.

* The bandwidth of the new bandwidth package is greater than or equal to the allocated inter\-region bandwidth of the original bandwidth package.

### Action description

* After replacement, The inter\-region bandwidth originally associated with the old package is automatically transferred to the new bandwidth package.

* After replacement, the new bandwidth package is automatically bound to the Cloud Enterprise Network (CEN), while the original bandwidth package is automatically unbound.

### Procedures

1. Log in to the [CEN console](https://console.byteplus.com/cen/EnterpriseNetwork).

2. Click the target CEN instance name.

3. Select the **Inter\-region bandwidth** tab, then click **Change bandwidth** to the right of the target bandwidth package.

4. Select the bandwidth package from the dropdown list.

5. Click **Save** to complete the action.

## Related documents

[ModifyCenBandwidthPackageAttributes](https://docs.byteplus.com/en/docs/cen/ModifyCenBandwidthPackageAttributes)
