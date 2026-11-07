---
title: "Configuring LVM logical volumes (Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configure_LVM_logical_volume_Linux"
---

This topic describes how to configure LVM logical volumes for a Linux instance.

<span id="U11JHYK1"></span>
## Background

Logical Volume Management (Logical Volume Manager, LVM) is a mechanism for managing disk partitions in the Linux environment. LVM abstracts physical storage devices (such as EBS volume) into one or more logical volumes, allowing users to create file systems and store data on logical volumes. After managing EBS volume with LVM, the file system is no longer limited by the size of the EBS volume. It can be distributed across multiple EBS volumes and dynamically scaled up without the need to repartition or reformat the entire disk.

<span id="rrKTr9lk"></span>
### LVM architecture

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9383557e2ec99d01f90f91604ae73eb4.png) </span>

From the architecture diagram, the basic process for managing EBS volume using LVM can be seen as follows:


1. [Create the EBS volume (data volume) as a physical volume](https://docs.byteplus.com/en/docs/49/47699#fiZz74lh).

2. [Combine multiple physical volumes into a volume group](https://docs.byteplus.com/en/docs/49/47699#QMsOXRPa).

3. [Create logical volumes within the volume group](https://docs.byteplus.com/en/docs/49/47699#eTx2uhvC).

4. [Create and mount a file system on the logical volume](https://docs.byteplus.com/en/docs/49/47699#QWnxRMnU).

5. [Scaling up the logical volume](https://docs.byteplus.com/en/docs/49/47699#k39qAPyg).


<span id="LDeCcrSq"></span>
### Related terms


|Terms |Description |
|---|---|
|Physical Volume (PV) |The basic storage unit of LVM, typically corresponding to physical hard disks or disk partitions in the system, is a storage device that can be directly recognized and managed within LVM. |
|Volume Group (VG) |A logical collection composed of one or more physical volumes. Volume group is the logical structure in LVM used for managing physical volumes and provides a unified storage capacity pool for logical volumes. |
|Logical Volume (LV) |The logical volume is the logical storage capacity divided from the volume group. It is the part in LVM actually used for creating the file system and storing data. Users can format and mount the logical volume like using traditional disk partitions. |


<span id="9Hdwz5qx"></span>
## Resource planning

Own an ECS instance with the following basic configuration. For purchase operations, refer to [Purchasing ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


* Instance type: This article selects the ecs.g3il.large specification.

* Image: This article selects CentOS Stream 9.

* Network: Requires [Associating an Elastic IP (EIP)](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP).


<span id="lPnekMTj"></span>
## Procedure

The following introduces how to create a 35GiB logical volume using two 20GiB data volumes.

<span id="fiZz74lh"></span>
### Step 1: Create the EBS volume as a physical volume


1. For the target instance, create and mount two data volumes with a capacity of 20 GiB each, without initialization. [Create an EBS volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume), [Mount an EBS volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

2. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

3. Run the following commands to view the data volumes and record the device names.

   ```Bash
   fdisk -l | grep /dev/vd | grep -v vda
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19d9077981dd7c46298a1c97787d632f.png) </span>

   You can see two data volumes with device names "/dev/vdb" and "/dev/vdc". These two data volumes will be used to create a scalable logical volume using LVM.

4. Run the following commands to install the LVM tools.

   ```Bash
   sudo yum install -y lvm2
   ```
   

   If the output is displayed as "Complete!", the installation is completed.

5. Run the command `sudo pvcreate <disk device name 1> <disk device name 2> <disk device name...>` to create the EBS volume as a physical volume. Command examples are as follows:

   ```Bash
   sudo pvcreate /dev/vdb /dev/vdc
   ```
   

   The following output indicates that the physical volume was created successfully.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_beafc11d82cccb429d8904013331cf9e.png) </span>

6. Execute the following command to view detailed information about the physical volume.

   ```Bash
   pvdisplay
   ```
   

   The following output shows that the system has two new physical volumes, named "/dev/vdb" and "/dev/vdc."

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fc207f4d4358dd7663a3d5a200efeb4.png) </span>


<span id="QMsOXRPa"></span>
### Step 2: Combine multiple physical volumes into a volume group


1. Execute `sudo vgcreate <volume group name> <physical volume name1> <physical volume name2> <physical volume name...>` command to create a volume group. This practice uses creating a volume group named vg_01 as an example. The command is as follows:

   ```Bash
   sudo vgcreate vg_01 /dev/vdb /dev/vdc
   ```
   

   The following output indicates that the volume group was created successfully.

    <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_86232a5af9dad7e2532782593927b371.png) </span>

2. (Optional) If you need to add new physical volumes to the volume group, execute the following command to add other created physical volumes.

   ```Bash
   sudo vgextend <Volume Group Name> <Physical Volume Name> <Physical Volume Name>
   ```
   

3. Execute the following command to view detailed information about the volume group.

   ```Bash
   vgdisplay
   ```
   

   The following output indicates that the volume group vg_01 has been created, with a capacity of approximately 40GiB (part of the storage capacity will be occupied by the file system itself).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec001a2f03fe9c7c1ba0625e2e036841.png) </span>


<span id="eTx2uhvC"></span>
### Step 3: Create a logical volume in the volume group


1. Execute `sudo lvcreate -L <logical volume size> -n <logical volume name> <volume group name>` command to create a logical volume. This practice uses the creation of a logical volume named lv_01 with a size of 35 GiB as an example, as shown in the following command:

   ```Bash
   sudo lvcreate -L 35g -n lv_01 vg_01
   ```
   

   The following output indicates that the logical volume was created successfully.

    <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dfb5d81ee66ea9814ddaaa5335d73e45.png) </span>

2. (Optional) To create multiple logical volumes in the volume group, repeat step 1.

3. Run the following command to view detailed information about the logical volume, including logical volume path, name, associated volume group, and other details. This information will be needed in subsequent procedures.

   ```Bash
   lvdisplay
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_714914036511654c9427532c309b0190.png) </span>


<span id="QWnxRMnU"></span>
### Step 4: Create and mount a file system


1. Execute `sudo mkfs.<file system format> <logical volume path>` command to create a file system on the logical volume. This practice uses the creation of an ext4 file system as an example.

   ```Shell
   sudo mkfs.ext4 /dev/vg_01/lv_01
   ```
   

2. (Optional) Create a new mount point, For example, /mnt/lv_01.

   > If you want to use an existing mount point, you can skip this step.   
   

   ```Bash
   sudo mkdir /mnt/lv_01
   ```
   

3. Execute `sudo mount <logical volume path> <mount point>` to mount the file system to the mount point. This practice takes mounting the logical volume (path: /dev/vg_01/lv_01) to the /mnt/lv_01 directory as an example.

   ```Shell
   sudo mount /dev/vg_01/lv_01 /mnt/lv_01
   ```
   

4. View the mount result of the logical volume.

   ```Bash
   df -h
   ```
   

   If the following output is returned, the partition is mounted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fddb2375c5bd2ee5948442622624efad.png) </span>

5. Configure automatic mounting at startup.

   Run the command `blkid /dev/vg_01/lv_01` to view the UUID of the logical volume, and edit the mount options in the /etc/fstab file to ensure the new mount persists after the instance restarts. For specific operations, refer to [setting up automatic mounting of disk partitions at startup](https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts).


<span id="k39qAPyg"></span>
### Step 5: Scaling up the logical volume


<Tabs>
<Tab zoneid="D5sZeFRz9L" title="Option 1: Use unallocated capacity to scale up the logical volume capacity.">
<TabTitle>Option 1: Use unallocated capacity to scale up the logical volume capacity.</TabTitle>

This action assumes that the 35GiB logical volume you created is no longer sufficient and requires an additional 4GiB of capacity.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When scaling up using this method, ensure that the volume group containing the logical volume to be scaled up has enough free space. If the free space in the volume group cannot meet the current logical volume scaling\-up needs, refer to method two or method three to scale up.</div>



1. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Scale up the logical volume and the file system.

   1. Run the `lvextend -L +<additional capacity> <logical volume path>` command to scale up the capacity of the logical volume.

      ```Bash
      lvextend -L +4G /dev/vg_01/lv_01
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_042f47ac336e9037562471f14ec66536.png) </span>

   2. Scale up the capacity of the file system.

      1. Run the following command to view the file system Type of the logical volume.

         ```Bash
         df -Th
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a8cea4952413d4589ca59b132ce0222.png) </span>

      2. If the file system is ext4, run the `resize2fs <logical volume path>` command to scale up the file system.

         ```Bash
         resize2fs /dev/vg_01/lv_01
         ```
         

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a22dd4cda4ae72453241f685561ce2e.png) </span>

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">If the file system is xfs, run the <code>sudo xfs_growfs <logical volume mount point></code> command to scale it up.         </div>
         

3. Run the following command to view whether the file system capacity has increased.

   ```Bash
   df -h
   ```
   

   The output indicates that the logical volume has been scaled up from 35GiB to 39GiB.

    <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b6a24315d380b569375f3198ac90636e.png) </span>


</Tab>
<Tab zoneid="xTl9u4lGHZ" title="Method Two: Scaling up the EBS volume to extend the capacity of the logical volume">
<TabTitle>Method Two: Scaling up the EBS volume to extend the capacity of the logical volume</TabTitle>

This procedure assumes that the 39GiB logical volume you created can no longer meet your needs. By scaling up one of the EBS volumes, add 10GiB of capacity.


1. Expanding volumes.

   1. Refer to [Expanding a single EBS volume](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux#.5omp5a655Y2V5Liq5LqR55uY) to add 10GiB of capacity to one of the data volumes (this article uses scaling up dev/vdc as an example).

   2. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   3. Run the following command to view whether the system has recognized the scaled\-up EBS volume correctly.

      ```Bash
      fdisk -l
      ```
      

      The following output indicates: Before scaling up, the capacity of /dev/vdc was 20GiB, and after scaling up, it became 30GiB.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8996e9d8f9b80f253979d281d435bff.png) </span>

2. Scale up the physical volume corresponding to the EBS volume /dev/vdc.

   1. Execute the following command to view relevant information about the physical volume before scaling up.

      ```Bash
      pvdisplay
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e77827b7cd244bebda98fea2aa6aaa14.png) </span>

      The capacity of /dev/vdc is 20GiB, indicating that the physical volume capacity has not increased.

   2. Execute `pvresize -v <physical volume name>` command to scale up the physical volume.

      ```Bash
      pvresize -v /dev/vdc
      ```
      

      The following output indicates that the physical volume was successfully scaled up. You can execute `pvdisplay` command to view information about the physical volume after scaling up.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6141688cce25abffc4e06d278fe15a2.png) </span>

3. Scale up the logical volume and file system.

   1. Execute `sudo lvextend -L +<logical volume capacity> <logical volume path>` command to scale up the logical volume.

      ```Bash
      sudo lvextend -L +10G /dev/vg_01/lv_01
      ```
      

      The output similar to the following indicates that you have added 10GiB of space to the logical volume.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4865590aa3ed2f734d1c456d284411c6.png) </span>

   3. Execute `resize2fs <logical volume path>` command to scale up the logical volume file system (this article takes the ext4 file system as an example).

      ```Bash
      resize2fs /dev/vg_01/lv_01
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If it is an xfs file system, please execute <code>sudo xfs_growfs <logical volume mount point></code> command for scaling up.      </div>
      

5. Execute the following command to view extend results.

   ```Bash
   df -h
   ```
   

   You can see that the capacity of the logical volume has increased by 10 GiB (the file system itself will occupy part of the storage capacity).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b1ed0cdc3ccba977c16af136521a799a.png) </span>


</Tab>
<Tab zoneid="B1oFKW2q7R" title="Method Three: Adding a new EBS volume to extend the capacity of the logical volume">
<TabTitle>Method Three: Adding a new EBS volume to extend the capacity of the logical volume</TabTitle>

1. Add EBS volume.

   1. Create and mount a new data volume with a capacity of 20 GiB for the target instance without initialization. [Create EBS volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume), [Mount EBS volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

   2. [Log in to the instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   3. Execute the following command to view the data volume and record the device name.

      ```Bash
      fdisk -l | grep /dev/vd | grep -v vda
      ```
      

      You can see that the newly mounted data volume device is named /dev/vdd.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a60bd75a7f672c373ac52076e4c6aee5.png) </span>

2. Create a physical volume using the new EBS volume.

   ```Bash
   sudo pvcreate /dev/vdd
   ```
   

3. Scale up the volume group.

   1. Run the following command to view volume group information.

      ```Shell
      vgdisplay
      ```
      

      The output displays similar information, indicating the volume group name vg_01 and the current volume group capacity is 49.99GiB.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7b62ab73e803a6f687aff9ac4674be7.png) </span>

   2. Execute the command `sudo vgextend <volume group name> <physical volume name>` to scale up the volume group.

      ```Shell
      sudo vgextend vg_01 /dev/vdd
      ```
      

      Output similar to the following information indicates that the volume group was successfully scaled up.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1cb1c05da7f4085006c82fa25ccc7327.png) </span>

   3. Execute the following command to view volume group information.

      ```Shell
      vgdisplay
      ```
      

      An output similar to the example below is returned. If the capacity of volume group vg_01 is about 69.99 GiB, you have scaled up the volume group.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93af1e609149850c44bc99100cd5d186.png) </span>

6. Scale up the logical volume and file system.

   1. Execute `sudo lvextend -L +<Logical volume capacity> <Logical volume path>` command to scale up the logical volume

      ```Bash
      sudo lvextend -L +20G /dev/vg_01/lv_01
      ```
      

      The echoed information similar to the following indicates that 20GiB of space has been added to the logical volume

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_924088809cd37d7e5dd10a69b8f563cb.png) </span>

   2. Execute `sudo resize2fs <Logical volume path>` command to scale up the logical volume file system (taking ext4 file system as an example)

      ```Bash
      sudo resize2fs /dev/vg_01/lv_01
      ```
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Description      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If it is an xfs file system, execute <code>sudo xfs_growfs <Logical volume mount point></code> command to scale it up      </div>
      

7. Execute the following command to view the final scaling\-up results

   ```Bash
   df -h
   ```
   

   The following echo indicates that a 20GiB capacity has been added to the logical volume (the file system itself will occupy some storage capacity)

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19aa6e30a9708f938fa2636599835d0c.png) </span>


</Tab>
</Tabs>
