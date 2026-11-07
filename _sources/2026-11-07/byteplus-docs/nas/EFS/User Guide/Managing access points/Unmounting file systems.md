---
title: "Unmounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Unmounting_file_systems"
---

This topic explains how to unmount a file system that was mounted via an access point using FSX. This can be done via the EFS console.

<span id="dhsT1hqd"></span>
## Prerequisites


* The file system must be mounted on an Elastic Compute Service (ECS) instance. For instructions, see [Mounting with access points and FSX](https://docs.byteplus.com/en/docs/nas/Mounting_with_access_points_and_FSX).

* Make sure that the ECS instance meets the following conditions:

   * **ECS instance status**: Running

   * **FSX status**: Running

   * **Mount status**: Mounted


<span id="ybXolhKx"></span>
## Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access Point**.

6. On the **Access Point** page, click **Client side list** in the **Actions** column of the access point you want to manage.

7. In the **client side list** panel, perform the following operations:

   
   <Tabs>
   <Tab zoneid="Q9w5x3Mj" title="Unmount from a single instance">
   <TabTitle>Unmount from a single instance</TabTitle>
   
   1. Click  **... ** \> **uninstall** in the **operation** column of the access point.
   
   2. In the **Uninstall directory** dialog, verify the following parameters.
   
      * **ECS instance ID**: The ID of the ECS instance from which you want to unmount the file system. It is automatically displayed and cannot be modified.
   
      * **Cancel auto mount**: Selecting this option disables automatic mounting upon restart after the file system is unmounted. This option is selected by default.
   
   3. Click **OK**.
   
   
   </Tab>
   <Tab zoneid="sWsZcjfx" title="Unmount from multiple instances">
   <TabTitle>Unmount from multiple instances</TabTitle>
   
   1. Check the boxes next to the ECS instances from which you want to unmount the file system.
   
   2. Click **batch uninstall** below the list.
   
   3. In the **Uninstall directory** dialog, verify the following parameters.
   
      * **ECS instance ID**: The ID of the ECS instance from which you want to unmount the file system. It is automatically displayed and cannot be modified.
   
      * **Cancel auto mount**: Selecting this option disables automatic mounting upon restart after the file system is unmounted. This option is selected by default.
   
   4. Click **OK**.
   
   
   </Tab>
   </Tabs>
