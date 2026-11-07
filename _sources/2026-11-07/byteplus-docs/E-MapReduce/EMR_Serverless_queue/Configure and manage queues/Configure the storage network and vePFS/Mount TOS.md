---
title: "Mount TOS"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Mount_TOS"
---

This article introduces the complete process for mounting TOS.

<span id="be054d8a"></span>
# Background information

Currently, TOS supports two mounting methods: FSX and S3FS.


|Important notes |Note |
|---|---|
|Key points for mounting |You need to obtain access keys AK and SK with TOS access permissions. Use AK and SK to enable mounting and encrypted authentication. |
|Network/region requirements |You must ensure that the region of the TOS bucket is the same as the region of the EMR/storage network VPC. |


<span id="c6d66eeb"></span>
# Prerequisites


* Create a TOS object storage bucket to mount to an EMR Serverless queue. For detailed instructions, see:[Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* Prepare access keys AK and SK with permissions to access TOS. Obtaining access keys: Log in to BytePlus console, and on the **Access Control** ＞ **API Access Key** page, create and manage your Access Key.

* A dedicated EMR Serverless queue has been created.


<span id="6384bb0f"></span>
# Mount TOS

<span id="0cae973d"></span>
### Step 1: Queue storage network configuration (required for FSX method)


1. After logging in to the EMR console, click Resource Management \> Serverless in the left navigation panel, then click the Serverless queue to which storage will be bound to enter the queue details.

2. Click "Storage Network and vePFS" in the left navigation, then click "Configure Now" in the "Storage Network Configuration" module.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92c94c642a3d4bc7abf5f535bac0cf5b~tplv-goo7wpa0wc-image.image) </span>

3. Select a private network, and configure the subnet and security group.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5330dfc82f9a4220bf874d347f9b7af0~tplv-goo7wpa0wc-image.image) </span>


<span id="fdd31794"></span>
### Step 2: Configure shared file storage for the compute group

You can configure shared file storage when creating the compute group, or modify the configuration when editing the compute group.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f96347ec79545ebb951c2e3d19fee7a~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration note |
|---|---|
|AK / SK |Enter the prepared AK and SK information, click "Connectivity test," and after completing the connectivity test, proceed to configure the subsequent parameters. |
|Source address |Select the TOS bucket path to be mounted. |
|mount path |Set the mount path in the current EMR queue storage. |
|Read\-only |After mounting the storage, set whether it is "read\-only." After enabling the switch, only reading data from the mounted storage path is supported; writing data is not supported. |


<span id="334d428e"></span>
### Step 3: Configure shared file storage in the task

Currently, the EMR Serverless product supports mounting storage in jobs for the following engine types.


* Spark

* Ray

* CustomJob


Settings can be configured in the interface or in the task submission code.


* Interface configuration

   1. Log in to EMR Serverless console, click Job center \> Job management in the left navigation bar, then click "Create job" in the upper right corner of the job management page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e7c6b3ca8f50408099947bf93322a75c~tplv-goo7wpa0wc-image.image) </span>

   2. Configure storage mount in the job parameter configuration during job creation. The configuration parameters are consistent with those in "Configure shared file storage for the compute group" above.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbd210a68bc9492a8c6c6f06fdc62abe~tplv-goo7wpa0wc-image.image) </span>

* Code configuration

   Based on the original job parameter settings, you can add the `serverless.tos.volumes` parameter to specify the file system path to be mounted in the job and the corresponding path in the Pod.

   Additionally, since the FSX access protocol service endpoint requires cross\-VPC access, when using FSX mounting, you must enable cross\-VPC settings when submitting the task.

   * Configuration example

      ```SQL
      -- Mount TOS using fsx mode:
      set serverless.tos.volumes=[{"type": "fsx", "tosPath": "tos://bucket1/path1/", "mountPath": "/abc/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}];
      -- Mount TOS using s3fs mode:
      set serverless.tos.volumes=[{"type": "s3fs", "tosPath": "tos://bucket1/path1/", "mountPath": "/abc/", "readOnly": false,"ak":"xxxx", "sk":"xxxxx"}];
      
      select 1;
      ```
      

   * Parameter description

      
      |Parameter name |Required |Default value |Note |
      |---|---|---|---|
      |type |Yes |None |File system type. The available values are: fsx, s3fs |
      |tosPath |Yes |None |TOS path |
      |mountPath |Yes |None |Path mounted in the Pod |
      |readOnly |No |FALSE |Read\-only status: false means read/write, true means read\-only |
      |ak |Yes |None |AK for accessing TOS |
      |sk |Yes |None |SK for accessing TOS |
      


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Jobs configured with storage mounting cannot currently use elastic resources in exclusive queues; they can only be executed in fixed resources. If fixed resources are fully occupied, these jobs will queue and wait until the fixed resources are released before being scheduled for execution.</div>


&nbsp;
