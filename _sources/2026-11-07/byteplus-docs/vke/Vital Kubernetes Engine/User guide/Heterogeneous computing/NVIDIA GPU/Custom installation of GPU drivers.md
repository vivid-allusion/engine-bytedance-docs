---
title: "Custom installation of GPU drivers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Installing-custom-GPU-drivers"
---

Vital Kubernetes Engine (VKE) provides the automatic GPU driver installation capability. GPU drivers can be automatically installed for nodes that are created through public images and in GPU\-related instance families. This topic describes how to automatically install GPU drivers in detail.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

Cloud\-native machine learning is one of the major scenarios for VKE, and the usage requirements for GPU and other heterogeneous resources are growing. In the following complex scenarios with different usage habits and environments, automatic GPU driver installation becomes necessary.


* New users who develop their applications based on VKE need to fully use the basic environment provided by VKE, which includes GPU instances, OS images, and GPU drivers.

* Existing users of VKE have a set of mature VKE\-based environment dependencies and need to reuse the dependencies as the base environment.

* Users who have migrated from other cloud platforms have become dependent on GPU environments. For example, when CUDA is packaged into container images, an operating system that is compatible with the required environment needs to be provided.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A TOS bucket has been created. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* **Disclaimer: This feature cannot guarantee that all drivers are available for all GPU types. Therefore, you need to make sure that the uploaded GPU driver version is compatible with the GPU type and is fully tested. Otherwise, issues such as performance degradation and unknown risks may occur.** 

* Make sure that the container cluster and TOS are interconnected. We recommend that you enable public access to ensure network connectivity.

* To use the automatic GPU driver installation feature, take note of the following items during node configuration:

   * **System image**: Only the following public images are supported: veLinux Standard Edition and Ubuntu.

   * **Instance type**: Only High Performance Computing Optimized and certain GPU Accelerated instance families are supported. GPU rendering instance families that end with vws are not supported.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5LiL6L29LWdwdS3pqbHliqjmlofku7Y="></span>
### Step 1: Download the GPU driver file

Click the official GPU driver download link provided by NVIDIA and download the GPU driver and related documentation that meet your business requirements.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure that the fabricmanager file matches the NVIDIA driver version. Otherwise, the installation may fail.</div>



* Go to the [NVIDIA driver website](http://www.nvidia.com/Download/Find.aspx) to search for and download the required GPU driver file.

* (Optional) If you need to use fabricmanager on instance types with NVSwitch, go to the [official repository](https://developer.download.nvidia.cn/compute/cuda/repos/) to download the file that matches your scenario.


<span id=".5q2l6aqk5LqM77ya5bCGLWdwdS3pqbHliqjkuIrkvKDliLDlr7nosaHlrZjlgqg="></span>
### Step 2: Upload the GPU driver to TOS

Upload the GPU driver and related files downloaded in Step 1 to TOS, and obtain the file names and TOS download links.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Make sure that the container cluster and TOS are interconnected. We recommend that you enable public access to ensure network connectivity.</div>



1. Log in to the [TOS console ](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets** to go to the Buckets page.

3. Click the name of the created bucket. In the left navigation bar, click **Overview** to obtain the domain name of the bucket, which is the TOS download link required for Step 3. Example: `bucket.tos-cn-beijing.ivolces.com`.

4. Click **Objects** in the left navigation bar. On the Objects page, click **Upload file** to upload the GPU driver file prepared in Step 1 to TOS. You can obtain the file name after the file is uploaded to TOS, such as `NVIDIA-Linux-x86_64-515.86.01.run`.

5. On the Objects page, find the target file and click `...` \> **Modify Access Permission** in the Actions column. Then, sequentially change the access permissions of the GPU driver file prepared in Step 1 to **Public read**.


<span id=".5q2l6aqk5LiJ77ya6IqC54K55rGg5re75Yqg6IqC54K55qCH562-"></span>
### Step 3: Add node labels to the node pool

Configure custom information about the GPU driver by adding node labels for the node pool. When the node driver does not match the actual configuration, the system will automatically uninstall the default driver and install the prebuilt custom GPU driver.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Driver installation is triggered only when nodes are added to the node pool and identified based on the node labels in the node pool. Common usage scenarios are as follows:</div>



* <div data-tips="true" data-tips-type="warning">When you create a node pool, all nodes are newly added to the pool. These nodes can be identified to trigger driver installation based on the node labels in the node pool. We recommend that you use this method to use the custom GPU driver feature.</div>


* <div data-tips="true" data-tips-type="warning">New nodes added to an existing node pool are still considered newly added nodes. They can be identified by the node labels in the node pool to trigger driver installation.</div>


* <div data-tips="true" data-tips-type="warning">Existing nodes in an existing node pool are not newly added nodes, which <strong>cannot be identified based on the node labels in the node pool to trigger driver installation</strong>. The following solutions are for reference:</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Solution 1</strong>: Manually remove existing nodes and add them again. Make sure that the normal operations of your business are not affected.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Solution 2</strong>: Use the node scaling feature to scale in all existing nodes and then scale out the nodes again. Make sure that the normal operations of your business are not affected.</div>



Node labels related to custom GPU drivers are as follows:


|**Node label (key: value)**  |**Sample node label value** |**Required** |**Description** |
|---|---|---|---|
|vke.volcengine.com/nvidia\-driver\-tos\-endpoint: <TOS download link\> |bucket.tos\-cn\-beijing.ivolces.com |Yes |The directory address of the GPU custom driver after being uploaded to TOS, which is the bucket domain name. |
|vke.volcengine.com/nvidia\-driver\-runfile: <NVIDIA driver file name\> |NVIDIA\-Linux\-x86_64\-515.86.01.run |Yes |The file name in TOS for the NVIDIA driver to be installed. Use this label to specify the driver file to be downloaded. |
|vke.volcengine.com/nvidia\-fabricmanager\-file: <fabricmanager file name\> |nvidia\-fabric\-manager\-515.86.01\-1.x86_64.deb |No |The file name of the fabricmanager package stored in TOS. This label is supported only for instance types with NVSwitch, such as A100.  |


Perform the following steps to add node labels to a node pool:


1. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

2. In the left navigation bar, click **Node pool** to go to the node pool management page.

3. Click **Create node pool** or click **Edit** in the Actions column that corresponds to an existing node pool. In the **More configurations** section, add the preceding node labels to the node pool, and then click **Confirm**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5e43c8fbda042f893875a7bab4bf833.png) </span>


<span id="OKt1F8WL"></span>
## Validating results


1. Use **ECS Terminal** to log in to the node. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to view GPU\-related information.

   ```Bash
   nvidia-smi
   ```
   

   The expected result is as follows: driver version 515.86.01. This indicates that the custom NVIDIA driver installation was successful.

   ```Bash
   Mon Jan  5 19:47:34 2026       
   +---------------------------------------------------------------------------------------+
   | NVIDIA-SMI 515.86.01               Driver Version: 515.86.01   CUDA Version: 12.2     |
   |-----------------------------------------+----------------------+----------------------+
   | GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
   | Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
   |                                         |                      |               MIG M. |
   |=========================================+======================+======================|
   |   0  NVIDIA L4                      On  | 00000000:65:01.0 Off |                    0 |
   | N/A   33C    P8              16W /  72W |      0MiB / 23034MiB |      0%      Default |
   |                                         |                      |                  N/A |
   +-----------------------------------------+----------------------+----------------------+
                                                                                            
   +---------------------------------------------------------------------------------------+
   | Processes:                                                                            |
   |  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
   |        ID   ID                                                             Usage      |
   |=======================================================================================|
   |  No running processes found                                                           |
   +---------------------------------------------------------------------------------------+
   ```
   


<span id="DZn9DPjt"></span>
##
