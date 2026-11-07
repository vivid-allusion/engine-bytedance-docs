---
title: "FAQs"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/FAQs"
---

This topic bundles together answers to frequently asked questions, and also error messages that you may encounter while using FSX.

<span id="d3NpBWYl"></span>
## Background information

If you encounter any issues while using FSX, we recommend first running the `/opt/fsx/tools/sysinfo_collector.sh` script. This script automatically collects file system information, access point details, system logs, and other relevant data. Then, it generates a compressed file named `system_info__.tar.gz` in the script's directory. Submit this file [via a ticket](https://console.byteplus.com/workorder/create), and our team will help resolve the issue.

<span id="qa8MnBxh"></span>
## Mounting FAQs

<span id="570lTk5p"></span>
### Error: "failed to check auth" during mounting


* #### Cause <span id="AUBSo47C"></span>

   You have enabled access point IAM policies for your EFS file system, but the provided Access Key ID or Secret Access Key is either incorrect or lacks sufficient permissions.

* #### Solution <span id="sC39W7sG"></span>

   * Verify that the Access Key ID and Secret Access Key entered during mounting are correct.

   * Make sure the account associated with the provided Access Key ID and Secret Access Key has the necessary permission for the access point.


<span id="oRc0sVpz"></span>
### Error: "Mount target directory is not exist" during mounting


* #### Caused  <span id="Z8I4aPhQ"></span>

   #### You did not create the mount directory before mounting the access point.    <span id="8LXMATZj"></span>

* #### Solution <span id="Adiaui3b"></span>

   Create a mount directory before mounting. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX).


<span id="E6PyJkqY"></span>
### Issue: After mounting an EFS file system with FSX, rebooting a Linux system using the command `reboot -t` causes the system to become unresponsive.


* #### Cause <span id="Aghp7NyV"></span>

   The reboot process was initiated without first unmounting the access point. In this case, the `reboot` command terminates all user processes (including FSX) before running the `umount` command. Since FSX supports crash recovery, the `umount` operation does not fail immediately. Instead, it waits for FSX to recover, causing the `reboot` command to hang.

* #### Solution <span id="D9KfDOB1"></span>

   Force restart the system, or wait for FSX to complete recovery. The system will automatically resume rebooting.


<span id="D4kEuZpd"></span>
## Unmounting FAQs

<span id="uNEE6ZLV"></span>
### Error: "target is busy" during unmounting


* #### Cause <span id="MfHNnMQ5"></span>

   Unmounting will fail if there are still active processes accessing the mount directory.

* #### Solution <span id="QuhfS647"></span>

   To resolve the issue, follow these steps (using `/mnt/point` as an example):

   1. Identify the processes using the `lsof /mnt/point` command.

   2. Force close the processes accessing the mount directory.

   3. Try unmounting again using the `umount /mnt/point` command.
