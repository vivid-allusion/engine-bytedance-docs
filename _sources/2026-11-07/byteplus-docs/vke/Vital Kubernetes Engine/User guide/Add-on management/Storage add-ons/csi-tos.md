---
title: "csi-tos"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-tos-add-on"
---

The csi\-tos add\-on is a TOS driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-tos add\-on and provides relevant considerations.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The csi\-tos add\-on will no longer be maintained soon. We recommend promptly switching to the <a href="https://docs.byteplus.com/en/docs/vke/csi-fsx-add-on">csi\-fsx</a> add\-on for stable TOS mounting and new functionality. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Product_changes_csi-tos_add-on_EOM">[Product update] csi\-tos EOM</a>.</div>


<span id="p31MLlRt"></span>
## Add\-on overview

The csi\-tos add\-on is a storage add\-on provided by VKE for mounting TOS to Pods in clusters. TOS mounting allows applications in clusters to directly access data stored in TOS buckets.

As a ‌non\-managed add\-on, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-tos\-controller |Deployment |The Pod for the TOS management controller. It is responsible for monitoring storage requirements (PVCs/PVs) within the cluster and interacting with TOS. |
|csi\-tos\-node |DaemonSet |The Pod for the TOS mount controller. It runs on each worker node in the cluster and is responsible for mounting TOS buckets to the specified node directory. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="8acLiEVC"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-vepfs).

<span id="0oJvlEOb"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. Specify the type of nodes on which the add\-on is deployed. Valid values:<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on Elastic Compute Service (ECS) nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on a VCI with 2 vCPUs and 4 GiB specifications. This will incur extra fees. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |History directory for client cache |The node directory that is mounted to the `/tmp` directory of the client container. Default value: `/etc/csi-tos`. The value needs to be set to an absolute path. |
   

5. Click **Confirm** to finish configuration.


<span id="dS5vG5kK"></span>
## Upgrading add\-ons

<span id="cOFwHRxJ"></span>
### Known issues

For csi\-tos update history, see[ csi-tos](https://docs.byteplus.com/en/docs/vke/csi-tos). If you use an earlier version of the add\-on, the following issues may occur.


|**Issue description** |**Cause** |**Impacted version** |**Fixed in version** |
|---|---|---|---|
|A large number of pods in completed status on a node can cause csi\-tos\-node to experience out\-of\-memory (OOM). |csi\-tos\-node uses the kubelet API to query node pod information. An excessive number of leftover pods can cause the deserialization process in csi\-tos\-node to consume a large amount of memory, triggering OOM. |* v0.2.2<br><br>* v0.2.4<br><br>* v0.2.5<br><br>* v0.2.6<br><br>* v0.2.7<br><br>* v0.2.8<br><br>* v0.2.9 |v1.0.0 |
|The TOS client prevents cluster\-autoscaler from automatically scaling node pools. |* The client pod is not set as a DaemonSet pod.<br><br>* After the client pod is cleaned up, it will be restored by csi\-tos\-node.<br><br>* The client pod has a finalizer. |* v0.2.2<br><br>* v0.2.4<br><br>* v0.2.5<br><br>* v0.2.6<br><br>* v0.2.7<br><br>* v0.2.8 |v0.2.9 |
|The node has a taint, which prevents client pods from being scheduled. |The client pod does not tolerate node taints. |* v0.2.2<br><br>* v0.2.4 |v0.2.5 |
|The absence of multi\-level subdirectories leads to mounting failures. |None. |< v0.2.1 |v0.2.1 |


<span id="70B8tECl"></span>
### Upgrade risks

The upgrade of add\-ons, whether successful or unsuccessful, will not affect existing applications. But the ongoing tasks will be disrupted during the add\-on upgrade because the related workloads will be recreated, causing the resource status to become not ready. Once the add\-on upgrade is completed successfully, the disrupted tasks will rerun automatically. There is no need to intervene, but wait until the resource status turns to ready.

The following list contains actions that may be impacted during the add\-on upgrade process:


* Create workloads. A failed volume mount operation causes the workload to enter the `ContainerCreating` state.

* Delete workloads. A failed volume unmount operation causes the workload to enter the `Terminating` state.


<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Versions earlier than v0.2.4 cannot be seamlessly upgraded to v0.2.4 or later due to architectural changes. In this case, you need to migrate all TOS\-related workloads before you upgrade the add\-on.</div>


* <div data-tips="true" data-tips-type="danger">If your business application requires fast PersistentVolumeClaim binding and workload start, further evaluate the risks and upgrade the add\-on during off\-peak hours.</div>



<span id="IEOtesNu"></span>
### Procedure

Go to the add\-on management page of the target cluster, and in the upper\-right corner of the add\-on card, click `...` \> **Upgrade** to upgrade to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">In case of an upgrade failure, follow the error messages to fix it and try to upgrade the add\-on again.</div>


* <div data-tips="true" data-tips-type="warning">If you encounter issues during the upgrade process or want to upgrade to a specific version, contact presales support or <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to obtain technical support.</div>



<span id="8fUpngGa"></span>
## Check add\-on status

After the add\-on installation/upgrade is complete, confirm whether the add\-on is working normally by using the console or the command\-line tool kubectl.


<Tabs>
<Tab zoneid="Mzv1JgXQ" title="Use the console">
<TabTitle>Use the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke) **.** 

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Workload** \> **DaemonSet**. On the DaemonSet page, check whether the DaemonSet `csi-tos-node` in the `kube-system` namespace is in the Ready state. If all the Pods are ready, the upgrade is successful.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ac7476591fe576b0df9931fd0f1c341.png) </span>


</Tab>
<Tab zoneid="UO27bL1x" title="Use the kubectl CLI">
<TabTitle>Use the kubectl CLI</TabTitle>

1. [Connect to the target cluster using kubectl.](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster)

2. Run the following command to check whether the DaemonSet `csi-tos-node` in the `kube-system` namespace is in the Ready state. If all the Pods are in the `Ready` state, the upgrade is successful.

   ```Bash
   kubectl get daemonset csi-tos-node -nkube-system
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8ffc176ac586e07d1b479e76e8d2dbc6.png) </span>

3. Run the following command to check whether the Pods related to the csi\-tos add\-on are running normally. If all the Pods are in the `Running` state, they are running as expected.

   ```Bash
   kubectl get pods -nkube-system | grep csi-tos
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b0e12c0b0b86e6f6607d9c07def3062b.png) </span>


</Tab>
</Tabs>


<span id="c1a8ZNs2"></span>
## Related documentation

[Using static TOS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-TOS-Volumes)
