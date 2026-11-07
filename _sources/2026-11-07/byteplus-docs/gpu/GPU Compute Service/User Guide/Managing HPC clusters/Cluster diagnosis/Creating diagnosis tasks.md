---
title: "Creating diagnosis tasks"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Creating_diagnosis_task"
---

This topic describes how to diagnose the health status of HPC\-optimized instances. This helps you locate related exceptions or performance metrics that do not meet your expectations.

<span id="8qXOGHfK"></span>
## Limits


* Currently, this feature is only available for Linux instances in the **Running** state.

* Instances to be diagnosed need to have [the cloud assistant Agent installed](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client).

* If the target instance is in the diagnosis analysis, wait for the diagnosis to complete before you select the instance for a new diagnosis.


<span id="sXEiRaa2"></span>
## Usage notes

If you are using the cluster diagnosis service for the first time, you need to click the "Create now" button. This grants role\-related permissions to your account (CustomRoleForDiagnose and CustomRoleForHpcDiagnose) that have read and write permissions for ECS resources. This allows the HPC cluster to assume the corresponding role to access the cloud resources involved in your diagnosis task.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">After you click the "Create now" button, the system automatically completes the role\-related authorization.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">If only one role (CustomRoleForDiagnose or CustomRoleForHpcDiagnose) is displayed, this indicates that the other role has been granted the corresponding permissions.</div>


* <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Cross\-service access is performed by using IAM roles. An IAM role is granted permissions to access specific cloud resources, and the current service can assume this role to access resources of other cloud services. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Overview-3">IAM</a>.</div>



<span id="rraOzuFR"></span>
## Procedure

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">This diagnosis process may affect the businesses that run on the instance and stop your businesses. Before you start the diagnosis, confirm the business status and select an appropriate time. For example, you can diagnose the instance during business idle periods.</div>


* <div data-tips="true" data-tips-type="warning">Before the diagnosis, related packages and dependencies are automatically installed on the instance. If the instance is based on a custom image, you may fail to install required packages and dependencies and thereby fail to detect some diagnostic items.</div>


1. Log in to the [instance console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance?projectName=default).

2. In the left\-side navigation pane, select "Instances & Images \> HPC Cluster".

3. In the top navigation bar, select the project and region of the target instance.

4. Click the "Cluster diagnosis" tab.

5. Click the "Create diagnosis" button and configure the following information.

   
   |**Parameter​**  |**Description** |**Sample value** |
   |---|---|---|
   |Diagnosis selected |Select the item to be diagnosed. Stand\-alone diagnosis and cluster diagnosis are supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Both stand\-alone diagnosis and cluster diagnosis options are applicable to all <a href="https://docs.byteplus.com/en/docs/gpu/High-Performance-Computing-Optimized-hpcpni3h">HPC\-optimized</a> instances.</div><br><br><br><br>* **Stand\-alone diagnosis**<br><br>   Instance\-level diagnosis, mainly used for health checks of GPU devices. Diagnosis items include devices within one GPU instance (such as driver configuration, GPU card, and network interface configuration), NCCL Test, intra\-machine bandwidth, and other items. For more details, refer to [Diagnosis overview](https://docs.byteplus.com/en/docs/gpu/Diagnosis_summary?LibVersion=markdown备份版本). You can select the following methods for diagnosis:<br><br>   * **GPU device Health Check**: The diagnostic items checked are exactly the same as those of the "GPU device health check" option. This option offers a faster diagnostic process, which is applicable for quickly troubleshooting small faults.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you select "GPU device health check", the diagnosis is expected to take 5 minutes.      </div><br>      <br><br>   * **In\-depth health check of GPU device**: The diagnostic items checked are exactly the same as those of the "GPU device Health Check" option. If this option is configured, the diagnosis is slower, with more content covered. This causes a longer diagnosis process and more occupied disk space, which is applicable for troubleshooting complex faults.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you select "In\-depth health check of GPU device", the diagnosis is expected to take 40 minutes.      </div><br>      <br><br>* **Cluster diagnosis**<br><br>   Cluster\-level detection, mainly used to diagnose connectivity and performance in HPC clusters. Diagnosis items include the connectivity of RDMA network interfaces and switches within a cluster, as well as nccl\-tests connections and nccl\-tests performance between instances in the cluster. For more details, refer to [Diagnosis item overview](https://docs.byteplus.com/en/docs/gpu/Diagnosis_summary?LibVersion=markdown备份版本). |Stand\-alone diagnosis/GPU device Health Check |
   |HPC cluster |Select the HPC cluster where the instance to be diagnosed is deployed. Learn more about [creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters?LibVersion=markdown备份版本). |\- |
   |Instance selected |Select the target instance to be diagnosed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the target instance is <strong>undergoing diagnosis analysis</strong>, wait for the diagnosis to complete before you reselect the instance for another diagnosis.</div><br> |\- |
   |Cloud assistant installation detection |Check if the instance has the cloud assistant Agent installed. If not, we recommend installing the [cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client) first.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If cloud assistant is not installed, you can not perform instance diagnosis.</div><br> |\- |
   

6. After you complete the configuration, click the "Create" button to begin the diagnosis.

7. Once the diagnosis is complete, you can view the results.


<span id="zmpboIXl"></span>
## Subsequent steps

If there are exceptions that you are suggested to fix, you can follow the repair suggestion or[ the diagnosis item repair suggestions](https://docs.byteplus.com/en/docs/gpu/Diagnosis_summary?LibVersion=markdown备份版本). Then click the "Re\-diagnosis" button to confirm whether the exceptions have been resolved.
