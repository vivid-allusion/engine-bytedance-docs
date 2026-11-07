---
title: "RayCluster management"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/RayCluster_management"
---

<span id="ff970fda"></span>
# Prerequisites


* The EMR virtual cluster has already deployed the Ray service.

* The cluster status is running.


<span id="38c514ae"></span>
# Procedure

<span id="6facfa3a"></span>
## Add RayCluster

<span id="0f1abd94"></span>
### Method 1: Add via form


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to the **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray** tab.

3. Click **Add RayCluster \> Add via form**. Enter the **Add RayCluster** page.


<span id="77906823"></span>
##### Note

After entering the create RayCluster page, configure the following: basic information, resource configuration, advanced configuration, and more.


|Configuration items |Note |
|---|---|
|**Basic information** ||
|Name |RayCluster name, length limited to 1–16 characters, only lowercase letters are allowed |
|**Resource configuration** ||
|Group name |Headgroup and Workergroup names must be between 1 and 16 characters in length, and can only contain lowercase letters, numbers, and hyphens. |
|Headgroup |Mainly responsible for scheduling and control, task distribution, and cluster management of the entire Ray cluster.<br><br><br>* Quantity: 1. There is one and only one Headgroup.<br><br>* Pod resources: Supports configuration of CPU and memory for the Pod.<br><br>* Pod quantity: 1<br><br>* Storage configuration: Supports mounting various storage media via Hostpath and PVC, such as vePFS, EBS, and TOS.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To mount storage media using the PVC method, create the PVC in advance. For detailed instructions, refer to: <a href="https://docs.byteplus.com/en/docs/vke/Storage-overview">Storage management</a>.</div><br><br><br><br>* Resource labels: Allows users to precisely control resource allocation for tasks and participants.<br><br>* Scheduling policy: Node selection mechanism, supports scheduling Pods to nodes with specific labels. |
|Workergroup |Mainly responsible for executing computational tasks and providing scalable compute resources.<br><br><br>* Quantity: Default is 1. Up to 10 can be added in table format.<br><br>* Pod resources: Supports configuration of CPU, memory, GPU performance, and GPU cards for the Pod, and supports setting mGPU allocation policies.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To use GPU resource types, ensure that GPU resources are deployed in the node pool.</div><br><br><br><br>* Pod quantity: Default is 1, value range is 1~999.<br><br>* Storage configuration: Supports mounting various storage media via Hostpath and PVC, such as vePFS, EBS, and TOS.<br><br>* Resource labels: Allows users to precisely control resource allocation for tasks and participants.<br><br>* Scheduling policy: Node selection mechanism, supports scheduling Pods to nodes with specific labels. |
|**Advanced configuration** ||
|Taint tolerance |* NoSchedule: Newly scheduled Pods are not allowed to be scheduled to this node.<br><br>* NoExecute: Newly scheduled Pods are not allowed to be scheduled to this node; Pods already running that do not tolerate this taint will be evicted.<br><br>* PreferNoSchedule: Whenever possible, avoid scheduling Pods to this node; if no other suitable nodes are available, scheduling will still occur. |
|Image type |Supports both EMR base images and user\-defined images.<br><br>These [Ray image list](https://docs.byteplus.com/docs/undefined/69aa39258f7b90052e4c5ea4) are divided into the following categories, suitable for different scenarios:<br><br><br>* ray: An image containing Ray and its required dependencies, with built\-in Conda, Java8, and Hadoop services.<br><br>* ray\-ds: Based on the Ray base image, provides Spark, RayDP, and their dependencies, suitable for data processing scenarios.<br><br>* ray\-ml: Based on the ray\-ds image, provides Torch, Tensorflow, and their dependencies, suitable for machine learning scenarios.<br><br>* ve\-daft: A customized version of daft launched by the BytePlus EMR team, which includes Daft and dependencies related to multimodal operators and runtime environments, such as Cuda, Conda, Ray, and more.<br><br><br>Supports users in building custom images based on the EMR base image, including adding third\-party packages. For details, see [Run jobs with a custom Docker image](https://docs.byteplus.com/docs/E-MapReduce/109074). |
|Image name |Custom images require entering the image repository account and repository password. |
|GOS high availability |When enabled, data is persisted to an external Redis to ensure continued normal operation if the Head node fails. |
|Ray Data Checkpoint |Disabled by default. When enabled, it automatically records data processing progress and task status. If a task fails unexpectedly, RayCluster will resume from the latest checkpoint, skipping completed work to save time and computing resources. |


After configuration is complete, in the lower right corner, check the  **"** [Special terms for Data Middle Platform products and services](https://docs.byteplus.com/docs/undefined/6a18f91f9a082404cc2e262c)I agree to the EMR service terms\*\*"\*\* option and click **OK**.

<span id="f97edb7a"></span>
##### Modify RayCluster configuration

After RayCluster is created, you can modify the RayCluster configuration, including enabling or disabling Ray Data Checkpoint, scaling the number of Ray Workers, modifying storage configuration, and more.


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray \> RayCluster name**.


&nbsp;

<span id="3c7c5c2c"></span>
### Method 2: Add RayCluster via YAML

<span id="cf3f5c9a"></span>
##### Create RayCluster

Users can create a new RayCluster by editing YAML.


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to the **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray tab**.

3. Click **Add RayCluster \> Add via YAML**.


<span id="6f5be662"></span>
##### Manage RayCluster

Users can edit YAML to add, delete, or edit RayCluster Workergroups, Pod resources, Pod count, scheduling policies, and more.


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray \> RayCluster**.

3. Click **Edit YAML**.


<span id="f7377b5c"></span>
## Release RayCluster


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray \> RayCluster**.

3. Click **Remove.** 


<span id="58be0ad1"></span>
## Add Workergroup


1. Log in to the [EMR console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home).

2. From the left navigation bar, go to **Resource Management \> on VKE \> Virtual Cluster Details \> Service List \> Ray \> RayCluster**.

3. Click **Add workergroup**.



|Configuration items |Note |
|---|---|
|**Basic information** ||
|Name |Length limit is 1–16 characters. Only lowercase letters, numbers, and hyphens are allowed. |
|**Resource configuration** ||
|Pod specifications |Supports setting CPU, memory, GPU computing power, and GPU cards for Pods, and supports configuring the mGPU allocation policy. |
|Pod quantity |Default is 1. Value range is 1–999. |
|Scheduling policy |Node selection mechanism. Supports scheduling Pods to nodes with specific labels. |
|**Advanced configuration** ||
|Resource labels |Supports users in fine\-grained control of resource allocation for tasks and participants. |
|Storage configuration |Supports mounting various storage media using Hostpath and PVC methods, such as vePFS, EBS, and TOS. |


After configuration is complete, in the lower right corner, check the  **"** [Special terms for Data Middle Platform products and services](https://docs.byteplus.com/docs/undefined/6a18f91f9a082404cc2e262c)I agree to the EMR service terms\*\*"\*\* option and click **OK**.
