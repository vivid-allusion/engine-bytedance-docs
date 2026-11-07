---
title: "Upgrade instance kernel version"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Upgrade_kernel_version"
---

Milvus for VectorDB regularly optimizes the kernel and performance. We recommend manually upgrading to the latest kernel version. This topic describes how to upgrade the instance kernel version.

## Precautions

* Only Dedicated instances support kernel version upgrades.

* Once the version upgrade starts, the process cannot be canceled. You can continue to write and read data during the upgrade but cannot make other changes. Perform the upgrade during off\-peak hours.

* Manually backup data before upgrading. For specific actions, see [Manually create a backup](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Manually_create_a_snapshot).

* The upgrade will trigger instance restart. The duration depends on the instance specifications (usually under 30 seconds per node).

* During the upgrade, some requests may time out or fail.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. On the **Instance details** tab, click **Version upgrade** after the **Kernel version** field in the **Basic information** section.

6. In the pop\-up dialog, confirm the upgrade information, check **I completed data back up or confirmed no need to back up.** , then click **Now upgrade**.

   > **tip**

   > If **Version upgrade** does not appear after the version number, the instance kernel version is already the latest and no action is needed.
