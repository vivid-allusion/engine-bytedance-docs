---
title: "csi-ebs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-ebs-add-on"
---

The csi\-ebs add\-on is an EBS driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-ebs add\-on and provides relevant considerations.

## Add\-on overview

csi\-ebs is a core storage add\-on provided by VKE for integrating and managing EBS resources in clusters. It bridges the cluster with the underlying storage service. When your workload requires persistent data storage, this add\-on will automatically apply for a cloud disk, format it, and mount it to the specified Pod. This ensures that data is not lost when the Pod restarts or migrates.

As a ‌non\-managed add\-on, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-ebs\-controller |Deployment |The Pod for the EBS management controller. It monitors storage requirements (PVCs/PVs) within the cluster, and automatically completes EBS resource creation, scale\-out, deletion, and mounting/uninstalling by calling the API. |
|csi\-ebs\-node |DaemonSet |The Pod for the EBS mount controller. It runs on each worker node in the cluster and is responsible for formatting the EBS volumes locally on the node and mounting them to the container directory where the Pod resides. |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-ebs).

## Install the add\-on

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on a VCI with 2 vCPUs and 4 GiB specifications. This will incur extra fees. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Project |Select the project to which the add\-on belongs. By default, the **default** project is selected. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Node reserve volumes count |Specify the number of EBS volumes reserved at the cluster level. This parameter is used to reserve system resources to prevent disk resources from being completely exhausted.<br><br><br>* When this parameter is left empty:<br><br>   * If the node specification supports mounting ≥ 16 EBS disks, the system reserves 4 disks by default as reserved disks.<br><br>   * If the node specification supports mounting < 16 EBS disks, the system reserves 30 percent of the disks as reserved disks. For example, if the node specification allows up to 15 cloud disks to be mounted, VKE allows up to 10 cloud disks to be mounted, which is calculated by using the following formula: 14 × (1 \- 0.3).<br><br>* If you specify a value, the system reserves volumes based on this setting. For example, if the node specification allows up to 16 cloud disks to be mounted, and this parameter is set to 1, VKE allows up to 15 cloud disks to be mounted.<br><br><br>> **warning**<br><br><br>> After you modify the number of reserved disks for nodes, the system automatically restarts the csi\-ebs add\-on to ensure that the modified configuration takes effect. To prevent your online business from being affected, we recommend performing this operation during off\-peak hours.<br> |
   |Node reserve volumes Synchronization period |Synchronize node label `ebs.csi.volcengine.com/reserve-volumes` to update the cycle for reserved node volume count. An empty value disables this feature. |
   |Enable online volume modification |If you enable this feature, you can use VolumeAttributesClass resources to change the cloud disk type, Burst, and extra performance online. For more information, see [Changing cloud disk types](https://docs.byteplus.com/en/docs/vke/Changing_cloud_disk_types). |
   |Enable node allocated volumes metric |If you enable this feature, the controller exposes the count of allocated volumes (excluding volumes allocated to VCIs). In certain abnormal scenarios, the value of this metric may be inaccurate. We recommend using the `kube_volumeattachment_info` metric provided by kube\-state\-metrics. |
   |metrics port on node |The port used for collecting node monitoring data. The default is 11815. We recommend using a port number lower than 12000. |
   |Node health check port |The node health check port. The default is 9808. We recommend using a port number lower than 12000. |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Enable wait for API Server Cluster IP Ready |After this feature is enabled, the node csi\-ebs\-node add\-on will continuously probe the API Server during startup and will wait for the network to be available before continuing to start. This can reduce the possibility of abnormal events during startup. |
   |Resource configuration |Specify the CPU requests, CPU limits, memory requests, and memory limits of various resources in the add\-on. |

5. Click **Confirm** to finish configuration.

## Upgrading add\-ons

### Known issues

We recommend upgrading the add\-on version promptly. Using an earlier add\-on version may cause the following issues.

|**Issue description** |**Cause** |**Impacted version** |**Fixed in version** |
|---|---|---|---|
|The mount operation fails when the access mode of the PersistentVolume is ReadWriteMany. |This issue results from invalid usage. Because a cloud disk cannot be mounted to multiple nodes simultaneously, the earlier versions did not require access mode validation. |\>= v1.1.0<br><br> |Invalid usage. No fix is planned.<br><br> |
|The csi\-ebs\-node failed to start on the Dedicated Host. The add\-on status is abnormal. |The [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API uses the InstanceTypeIds request parameter, which is not supported by Dedicated Host. |< v1.2.9 |v1.2.9 |
|The quantity of cloud disks allocatable to workloads on the node is inaccurate. |During the startup of csi\-ebs\-node, access to the Metadata Server or OpenAPI fails. The maximum number of available cloud disks is the default value of 16. |< v1.2.6<br><br> |v1.2.6 |
|The csi\-ebs\-node has not been registered with kubelet. The pod is in the ContainerCreating state. |Before you uninstall an earlier version of the add\-on, the new pod has already been launched, causing registration with kubelet to occur before the previous registration is cancelled. |< v1.1.8 |v1.1.8 |
|Access to the Metadata Server times out, causing the zone to be an empty string. The CSI node or controller cannot function normally. |No check is performed to determine whether the zone parameter is an empty string.<br><br> |< v1.1.7<br><br> |v1.1.7 |
|A projectName check fails in scenarios where the StorageClass does not specify a projectName but the cloud disk already exists. |When the StorageClass does not specify a projectName, the project for the cloud disk is the "default" project. |v1.1.5<br><br> |v1.1.6 |
|Add\-on installation fails on clusters that have third\-generation models. |The add\-on mounts the SCSI device by default, but third\-generation models do not have this device. |< v1.1.2 |v1.1.2 |

### Upgrade risks

The upgrade of add\-ons, whether successful or unsuccessful, will not affect existing applications. But the ongoing tasks will be disrupted during the add\-on upgrade because the related workloads will be recreated, causing the resource status to become not ready. After the add\-on is upgraded, unfinished operations are automatically retried. You only need to wait until the resource status becomes Ready, and no manual intervention is required.

The following list contains actions that may be impacted during the add\-on upgrade process:

* Create PersistentVolumeClaims (dynamic volumes). Failed volume creation causes the PersistentVolumeClaim to remain unbound.

* Delete PersistentVolumeClaims (dynamic volumes). Failed PersistentVolume deletion causes the PersistentVolumeClaim to be stuck in the `Terminating` state

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

1. Log in to the [VKE console](https://console.byteplus.com/vke) **.**

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Workload** \> **Deployment**. On the Deployment page,  check whether the Deployment `csi-ebs-controller` in the `kube-system` namespace is in the Ready state. If all the Pods are ready, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fba5cd829bbfbc09987a32d0a845c8d.png)

4. In the left navigation pane, click **Workload** \> **DaemonSet**. On the DaemonSet page, check whether the DaemonSet `csi-ebs-node` in the `kube-system` namespace is in the Ready state. If all the Pods are ready, the upgrade is successful.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9904938e0a20ed29d607ce232f4731d.png)

**Use the kubectl CLI**

1. [Connect to the target cluster using kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster) and then execute the following commands in sequence to check the add\-on status.

2. Run the following command to check whether the Deployment `csi-ebs-controller` in the `kube-system` namespace is in the Ready state. If all the Pods are in the `Ready` state, the upgrade is successful.

   ```Bash
   kubectl get deployment csi-ebs-controller -nkube-system
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e959447d53eab8a8214c667ab7428964.png)

3. Run the following command to check whether the DaemonSet `csi-ebs-node` in the `kube-system` namespace is in the `Ready` state. If all the Pods are in the Ready state, the upgrade is successful.

   ```Bash
   kubectl get daemonset csi-ebs-node -nkube-system
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90cf4fc3d073adc3b2ae34b6919c2c27.png)

4. Run the following command to check whether the Pods related to the csi\-ebs add\-on are running normally. If all the Pods are in the `Running` state, they are running as expected.

   ```Bash
   kubectl get pods -nkube-system | grep csi-ebs
   ```

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0cf68adada15dfbc50b47edc923fcabf.png)

## Monitoring and alerting

### Add\-on observability

The stability and performance of the csi\-ebs add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [CSI Storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the running status of the csi\-ebs add\-on and the cloud disk volume operation workflow, including Controller Pod availability, Node Pod availability, control plane operation backlog, control plane RPC call failures, node RPC call failures, cloud storage API call failures, cloud storage API latency, and node RPC latency. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Storage service monitoring** \> **EBS monitoring** to view the monitoring dashboard.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f33b78b455f6c9c996269907df1cd80.png)

### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:

* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)

Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

## Related documentation

* [Using static PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes)

* [Using dynamic PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes)

* [Dynamically expanding EBS data volumes](https://docs.byteplus.com/en/docs/vke/Dynamically-expanding-EBS-Volumes)

* [Expanding by using statically provisioned EBS data volumes](https://docs.byteplus.com/en/docs/vke/Statically-expanding-EBS-Volumes)

* [Changing cloud disk types](https://docs.byteplus.com/en/docs/vke/Changing_cloud_disk_types)
