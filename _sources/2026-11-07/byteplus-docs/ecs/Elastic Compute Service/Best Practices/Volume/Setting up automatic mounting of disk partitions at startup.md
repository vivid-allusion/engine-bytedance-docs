---
title: "Setting up automatic mounting of disk partitions at startup"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts"
---

In Linux systems, you can configure the `fstab` file to set the Elastic Compute Service system to automatically mount disk partitions at startup.

This article describes how to use UUID in the `fstab` file to set up automatic mounting of disk partitions. It is not recommended to directly specify device names in `/etc/fstab` (such as `/dev/vdb1`), because the sequential encoding of devices in the cloud may change during the process of disabling or enabling the Elastic Compute Service. For example, `/dev/vdb1` could become `/dev/vdb2`, which may cause the Elastic Compute Service to fail to function properly after rebooting.

## Before you begin

The Data Volume has been created and mounted to the ECS instance. For specific steps, [refer to creating Volumes](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) and [refer to mounting Volumes](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

## Background information

UUID (universally unique identifier) is a unique string of identifiers provided by the Linux system for disk partitions.

## Procedures

1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the `blkid disk partition` command to query the UUID of the disk partition.

   For example, query the UUID of the disk partition `/dev/vdc1`:

   ```Shell
   blkid /dev/vdc1
   ```

   The output is similar to the following information:

   ```Shell
   [root@ecs-test-0001 ~]# blkid /dev/vdc1
   /dev/vdc1: UUID="0b3040e2-1367-4abb-841d-ddb0b926****" TYPE="ext4"
   ```

   This indicates the UUID of `/dev/vdc1`.

3. Execute the following command to open the `fstab` file using the VI editor.

   ```Shell
   vi /etc/fstab
   ```

4. press`i`to enter edit mode and add the following file information.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_95436ac8076b9bd661a8e8a1cf4f276d.png)

   For example content only; please base specifics on actual conditions. The argument Description is as follows:

   * The first column is the UUID, where you should fill in the UUID of the disk partition queried in the step.

   * The second column is the mount directory of the disk partition, which can be queried using the `df -TH` command.

   * The third column represents the file system format of the disk partition, and it can be queried using the `df -TH` command.

   * The fourth column represents the mount options of the disk partition; usually, the default settings will suffice here.

   * The fifth column represents the Linux dump backup options.

      * 0 means Linux dump backups are not used Dump backups are usually not used now; setting this to 0 will suffice.

      * 1 means Linux dump backups are used.

   * The sixth column represents the fsck options, which determine whether fsck checks the disk at startup.

      * 0 means no checks are performed.

      * Mount point is`/`For the partition of the root directory, this must be set to 1.

      * Set the root partition to 1, and other partitions can only start from 2. The system will check sequentially in ascending numerical order.

5. Press ESC and then `input :wq`, press Enter to save the settings and exit the editor.

6. Execute the "umount" disk partition command to unmount the mounted partition.

   For example, to unmount `/dev/vdc1`, the example command is as follows:

   ```Shell
   umount /dev/vdc1
   ```

7. Execute the `mount -a` command to reload all contents of the `/etc/fstab` file.

8. Execute the `mount | grep mount directory` command to query file system mount information.

   For example, to query `/dev/vdc1`, the example command is as follows:

   ```Shell
   mount | grep /mnt/sdc
   ```

   The echo displays information similar to the following, indicating that the automatic mounting feature has been enabled:

   ```Shell
    root@ecs-test-0001 ~]# mount | grep /mnt/sdc
       /dev/vdc1 on /mnt/sdc type ext4 (rw,relatime,errors=remount-ro,data=ordered)
   ```

## Related action

If you want to disable automatic mounting of disk partitions on startup, you can comment out the automatic mounting commands in the `/etc/fstab` file.

1. [Log in to the Linux instance through the console](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run the following command to edit `/etc/fstab`.

   ```Shell
   vim /etc/fstab
   ```

3. Add information before automatic mounting`#`, comment out the disk auto\-mount command at startup, then save and exit `/etc/fstab`.

   ```Shell
   # UUID=0b3040e2-1367-4abb-841d-ddb0b926**** /mnt/sdc ext4 defaults,errors=remount-ro 0 2
   ```
