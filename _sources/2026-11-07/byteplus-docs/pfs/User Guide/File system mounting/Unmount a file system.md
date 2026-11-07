---
title: "Unmount a file system"
product: "Parallel File Storage"
product_code: "pfs"
source: "https://docs.byteplus.com/en/docs/pfs/Unmount-a-file-system"
---

This topic describes the steps to unmount a PFS file system on an ECS instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite


* The file system has been mounted on the compute node. For specific steps, please refer to [Mounting a file system](https://docs.byteplus.com/docs/pfs/Mounting-a-file-system).

* Please ensure that the mounted file exists on your management node. For specific steps, please refer to [Mounting file systems FAQ](https://docs.byteplus.com/docs/pfs/Mounting-file-systems-FAQ).


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Log in to one of the PFS management nodes. For specific steps, please refer to [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

2. Execute the following command to unmount the PFS file system.

   ```Plain
   vepfs del {ECS IP address}
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You need to replace {ECS IP address} with the private IP address of the ECS instance where you want to unmount the PFS file system.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add multiple IP addresses to be uninstalled, separated by spaces.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After executing the uninstall command, the system will automatically unmount the PFS file system.   </div>
   

3. After unmounting is completed, please refer to the following steps to delete the previously associated security group information in the ECS instance where the PFS file system is mounted.

   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

   2. In the top navigation bar, select the region of the target instance.

   3. In the left navigation bar, select **Instances & Images** \> **Instances**.

   4. On the instance list page, locate the ECS instance with PFS mounted and click the instance name.

   5. On the instance details page, click **Security Group** tab.

   6. On the **Security Group** tab, click **Change** on the right side of **Security Group**.

   7. In the **Change Security Group** panel, deselect the target security group and click **Confirm**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">Tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Each network interface must have at least one security group.      </div>
