---
title: "Mount vePFS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mount_vePFS"
---

This document provides a complete procedure for mounting vePFS.

<span id="fbbf4c8a"></span>
# context

Currently, vePFS can be mounted using either the FSX or Native method.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08e6409fd4764edf95328de4727692cf~tplv-goo7wpa0wc-image.image) </span>


|Comparison criteria |FSX method |Native method |
|---|---|---|
|Mounting access points / mounting services |You need to create the FSX protocol service and an access point for mounting. |You can add vePFS as EMR global storage. After adding, EMR will automatically create a vePFS mounting service for you, which will be used to mount. |
|Key points for mounting |You need to manually create the FSX protocol service and access point. |The system automatically creates the mounting service for you. The logic for creating the mounting service is as follows.<br><br><br>* When adding the first vePFS as EMR global storage, EMR will create a mounting service for you and bind the vePFS instance to it.<br><br>* When continuing to add vePFS as EMR global storage:<br><br>   * If the VPC/subnet associated with the vePFS to be added is **consistent** with the VPC/availability zone of the existing mounting service, the added vePFS will be bound to the previously created mounting service.<br><br>   * If the VPC/availability zone associated with the vePFS to be added is **inconsistent** with the VPC/subnet of the existing mounting service, EMR will create a new mounting service for you, and the added vePFS will be bound to this newly created mounting service. |
|Network requirements |Ensure that the access point's VPC and the EMR storage network VPC are the same VPC. |Queues can only be added to vePFS instances under their storage network VPC. |
|Quantity limits |EMR has no special restrictions; follow vePFS limits. |Mounting service quantity limits:<br><br><br>* When adding EMR global storage, each region supports up to 2 mounting services; each mounting service supports binding up to 2 vePFS instances.<br><br>* When associating a queue with vePFS, each queue can be linked to a maximum of one mount service, that is, each queue can be associated with up to two vePFS instances within the same mount service. |
|Resource type requirements |Currently, only the dedicated portion of computing resources in a queue supports mounting vePFS. The elastic portion of resources does not support mounting. ||


<span id="c6633b59"></span>
# prerequisites


* The vePFS file system has been created for mounting to the EMR Serverless queue. For detailed instructions, see [Creating a file system](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system).

* The EMR Serverless dedicated queue has been created.


<span id="90fd11b8"></span>
# Mount vePFS

<span id="86dcfb28"></span>
## vePFS\-side configuration (required for FSX method)

When mounting using the FSX method, you must create the FSX protocol service and access point on the vePFS side. This step is not required for the Native method.

<span id="eb8e5d2c"></span>
### Step 1: Create the FSX protocol service

When mounting vePFS using the FSX protocol, you need to create the FSX protocol service for the veFSX file system.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad75ae99575843178898bb226a2bd4d3~tplv-goo7wpa0wc-image.image) </span>

<span id="95687f40"></span>
### Step 2: Create an access point

When EMR Serverless mounts vePFS via the FSX protocol, you also need to create an access point for the FSX protocol service in vePFS to facilitate subsequent mounting and access.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df107d103a86432382a5d4ec1ab33fdc~tplv-goo7wpa0wc-image.image) </span>

The key configuration parameters are described as follows.


|Key parameters |Note |
|---|---|
|Private network |It is recommended to keep the VPC consistent with the EMR storage network configuration. |
|Access point root directory |Enter "/" (to restrict access to files in a specific directory, specify the desired directory). |


<span id="6a4c8bfd"></span>
## EMR\-side configuration

<span id="77ea975a"></span>
### Step 1: Add a global storage configuration (required for Native method)

When mounting using the Native method, you must first add vePFS as global storage for EMR. During the addition, EMR will automatically create a mount service for you. For the logic and quantity limits of creating mount services, see [context](https://docs.byteplus.com/docs/E-MapReduce/Mount_vePFS#fbbf4c8a) above.


1. After logging in to the EMR console, click Configurations\>Global storage configuration in the left navigation pane. On the global storage configuration page, click the "Add Mount" button in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c2b0a6025af45c1b19549a668dd74f9~tplv-goo7wpa0wc-image.image) </span>

2. Select the file system to add and click OK.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/955e89be701c49d7a30a82e1bf666c86~tplv-goo7wpa0wc-image.image) </span>

3. Wait for the system to create the mount service for you and complete the addition of global storage.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Creating a mount service takes some time. Please wait patiently.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Additionally, to replace a vePFS instance in the global storage configuration, first bind the new vePFS instance to be mounted, then unbind the old instance that is no longer needed. When the platform detects that no vePFS instance is bound to the mount service, it will automatically delete the vePFS mount service.   </div>
   

   When the status of the created mount service is "Running" and the status of the added vePFS instance is "Bound", the addition of global storage is complete.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbbf9db5e1144aa4a1233ccaf3b9501b~tplv-goo7wpa0wc-image.image) </span>

   After the addition is complete, you can also view the mount services created for you in the list of added vePFS instances and learn about the mount service information associated with each added vePFS instance.


<span id="40c61449"></span>
### Step 2: Configure the queue storage network


1. After logging in and entering the EMR console, click Resource Management \> Serverless in the navigation pane on the left side of the page, then click the Serverless queue to be bound to storage to enter the queue details.

2. Click "Storage network and vePFS" in the left navigation, then click "Configure now" in the "Storage network configuration" module.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92c94c642a3d4bc7abf5f535bac0cf5b~tplv-goo7wpa0wc-image.image) </span>

3. Select the private network, and configure the subnet and security group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5330dfc82f9a4220bf874d347f9b7af0~tplv-goo7wpa0wc-image.image) </span>

   * FSX: Ensure that the VPC selected here is the same VPC as the one where the access point of the file system instance is located in the previous steps.

   * Native: Ensure that the VPC selected here is the same VPC as the VPC of the vePFS instance added in the global storage configuration.


<span id="a88423ea"></span>
### Step 3: Associate the queue with vePFS (required for Native mode)


1. On the Storage network and vePFS page in the Serverless queue details, click "Associate vePFS file system" and select the vePFS to associate in the pop\-up window.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">vePFS must be added to the global storage configuration of EMR before the corresponding vePFS can be selected from the dropdown list here.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Within the same queue, a maximum of two vePFS instances from the same mount service can be added. You can view the mount service details for the corresponding vePFS in the global storage configuration.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07067bb370dd4066a283e38ff48baf01~tplv-goo7wpa0wc-image.image) </span>

2. After the association is complete, you can view all vePFS file systems associated with the current queue here, and view the mount service information for the associated vePFS instance.


<span id="1aa3fe69"></span>
### Step 4: Configure shared file storage for the compute group

You can choose to configure shared file storage when creating a compute group, or configure it when modifying the compute group configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ea4e608b2aa45b99120fb0c9013a0a1~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Note |
|---|---|
|file system name |Select the file system to be mounted from the dropdown list. |
|File System Access Point<br><br>(Required for FSX type) |Select the created access point from the dropdown list. |
|file system path |View the file system path of the vePFS to be mounted. The access point's file path configuration result will be displayed here; no further configuration is required. |
|mount path |Set the path to be mounted in the EMR queue for the current storage. |
|Read\-only |After mounting the storage, specify whether to set it as "read\-only". After enabling the switch, only data reading from the mounted storage path is supported; data writing is not supported. |


<span id="6160df43"></span>
### Step 5: Configure shared file storage in the task

Currently, the EMR Serverless product supports mounting storage in jobs of the following engine types.


* Spark

* Ray

* CustomJob


You can configure this in the interface, or in the task submission code.


* Interface configuration method

   1. Log in to EMR Serverless console, click Job center \> Job management in the left navigation bar, then click "Create job" in the upper right corner of the job management page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image) </span>

   2. Configure storage mount when configuring job parameters during job creation. The configuration parameters are consistent with those in "Configure shared file storage for the compute group" above.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f901e00f58b4aff8b86039595031534~tplv-goo7wpa0wc-image.image) </span>

* Code configuration method

   Based on the original job parameter settings, you can specify the path of the file system to be mounted in the job and the corresponding path in the Pod by adding the `serverless.vepfs.volumes` parameter.

   Additionally, since the access point of the FSX access protocol service requires cross\-VPC access, when using FSX mounting, you must enable cross\-VPC settings when submitting the task.

   * Configuration example

      ```SQL
      -- Set fsx storage mount parameters
      set serverless.vepfs.volumes=[{"type": "fsx", "fileSystemId": "vepfs-cnxxx", "accessPointId":"ap-xxx", "subPath": "/abc/", "mountPath": "/data/def", "readOnly": false}];
      
      -- Set native storage mount parameters
      set serverless.vepfs.volumes=[{"type": "native", "fileSystemId": "vepfs-cnxxx", "subPath": "/abc/", "mountPath": "/data/def", "readOnly": false}];
      
      select 1;
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Mounting NAS and TOS via fsx is described in the NAS and TOS documentation.      </div>
      

   * Parameter description

      
      |Parameter name |Required |Default value |Note |
      |---|---|---|---|
      |type |Yes |None |File system type. The available options are:<br><br><br>* fsx<br><br>* native |
      |fileSystemId |Yes |None |File system ID |
      |accessPointId |No |None |Access point ID is required for the fsx method, but not for the native method. |
      |subPath |Yes |None |The path to be mounted in the file system (the original path in vePFS/NAS) must meet the following requirements: the path already exists in the file system instance, and the path is a subdirectory of the root directory of a protocol service access point in the file system. |
      |mountPath |Yes |None |The path mounted in the Pod. |
      |readOnly |No |FALSE |Indicates whether it is read\-only. 'false' means read\-write, 'true' means read\-only. |
      


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Jobs configured with storage mounts cannot currently use elastic resources from exclusive queues and can only be executed on fixed resources. If fixed resources are fully occupied, these jobs will queue and wait until the fixed resources are released before being scheduled for execution.</div>


<span id="c0839e0a"></span>
# Access point permission management (FSX support)

By default, vePFS access points grant read and write permissions to all sub\-users under this account. If you need to control sub\-user read and write permissions, you can control permissions as follows.


1. Log in to the vePFS console, select **File System \> File System List**, choose the required file system, and go to the file system details page.

2. Select **Protocol Service \> Access Point Management**, choose the access point to manage, click **Access Point Policy**, and enable **IAM Policy**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dafdeffba2649109af2f07f9c34528a~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the IAM policy is enabled, all sub\-users have no access permissions by default. Specific sub\-users require read and write permissions to the access point; refer to the <a href="https://www.volcengine.com/docs/6257/65059?lang=zh">permission policy</a>.   </div>
