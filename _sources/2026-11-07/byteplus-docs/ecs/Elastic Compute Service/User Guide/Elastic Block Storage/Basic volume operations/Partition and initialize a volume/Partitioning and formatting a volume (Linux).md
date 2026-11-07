---
title: "Partitioning and formatting a volume (Linux)"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB"
---

This topic explains how to partition and format a data volume in the Linux operating system.

## Prerequisites

You have created a data volume and attached it to an ECS instance. For more information, see [Creating a volume](https://docs.byteplus.com/en/docs/ecs/Create-a-volume) and [Attaching a volume](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume).

## Notes

|Category |Description |
|---|---|
|Data security |Partitioning and formatting a data volume will erase all data. Make sure that there is no important data on the volume, or back up any important data first. |
|Selecting the partitioning scheme |* You must use GPT when your volume capacity is equal to or greater than 2 TiB.<br><br>* MBR is limited to disks of 2 TiB or smaller, whereas GPT supports up to 18 EB. The maximum size of a data volume is 32 TiB. |
|MBR partitioning scheme |MBR supports up to four primary partitions or three primary partitions and one extended partition. |
|Using extended partitions |An extended partition cannot be used directly and must be divided into logical partitions. |
|GPT partitioning scheme |GPT does not use primary, extended, or logical partitions. |
|Discarding changes in fdisk |If you made a mistake during partitioning, enter "q" to exit fdisk without saving changes. |
|Automatic mounting upon boot |The mount will be lost when your ECS instance reboots. You can edit the /etc/fstab file to set up automatic mounting at boot. For more information, see [Setting up automatic mounting of volume partitions upon boot](https://docs.byteplus.com/en/docs/ecs/Allowing-disk-partitions-to-be-automatically-mounted-during-restarts). |

## Partitioning and formatting a volume (≤ 2 TiB)

This guide uses CentOS 7.6 to demonstrate how to create a primary partition with **fdisk** after attaching a new data volume to an instance. The MBR partitioning scheme is used, the file system is `ext4`, and the partition is mounted to `/mnt/sdc`. Note that these steps may differ depending on the operating system, so use this guide for reference only.

1. View the newly added data volume.

   [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance). Then, run the `fdisk -l` command to view the newly added data volume.

2. Create a partition.

   Create a partition for the new data volume `/dev/vdc`.

   1. Run the `fdisk /dev/vdc` command to enter the partitioning tool.

   2. Enter `n` to start creating a partition. There are two types of partitions:

      * `p`: Primary partition.

      * `e`: Extended partition.

   3. Enter `p` to create a primary partition.

   4. Enter `1` to set the primary partition number to `1`.

      `Partition number` indicates the serial number of the primary partition. The valid range is 1 to 4.

   5. Enter `2048` as the first sector.

      For optimal performance, set the first sector to `2048`. The system will automatically suggest an available range for the first and last sectors. You can customize within that range or use the default values, but remember that the first sector must be smaller than the last sector.

      * `First sector` indicates the sector at which the partition begins. The valid range is 2048 to 209715199. The default value is 2048.

      * `Last sector` indicates the sector at which the partition ends. The valid range is 2048 to 41943039. The default value is 41943039.

      The following output indicates that a new partition has been added to the data volume.

      ```Plain Text
      Last sector, +sectors or +size{K,M,G} (2048-41943039, default 41943039): 
      Using default value 41943039
      Partition 1 of type Linux and of size 20 GiB is set
      
      Command (m for help): 
      
      ```

3. View the details of the new partition.

   1. Enter `p` to view the details of the partition.

   2. Enter `w` to write the changes to the partition table.

      You will see output similar to the following if the partition has been created successfully:

      ```Plain Text
      Command (m for help): w
      The partition table has been altered!
      
      Calling ioctl() to re-read partition table.
      Syncing disks.
      ```

4. Synchronize the partition table changes.

   Run the `partprobe` command to synchronize the new partition table with the operating system.

5. Format the partition.

   Different file systems support different partition sizes. Select a file system that best meets your business needs.

   Run this command to format the partition with the desired file system. Formatting takes time. Monitor the system status and do not exit.

   ```Shell
   # Set file system to ext4
   mkfs -t ext4 /dev/vdc1 
   ```

6. Mount the partition.

   1. Run the `mkdir _mount directory_` command to create a mount directory.

   2. Run the `mount _partition_ _mount directory_` command to mount the partition to the directory you have created.

   3. Run the `df -Th` command to verify the mount result.

      The following output indicates that the `/dev/vdc1` partition has been mounted to `/mnt/sdc`.

      ```Plain Text
      [root@i-IVwlb**** ~]# df -Th
       Filesystem     Type      Size  Used Avail Use% Mounted on
       /dev/vda1      ext4       39G  1.7G   38G   5% /
       devtmpfs       devtmpfs  4.1G     0  4.1G   0% /dev
       tmpfs          tmpfs     4.2G     0  4.2G   0% /dev/shm
       tmpfs          tmpfs     4.2G  9.1M  4.1G   1% /run
       tmpfs          tmpfs     4.2G     0  4.2G   0% /sys/fs/cgroup
       tmpfs          tmpfs     821M     0  821M   0% /run/user/0
       /dev/vdb       xfs        21G   34M   21G   1% /data
       /dev/vdc1      ext4       21G   47M   20G   1% /mnt/sdc
      ```

## Partitioning and formatting a volume (\> 2 TiB)

This guide uses CentOS 7.6 to demonstrate how to create a partition with `parted` after attaching a new data volume to an instance. The GPT partitioning scheme is used, the file system is `ext4`, and the partition is mounted to `/mnt/sdc`.

1. Install the partitioning tool.

   Before formatting a volume on Linux, make sure that you have installed the parted and e2fsprogs packages for your Linux instance. Use the following commands to install the corresponding packages:

   * Run the `yum install -y parted` command to install the parted package.

   * Run the `yum install -y e2fsprogs` command to install the e2fsprogs package.

      * To check the version of the e2fsprogs package, run the `rpm -qa | grep e2fsprogs` command.

      * Use e2fsprogs version 1.42 or later if your volume is 16 TiB or larger, or if you plan to extend it to that size. Errors will occur during formatting if the e2fsprogs package version is below 1.42. For more information, see [How to upgrade e2fsprogs version for a Linux instance](https://docs.byteplus.com/en/docs/ecs/Partition-and-initialize-a-volume-less-than-or-equal-to-2-tiB?lang=en#0hpkIIEw).

2. View the newly added data volume.

   Run the `lsblk` command to view the newly added data volume.

3. Create a partition.

   Create a partition for the new data volume `/dev/vdb`.

   1. Run the `parted _new data volume_` command to start partitioning the new data volume.

   2. Enter `p` to view the current partitioning scheme.

      `Partition Table: unknown` means that the new data volume has not yet been configured with a partitioning scheme.

   3. Run the `mklabel _partitioning scheme_` command to set the partitioning scheme for your volume.

      * There are two schemes available: MBR and GPT. Run the `mklabel gpt` command to use GPT.

      * Once a volume is in use, changing its partitioning scheme will erase all existing data. Choose the partitioning scheme carefully during initialization.

   4. Enter `p` again to verify the partitioning scheme.

      `Partition Table: gpt` means that the partitioning scheme for your volume is GPT.

   6. Enter `unit` to set the measurement unit to sectors.

   7. Run the command `mkpart _partition name first sector_ _last sector_` to create a partition that uses the entire volume space,

      For optimal performance, set the first sector to `2048`. The system will automatically suggest an available range for the first and last sectors. You can customize within that range or use the default values, but remember that the first sector must be smaller than the last sector.

      * `First sector` indicates the sector at which the partition begins. The valid range is 2048 to 209715199. The default value is 2048.

      * `Last sector` indicates the sector at which the partition ends. The valid range is 2048 to 41943039. The default value is 41943039.

4. View the details of the new partition.

   1. Enter `p` to view the details of the partition.

   2. Enter `q` to exit parted.

      You will see output similar to the following:

      ```Shell
      (parted) q
      Information: You may need to update /etc/fstab.
      ```

      The `/etc/fstab` file is where you can set up automatic mounting of your partitions at boot time. To do so, format your partition with a file system and mount it. Then, refer to the relevant documentation to edit the `/etc/fstab` file.

   3. Run the `lsblk` command to view the partition you have created.

5. Format the partition.

   Run the `mkfs -t ext4 /dev/vdb1` command to format the partition with an `ext4` file system.

   * Formatting takes time. Monitor the system status and do not exit.

   * Different file systems support different partition sizes. Select a file system that best meets your business needs.

6. Mount the partition.

   1. Run the `mkdir /mnt/sdc` command to create the mount directory `/mnt/sdc`.

   2. Run the `mount /dev/vdb1 /mnt/sdc` command to mount the partition to `/mnt/sdc`.

   3. Run the `df -Th` command to verify the mount result.

## How to upgrade e2fsprogs version for a Linux instance

Follow these steps to upgrade e2fsprogs to version 1.42 or higher:

1. Run the `rpm -qa | grep e2fsprogs` command to check the version of the e2fsprogs package.

2. Run this command to download version 1.42.8 of e2fsprogs. For download links, visit [e2fsprogs](https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/?spm=a2c4g.11186623.2.14.Pb5baW).

   ```Plain Text
   wget https://www.kernel.org/pub/linux/kernel/people/tytso/e2fsprogs/v1.42.8/e2fsprogs-1.42.8.tar.gz
   ```

3. Run the `tar xvzf e2fsprogs-1.42.8.tar.gz` command to extract the installation package.

4. Run the `cd e2fsprogs-1.42.8` command to enter the directory where the package is extracted.

5. Run the `./configure` command to generate a Makefile.

6. Run the `make` command to compile e2fsprogs.

7. Run the `make install` command to install e2fsprogs.

8. Once installation is complete, run the `rpm -qa | grep e2fsprogs` command to verify the version.
