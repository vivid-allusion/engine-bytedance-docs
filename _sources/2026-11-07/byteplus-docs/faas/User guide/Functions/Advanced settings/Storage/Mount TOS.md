---
title: "Mount TOS"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Mount_TOS"
---

FaaS supports mounting TOS, storing data on BytePlus [Torch Object Storage (TOS)](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos). This article introduces how to mount TOS.

<span id="prerequisites"></span>
## Prerequisites


* Torch Object Storage (TOS) has been activated.

* TOS Buckets have been created in the designated deployment region. For details refer to [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* API access keys have been obtained, which must have access permission for TOS. For detailed operations, refer to [Managing access keys](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-access-keys) and [Creating a user](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To better control permissions, it is recommended to use minimal authorization IAM user keys, and it is not advisable to directly use BytePlus account keys or IAM user keys with extensive permissions.   </div>
   

<span id="usage-limit"></span>
## Usage limit


* A function can support up to 10 TOS mount points at most.

* When configuring multiple TOS mount points for the same function, duplicate TOS Buckets and subdirectories are allowed, but local directories must not be duplicated.

* If a function is mounted with both NAS and TOS, the local directories set for NAS and TOS mount points cannot be duplicated.

* Only TOS Buckets in the same region are supported for mounting. After mounting, only the internal network Endpoint of TOS is supported as the access address.


<span id="procedures"></span>
## Procedures


1. There are two ways to configure TOS mount points:

* Function not created

   When creating a function, configure the TOS mount in the **Advanced Settings \> Storage** area. For detailed steps on creating a function, refer to [Function creation method selection](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection).

* Function created

   1. Log in to the [Function Service console](https://console.byteplus.com/vefaas), and in the top navigation bar, select the region where your business is located.

   2. In the function list, click the target function name to enter the **function configuration** page.

   3. On the function configuration page, click the edit icon next to the storage configuration.

   4. In the edit storage configuration panel, enable TOS mount.

2. Configure the TOS mount parameters as required, and save once configured.



|**Parameter** |**Description** |
|---|---|
|AKSK |Enter the Access Key ID and Secret Access Key for authorizing the function service to use TOS. The access key must have read and write permissions for TOS. |
|TOS mounting |Add TOS mount points, supporting up to 5. Configuration of each mount point is as follows:<br><br><br>* **Bucket**: Select the TOS Bucket to be mounted.<br><br>* **Access Address**: Automatically obtained after selecting the Bucket.<br><br>* **Bucket Subdirectory**: Select the subdirectory of the Bucket that the function will access. Must start with`/`Introduction. Set as`/`Indicates the root directory where the Bucket is mounted.<br><br>* **Local directory**: Configure the local directory in the function execution environment. The local directory must follow the rules below:<br><br>   * Must start with`/`the beginning.<br><br>   * It is not permitted to set as `/tmp`, `/opt/bytefaas`, `/opt/tiger/bytefaas/binary`.<br><br>   * When setting multiple TOS mount points simultaneously, the local directory must not be duplicated.<br><br>   * The local directories for NAS mount points and TOS mount points must not be duplicated.<br><br>* **Permission**: Choose the access permission for the local directory mounted to the Bucket.<br><br>   * **Read and write permission**: Allow functions to read and write to the local directory mounted to the Bucket.<br><br>   * **Read\-only permission**: Only allow functions to read the contents of the local directory mounted to the Bucket. |


<span id="what-to-do-next"></span>
## What to do next


* Release function

   Storage configuration needs the function to be released to take effect. For specific actions, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

* View the mounted TOS Bucket information

   In the function's base information tab, select the TOS mount card and click the adjacent jump icon to quickly navigate to the object storage console and view detailed information about the current Bucket.

* View the monitoring metrics of the mounted TOS Bucket

   In the function's base information tab, select the TOS mount card and click the monitoring icon to quickly jump to the cloud monitoring console and view the monitoring metrics of the current TOS Bucket.
