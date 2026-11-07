---
title: "Solution of /etc/fstab configuration repair for Linux instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Linux_instance_fstab_configuration_repair_solution"
---

<span id="eXn9AAts"></span>
## Problem description

A Linux instance has a login failure via remote connection tools such as PuTTY. And during its remote login via VNC, emergency mode is triggered, or the instance diagnosis reports an abnormally mounted device in the /etc/fstab file.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69fe7b2a317533ab790f50148102b527.jpg) </span>

<span id="GaahMd6z"></span>
## Causes

In the /etc/fstab file, mounting information or disk partition information may be incorrectly written, or certain persistent information may cause instance startup failure after cold migration. The /etc/fstab file is used to specify file systems and other devices that need to be mounted during system startup. Incorrect file configurations can cause instance startup failure.

<span id="nd6qwW5c"></span>
## Solutions

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before you modify the configuration or data of an instance, we recommend that you <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">create a snapshot</a> first to improve fault tolerance and ensure data security.</div>


<span id="f5NE0fF2"></span>
### Step 1: Locate file configuration issues


1. Log in to the affected instance via VNC. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. After you enter the emergency mode interface, enter the login password of the root user and press the Enter key to enter emergency mode.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the password\-based login failure occurs as the root user, you can also enter<a href="https://docs.byteplus.com/en/docs/ecs/Booting-in-single-user-mode"> Linux one\-user mode</a> and repair the /etc/fstab file in this mode.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d7b595388a615af1ea448d82589d344.png) </span>

3. Execute the following command to remount the root partition in read\-write mode.

   ```Plain Text
   mount / -o remount,rw
   ```
   

4. Execute the following command to verify whether an error exists in the /etc/fstab file.

   ```Plain Text
   mount -a
   ```
   

   * If the returned information is `mount point does not exist`, this indicates that the mount point (which is `/test/mnt/b` in the following example) does not exist. You need to create the missing mount point or replace the mount point.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c760132cc5c08cdac2bab436f0ad427.png) </span>

   * If the returned information is `special device xxx does not exist` or `can't find xxx`, this indicates that the device does not exist. You can remove the block device that does not exist.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e39fd98a8c92a2c4cd02e322acc68f7.png) </span>

   * If the returned information is `an incorrect mount option was specified` or `Unrecognized mount option "xxx" or missing value`, this indicates that one or multiple mount parameters are incorrect. You need to modify such parameter to the correct one.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44d244da1eb56ac4ea1a8cb73ea182d0.png) </span>

   * If the returned information is `UNEXPECTED INCONSISTENCY;RUN fsck MANUALLY`, this is typically caused by file system errors. To fix the issue, refer to [Solution for handling file system corruption of Linux instances](https://docs.byteplus.com/en/docs/ecs/Repair_plan_for_damaged_file_system_of_Linux_instance).


<span id="DttmJ9iu"></span>
### Step 2: Repair the file

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before fixing the error in the /etc/fstab file, you need to:</div>



* <div data-tips="true" data-tips-type="default">Learn about <a href="https://docs.byteplus.com/en/docs/ecs/Linux_instance_fstab_configuration_repair_solution#GalrIr40">file format</a>.</div>


* <div data-tips="true" data-tips-type="default">Execute the <code>cp /etc/fstab /etc/fstab.bak</code> command to back up the /etc/fstab file.</div>



<span id="0DhXvWdJ"></span>
#### Create/replace a mount point


1. Create or replace a mount point based on your needs.

   
   <Tabs>
   <Tab zoneid="KKfHrD6sdC" title="Create the missing mount point">
   <TabTitle>Create the missing mount point</TabTitle>
   
   Execute the following command to create the missing mount point.
   
   ```Plain Text
   mkdir /test/mnt/b
   ```
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Replace <code>/test/mnt/b</code> with the actual mount point.</div>
   
   
   
   </Tab>
   <Tab zoneid="CAF2eoTQ33" title="Replace the mount point">
   <TabTitle>Replace the mount point</TabTitle>
   
   1. Execute the following command to open the /etc/fstab file.
   
      ```Plain Text
      vim /etc/fstab
      ```
      
   
   2. Press the `i` key to enter the edit mode. Based on the error prompts from step 1, modify the mount point of the target block device.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bb92d2f99accb1e72a8218629dfc6fa.png) </span>
   
   3. Press the `Esc` key to exit edit mode, enter `:wq`, and press the `Enter` key to save and exit the file.
   
   
   </Tab>
   </Tabs>
   

2. Execute the following command to confirm whether the error still exists in the /etc/fstab file.

   ```Plain Text
   mount -a
   ```
   

   No output indicates a successful repair.


<span id="TezoD7nC"></span>
#### Remove the block device that does not exist


1. Execute the following command to open the /etc/fstab file.

   ```Plain Text
   vim /etc/fstab
   ```
   

2. Press the `i` key to enter the edit mode. Based on the error prompts from step 1, add `#` at the beginning of the line corresponding to the non\-existent block device, to comment it out, or delete the mounting information of that line.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bb92d2f99accb1e72a8218629dfc6fa.png) </span>

3. Press the `Esc` key to exit edit mode, enter `:wq`, and press the `Enter` key to save and exit the file.

4. Execute the following command to confirm whether the error still exists in the /etc/fstab file.

   ```Plain Text
   mount -a
   ```
   

   No output indicates a successful repair.


<span id="S3b6KotL"></span>
#### Modify the incorrect mount option


1. Execute the following command to open the /etc/fstab file.

   ```Plain Text
   vim /etc/fstab
   ```
   

2. Press the `i` key to enter the edit mode. Based on the error prompts from step 1, modify the incorrect mount option, as `noexist` in the following picture.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1015da40ffe02ed82f5dc4eb3306d365.png) </span>

3. Press the `Esc` key to exit edit mode, enter `:wq`, and press the `Enter` key to save and exit the file.

4. Execute the following command to confirm whether the error still exists in the /etc/fstab file.

   ```Plain Text
   mount -a
   ```
   

   No output indicates a successful repair.


<span id="n9TOnusq"></span>
## Appendix

<span id="GalrIr40"></span>
### Description of /etc/fstab file arguments

In the /etc/fstab file, the format of each mount information line is `fs_spec fs_file fs_vfstype fs_mntops fs_freq fs_passno`. [Learn more](https://man7.org/linux/man-pages/man5/fstab.5.html).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d6704ae88064be7dc73ed9de28b997d.png) </span>


|**Parameter​**  |**Description** |
|---|---|
|fs_spec |Indicates mounted partitions or storage devices. Valid values:<br><br><br>* Device node. For example, /dev/vdb.<br><br>* UUID. For example, UUID=3e6bxxx\-8139.<br><br>* LABEL. For example, LABEL=root.<br><br>* NFS path. For example, host:/path.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend using the UUID of a partition or storage device. This can avoid issues in scenarios where the storage device order may change, such as after re\-plugging storage devices. You can execute the <code>blkid</code> command to query the UUID of a partition or storage device.</div><br> |
|fs_file |Specifies the absolute path of the mount point. For example, /mnt/test. |
|fs_vfstype |Specifies the file system type of a mounted partition or storage device. For example, `ext4`, `xfs`, `btrfs`, `f2fs`, `vfat`, and `ntfs`. |
|fs_mntops |Specifies mount options. Multiple mount options are connected by `,`. Value:<br><br><br>* `defaults`: Specifies default mount parameters of the file system to be used. For example, the default parameters of the `ext4` file system include `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, and `async`.<br><br>* For more mount options, view [mount](https://man7.org/linux/man-pages/man8/mount.8.html). |
|fs_freq |Specifies whether to use Dump to back up file system configurations. Value:<br><br><br>* 0: No backup with Dump.<br><br>* 1: Backup with Dump.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If Dump is not installed in your operating system, set the parameter to <code>0</code>. To install the Dump tool, execute the following commands:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Ubuntu/Debian: <code>sudo apt install -y dump</code></div><br><br><br>* <div data-tips="true" data-tips-type="default">RHEL/CentOS: <code>sudo yum install -y dump</code></div><br> |
|fs_passno |Specifies the order in which filesystem checks (fsck) are performed at boot time. Value:<br><br><br>* 0: Default value, indicating no check is performed.<br><br>* 1: Highest priority, indicating the check is performed for the root directory.<br><br>* 2: Indicates the check is performed for other devices that require inspection after the root directory check completes. |
