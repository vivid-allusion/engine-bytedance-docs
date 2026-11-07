---
title: "FAQs"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/fsx-client-FAQs"
---

This topic bundles together answers to frequently asked questions, and also error messages that you may encounter while using FSX.

<span id="5e25f7d1"></span>
## Background information

If you encounter any issues while using FSX, we recommend first running the `/opt/fsx/tools/sysinfo_collector.sh` script. This script automatically collects file system information, mount target details, system logs, and other relevant data. Then, it generates a compressed file named `system_info__.tar.gz` in the script's directory. 

<span id="ffba86c3"></span>
## Mounting FAQs

<span id="4e912722"></span>
### Error: "failed to check auth" during mounting


* What it means

   You have enabled access point IAM policies for your FileNAS file system, but the provided Access Key ID or Secret Access Key is either incorrect or lacks sufficient permissions.

* How to fix it

   * Verify that the Access Key ID and Secret Access Key entered during mounting are correct.

   * Make sure the account associated with the provided Access Key ID and Secret Access Key has the necessary permission for the access point.


<span id="c8994fa2"></span>
### Error: "Mount target directory does not exist" during mounting


* What it means

   You did not create the mount directory before mounting the access point.

* How to fix it

   Create a mount directory before mounting. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/Mounting_file_systems).


<span id="0fb1c054"></span>
### Issue: After mounting a FileNAS file system with FSX, rebooting a Linux system using the command reboot \-t causes the system to become unresponsive.


* What it means

   The reboot process was initiated without first unmounting the FileNAS file system. Since FSX supports crash recovery, the `reboot` command attempts to terminate all user processes (including FSX) before unmounting. However, the `umount` operation does not immediately fail. Instead, it waits for FSX to recover, which causes the `reboot` command to hang.

* How to fix it

   Force restart the system, or wait for FSX to complete recovery. The system will automatically resume rebooting.


<span id="6b008058"></span>
## Unmounting FAQs

<span id="231e635f"></span>
### Error: "target is busy" during unmounting


* What it means

   Unmounting will fail if there are still active processes accessing the mount directory.

* How to fix it

   To resolve the issue, follow these steps (using `/mnt/point` as an example):

   1. Identify the processes using the `lsof /mnt/point` command.

   2. Force close the processes accessing the mount directory.

   3. Try unmouting again using the `umount /mnt/point` command.
