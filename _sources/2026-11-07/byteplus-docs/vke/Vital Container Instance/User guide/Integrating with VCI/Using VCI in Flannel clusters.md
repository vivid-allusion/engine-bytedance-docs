---
title: "Using VCI in Flannel clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster"
---

VKE clusters that use the Flannel network model support application deployment to VCI. This topic describes the procedure and considerations for using VCI in Flannel clusters.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

Pods and workloads (Deployment and StatefulSet) deployed to VCI in Flannel VKE clusters do not support secondary NICs.

<span id=".5YeG5aSH5bel5L2c"></span>
## Preparations

When using VCI in Flannel clusters, follow these steps to prepare a Flannel cluster that meets the following requirements:


* A pod subnet has been configured in the cluster to assign unique IP addresses to VCI pods for network communication.

* The vci\-virtual\-kubelet add\-on has been installed in the cluster to schedule to VCI via virtual nodes.


You can follow these procedures to prepare a Flannel cluster:


* **Create a Flannel cluster**: The parameters mentioned below must be configured as described here. For other parameters, see [Creating managed clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

   1. Specify the **Pod subnets** parameter in the **Cluster configuration** step.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If the <strong>Pod subnets</strong> parameter is unavailable for the <strong>Flannel</strong> network model, it indicates that the selected Kubernetes version does not support VCI. For specific support status, see <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes">Kubernetes version release notes</a>.      </div>
      

   2. Install the **vci\-virtual\-kubelet** add\-on in the **Addon configuration** step.

* **Use an existing Flannel cluster**: Follow the steps below.

   1. On the **Overview** tab of the **Overview** page for the cluster, add Pod subnets to the cluster in the **Cluster network configuration** section. For details, see [Viewing cluster information](https://docs.byteplus.com/en/docs/vke/Cluster-basics).

   2. Install the vci\-virtual\-kubelet add\-on in the cluster. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).


<span id=".5L2_55So5pa55rOV"></span>
## Procedure

In the prepared cluster that uses the Flannel network model, use VCI to deploy workloads or Pods. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).
