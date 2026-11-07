---
title: "Mounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX"
---

This topic demonstrates how to mount a file system on an ECS instance, using CentOS as an example.

<span id="GtNQrwxS"></span>
## Notes


* We recommend mounting the file system on Linux using FSX, which is not available on Windows and macOS. For more notes, see [Usage limits](https://docs.byteplus.com/en/docs/nas/efs_FSX_overview#K0WB9pCP).

* If you have problems mounting, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001576) for help.


<span id="yMrUsZSd"></span>
## Prerequisites


* You have created a file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

* You have created an access point. For instructions, see [Creating an access point](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW). If you have configured IAM policies for the access point, then configure the access point policy as well. For more information, see [Configuring access point policies](https://docs.byteplus.com/en/docs/nas/efs_Configuring_access_point_policies).

* You have installed the FSX client. For more information, see [Installing FSX](https://docs.byteplus.com/en/docs/nas/efs_Installing_FSX).

* You have created an ECS instance within the same VPC as the access point. For instructions, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For optimal performance, deploy your file system and ECS instance in the same availability zone.   </div>
   

<span id="Zx656n6d"></span>
## Steps


1. Log in to the ECS instance on which you want to mount the file system. For instructions, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to create the mount directory.

   ```Plain
   mkdir <mount directory>
   ```
   

   In this example, the mount directory is `/localdir`.

   ```Plain
   mkdir /localdir
   ```
   

3. (Optional) Configure account authentication credentials.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If IAM policies are enabled for the access point and an access point policy is configured, you must complete this step to specify the AK/SK of your account.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After an access point policy is configured, any policy changes (including modifications or additions) take effect in about 90 seconds.   </div>
   

   FSX supports multiple ways to configure AK/SK credentials. If multiple authentication methods are configured simultaneously, they take effect in the following priority order:

   `Specify AK/SK in mount command` \> `Specify credential file in mount command` \> `Set AK/SK via environment variables` \> `Set credential file via environment variables` \> `Add IAM credentials to global credential file in user’s HOME directory` \> `Add IAM credentials to FSX credential file in user’s HOME directory` \> `Add IAM credentials to FSX credential file in system shared directory`

   The authentication method is specified as follows:

   
   |**Mode** |**Description** |
   |---|---|
   |Specify AK/SK in mount command |When FSX mounts an EFS access point, account authentication credentials are required. You can specify the account's AK/SK information directly in the mount command. The parameters for specifying AK/SK are `-o access_key_id=<ak_string>,secret_access_key=<sk_string>[,security_token=<sts_string>]`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Specifying AK/SK in the mount command carries a risk of AK/SK exposure.</div><br> |
   |Specify credential file in mount command |When FSX mounts an EFS access point, account authentication credentials are required. You can specify the authentication credential file in the mount command using the parameter `-o credential_filepath=/path/to/credentials`.<br><br>The credential file extension must be `json`, with the following format:<br><br>```JSON```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   |Set AK/SK via environment variables |You can configure **VOLC_ACCESSKEY**, **VOLC_SECRETKEY**, and **VOLC_SECURITY_TOKEN** in environment variables to specify AK/SK. |
   |Set credential file via environment variables |You can configure **VOLC_CREDENTIAL_FILE** in environment variables to specify the credential file path.<br><br>The credential file extension must be `json`, with the following format:<br><br>```JSON```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   |Add credentials to global credential file in user’s HOME directory |Add the following information to the `~/.volc/credentials` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>",```<br>```"VOLC_SECRETKEY": "<sk_string>",```<br>```"VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   |Add credentials to FSX credential file in user’s HOME directory |Add the following information to the `~/.passwd-fsx` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>",```<br>```"VOLC_SECRETKEY": "<sk_string>",```<br>```"VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   |Add credentials to FSX credential file in system shared directory |Add the following information to the `/etc/.passwd-fsx` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>",```<br>```"VOLC_SECRETKEY": "<sk_string>",```<br>```"VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   

4. Run this command to mount the file system.

   Log in to the [EFS console](https://console.byteplus.com/efs) and go to the Access point page to view and copy the mount command. Append `<mount directory>` after the mount command. For example, the mount directory in this topic is `/localdir`, so you need to append `/localdir` after the mount command. For instructions, see [Viewing access point mount commands](https://docs.byteplus.com/en/docs/nas/efs_Viewing_access_point_mount_commands).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Caution   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not mount the file system to the <code>/tmp</code> directory. Some operating systems automatically clean this directory, which may cause data loss.   </div>
   

   ```Plain
   mount -t fsx /efs/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.efs.ivolces.com:/ <mount directory>
   ```
   

   Example command:

   ```Bash
   mount -t fsx /efs/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.efs.ivolces.com:/ /localdir
   ```
   

   The mount command supports the `-o` option, which you can use to modify mount settings：

   ```Bash
   mount -t fsx -o rw /efs/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.efs.ivolces.com:/ <mount directory>
   ```
   

   The description for the `-o` parameter is as follows:

   
   |**Mount options** |**Description** |
   |---|---|
   |persist_dir |FSX needs disk space to save the inode map for recovery after any crashes. By default, this map is stored in the `/opt/tmp/fsx` directory. The disk space needed to store the inode map is proportional to the client’s memory size. A client with 1 TB memory may require up to 45 GB of disk space in extreme cases.<br><br>You can change the disk directory for inode map storage by specifying the mount option `-o persist_dir=/persist_dir`. |
   |enable_xattr |FSX disables support for xattr by default when mounting EFS file systems. You can enable xattr support by specifying the mount option `-o enable_xattr`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Caution</div><br><br><br><div data-tips="true" data-tips-type="warning">Enabling xattr support reduces performance by about 30%. Enable this option only when needed.</div><br> |
   |rw |Mount the file system with read\-write access. This permission is enabled by default. |
   |ro |Mount the file system as read\-only. This permission is disabled by default. Enable it with the `-o ro` option. |
   |access_key_id |Specify key information in the mount command.  |
   |secret_access_key ||
   |security_token ||
   |credential_filepath |Specify the file path containing credentials in the mount command. The file extension must be `json`, and the format is as follows:<br><br>```Bash```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   

5. Run this command to see the details of the file system mounted.

   ```Bash
   df -h
   ```
   


<span id="pHLtrecG"></span>
## Related operations

<span id="9LObNw61"></span>
### Unmounting access points

Run the `umount <mount directory>` command to unmount an access point in Linux.
