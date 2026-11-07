---
title: "Configuration and mounting"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting"
---

This topic introduces notes and steps for mounting buckets via FSX.

<span id="a0603b4b"></span>
## Prerequisites

You have installed FSX. For instructions, see [Downloading and installing FSX](https://docs.byteplus.com/docs/tos/Install-fsx).

<span id="c4636f81"></span>
## Permissions

<span id="b5294119"></span>
### Permissions required to mount a bucket

If you are an Identity and Access Management (IAM) user, you must have the necessary permissions to mount a bucket and perform relevant operations. Otherwise, the mount or operation will fail. Specifically:


* Mounting a bucket requires ListBucket and HeadBucket permissions.

* Reading objects within the mounted bucket requires GetObject permission.

* Writing objects to the mounted bucket requires PutObject and AbortMultipartUpload permissions.

* Deleting objects from the mounted bucket requires DeleteObject permission.


Buckets with server\-side encryption (SSE\-KMS) require additional Key Management Service (KMS) permissions for reading and writing objects. To upload objects with SSE\-KMS, you need the `kms:GenerateDataKey` permission. To download SSE\-KMS\-encrypted objects, you need the `kms:Decrypt` permission. For more information, see [Server-side encryption overview](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview).

The example below illustrates a minimal set of permissions in an IAM policy.

```Bash
{
        "Statement": [{
                "Effect": "Allow",
                "Action": [
                        "tos:GetObject",
                        "tos:PutObject",
                        "tos:DeleteObject",
                        "tos:AbortMultipartUpload",
                        "tos:ListBucket",
                        "tos:HeadBucket"
                ],
                "Resource": [
                        "*"
                ]
        }]
}
```


You can add more actions to the policy statement to grant the IAM user additional permissions as needed. For actions supported by IAM policies, see [IAM policy overview](https://docs.byteplus.com/en/docs/tos/docs-configuring-an-iam-policy).

After confirming which permissions to grant, create a customer\-managed permission policy using the[ IAM console](https://console.byteplus.com/iam/). Then, assign the policy to the IAM user. For instructions, see [Configuring IAM policies](https://docs.byteplus.com/en/docs/tos/docs-configuring-an-iam-policy) and [Adding authorization](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

<span id="d6420c89"></span>
### Permissions to access the mounted bucket

By default, the UID and GID of the FSX process own all the objects and directories in the mounted bucket. These objects have 644 permissions and these directories have 755 permissions. You can modify these attributes using the `chown` and `chmod` commands. You can also override the default values by specifying the `uid`, `gid`, `file_mode`, and `dir_mode` parameters when mounting the bucket.

These parameters are explained below.


|**Parameter** |**Required** |**Description** |
|---|---|---|
|uid |No |The user ID (UID) that will be assigned as the owner of files or directories. |
|gid |No |The group ID (GID) that will be assigned as the group owner of objects or directories. |
|file_mode |No |The permission mode for objects. The default value is 644. |
|dir_mode |No |The permission mode for directories. The default value is 755. |


Example:

Set the file_mode and dir_mode parameters to 777 (chmod 777). This gives all users access to the objects and directories within the mounted bucket.

```Bash
mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of the credentials file>",no_writeback_cache,file_mode=777,dir_mode=777
```


<span id="ed31778a"></span>
## Key\-based mount

A key\-based mount uses the long\-term access key ID and secret access key to mount a bucket on Linux via FSX. A key\-based mount does not rely on a specific cloud infrastructure and can mount buckets on various Linux systems. For more information, see [Operating environment](https://docs.byteplus.com/docs/tos/Overview#e82382a8).


1. Type this command into your Linux terminal to create a mount point.

   ```Bash
   mkdir /mnt/point
   ```
   

2. Run this command to mount the bucket or a specific directory within it.

   
   <Tabs>
   <Tab zoneid="ncD8WBfI46" title="Mount a bucket">
   <TabTitle>Mount a bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of the credentials file>",no_writeback_cache
   ```
   
   
   Example:
   
   ```Bash
   mount -t fsx /tos/bucketname /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",credential_filepath="/root/credential.json",no_writeback_cache
   ```
   
   
   
   </Tab>
   <Tab zoneid="GxRh63xYvB" title="Mount a specific directory within the bucket">
   <TabTitle>Mount a specific directory within the bucket</TabTitle>
   
   Run this command to mount a specific directory within the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",credential_filepath="<absolute path of the credentials file>",no_writeback_cache
   ```
   
   
   Example:
   
   ```Bash
   mount -t fsx /tos/bucketname:/dir /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",credential_filepath="/root/credential.json",credential_timeout_sec=100,no_writeback_cache
   ```
   
   
   
   </Tab>
   </Tabs>
   

   The parameters are described below:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following section introduces the basic parameters for mounting buckets with FSX. You can also configure prefetch and read cache parameters when mounting a bucket. For more information, see <a href="https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description">Mount parameters</a>.   </div>
   

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |region |Yes |The region of the bucket that you want to mount. |
   |no_writeback_cache |Yes |Disables kernel page cache writeback, which ensures that write requests are sequential. |
   |endpoint |Yes |The endpoint that follows the TOS protocol. Endpoints that follow the S3 protocol are not supported. Unless otherwise specified, HTTPS is used by default in the format `https://{host}:{port}`. |
   |credential_filepath |No |The absolute path of the credentials file used to load the required access credentials. You need to create the credentials file yourself. The file must have a `json` extension and contain the following content:<br><br>```JSON```<br>```{```<br>```    "VOLC_ACCESSKEY": "<ak_string>",```<br>```    "VOLC_SECRETKEY": "<sk_string>",```<br>```    "VOLC_SECURITY_TOKEN": "<sts_string>"```<br>```}```<br> |
   |credential_timeout_sec |No |The refresh interval in seconds that FSX uses to dynamically update the credentials configuration file.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>credential_timeout_sec</code> and <code>credential_filepath</code> must be used together.</div><br> |
   |part_size |No |The size of each part for a multipart upload in MB. The default size is 8 MB, and valid sizes range from 4 to 5,120 MB. TOS limits a single multipart upload to a maximum of 10,000 parts. You can adjust the size of the final object by changing the part size. For instructions, see [Uploading large objects](https://docs.byteplus.com/docs/tos/Upload-large-files).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of <code>part_size</code> must be a positive integer.</div><br> |
   

3. Run this command to verify that the mount was successful.

   ```Bash
   df -h
   ```
   

   If successful, the command returns output containing the mount point and bucket name.

   ```Bash
   Filesystem                  Size   Used Avail Use% Mounted on
   BFA281845F:tos-fuse-test    8.0E      0  8.0E   0% /mnt/fuse_shm
   ```
   


<span id="14012d4a"></span>
## Passwordless mount

A passwordless mount uses temporary security credentials provided by Security Token Service (STS), instead of long\-term access key credentials, to verify identity when mounting buckets via FSX. Exposing long\-term access key credentials puts their security at risk. This method does not need these credentials.

<span id="6faf203c"></span>
### Mounting buckets to Elastic Compute Service (ECS) instances


1. Create an IAM role for ECS and bind it to your ECS instance. Then, obtain the role TRN. For instructions, see [Authorizing ECS instances to access cloud resources based on instance IAM roles](https://docs.byteplus.com/en/docs/ecs/Authorize_ECS_to_access_other_cloud_resources_based_on_instance_IAM_roles).

2. Type this command into your Linux terminal to create a mount point.

   ```Bash
   mkdir /mnt/point
   ```
   

3. Run this command to mount the bucket or a specific directory within it.

   
   <Tabs>
   <Tab zoneid="IDstEQKthT" title="Mount a bucket">
   <TabTitle>Mount a bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name> <mount point> -o region="<your region>",endpoint="<your endpoint>",tos_auth_role_trn=<role TRN>,tos_auth_type=IMDS,no_writeback_cache
   ```
   
   
   Example:
   
   ```Bash
   mount -t fsx /tos/bucketname /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",tos_auth_role_trn=trn:iam::210671****:role/fsx_role2,tos_auth_type=IMDS,no_writeback_cache
   ```
   
   
   
   </Tab>
   <Tab zoneid="Ir64wplJOw" title="Mount a specific directory within the bucket">
   <TabTitle>Mount a specific directory within the bucket</TabTitle>
   
   Run this command to mount the bucket.
   
   ```Bash
   mount -t fsx /tos/<bucket name>:/<bucket directory> <mount point> -o region="<your region>",endpoint="<your endpoint>",tos_auth_role_trn=<role TRN>,tos_auth_type=IMDS,no_writeback_cache
   ```
   
   
   Example:
   
   ```Bash
   mount -t fsx /tos/bucketname:/dir /mnt/point -o region="cn-beijing",endpoint="https://tos-cn-beijing.volces.com",tos_auth_role_trn=trn:iam::210671****:role/fsx_role2,tos_auth_type=IMDS,no_writeback_cache
   ```
   
   
   
   </Tab>
   </Tabs>
   

   The parameters are described below:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The following section introduces the basic parameters for mounting buckets with FSX. You can also configure prefetch and read cache parameters when mounting a bucket. For more information, see <a href="https://docs.byteplus.com/docs/tos/FSX-mount-parameter-description">Mount parameters</a>.   </div>
   

   
   |**Parameter** |**Required** |**Description** |
   |---|---|---|
   |region |Yes |The region of the bucket that you want to mount. |
   |endpoint |Yes |The endpoint that follows the TOS protocol. Endpoints that follow the S3 protocol are not supported. Unless otherwise specified, HTTPS is used by default in the format `https://{host}:{port}`. |
   |tos_auth_role_trn |Yes |The temporary access credentials. Enter the role TRN obtained in Step 1. |
   |tos_auth_type |Yes |Specifies whether it is a key\-based or passwordless mount. When mounting the bucket on an ECS instance, set this parameter to `IMDS`. |
   |no_writeback_cache |Yes |Disables kernel page cache writeback, which ensures that write requests are sequential. |
   |part_size |No |The size of each part for a multipart upload in MB. The default size is 8 MB, and valid sizes range from 4 to 5,120 MB. TOS limits a single multipart upload to a maximum of 10,000 parts. You can adjust the size of the final object by changing the part size. For instructions, see [Uploading large objects](https://docs.byteplus.com/docs/tos/Upload-large-files).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The value of <code>part_size</code> must be a positive integer.</div><br> |
   

4. Run this command to verify that the mount was successful.

   ```Bash
   df -h
   ```
   

   If successful, the command returns output containing the mount point and bucket name.

   ```Bash
   Filesystem      Size   Used Avail Use% Mounted on
   BFAACBA3B3:bucketname  8.0E     0  8.0E   0% /mnt/point
   ```
   


<span id="07f2f303"></span>
### Mounting buckets to Vital Kubernetes Engine (VKE) pods

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Authentication with IAM roles for service accounts (IRSA) can be enabled only after the cluster is created. To use the IRSA authentication capability of the csi\-fsx add\-on, do not install the add\-on when creating the cluster.</div>


* <div data-tips="true" data-tips-type="warning">Once IRSA authentication has been enabled for the csi\-fsx add\-on, it is not possible to directly switch to a different authentication method. To use a different method, uninstall the add\-on and reinstall it.</div>


* <div data-tips="true" data-tips-type="warning">IRSA authentication cannot be used when IRSA OIDC is not enabled.</div>


* <div data-tips="true" data-tips-type="warning">The IAM role must fall within the OIDC identity provider type and have a trust relationship bound to the service account of the add\-on.</div>


* <div data-tips="true" data-tips-type="warning">Once the csi\-fsx add\-on is installed, the authentication method cannot be changed. However, you can change the IAM role. This change only applies to new PersistentVolumes (PVs) and does not affect existing PVs. Additionally, note that changing IAM roles will trigger a brief restart of the add\-on. We recommend performing this operation during off\-peak hours.</div>


1. Log in to the [Vital Kubernetes Engine](https://console.byteplus.com/vke) console to create a cluster. For instructions, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster?lang=en).

2. Enable IRSA for the cluster and create an IAM role that trusts the OIDC identity provider. For instructions, see [Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters?lang=en).

3. [Use IRSA to implement authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx?lang=en).

4. After establishing a trust relationship and installing the csi\-fsx add\-on, configure access key authentication for PVs in the cluster. Alternatively, you can use IRSA authentication to mount buckets to VKE pods without access keys.

5. After creating a PV, add the corresponding volume when creating a workload and mount the bucket in the pod to use the PV.


<span id="5fabce00"></span>
## Viewing logs

By default, log files are stored in the `/var/log/fsx` directory.


* To view FSX client logs, navigate to `/var/log/fsx/fusedaemon/tos/fusedaemon`.

* To view TOS server interaction logs, navigate to `/var/log/fsx/fusedaemon/tos/tos-fuse`.


For deeper diagnostics and troubleshooting, you may need to set the log level to debug. Use the following commands to do so:


* Set the log level of FSX client logs to debug.

   ```Bash
   cd /opt/fsx/bin && ./fusetool flags set --instance tos --flag v --value 20 --force
   ```
   

* Set the log level of TOS server interaction logs to debug.

   ```Bash
   cd /opt/fsx/bin &&  ./fusetool flags set --instance tos --flag tosfuse_log_level --value 1  --force
   ```
   


<span id="570d17e6"></span>
## Unmounting mount points

Run the `umount <mount directory>` command to unmount a mount point in Linux.

<span id="6ee47c7d"></span>
## Troubleshooting

If you encounter any issues while using FSX, we recommend first running the `/opt/fsx/tools/sysinfo_collector.sh` script. This script automatically collects system information, mount point details, system logs, and other relevant data. Then, it generates a compressed file named `system_info_****_****.tar.gz` in the script's directory. [Submit this file via a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245), and our team will help resolve the issue.
