---
title: "[Product announcement] The XID error isolation feature is disabled for the nvidia-device-plugin add-on by default"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product_Announcement_The_nvidia-device-plugin_add-on_disables_XID_exception_isolation"
---

<span id="JmSVWzq4"></span>
## Background

The Nvidia Device Plugin natively provides the GPU isolation capability. When certain XID errors occur on a GPU in a node, the add\-on automatically isolates the GPU to prevent workloads from being scheduled onto the abnormal GPU. This ensures business security. However, after automatic isolation is performed, the Nvidia Device Plugin does not automatically restore the isolated GPU. You need to manually restart the Nvidia Device Plugin to resume scheduling. Therefore, if you do not promptly handle the isolated GPU, or if the remaining number of GPUs after isolation does not meet the requirements of scheduling tasks, GPU resources may become idle.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about the native GPU isolation capability of Nvidia Device Plugin, see the <a href="https://github.com/NVIDIA/k8s-device-plugin">official documentation</a>. For more methods of handling common XID errors, see <a href="https://docs.byteplus.com/en/docs/gpu/Common_NVIDIA_GPU_XIDs_and_solutions">Methods of handling common NVIDIA GPU XID errors</a>.</div>


<span id="DibCOBCw"></span>
## **Impacted version**

The nvidia\-device\-plugin add\-on of v2.2.0 and later. For the release notes of the add\-on, see [nvidia-device-plugin](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin?lang=zh).

<span id="kJ6i4tbn"></span>
## **Change description**

Starting from v2.2.0, the nvidia\-device\-plugin add\-on makes the following changes:


* By default, the XID health check feature is disabled, and GPUs are no longer automatically isolated based on certain XID errors. To automatically handle XID errors, you can enable GPU self\-healing in node check and self\-healing. For details, see [Configuring node check and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair).

* The `DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER` and `DCGM_CUSTOM_XID_ERRORS_TOTAL_COUNTER` metrics are deprecated and replaced with the `DCGM_EXP_XID_ERRORS_COUNT` metric.


<span id="FgxmboCt"></span>
## Configuration method

To use the GPU isolation capability based on XID errors, you can manually modify the default configuration of the nvidia\-device\-plugin add\-on.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. In the left navigation bar of the cluster management page, click **Addons. On the page that appears, click the GPU tab.** 

4. Move the pointer over the nvidia\-device\-plugin add\-on and click **Configuration**. Manually unselect the **Disable XID health check** parameter to enable the feature of automatically isolating abnormal GPUs based on XID errors.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d8f117c285941990e407950645eb76c.png) </span>

5. [Recommended] Enable cloud\-native observability and configure GPU alert rules to promptly identify and handle idle GPU resources. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).
