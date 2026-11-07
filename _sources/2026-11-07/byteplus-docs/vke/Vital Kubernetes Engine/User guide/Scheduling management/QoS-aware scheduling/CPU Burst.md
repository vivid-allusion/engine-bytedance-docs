---
title: "CPU Burst"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability"
---

Vital Kubernetes Engine (VKE) provides the CPU Burst capability for pods based on Katalyst, an open\-source resource management system from ByteDance.

## Background

In Kubernetes, CPU Burst is an optimization policy designed to improve the performance of containers running latency\-sensitive applications. It allows containers to accumulate CPU time slices during periods of low CPU utilization, which can then be used to meet sudden resource demands, ultimately improving container performance and reducing latency.

The CPU Burst policy works as follows: when the CPU usage of a container is below its CPU Limit, it accumulates additional CPU time slices. These time slices can be used when the container needs to process burst tasks, for example, sudden spikes in traffic or requests. When a container needs to process more tasks within a short period, it utilizes these accumulated time slices to avoid CPU throttling (CPU Throttle), thereby reducing response latency.

Based on the kernel's CPU Burst capability, VKE supports adjusting the kernel parameter `cpu.cfs_quota_us` to allow containers to temporarily exceed their configured CPU limits when nodes have idle computing power. Containers can use a small amount of extra CPU resources to handle traffic spikes smoothly and reduce response latency without upgrading workload specifications.

## Usage limits

* Currently, CPU Burst is available only to pods deployed on ECS instances instead of VCIs.

* Full use of this feature depends on katalyst version v0.5.13\-vke.14 or later.

* The CPU Burst capability does not apply to Pods in the namespaces of the following VKE system components:

   * kube\-system

   * kube\-flannel

   * cloudfs\-system

   * katalyst\-system

   * kruise\-system

   * kruise\-daemon\-config

   * kueue\-system

   * varmor

   * apmplus\-opentelemetry\-operator

## Prerequisites

* The cluster is in the **Running** state and has available ECS nodes. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).

* The katalyst add\-on version v0.5.13\-vke.14 or later has been installed in the cluster, with **QoS\-Aware Scheduling** selected on the add\-on configuration page to enable the **CPU Burst** capability. For details, see [katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).

## Procedure

### Step 1: Add a label to a node

After configuring the node label, you can use the CPU Burst capability of the katalyst add\-on to manage the corresponding node.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. On the left navigation bar, select **Cluster**, and click the name of the target cluster.

3. On the cluster management page, add a label to the node where the pod is located by following the steps below.

   **Add a label at the node pool level**

> **tip**

   > We recommend using this labeling method, as it allows labels to be added to nodes within the node pool.

   1. In the left navigation bar, click **Nodes** \> **Node pool**.

   2. On the **Node pool** page, find the target node pool and click **Edit** in the **Actions** column.

   3. On the **Edit node pool** page, specify the **Node labels** parameter and select **Enable auto renew for node labels and taints** in the **Advanced configurations** section in the **Node pool configuration** step.

      * **Label key**: `vke.node.katalyst.deploy`

      * **Label value**: `true`

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec8a2ae2c96668ee278b964df334b9a8.png)

   4. Update the configurations of the node pool based on the console wizard.

   **Add a label at the node level**

1. In the left navigation bar, click **Nodes** \> **Node**.

   2. On the **Node** page, find the target node and click `...` \> **Label management** in the **Actions** column.

   3. On the **Node details page**, click **Add new** on the **Label** tab, add the following label to the node, and then click **Confirm**.

      * **Label key**: `vke.node.katalyst.deploy`

      * **Label value**: `true`

### Step 2: Enable CPU Burst for pods

VKE supports enabling CPU Burst for Pods at the Pod or cluster level.

> **warning**

* > To disable CPU Burst at the pod level, set `cpuBurstPolicy` to `none` in the annotation instead of deleting the annotation directly.

* > To disable the CPU Burst feature at the cluster level, set `cpuBurstPolicy` to `none` in the AdminQoSConfiguration CRD instead of directly deleting the CRD.

> For detailed instructions, see **More operations** in this topic.

**Pod level**

Configure the CPU burst policy for a single Pod by adding a specific annotation to the Pod. The following table describes the annotations.

|**Annotation key** |**Annotation sample value** |**Description** |**Required** |
|---|---|---|---|
|katalyst.kubewharf.io/cpu_enhancement |'{"cpu_burst_policy":"cpuBurstOnly","cpu_burst_percent":"100"}' |Pod\-level CPU Burst configuration. The parameter value format is String[JSON]. For a detailed sub\-parameter description, see the **JSON parameters** table below. |No |

**JSON parameters**

|**Key** |**Meaning** |Required |**Value type** |**Value description** |
|---|---|---|---|---|
|cpu_burst_policy<br><br> |CPU Burst enablement/disablement policy.<br><br> <br><br> <br><br> |Yes |String |* **none**: Disables the CPU Burst policy.<br><br>* **static**: (Deprecated) Uses the static policy.<br><br>   > **warning**<br>   <br><br>   > The **static** value is deprecated. If you have specified this value, we recommend replacing it with the **cpuBurstOnly** value.<br>   <br><br>* **cpuBurstOnly**: Enables only the ‌kernel\-level CPU Burst elasticity‌.<br><br>   > **warning**<br>   <br><br>   > The CPU Burst feature supports only the following node [OS images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images):<br>   <br><br>   * > Public veLinux images with kernel version 5.4, 5.10, or 5.15<br>   <br><br>   * > Public Ubuntu images with kernel version 5.15<br>   <br><br>   * > Custom images created based on the preceding public images built on two kernel versions<br>   <br><br>* **cfsQuotaBurstOnly**: Enables only ‌CFS Quota‌ auto\-elasticity.<br><br>   > **tip**<br>   <br><br>   > CFS Quota elasticity supports all OS images.<br>   <br><br>* **auto**: Adaptively enables cpuBurstOnly and cfsQuotaBurstOnly. |
|cpu_burst_percent<br><br> |The upper CPU Burst percentage limit.<br><br> |No |String |* Value range: a positive integer from 1 to 100 (inclusive)<br><br>* Default value: 100.<br><br><br> |
|cfs_quota_burst_percent |The maximum percentage threshold for CFS Quota. It defines the maximum percentage of extra CPU resources available when a container temporarily exceeds its configured CPU limit. |No |String |* Value range: Positive integers greater than 100.<br><br>* Default value: 300.<br><br><br> |
|cfs_quota_burst_period_seconds |The maximum duration a container can sustain CPU usage at the cfsQuotaBurstPercent limit when CFS Quota elasticity is enabled. <br><br>After the container exceeds this period, its elevated cgroup parameters gradually revert to the original values without affecting other Pods. |No |String |* Value range: Positive integers.<br><br>* Default value: \-1, indicating no limit is applied.<br><br>* Unit: seconds. |

The following content uses Deployment creation as an example. For more workload operations, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).

1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following YAML file `cpu-burst-demo.yaml` serves as an example.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: cpu-burst-demo  # The Deployment name.
     namespace: default  # The namespace where the Deployment resides.
   spec:
     replicas: 1  # The number of Deployment replicas.
     selector:
       matchLabels:
         app: cpu-burst-demo
     template:
       metadata:
         labels:
           app: cpu-burst-demo
         annotations: 
           katalyst.kubewharf.io/cpu_enhancement: '{"cpu_burst_policy":"auto","cpu_burst_percent":"100"}'  # The CPU Burst configuration.
       spec:
         containers:
         - name: container-1  # The container name.
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
           resources:
             limits:  # The maximum CPU or memory limit for the container. To enable CPU Burst, the CPU Limit must be configured.
               cpu: "4"
             requests:  # CPU or memory requests for the container.
               cpu: "2"
   ```

3. Run the following command to create the Deployment.

   ```bash
   kubectl apply -f cpu-burst-demo.yaml
   ```

**Cluster level**

To enable CPU Burst for all pods deployed on ECS at the cluster level, you need to configure an AdminQoSConfiguration object named **katalyst\-config** in the katalyst\-system namespace.

> **tip**

* > The katalyst\-system namespace is automatically generated by the system when the katalyst add\-on is enabled.

* > AdminQoSConfiguration is a katalyst configuration for fine\-grained resource management.

1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create an AdminQoSConfiguration object. The following YAML file `katalyst-config.yaml` serves as an example.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: AdminQoSConfiguration
   metadata:
     name: katalyst-config  # This field has a fixed value: the name of the AdminQoSConfiguration object.
     namespace: katalyst-system  # This field has a fixed value: the namespace of the AdminQoSConfiguration object.
     labels:
       vke.node.katalyst.deploy: "true"  # The label related to the fine-grained resource management feature of node pool configuration. This feature applies only to nodes with this label.
   spec:
     config:
       fineGrainedResourceConfig:
         cpuBurstConfig:  # Configure CPU Burst for pods at the cluster level.
           cpuBurstPolicy: "auto"  # Enable the dynamic CPU Burst capability.
           cpuBurstPercent: 100 # Maximum percentage for CPU Burst.
           cfsQuotaBurstPercent: 300 # The upper percentage limit for CFS Quota bursting. Default value: 300. Unit: percentage.
           sharePoolThresholdPercent: 50 # Node CPU utilization safety threshold when CFS Quota elasticity is enabled.
   ```

   The following table describes CPU Burst parameters.

   |cpuBurstConfig parameter |Description |
   |---|---|
   |cpuBurstPolicy |Enable CPU Burst for the current pod. Valid values:<br><br><br>* **none**: Disables the CPU Burst policy.<br><br>* **static**: (Deprecated) Uses the static policy.<br><br>   > **warning**<br>   <br><br>   > The **static** value is deprecated. If you have specified this value, we recommend replacing it with the **cpuBurstOnly** value.<br>   <br><br>* **cpuBurstOnly**: Enables only the ‌kernel\-level CPU Burst elasticity‌.<br><br>   > **warning**<br>   <br><br>   > The CPU Burst feature supports only the following node [OS images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images):<br>   <br><br>   * > Public veLinux images with kernel version 5.4, 5.10, or 5.15<br>   <br><br>   * > Public Ubuntu images with kernel version 5.15<br>   <br><br>   * > Custom images created based on the preceding public images built on two kernel versions<br>   <br><br>* **cfsQuotaBurstOnly**: Enables only ‌CFS Quota‌ auto\-elasticity.<br><br>   > **tip**<br>   <br><br>   > CFS Quota elasticity supports all OS images.<br>   <br><br>* **auto**: Adaptively enables cpuBurstOnly and cfsQuotaBurstOnly. |
   |cpuBurstPercent |Maximum burst percentage for CPU Burst:<br><br><br>* Value range: a positive integer from 1 to 100 (inclusive)<br><br>* Default value: 100. |
   |cfsQuotaBurstPercent |The maximum percentage threshold for CFS Quota. It defines the maximum percentage of extra CPU resources available when a container temporarily exceeds its configured CPU limit. Valid values:<br><br><br>* Value range: Positive integers greater than 100.<br><br>* Default value: 300. |
   |cfsQuotaBurstPeriodSeconds |The maximum duration a container can sustain CPU usage at the cfsQuotaBurstPercent limit when CFS Quota elasticity is enabled. Valid values:<br><br><br>* Value range: Positive integers.<br><br>* Default value: \-1, indicating no limit is applied.<br><br>* Unit: seconds. |
   |sharePoolThresholdPercent |The safety percentage threshold for node CPU utilization when CFS Quota elasticity is enabled. If this threshold is exceeded, all elevated CFS Quota parameters on the node will revert to their original values configured at creation. Valid values:<br><br><br>* Value range: a positive integer from 1 to 100 (inclusive)<br><br>* Default value: 50. |

3. Create a KatalystCustomConfig (KCC) object. The KCC object defines the Group, Version, Resource (GVR) information and management behavior of the AdminQosConfiguration.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: KatalystCustomConfig
   metadata:
     name: katalyst-config  # This field has a fixed value: the name of the KatalystCustomConfig object.
     namespace: katalyst-system  # This field has a fixed value: the namespace of the KatalystCustomConfig object.
     labels:
       vke.node.katalyst.deploy: "true"  # This field has a fixed value. The label related to the fine-grained resource management feature of node pool configuration.
   spec:
     targetType:  # This field has a fixed value. It describes the GVR information of the AdminQosConfiguration.
       group: config.katalyst.kubewharf.io
       resource: adminqosconfigurations
       version: v1alpha1
   ```

## Validating results

1. View the UID of the pod with the CPU Burst capability enabled.

   ```Bash
   # Replace <pod_name> with the actual Pod name.
   kubectl get pod <pod_name> -o jsonpath='{.metadata.uid}'
   ```

2. View the ID of the container in the pod.

   ```Bash
   # Replace the <pod_uid> below with the Pod's UID value obtained in the previous step.
   kubectl get pod <pod_uid> -o jsonpath='{.status.containerStatuses[*].containerID}'
   ```

3. Log in to the ECS node where the pod is located. For login methods, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

4. View the `burst_us` value of the CPU in the container's cgroup.

   **cgroup v1**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/cpu/kubepods/pod<pod-uid>/<container-id>/cpu.cfs_burst_us
   ```

   **cgroup v2**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpu.max.burst
   ```

   Replace `<pod_uid>` and `<container-id>` with the values obtained in the preceding step.

5. View the `quota_us` value of the CPU in the container's cgroup.

   **cgroup v1**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/cpu/kubepods/pod<pod-uid>/<container-id>/cpu.cfs_quota_us
   ```

   **cgroup v2**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpu.max
   
   # The first value is CFS quota (unit: μs), and the second value is the default CPU execution cycle (default: 100000μs, that is, 100ms).
   100000 100000
   ```

6. Calculate the values of `cpu.cfs_burst_us` and `cpu.cfs_quota_us` using the following method.

   If `cpu.cfs_burst_us` equals `cpu.cfs_quota_us` multiplied by `the maximum percentage limit you have set for CPU Burst`, the CPU Burst configuration has been correctly applied.

7. The duration of CPU throttling.

   **cgroup v1**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/cpu/kubepods/pod<pod-uid>/<container-id>/cpu.stat
   ```

   The expected response is as follows:

   ```Bash
   nr_periods 1215
   nr_throttled 0
   throttled_time 0 # The duration of CPU throttling. After CPU Burst is enabled, the increase in the metric per unit time will decrease.
   nr_bursts 401
   burst_time 66399120464
   ```

   **cgroup v2**

```Bash
   # Replace <pod_uid> and <container-id> with the values obtained in the previous steps.
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpu.stat
   ```

   The expected response is as follows:

   ```Bash
   usage_usec 45031
   user_usec 19629
   system_usec 25402
   nr_periods 23
   nr_throttled 0    # The number of times for CPU throttling.
   throttled_usec 0  # The total period of time of CPU throttling.
   ```

## More operations

Use the following method to disable the CPU Burst feature for the pod.

**Pod level**

Change the value of the CPU Burst\-related annotation on the corresponding Pod to `none`, as in `katalyst.kubewharf.io/cpu_enhancement: '{"cpu_burst_policy":"none","cpu_burst_percent":"100"}'`.

**Cluster level**

In the YAML file for the AdminQoSConfiguration object named **katalyst\-config**, change the value of the CPU Burst\-related annotation to `none` (namely, `cpuBurstPolicy: "none"`).

After you disable the pod CPU Burst feature at the cluster level, the feature will be automatically disabled for all pods in the cluster.
