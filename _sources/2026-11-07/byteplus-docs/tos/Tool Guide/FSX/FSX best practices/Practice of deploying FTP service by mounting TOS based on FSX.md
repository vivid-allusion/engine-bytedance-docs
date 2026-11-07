---
title: "Practice of deploying FTP service by mounting TOS based on FSX"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Practice_of_deploying_FTP_service_by_mounting_TOS_based_on_FSX"
---

Mounting the object storage (TOS) bucket as a local file system directory through FSX allows traditional applications (such as FTP services) to directly access and operate objects stored in TOS without code changes, fully leveraging its massive storage capacity, high reliability, and cost\-effectiveness. This article explains how to deploy an FTP Server using FSX mounting to provide FTP/FTPS services, enabling clients (using FileZilla as an example) to easily read and write files to TOS.

<span id="5184ff68"></span>
## Prerequisites


* A Linux cloud server with a [public IP bound](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP), running normally and with administrator privileges.

* A bucket created in object storage to store files uploaded via FTP.

* The network environment (firewall, security group) allows external clients to access the ports required for FTP/FTPS.


<span id="b9807385"></span>
## Software versions


* Linux operating system: CentOS 7.6 is used as an example in this article.

* FTP client: FileZilla is used as an example in this article.

* FTP server: this article uses Vsftpd 3.0.2 as an example.


<span id="8374cc36"></span>
## Steps

<span id="80931c2b"></span>
### 1. Install FSX

Complete the download and installation of the FSX client according to the official document [Download and install FSX](https://docs.byteplus.com/docs/tos/Install-fsx) guide.

<span id="b807baa0"></span>
### 2. Mount the object storage bucket

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><code>tos_allow_delete</code> and <code>tos_incremental_upload</code> are new required parameters for FTP scenarios. Other parameters are optional and can be configured according to actual needs.</div>


<span id="dd103c9c"></span>
#### Key\-based mount

A key\-based mount uses the long\-term access key ID and secret access key to mount a bucket on Linux via FSX. Key\-based mounts do not depend on specific cloud infrastructure environments and support mounting buckets on various Linux systems. For more information, see [Operating environment](https://docs.byteplus.com/docs/tos/Overview#e82382a8).


1. Type this command into your Linux terminal to create a mount point.

   ```Bash
   mkdir /mnt/point
   ```
   

2. Run this command to mount the bucket or a specific directory within it.

   
   <Tabs>
   <Tab zoneid="yXVAdWZ3s8" title="Mount a bucket">
   <TabTitle>Mount a bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Shell
   mount -t fsx /tos/<bucket name> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of the credentials file>",no_writeback_cache,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   Example:
   
   ```Shell
   mount -t fsx /tos/bucketname /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",credential_filepath="/root/credential.json",no_writeback_cache,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   
   </Tab>
   <Tab zoneid="NSStBbElrU" title="Mount a specific directory within the bucket">
   <TabTitle>Mount a specific directory within the bucket</TabTitle>
   
   Run this command to mount a specific directory within the bucket.
   
   ```Shell
   mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of the credentials file>",no_writeback_cache,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   Example:
   
   ```Shell
   mount -t fsx /tos/bucketname:/dir /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",credential_filepath="/root/credential.json",credential_timeout_sec=100,no_writeback_cache,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

3. Run this command to verify that the mount was successful.

   ```Shell
   df -h
   ```
   

   If successful, the command returns output containing the mount point and bucket name.

   ```Shell
   Filesystem                  Size   Used Avail Use% Mounted on
   BFA281845F:tos-fuse-test    8.0E      0  8.0E   0% /mnt/fuse_shm
   ```
   


<span id="e5201072"></span>
#### Passwordless mount

A passwordless mount uses temporary security credentials provided by Security Token Service (STS), instead of long\-term access key credentials, to verify identity when mounting buckets via FSX. This method avoids exposing long\-term Access Key credentials, ensuring key security within the account.


1. Create an IAM role for ECS and bind it to your ECS instance. Then, obtain the role TRN. For detailed instructions, see [Authorize ECS to access other cloud resources based on instance IAM roles](https://docs.byteplus.com/en/docs/ecs/Authorize_ECS_to_access_other_cloud_resources_based_on_instance_IAM_roles).

2. Type this command into your Linux terminal to create a mount point.

   ```Bash
   mkdir /mnt/point
   ```
   

3. Run this command to mount the bucket or a specific directory within it.

   
   <Tabs>
   <Tab zoneid="B1Jq16hhTF" title="Mount a bucket">
   <TabTitle>Mount a bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name> <mount point> -o region="<your region>",endpoint="<your endpoint>",tos_auth_role_trn=<role TRN>,tos_auth_type=IMDS,no_writeback_cache,file_mode=777,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   Example:
   
   ```Shell
   mount -t fsx /tos/bucketname /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",tos_auth_role_trn=trn:iam::210671****:role/fsx_role2,tos_auth_type=IMDS,no_writeback_cache,file_mode=777,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   
   </Tab>
   <Tab zoneid="P71AOewmeo" title="Mount a specific directory within the bucket">
   <TabTitle>Mount a specific directory within the bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",tos_auth_role_trn=<role TRN>,tos_auth_type=IMDS,no_writeback_cache,file_mode=777,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   Example:
   
   ```Shell
   mount -t fsx /tos/bucketname:/dir /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",tos_auth_role_trn=trn:iam::210671****:role/fsx_role2,tos_auth_type=IMDS,no_writeback_cache,file_mode=777,dir_mode=777,tos_allow_delete=true,tos_incremental_upload=true
   ```
   
   
   
   </Tab>
   </Tabs>
   

4. Run this command to verify that the mount was successful.

   ```Bash
   df -h
   ```
   

   If successful, the command returns output containing the mount point and bucket name.

   ```Shell
   Filesystem      Size   Used Avail Use% Mounted on
   BFAACBA3B3:bucketname  8.0E     0  8.0E   0% /mnt/point
   ```
   


<span id="2a7ca270"></span>
#### Parameter description

The following introduces the basic parameters for mounting a bucket using the FSX client. You can also set parameters such as preheat and read cache when mounting the bucket. For more information, see [FSX mounting parameter description](https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description).


|Parameter |Description |
|---|---|
|`region` |The region of the bucket that you want to mount. |
|`endpoint` |TOS access domain name, supporting the format `https://{host}:{port}`. |
|`credential_filepath` |The absolute path to the JSON credential file containing AK/SK/STS. |
|`no_writeback_cache` |Disable write\-back cache. When disabled, data is written directly to object storage, suitable for scenarios requiring high data consistency. |
|`file_mode` |The default file permission after mounting is 777 (read/write/execute for all users). |
|`dir_mode` |The default permissions for the mounted directory are 777. |
|`tos_allow_delete` |Allow direct deletion of objects/files on TOS via the mount directory. |
|`tos_incremental_upload` |Enable incremental upload (typically means chunked/on\-demand upload to reduce overall retransmission overhead). |
|`num_prefetch_threads` |Number of prefetch threads used to optimize read performance. |
|`allow_other` |Allow other system users (such as the vsftpd user) to access the mount point.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Using this option requires modifying the /etc/fuse.conf file to uncomment <code>user_allow_other</code>.</div><br> |


<span id="f1b63b47"></span>
### 3. Install and configure FTP/FTPS service

Build the FTP site according to the guide document. For detailed steps, see [Set up FTP site (CentOS 7.6)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Linux).

<span id="0c863ae9"></span>
### 4. Bind the FSX mount point as the FTP service directory

After completing the FSX mount and FTP site setup, bind the FSX mount point to the FTP service directory using the following command.

```Shell
# /mnt/point  FSX example mount point (TOS directory mounted locally)
# /home/ftp   Example root directory of FTP service (directory accessible to the outside world)
sudo mount --bind /mnt/point /home/ftp
```


Verify the binding with the `mount | grep '/home/ftp'` command. If the output matches the following, the binding is successful.

```Shell
BFAACBA3B3:bucketname:/data on /home/ftp type hpvs_fs (rw,nosuid,nodev,relatime,user_id=0,group_id=0,default_permissions,allow_other,dev=39)
```


<span id="b7bf3a6d"></span>
### 5. Connect to the cloud server remote site

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">The file transfer type must be set to binary for uploading; otherwise, breakpoint resume is not supported.</div>


* <div data-tips="true" data-tips-type="warning">The request timeout defaults to 20 seconds. Increase the time if requests fail.</div>


1. Download and install [FileZilla](https://www.filezilla.cn/download/client) on your local computer.

2. Double\-click FileZilla to open the client.

   * In the FileZilla navigation bar, enter the information below and click **Quickconnect (Q)** .

   * Host: The public IP of the cloud server. Log in to the [Cloud Server Console](https://console.byteplus.com/ecs/instance) to view the public IP of the corresponding cloud server in the instance list.

   * Username: the FTP user account set when configuring the FTP service. This article uses ftptest as an example.

   * Password: the FTP user password set when configuring the FTP service.

   * Port: FTP's default listening port is 21.

   Once connected successfully, you can view remote site files on the cloud server.

3. Upload files: in the lower pane under **Local Site** on the left side of FileZilla, right\-click the local file to upload and select **Upload** to transfer the file to the cloud server.

4. Download files: in the lower pane under **Remote Site** on the right side of FileZilla, right\-click the remote site file to download and select **Download** to save the file to your local computer.


<span id="b2d24e2b"></span>
## Related documentation

[Set up FTP site (Ubuntu 22.04)](https://docs.byteplus.com/en/docs/ecs/Setting_up_FTP_sites_Ubuntu)

[Set up an FTP site (Windows 2019)](https://docs.byteplus.com/en/docs/ecs/Building-an-FTP-site-Windows)
