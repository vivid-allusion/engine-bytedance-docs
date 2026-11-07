---
title: "Mounting file systems"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Mounting_file_systems"
---

This topic demonstrates how to mount a file system on an ECS instance, using CentOS as an example.

<span id="92ca6eb8"></span>
## Notes


* We recommend mounting the file system on Linux using FSX, which is not available on Windows and macOS. For more notes, see [FSX overview](https://docs.byteplus.com/en/docs/nas/FSX_overview).

* If you have problems mounting, please contact the technical team for support.


<span id="8e8ead06"></span>
## Prerequisites


* The file system has been created. For detailed steps, see [Creating file systems](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system).

* The access point has been created. For specific steps, see [Creating access points](https://docs.byteplus.com/en/docs/nas/Managing_access_points#a4a6cb20). If IAM policies are enabled, you need to set up the access point policy as well. For more information, see [Configuring access point policies](https://docs.byteplus.com/en/docs/nas/Configuring_access_point_policies).

* The FSX client is installed. For specific steps, see [Installing FSX](https://docs.byteplus.com/en/docs/nas/Installing_FSX).

* The ECS instance has been created within the same VPC as the access point. For detailed steps, see [Using the wizard to buy ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For optimal performance, deploy your file system and ECS instance in the same availability zone.   </div>
   

<span id="477dd76e"></span>
## Steps


1. Log in to the ECS instance where the file system needs to be mounted. For detailed steps, see [Using the console to log on to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Run this command to create the mount path.

   ```Plain
   mkdir <directory to be mounted>
   ```
   

   Example folder: `localdir`.

   ```Plain
   mkdir /localdir
   ```
   

3. (Optional) Configure account authentication credentials.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If both IAM policies and access point policies are enabled, configure AK/SK credentials for your BytePlus account.   </div>
   

   FSX allows several ways to set up AK/SK credentials, and if you use multiple methods, they follow this priority order:

   Specify AK/SK in mount command \> Specify credential file in mount command \> Set AK/SK via environment variables \> Set credential file via environment variables \> Add IAM credentials to global credential file in user’s HOME directory \> Add IAM credentials to FSX credential file in user’s HOME directory \> Add IAM credentials to FSX credential file in system shared directory

   The authentication method is specified as follows:

   
   |**Mode** |**Description** |
   |---|---|
   |Specify AKSK in the mount command |When FSX mounts the FileNAS access point, account authentication credentials are required. You can specify the account's AK/SK information directly in the mount command. The parameters for specifying AK/SK are `-o access_key_id=&lt;ak_string&gt;,secret_access_key=&lt;sk_string&gt;[,security_token=&lt;sts_string&gt;]`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Specifying AKSK in the mount command carries a risk of AKSK exposure. Use with caution.</div><br> |
   |Specify credential file in mount command |When mounting a FileNAS access point with FSX, account authentication credentials are required. You can specify the authentication credential file in the mount command using the parameter `-o credential_filepath=/path/to/credentials`. The credential file extension must be `json`, with the following format:<br><br>```JSON```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   |Set AKSK via environment variables |You can configure **VOLC_ACCESSKEY**, **VOLC_SECRETKEY**, and **VOLC_SECURITY_TOKEN** in environment variables to specify AK/SK. |
   |Set credential file via environment variables |You can configure the **VOLC_CREDENTIAL_FILE** environment variable to specify the credential file path. The credential file extension must be `json`, with the following format:<br><br>```JSON```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   |Add credentials to global credential file in user’s HOME directory |Add the following information to the `~/.volc/credentials` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>","VOLC_SECRETKEY": "<sk_string>","VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   |Add credentials to FSX credential file in user’s HOME directory |Add the following information to the `~/.passwd-fsx` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>",```<br>```"VOLC_SECRETKEY": "<sk_string>",```<br>```"VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   |Add credentials to FSX credential file in system shared directory |Add the following information to the `/etc/.passwd-fsx` file:<br><br>```Bash```<br>```"VOLC_ACCESSKEY": "<ak_string>","VOLC_SECRETKEY": "<sk_string>","VOLC_SECURITY_TOKEN": "<sts_string>"```<br> |
   

4. Run this command to mount the file system.

   Log in to the [FileNAS console](https://console.byteplus.com/filenas/) and go to the Mount Target page to view and copy the mount command. Append `/ <mount directory>` after the mount command. For example, the mount directory in this topic is `/localdir`, so you need to append `/localdir` after the mount command. For detailed steps, see [Checking access point mount command](https://docs.byteplus.com/en/docs/nas/Viewing_access_point_mount_commands).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Avoid mounting the file system to the <code>/tmp</code> directory, as some operating systems have automatic cleaning mechanisms that could result in file loss in <code>/tmp</code> directory.   </div>
   

   ```Plain
   mount -t fsx /nas/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.nas-boe.ivolces.com:/ <mount_directory>
   ```
   

   Example commands:

   ```Bash
   mount -t fsx /nas/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.nas-boe.ivolces.com:/ /localdir
   ```
   

   The mount command supports the `-o` parameter. You can modify the mount configuration in the mount command using the `-o` parameter. The example command is as follows:

   ```Bash
   mount -t fsx -o rw /nas/ap-add014a0.cncq6a772736e012.2gctm5rzca3uo50ztyz****.cn-beijing.nas-boe.ivolces.com:/ <mount_directory>
   ```
   

   The description for the `-o` parameter is as follows:

   
   |**Mount options** |**Description** |
   |---|---|
   |persist_dir |FSX needs disk space to save the inode map for recovery after any crashes. By default, this map is stored in the `/opt/tmp/fsx` directory. The disk space needed to store the inode map is proportional to the client’s memory size. A client with 1 TB memory may require up to 45 GB of disk space in extreme cases. You can change the disk directory for inode map storage by specifying the mount option `-o persist_dir=/persist_dir`. |
   |enable_xattr |FSX disables support for xattr by default when mounting FileNAS file systems. You can enable xattr support by specifying the mount option `-o enable_xattr`.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enabling xattr support reduces performance by about 30%. Enable it according to your actual needs.</div><br> |
   |rw |Mount the file system with read\-write access, enabled by default. |
   |ro |Mount the file system as read\-only by default; enable with `-o ro`. |
   |access_key_id |Specify key information in the mount command. For detailed steps on obtaining Access Key ID and Secret Access Key, refer to [Access Key Management](https://docs.byteplus.com/en/docs/IAM/about-access-keys). |
   |secret_access_key ||
   |security_token ||
   |credential_filepath |Specify the file path containing credentials in the mount command. The file extension must be `json`, and the format is as follows:<br><br>```Bash```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   

5. Run this command to see the details of the file system mounted.

   ```Bash
   df -h
   ```
   


<span id="98c0686d"></span>
## Related actions

<span id="e883c65a"></span>
### Unmounting file systems

Execute the `umount <mount_directory>` command to unmount the file system in Linux.
