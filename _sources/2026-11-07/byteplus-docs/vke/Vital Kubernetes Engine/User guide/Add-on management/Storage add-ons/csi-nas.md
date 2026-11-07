---
title: "csi-nas"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-nas-add-on"
---

The csi\-nas add\-on is a FileNAS driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-nas add\-on and provides relevant considerations.

## Add\-on overview

csi\-nas is a storage add\-on provided by VKE for mounting FileNAS to Pods in clusters. It enables multiple Pods to simultaneously read and write the same shared filesystem.

As a ‌non\-managed add\-on, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-nas\-controller |Deployment |The Pod for the FileNAS management controller. It is responsible for monitoring storage requirements (PVCs/PVs) within the cluster and interacting with FileNAS/EFS. |
|csi\-nas\-node |DaemonSet |The Pod for the FileNAS mount controller. It runs on each worker node in the cluster and is responsible for mounting FileNAS/EFS to the specified node directory. |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-nas).

## Install the add\-on

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the name of the target cluster to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   |Parameter |Description |
   |---|---|
   |Deployment method |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. Specify the type of nodes on which the add\-on is deployed. Valid values:<br><br><br>* **Elastic Compute Service deployment**: deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on a VCI with 2 vCPUs and 4 GiB specifications. This will incur extra fees. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Node health check port |Node health check port. The default is 9908. We recommend using a port number lower than 12000. |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Controller Resource configuration |Specify the CPU and memory requests and limits for the controller resources of the add\-on. |
   |Node Resource configuration |Specify the CPU and memory requests and limits for the node resources of the add\-on. |

5. Click **Confirm** to finish configuration.

## Upgrading add\-ons

### Known issues

For csi\-nas update history, see [csi-nas](https://docs.byteplus.com/en/docs/vke/csi-nas). If you use an earlier version of the add\-on, the following issues may occur.

|**Issue description** |**Cause** |**Impacted version** |**Fixed in version** |
|---|---|---|---|
|When the add\-on is deployed on VCI, the permissions of the dynamic volume subdirectory are not 777. |In case of VCI\-based add\-on deployment, a subdirectory for the dynamic volumes is still created on the node. Because the default umask of the node is 0022, the permissions of the created directory are set to 0755. |< v1.2.7<br><br> |v1.2.7<br><br> |
|The directory is not a mount point, which causes the unmount operation to fail and the pod to enter Terminating state. |The mount\-utils library from the Kubernetes community. If the directory in the umount command is not the mount point, an error is returned. |* v1.2.3<br><br>* v1.2.4<br><br><br> |v1.2.5 |
|The mount point is not available.<br><br> |Force Umount causes other local mount points that mount the same remote NAS to become unavailable. |< v1.2.3 |v1.2.3 |
|The NFS version resolution fails. |None. |< v1.0.3 |v1.0.3 |

### Upgrade risks

The upgrade of add\-ons, whether successful or unsuccessful, will not affect existing applications. But the ongoing tasks will be disrupted during the add\-on upgrade because the related workloads will be recreated, causing the resource status to become not ready. After the add\-on is upgraded, unfinished operations are automatically retried. You only need to wait until the resource status becomes Ready, and no manual intervention is required.

The following list contains actions that may be impacted during the add\-on upgrade process:

* Create PersistentVolumeClaims (dynamic volumes). Failed volume creation causes the PersistentVolumeClaim to remain unbound.

* Delete PersistentVolumeClaims (dynamic volumes). Failed PersistentVolume deletion causes the PersistentVolumeClaim to be stuck in the `Terminating` state.

* Create workloads. A failed volume mount operation causes the workload to enter the `ContainerCreating` state.

* Delete workloads. A failed volume unmount operation causes the workload to enter the `Terminating` state.

> **tip**

> If your business application requires fast PersistentVolumeClaim binding and workload start, further evaluate the risks and upgrade the add\-on during off\-peak hours.

### Procedure

Go to the add\-on management page of the target cluster, and in the upper\-right corner of the add\-on card, click `...` \> **Upgrade** to upgrade to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

> **warning**

* > In case of an upgrade failure, follow the error messages to fix it and try to upgrade the add\-on again.

* > If you encounter issues during the upgrade process or want to upgrade to a specific version, contact presales support or [submit a ticket](https://console.byteplus.com/workorder/create) to obtain technical support.

## Check add\-on status

After the add\-on installation/upgrade is complete, confirm whether the add\-on is working normally by using the console or the command\-line tool kubectl.

**Use the console**

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation pane, click **Workload \> Deployment**. On the Deployment page,  check whether the Deployment `csi-nas-controller` in the `kube-system` namespace is in the Ready state. If all the Pods are ready, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b4ae189f9060687c76e0cb27d2e85a0.png)

4. In the left navigation pane, click **Workload \> DaemonSet**. Check whether the DaemonSet `csi-nas-node` in the `kube-system` namespace is in the Ready state. If all the Pods are ready, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_52d99e0d0f8af0adeed941c9b68e92a5.png)

**Use the kubectl CLI**

1. [Connect to the target cluster using kubectl.](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster)

2. Run the following command to check whether the Deployment `csi-nas-controller` in the `kube-system` namespace is in the Ready state. If all the Pods are in the `Ready` state, the upgrade is successful.

   ```Bash
   kubectl get deployment csi-nas-controller -nkube-system
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c4d878875ce74148e603e1f6c766b5b.png)

3. Run the following command to check whether the DaemonSet `csi-nas-node` in the `kube-system` namespace is in the Ready state. If all the Pods are in the `Ready` state, the upgrade is successful.

   ```Bash
   kubectl get daemonset csi-nas-node -nkube-system
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0c7385cbc6adfc028df478dcd161b8d1.png)

4. Run the following command to check whether the Pods related to the csi\-nas add\-on are running normally. If all the Pods are in the `Running` state, they are running as expected.

   ```Bash
   kubectl get pods -nkube-system | grep csi-nas
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f9bc35dd6bbea7894ec7035da14aea10.png)

## Monitoring and alerting

### Add\-on observability

The stability and performance of the csi\-nas add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [CSI Storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the running status of the csi\-nas add\-on and the NAS volume operation workflow. It includes Controller Pod availability, Node Pod availability, control plane operation backlog, control plane RPC call failures, node RPC call failures, node RPC latency, and NAS operation status. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Storage service monitoring** \> **NAS monitoring** to view the monitoring dashboard.

### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:

* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)

## Related documentation

* [Using static FileNAS PVs via NFS](https://docs.byteplus.com/en/docs/vke/Using-static-NAS-Volumes)

* [Using dynamic FileNAS PVs via NFS](https://docs.byteplus.com/en/docs/vke/Using-dynamic-NAS-Volumes)
