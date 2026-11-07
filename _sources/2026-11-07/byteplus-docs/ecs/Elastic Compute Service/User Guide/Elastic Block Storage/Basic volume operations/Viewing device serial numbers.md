---
title: "Viewing device serial numbers"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/View-a-volume-serial-number"
---

A serial number is a unique identifier for a device that distinguishes it from other devices. This topic describes how to view the serial number of a device on a Linux or Windows instance.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Constraints and limitations

The operations described in this guide apply only to ESSD volumes and do not apply to PTSSD volumes or local disks.

<span id=".5ZyoTGludXjlrp7kvovmn6XnnIvno4Hnm5jluo_liJflj7c="></span>
## Viewing device serial numbers on Linux instances


1. [Use the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to get information about the device.

   ```Bash
   lsblk
   ```
   

   You will see output similar to the following:

   ```Bash
   NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   vda    253:0    0   40G  0 disk
   ├─vda1 253:1    0  200M  0 part /boot/efi
   └─vda2 253:2    0 39.8G  0 part /
   vdb    253:16   0   40G  0 disk
   └─vdb1 253:17   0  9.8G  0 part
   ```
   

   Obtain the device name from the output.

3. Run this command to obtain the serial number of the device.

   ```Bash
   udevadm info --query=all --name=<device name> | grep SERIAL
   ```
   

   Example:

   ```Bash
   udevadm info --query=all --name=vdb | grep SERIAL
   ```
   

   You will see output similar to the following:

   ```Bash
   E: ID_SERIAL=lq7n6xu2rdh8mjj9****
   ```
   


<span id=".5ZyoV2luZG93c-WunuS-i-afpeeci-ejgeebmOW6j-WIl-WPtw=="></span>
## Viewing device serial numbers on Windows instances


1. [Use the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. In the search bar next to the "Start" button, type `PowerShell`.

3. Click "Windows PowerShell".

4. Run this command to get information about the device.

   ```PowerShell
   Get-CimInstance -ClassName Win32_LogicalDiskToPartition |select Antecedent, Dependent |fl
   ```
   

   You will see output similar to the following:

   ```PowerShell
   Antecedent : Win32_DiskPartition (DeviceID = "Disk #0, Partition #1")
   Dependent  : Win32_LogicalDisk (DeviceID = "C:")
   
   Antecedent : Win32_DiskPartition (DeviceID = "Disk #1, Partition #0")
   Dependent  : Win32_LogicalDisk (DeviceID = "D:")
   ```
   

   Obtain the device ID from the output.

5. Run this command to obtain the serial number of the device.

   ```PowerShell
   Get-Disk |select Number, SerialNumber
   ```
   

   You will see output similar to the following:

   ```PowerShell
   Number SerialNumber
   ------ ------------
        0 in2jach25ii30xzx****
        1 in2ii1pk4pi30y32****
   ```
   

   Obtain the serial number based on the device ID.
