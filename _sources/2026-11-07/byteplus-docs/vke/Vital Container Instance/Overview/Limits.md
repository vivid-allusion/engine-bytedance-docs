---
title: "Limits"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-limits"
---

This topic describes limits of using VCI.

<span id=".5by55oCn5a655Zmo5a6e5L6L6ZmQ5Yi2"></span>
## VCI limits

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">If you reach the quota limits and need to increase the quotas, confirm the number of pods in the Pending state caused by insufficient quotas in the cluster.</div>


<div data-tips="true" data-tips-type="warning">When excessive pods in the Pending state exist in the cluster, we recommend deleting pods in this state before increasing the quota or gradually increasing the quota. This prevents a large number of pods in the Pending state from being scheduled at the same time after the quota is increased, which may cause excessive loads on services suddenly and affect business availability.</div>



|**Item** |**Description** |**Method of applying for more quota** |
|---|---|---|
|BytePlus root user accounts for creating VCIs |The root user must **complete real\-name authentication**. The account balance is not zero when vouchers are excluded. |No |
|Supported VKE cluster types |* Clusters with the **VPC\-CNI** network model<br><br>* Clusters with the **Flannel** network model |No |
|Maximum number of VCIs per virtual node in a VKE cluster |6,000 |[Submitting a ticket](https://console.byteplus.com/workorder/create) |
|Number of vCPUs allowed per AZ |The limits for different specifications vary by region and AZ. Refer to the displayed quota in the[ Quota Center](https://console.byteplus.com/quota/productList/ParameterList?ProviderCode=vke). |[Submitting an application in the quota center](https://console.byteplus.com/quota/productList) |
|Maximum number of data volumes allowed per VCI |16 (including one system volume) |No |
|Maximum number of containers supported per VCI |20 |No |
|The maximum number of layers on a single image |50 |No |
|Supported container operating system types |Linux |No |
|Supported Kubernetes versions |This limit aligns with the Kubernetes version limit of VKE. For details, see [Kubernetes version release history](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes). |No |
|enableServiceLinks |When a single namespace in a cluster has 100 or more Services, VCI disables the enableServiceLinks capability (`enableServiceLinks:false`) to override the Kubernetes\-native enableServiceLinks setting in Pod.Spec. |[Submitting a ticket](https://console.byteplus.com/workorder/create) |


<span id=".a3ViZXJuZXRlcy3pmZDliLY="></span>
## Kubernetes limits

Based on the Virtual Kubelet technology from the Kubernetes community, VCI achieves seamless integration with Kubernetes through virtual nodes. Therefore, VCIs do not run on a centralized physical node, but are distributed across the entire cloud resource pool.

Due to restrictions imposed by virtual nodes and public cloud security considerations, VCI has the following limitations on Kubernetes:


|Unsupported feature |Description |Recommended alternative solution |
|---|---|---|
|DaemonSet |Does not support using DaemonSet to deploy static pods on the host machine of containers. |Deploy multiple images in a pod using the Sidecar form. |
|HostPath |Does not support mounting local host files into containers via HostPath. |Use EmptyDir, cloud disks, or NAS file systems to meet local storage requirements. |
|Privileged permission |Does not support enabling the privileged mode for containers via privileged permissions. |Use security contexts to add Capabilities (limited support) to pods, and leverage Docker Container Capabilities to control permissions, achieving outcomes similar to the Privileged mode. |
|NodePort Service |Does not support mapping host ports to containers via a NodePort Service. |Use a Service of type LoadBalancer to enable external access to cluster services. |
|HostNetwork |Does not support mapping host ports to containers via HostNetwork. |Use a Service of type LoadBalancer to enable external access to cluster services. |
|NetworkPolicy |Does not support using NetworkPolicy to implement pod isolation and control network traffic. |Use pod security groups to define access rules. |
|Node\-related management and monitoring |Does not support worker node\-related capabilities. |VCI does not expose physical nodes, so no alternative is available. |


<span id=".56uv5Y-j5Y2g55So6K-05piO"></span>
## Port usage

The following table shows the port used by VCI. When deploying a service, avoid using the following port:


|**Port** |**Description** |
|---|---|
|1025 |Port used by VCI. Used by APIs such as `gpu metrics`. |


<span id=".6YWN6aKd5p-l55yL5ZKM55Sz6K-3"></span>
## Viewing and applying for quotas

VCI allows you to view the VCI resource usage in the VKE console and increase quotas of certain resources.


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Vital Container Instance** \> **Container instance overview**.

3. On the **Container instance overview** page, view the quota usage of VCIs in each AZ within a region. To increase the quota, click **Apply for quota**.

4. On the VKE quota page in the [Quota Center](https://console.byteplus.com/quota/productList), view the quota parameters of the VCI and submit a request to increase adjustable quotas.
