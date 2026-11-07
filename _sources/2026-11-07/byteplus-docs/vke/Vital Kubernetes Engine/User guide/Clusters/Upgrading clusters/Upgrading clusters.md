---
title: "Upgrading clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster"
---

Vital Kubernetes Engine (VKE) allows you to upgrade clusters. This topic mainly describes the instructions and steps for upgrading the Kubernetes version of a cluster.

<span id=".5Y2H57qn5rWB56iL"></span>
## Upgrade process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b48f70d12d1a3313b54cffdf9405ed7.png) </span>

&nbsp;

<span id=".5Y2H57qn6aG755-l"></span>
## Before you upgrade

Cluster upgrade consists of two parts: **control plane upgrade** and **node upgrade**. Each part includes two stages: **upgrade check** and **upgrade execution**. Before you start an upgrade, carefully read the instructions described in the **Upgrade policy**, **Control plane upgrade considerations**, and **Node upgrade considerations** sections in this topic.

<span id=".5Y2H57qn562W55Wl"></span>
### Upgrade policy

VKE guarantees the stable operation of the latest three minor versions of Kubernetes. Clusters running expired versions may encounter risks such as unstable operation and failed upgrades. However, this does not affect existing businesses. We recommend that you upgrade your cluster version in a timely manner. For more information, see the following topics:


* [Kubernetes version support policy](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy)

* [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes)


<span id=".5o6n5Yi26Z2i5Y2H57qn5rOo5oSP5LqL6aG5"></span>
### Control plane upgrade considerations


* The upgrade of a Kubernetes minor version may involve changes to Kubernetes resource versions. Before upgrading, check if your application uses deprecated resources. If the chart of your application uses deprecated resources, update the resource versions in the chart to the latest ones and then update the chart in the cluster. For detailed descriptions of resource changes and deprecations, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).

* During the upgrade of the Kubernetes version for the cluster control plane (master nodes), applications in the cluster are not interrupted. If the applications have a strong dependency on the API server, the applications may be affected for a short period of time.

* Five to ten minutes are taken to upgrade the cluster control plane. During this period, you cannot perform operations on your cluster.

* During the upgrade of the cluster control plane, the system automatically performs a pre\-upgrade check. Therefore, before the upgrade, we recommend that you independently perform a pre\-upgrade check and make sure that all check items have passed the check. This ensures a smooth upgrade.

* The pre\-upgrade check is performed on deprecated APIs for running resources.

* You cannot roll back the upgrade of the cluster control plane. Proceed with caution.

* If a custom operating system image is used in the cluster, the success of cluster upgrades cannot be guaranteed because this type of image is not strictly validated by VKE.

* The control plane can be upgraded only if the Kubernetes version of the nodes and the control plane are consistent.

* When you consecutively upgrade the minor version of Kubernetes for the same cluster, we recommend an interval of over 24 hours between upgrades. This ensures stable cluster operation. For example, after you upgrade the cluster control plane from Kubernetes v1.20 to v1.24 and the cluster has stably run for 24 hours, upgrade the cluster to v1.26.

* Parameter incompatibilities may occur after you upgrade the minor version of Kubernetes. Therefore, custom Kubelet parameters and other parameters of the cluster will not be retained after a minor version upgrade. In this case, you need to specify the parameters after the upgrade to ensure that the expected custom configurations are applied to new nodes. For related operations, see [Custom cluster kubelet parameters](https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter).

* When the control plane of a cluster that uses the VPC\-CNI network model is upgraded from Kubernetes v1.20 to v1.24, you need to manually obtain the EndpointSlices resource. For detailed operations and descriptions, see the [Appendix](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster#.6ZmE5b2V) section of this topic.

* The Kubernetes community has updated the value configuration method for kube\-proxy's `conntrack_max` parameter in versions after v1.29. The `conntrack_max` parameter value is now calculated and updated based on the kube\-proxy configuration and the node's CPU core count. For details, see [#120448](https://github.com/kubernetes/kubernetes/pull/120448). In VKE clusters running Kubernetes v1.28 or earlier, kube\-proxy does not override the `conntrack_max` parameter value manually set by the cluster administrator. After upgrading the cluster to v1.30, kube\-proxy may automatically lower the `conntrack_max` parameter value based on its new logic. Therefore, before upgrading your cluster, set parameters such as `conntrack_max` in the ConfigMap of kube\-proxy to prevent them from being overwritten. For detailed instructions, see [FAQ](https://docs.volcengine.com/docs/6460/2533593).


<span id="AFDWCqaC"></span>
### 

<span id=".6IqC54K55Y2H57qn5rOo5oSP5LqL6aG5"></span>
### Node upgrade considerations


* Kubernetes node upgrades can affect running applications. During the upgrade, pod probers and lifecycle hooks may fail, and in\-place restarts of pods may occur. Therefore, before the upgrade, you need to check whether the cluster is in a healthy state and whether applications are at off\-peak hours. This helps you determine whether to start upgrading nodes.

* During the upgrade of the node Kubernetes version, the system automatically performs a pre\-upgrade check. Therefore, before the upgrade, we recommend that you independently perform a pre\-upgrade check and make sure that all check items have passed the check. This ensures a smooth upgrade.

* You cannot roll back the upgrade of the node Kubernetes version. Proceed with caution.

* If you have modified the kubelet or containerd parameter configuration on the nodes, only compatible parameters will be retained during the node upgrade, and incompatible parameters will be removed. After the nodes are upgraded, you need to check the configuration again.

* When you upgrade nodes to v1.28 or later, the system updates the default values of kubelet parameters to the latest values. For details, see [Configuring Kubelet parameters for node pools](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).

* The target Kubernetes version of the node upgrade cannot be later than the Kubernetes version of the control plane.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The Kubernetes version of the target cluster is **Upgradable**, which indicates that the version is not the latest Kubernetes version released by VKE. For more information, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).

* The **Status** of the target cluster must be **Running**.

* Make sure that the business operations of the target cluster are performed during off\-peak hours.


<span id=".5o6n5Yi26Z2i5Y2H57qn"></span>
## Upgrading the control plane

<span id=".5q2l6aqk5LiA77ya5Y2H57qn5qOA5p-l"></span>
### Step 1: Check before the upgrade 

Before you upgrade the control plane, check and resolve all issues that may affect the cluster upgrade.


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Cluster upgrade**.

5. On the **Cluster upgrade** page, click the **Kubernetes upgrade check** tab to run the pre\-upgrade check.

6. Click **Control plane upgrade check**, and then click **Confirm** to start the control plane pre\-upgrade check.

   After the check is complete, perform the next step based on the value displayed in the **Check status** column:

   * **Pass**: The upgrade can be performed.

   * **Fail**: Click **View details** in the Actions column and address the failed check items based on the on\-screen instructions. After fixing the items, run the **control\-plane upgrade check** again. Ensure that **Pass** appears in the ** Check status** column before upgrading. For check item descriptions and fixes, see [Cluster upgrade check items](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">‌During cluster upgrades, the system analyzes cluster audit logs to assess upgrade risks. ‌If you have confirmed and resolved the relevant alerts, you may ignore them during upgrade execution. The specific check items are as follows:   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Important: check for Kubernetes APIs removal from audit logs   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">[Important] VPC\-CNI compatibility check   </div>
   

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Check for deprecated Kubernetes APIs in audit logs   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Clusters running Kubernetes v1.36 or later no longer support nodes or node configurations that use containerd 1.x. Before upgrading the control plane version, first upgrade the node container runtime version and update the container runtime configurations of the node pools. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Managing-NodePools">Managing node pools</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Clusters running Kubernetes v1.36 or later no longer support cgroup v1 nodes. Before upgrading the control plane, first perform a rolling upgrade of nodes to cgroup v2. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/How-are-data-plane-nodes-upgraded">FAQ</a>.   </div>
   


<span id=".5q2l6aqk5LqM77ya5Y2H57qn5o6n5Yi26Z2i"></span>
### Step 2: Upgrade the control plane


1. On the **Cluster upgrade** page, click the **Kubernetes upgrade** tab. Then, click **Control plane upgrade**.

2. In the **Control plane Kubernetes upgrade** dialog box, check the upgrade information.

   
   |Parameter |Description |
   |---|---|
   |Upgrade instructions |Carefully read and confirm **Upgrade instructions**. |
   |Upgrade target version |Select the target version to be upgraded to. Valid values:<br><br><br>* **Patch version**: Displays the VKE patch version available for upgrade based on the current Kubernetes minor version, such as v1.24.<br><br>* **Minor version**: Displays the Kubernetes minor version available for upgrade, such as v1.26, which can be upgraded from v1.24. |
   |Upgrade check warning |During the upgrade, the system automatically runs the pre\-upgrade checks again to ensure the Kubernetes upgrade proceeds smoothly. If any check item has a **Warning** **result** and you confirm it does not affect your workloads, you can select the **Upgrade check warning** option to ignore the item and proceed with the Kubernetes upgrade. |
   

3. Click **Confirm upgrade** to upgrade the control plane.

   During the upgrade process, you can click **View details** in the **Actions** column to view the control plane Kubernetes upgrade progress.

4. View upgrade results. If **Pass** is displayed in the **Status** column, it indicates that the Kubernetes upgrade is complete.

5. (Optional) If the upgrade fails, perform the operation again based on the on\-screen instructions.  If you encounter any further issues during the upgrade, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001270) for technical support.


<span id=".6IqC54K55Y2H57qn"></span>
## Upgrading nodes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When the Kubernetes version of the control plane is the same as that of the nodes, you need to upgrade the control plane before performing node upgrades. You can perform upgrades if there are no restrictions on upgrade pre\-checks.</div>


* <div data-tips="true" data-tips-type="tip">When the Kubernetes version of the control plane is later than that of the nodes, the nodes can be upgraded to the same Kubernetes version as the control plane.</div>



<span id=".5q2l6aqk5LiA77ya5Y2H57qn5qOA5p-l"></span>
### Step 1: Check before the upgrade


1. Log in to the [VKE console](https://console.byteplus.com/vke). 

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Cluster upgrade**.

5. On the **Cluster upgrade** page, click the **Kubernetes upgrade check** tab. Then, click **Node upgrade check**.

6. Specify parameters on the **Node upgrade check** page.

   
   |Parameter |Description |
   |---|---|
   |Basic information |Select **Upgrade content** based on your actual requirements:<br><br><br>* **Kubernetes version**: Select the target Kubernetes version (a patch or minor version) to upgrade to. For version information, see [Kubernetes version release history](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).<br><br>* **Container runtime**: Select a container runtime version.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">VKE currently supports only the <strong>containerd</strong> container runtime. If the runtime version is upgradable, the system will display available versions. For more information about containerd versions, see the <a href="https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes">containerd release notes</a>.   </div><br>    |
   |Node upgrade dimension |By default, VKE performs node upgrade checks at the **node** level. After you apply for a trial, you can upgrade nodes from the following dimensions:<br><br><br>* **Node**: Select nodes to be upgraded.<br><br>* **Node pool**: Select the node pools whose nodes are to be upgraded. |
   |Select the upgrade check node |* When you set the **Node upgrade dimension** parameter to **Node**, you can select **All nodes** or **Partial nodes** in the cluster to perform a node upgrade check.<br><br>* When you set the **Node upgrade dimension** parameter to **Node pool**, you can select a node pool to perform a node upgrade check on all its nodes. |
   

   After the check is complete, perform the next step based on the value displayed in the **Check status** column:

   * **Pass**: The upgrade can be performed.

   * **Fail** or **Warning**: Click **View details** in the Actions column and address the failed check items based on the on\-screen instructions. After fixing issues, perform the **node upgrade check** again. Ensure that **Pass** appears in the **Check status** column before upgrading. For check item descriptions and fixes, see [Cluster upgrade check items](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you confirm that pre\-upgrade check items with a <strong>check result</strong> of <strong>Warning</strong> do not affect your business operations, you can ignore these items and proceed with the Kubernetes upgrade.      </div>
      

<span id=".5q2l6aqk5LqM77ya5Y2H57qn6IqC54K5"></span>
### Step 2: Upgrade nodes


1. On the **Cluster upgrade** page, click the **Kubernetes upgrade** tab. Then, click **Node upgrade**.

2. In the Node Kubernetes upgrade message, carefully read **Upgrade instructions**. Then, click **Confirm upgrade**.

3. On the **Node Kubernetes upgrade** page, check the upgrade information.

   
   |Parameter |Description |
   |---|---|
   |Basic information |The following upgradable items are displayed:<br><br><br>* **Kubernetes version**: Upgradable Kubernetes version (a patch or minor version). For version information, see [Kubernetes version release history](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).<br><br>* **Container runtime**: The upgradable container runtime and its version.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">VKE currently supports only the <strong>containerd</strong> container runtime. For more information about containerd, see the <a href="https://docs.byteplus.com/en/docs/vke/Containerd_Runtime_release_notes">containerd release notes</a>.   </div><br>    |
   |Node upgrade dimension |By default, VKE performs node upgrades at the **node** level. After you apply for a trial, you can upgrade nodes from the following dimensions:<br><br><br>* **Node**: Select nodes to be upgraded.<br><br>* **Node pool**: Select the node pools whose nodes are to be upgraded. |
   |Select node to be upgraded |Select the target nodes that require a Kubernetes upgrade in the cluster. |
   |Upgrade check warning |During the upgrade, the system automatically runs the pre\-upgrade checks again to ensure the Kubernetes upgrade proceeds smoothly. If any check item has a **Warning** **result** and you confirm it does not affect your workloads, you can select "**I am aware of the check results before upgrades**" to ignore the warnings and proceed with the Kubernetes upgrade. |
   

4. Click **Confirm** to upgrade the nodes.

   During the upgrade process, you can click **View details** in the **Actions** column to view the Kubernetes upgrade progress of nodes.

5. View upgrade results. If **Pass** is displayed in the **Status** column, it indicates that the Kubernetes upgrade is complete.

6. (Optional) If the upgrade fails, perform the operation again based on the on\-screen instructions.  If you encounter any further issues during the upgrade, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001270) for technical support.


<span id=".5Y2H57qn5ZCO5qOA5p-l"></span>
## Post\-upgrade check

After the upgrade is complete, verify the Kubernetes versions for the cluster and nodes, and cluster status on the **Overview** page of the cluster. Also, check whether other applications in your cluster are running as expected. If your applications are abnormal, view the relevant events and logs for further processing.  You can also submit[ a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001270) for technical support.

<span id=".6ZmE5b2V"></span>
## Appendix

In a VPC\-CNI network model cluster, after the cluster control plane is upgraded from Kubernetes v1.20 to v1.24, you need to restart the Cello DaemonSet that belongs to the vpc\-cni add\-on to obtain the new version of the EndpointSlices resource. Perform the following steps to restart Cello DaemonSet:


1. Connect to the upgraded cluster by using kubectl. For more details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Run the following command to restart Cello DaemonSet that belongs to the vpc\-cni add\-on.

   ```bash
   kubectl rollout restart daemonset cello -n kube-system
   ```
