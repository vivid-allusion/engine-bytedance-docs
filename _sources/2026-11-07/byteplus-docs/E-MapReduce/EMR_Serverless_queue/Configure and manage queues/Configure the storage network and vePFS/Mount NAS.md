---
title: "Mount NAS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mount_NAS"
---

This article introduces the complete process for mounting NAS.

<span id="d52a6fca"></span>
# Background information

Currently, mounting NAS via FSX is supported.


|Important notes |Note |
|---|---|
|Storage type |NAS must use cache type. |
|Mounting essentials |You need to create the FSX access point yourself. |
|Network requirements |Ensure that the VPC of the access point and the VPC of the EMR storage network are the same VPC. |


<span id="af0ec137"></span>
# Prerequisites


* A NAS file system has been created for mounting to the EMR Serverless queue. For detailed instructions, see: [Creating a file system ](https://www.volcengine.com/docs/6453/1276604)[Creating a file system](https://docs.byteplus.com/en/docs/nas/Creating-a-file-system).

* An exclusive EMR Serverless queue has been created.


<span id="07d21134"></span>
# Mount NAS

<span id="7e759cf9"></span>
## NAS\-side configuration

<span id="a1167d58"></span>
### Step 1: Enable and bind FSX protocol service


* The NAS instance requires contacting the NAS storage team to enable and bind the FSX protocol service. If necessary, please [submit tickets](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) to contact technical personnel to enable the service.

* Ensure that the VPC where the file system instance access point is located is consistent with the VPC configured for EMR Serverless storage network.


<span id="db1873c9"></span>
### Step 2: Create an access point

When EMR Serverless mounts NAS via the FSX protocol, you also need to create an access point in NAS for subsequent mounting and access.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f998575d8a8448888820297eed94df48~tplv-goo7wpa0wc-image.image) </span>

The key configuration parameters are as follows.


|Key parameters |Configuration note |
|---|---|
|Private network |Ensure consistency with the EMR Serverless storage network configuration. |
|Permission group |Select the default permission group. |
|Access point root directory |Enter “/” (if you need to restrict access to files under a specific directory, enter the specific directory). |


<span id="c3bb75c2"></span>
## EMR\-side configuration

<span id="0afa193a"></span>
### Step 1: Queue storage network configuration


1. After logging in to the EMR console, click Resources\>Serverless in the left navigation, then click the Serverless queue to be bound to storage to enter the queue details.

2. Click "Storage Networking and vePFS" in the left navigation, then click "Storage Network Configuration" module's "configure now".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92c94c642a3d4bc7abf5f535bac0cf5b~tplv-goo7wpa0wc-image.image) </span>

3. Select the private network and configure the subnet and security group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5330dfc82f9a4220bf874d347f9b7af0~tplv-goo7wpa0wc-image.image) </span>

   Ensure that the VPC selected here is the same VPC as the file system instance access point in the steps above.


<span id="4e539ba1"></span>
### Step 2: Configure shared file storage for the compute group

You can configure shared file storage when creating a compute group, or configure it when modifying the compute group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd57b70d9d3049c3a5a862ff5ef963ef~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration note |
|---|---|
|file system name |Select the file system to be mounted from the dropdown list. |
|File System Access Point |Select the created access point from the dropdown list. |
|file system path |View the file system path of the NAS to be mounted. The access point file path configuration result will be displayed here; no further configuration is required. |
|mount path |Set the path to be mounted in the EMR queue for the current storage. |
|Read\-only |After mounting the storage, set whether it is “read\-only”. After turning on the switch, only reading data from the mounted storage path is supported; writing data is not supported. |


<span id="0780bf23"></span>
### Step 5: Configure shared file storage in the task

Currently, the EMR Serverless product supports mounting storage in jobs of the following engine types.


* Spark

* Ray

* CustomJob


Currently, settings can be configured in the interface or in the task submission code.


* Interface configuration

   1. Log in to EMR Serverless console, click Job center \> Job management in the left navigation bar, then click "Create job" in the upper right corner after entering the job management page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image) </span>

   2. Configure storage mounting in the job parameter configuration during creation. The configuration parameters are consistent with those in "Configure shared file storage for the compute group" above.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbd210a68bc9492a8c6c6f06fdc62abe~tplv-goo7wpa0wc-image.image) </span>

* Code configuration

   Based on the original parameter settings of the job, you can specify the file system path to be mounted in the job and the corresponding path in the Pod by adding the `serverless.nas.volumes` parameter.

   At the same time, since the FSX access protocol service endpoint requires cross\-VPC connectivity, you must enable cross\-VPC settings when submitting a task using FSX mounting.

   * Configuration example

      ```SQL
      -- Set storage mount parameters
      set serverless.nas.volumes=[{"type": "fsx", "fileSystemId": "nas-cnxxx","accessPointId":"ap-xxx", "subPath": "/abc/", "mountPath": "/data/def", "readOnly": false}];
      
      select 1;
      ```
      

   * Parameter description

      
      |Parameter name |Required |Default value |Note |
      |---|---|---|---|
      |type |Yes |None |File system type. The selectable value here is: fsx |
      |fileSystemId |Yes |None |File system ID |
      |accessPointId |Yes |None |Access point ID |
      |subPath |Yes |None |The path to be mounted in the file system (the original path in vePFS/NAS) must meet the following requirements: the path already exists in the file system instance, and the path is a subpath of the root directory of a protocol service access point in the file system. |
      |mountPath |Yes |None |The path mounted in the Pod |
      |readOnly |No |FALSE |Whether it is read\-only. If false, it is read\-write; if true, it is read\-only. |
      


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Jobs configured with storage mounts cannot currently use elastic resources in exclusive queues and can only be executed in fixed resources. If fixed resources are fully occupied, these jobs will queue and wait until the fixed resources are released before being scheduled for execution.</div>


<span id="1fd6060f"></span>
## Permission management

NAS access points are, by default, open for read and write access to all sub\-users under this account. If you need to control read and write permissions for sub\-users, you can manage permissions in the following ways.


1. Log in to the NAS console, select **File System \> File System List**, choose the required file system, and enter the file system details page.

2. After selecting the **Access Point** tab, click the access point you want to manage, turn on the **IAM Policy** switch, and configure the IAM policy.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After the IAM policy is enabled, all sub\-users have no access permissions by default. Specific sub\-users require read and write permissions for the access point. Refer to<a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax">What is the policy syntax</a>.</div>
