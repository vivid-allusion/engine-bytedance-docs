---
title: "CPU QoS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/CPU_QoS"
---

VKE provides the CPU QoS (Quality of Service) feature based on the katalyst add\-on. After CPU QoS is enabled, you can classify Pods into different QoS levels by workload type and prioritize high\-priority workloads through CPU core binding (CPUSet), dynamic pool adjustment, CPU scheduling priority, and pressure eviction policies.

## Background information

In a Kubernetes cluster, latency\-sensitive online workloads and offline or batch workloads are usually colocated on the same node to improve CPU utilization. Even with CPU requests and limits configured, the two workload types still compete for CPU resources. When offline jobs become busy, they interfere with online workloads, increasing response latency and degrading service quality.

VKE provides CPU QoS based on the katalyst add\-on to solve this problem. It marks online workloads as high priority and offline workloads as low priority, and uses the scheduling priority provided by the Linux kernel's [CPU Idle](https://docs.kernel.org/admin-guide/pm/cpuidle.html) capability to guarantee CPU scheduling for applications of different priorities. In hybrid deployment scenarios, this improves node utilization while prioritizing the service quality of high\-priority workloads.

## Feature introduction

### Applicable scenarios

CPU QoS applies to online\-offline hybrid deployment scenarios where workloads of different priorities are deployed on the same node, for example, deploying online services together with offline computing and batch jobs to improve overall CPU utilization of the node.

CPU QoS provides the following benefits after it is enabled:

* **When low\-priority jobs use more CPU resources**: The kernel's CPU Idle capability ensures that only the CPU resources idle in high\-priority workloads are allocated to low\-priority jobs, which prevents interference with running high\-priority jobs.

* **When high\-priority jobs use more CPU resources**: High\-priority workloads can preempt CPU resources from low\-priority in a timely manner, which guarantees their response speed and performance. When high\-priority workloads cause the overall CPU load to become too high, Pod eviction is triggered automatically based on the configured eviction policy to ensure overall workload stability.

### CPU QoS levels

CPU QoS divides node CPU resources into different resource pools based on CPUSet and runs Pods of different types in the corresponding resource pools. The following table describes the CPU QoS levels supported by VKE.

|QoS level |Applicable scenarios |CPU allocation mode |Description |
|---|---|---|---|
|dedicated_cores |Latency\-sensitive workloads<br><br> |Dedicated CPU resources are used. The Pod does not share CPU resources with other Pods. |On nodes with Hyper\-Threading enabled, we recommend requesting an even number of cores in the CPU request to prevent the two logical cores (SMT siblings) on the same physical core from interfering with each other. |
|shared_cores |General online workloads |Use the shared pool CPUSet. Multiple Pods share the same group of CPU resources. |This is the default QoS level that the system uses when no QoS level is declared. Multiple Pods share the same group of CPU resources.<br><br>This QoS level applies to general online workloads and uses CPU resources from the shared pool. |
|reclaimed_cores |Offline, batch, or interruptible jobs |Use the reclaimed pool's CPUSet. Pods use the idle CPU resources in the shared pool. |Available resources are determined dynamically by the idle resources of the `shared_cores` level.<br><br>This QoS level applies to offline or batch processing tasks. Pods may be suppressed or evicted when node pressure increases. |
|system_cores |Critical system components |Use the system\-reserved resource pool. |Pods use CPUs from the system\-reserved resource pool.<br><br>When you use this QoS level, you need to add the startup parameter `--cpu-resource-plugin-reserve` to katalyst\-agent, the workload of the katalyst add\-on, to reserve a specified number of CPU cores for system_cores pods. For example, `--cpu-resource-plugin-reserve=4` reserves 4 CPU cores for Pods. If no cores are reserved, the resource pool is empty, and no core is available for scheduling system_cores Pods. |

### Notes on CPU core sharing between online and offline workloads

VKE provides the Overlap capability for online\-offline hybrid deployment scenarios to improve overall CPU utilization on nodes. The following table describes the capability in detail.

|**Status of the capability switch** |**Description** |**Advantage** |**Disadvantage** |
|---|---|---|---|
|Overlap enabled |Allow shared CPU cores (overlapping CPUSet pools):<br><br><br>* When online workloads have idle CPU resources, offline (reclaimed_cores) jobs can reuse them promptly.<br><br>* When online workloads need CPU resources, Overlap uses CPU Idle to make reclaimed_cores yield CPU core resources to online workloads. |Resource preemption and yielding are completed automatically by CPU Idle scheduling, with a switchover delay as low as milliseconds.<br><br> |This level depends on a kernel version that supports the CPU Idle feature. |
|Overlap disabled |CPU core sharing is not allowed (the CPUSet pools do not overlap). Online and offline workloads use separate, non\-overlapping CPU cores. |High compatibility. It does not depend on the CPU Idle capability of a later kernel version.<br><br> |Adjusting resources between online and offline workloads requires CPU cores to be reallocated. This process involves many steps and causes a high switchover delay. |

## Limits

* This feature is only supported for Pods deployed on Elastic Compute Service (ECS). Pods deployed on Elastic Container Instance (VCI) are not supported.

* Enabling CPU Idle depends on the following kernel features:

   * veLinux 1.0 images are supported, with kernel version 5.4.250\-9\-velinux1u2\-amd64 (veLinux 1.0) or 5.4.250\-9.2.ve1.x86_64 (veLinux 1.0 CentOS\-compatible version).

   * All veLinux 2.0 images, or Ubuntu 22.04 and later versions, are supported.

* We recommend against using In\-Place Pod Resize together with the Overlap capability, because the `cpu.weight` and `cpu.shares` values of Pods may fail to update.

## Prerequisites

* The cluster is in the **Running** state and has available ECS nodes. For details, see [Adding nodes](https://docs.byteplus.com/en/docs/vke/Adding-nodes) and [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).

* The katalyst add\-on version v0.5.13\-vke.19 or later has been installed in the cluster, with **QoS\-Aware Scheduling** selected on the add\-on configuration page and the **CPU QoS** capability enabled. For details, see [katalyst](https://docs.byteplus.com/en/docs/vke/katalyst-add-on).

## Procedure

### Step 1: Add a label to a node

After configuring the node label, you can use the CPU QoS capability of the katalyst add\-on to manage the corresponding node.

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the target cluster.

3. On the cluster management page, add labels to nodes as follows.

   **Add a label at the node pool level**

> **tip**

   > We recommend using this labeling method, as it allows labels to be added to nodes within the node pool.

   1. In the left navigation pane, click **Nodes** \> **Node pool**.

   2. On the **Node pool** page, find the target node pool and click **Edit** in the **Actions** column.

   3. On the **Edit node pool** page, specify the **Node labels** parameter and select **Enable auto renew for node labels and taints** in the **Advanced configurations** section in the **Node pool configuration** step.

      * **Label key**: `vke.node.katalyst.deploy`

      * **Label value**: `true`

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c549332a190171341caff0a325da7731.png)

   4. Update the configurations of the node pool based on the console wizard.

   **Add a label at the node level**

1. In the left navigation pane, click **Nodes** \> **Node**.

   2. On the **Node** page, find the target node and click `...` \> **Label management** in the **Actions** column.

   3. On the **Node details page**, click **Add new** on the **Label** tab, add the following label to the node, and then click **Confirm**.

      * **Label key**: `vke.node.katalyst.deploy`

      * **Label value**: `true`

### Step 2: (Optional) Enable Overlap

shared_cores and reclaimed_cores Pods share CPU cores

1. Create or edit an AdminQoSConfiguration object. The following YAML file `katalyst-config.yaml` serves as an example.

   > **tip**

   * > If an AdminQoSConfiguration object already exists in the cluster (for example, it was created when you configured Pod CPU Burst), you do not need to create another one. Edit the CPU core sharing settings in the existing AdminQoSConfiguration YAML instead.

   * > Make sure the node kernel and OS image meet the kernel version requirements for CPU Idle described in the "Limits" section.

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
       advisorConfig:
         cpuAdvisorConfig:
           allowSharedCoresOverlapReclaimedCores: true   # Allow shared_cores and reclaimed_cores to share CPU cores
           enabledReclaimedCoresCPUIdle: true            # Enable cpu.idle for reclaimed_cores Pods so that they yield CPU resources when they compete for cores with shared_cores pods
   ```

2. Create a KatalystCustomConfig (KCC) object. KCC provides resource management and hot reloading for AdminQoSConfiguration.

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

### Step 3: Create a workload

Declare the QoS type of the workload through a Pod annotation. The following table describes the annotations.

|**Annotation key** |**Annotation sample value** |**Description** |**Required** |
|---|---|---|---|
|katalyst.kubewharf.io/qos_level |dedicated_cores |CPU QoS level of the workload. Valid values:<br><br><br>* **dedicated_cores**: The Pods have dedicated CPU resources.<br><br>* **shared_cores**: Multiple Pods share the same group of CPU resources.<br><br>* **reclaimed_cores**: The Pods use the idle CPU resources in the shared pool.<br><br>* **system_cores**: The Pods use CPU resources in the system\-reserved resource pool.<br><br><br>> **tip**<br><br><br>> Generally, only VKE components use this QoS type. For actual workloads, we recommend against configuring this.<br> |No |

The following content uses Deployment creation as an example. For more workload operations, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).

1. Connect to the cluster via kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the Deployment. The following YAML file `cpu-qos-demo.yaml` serves as an example.

   **shared_cores**

The following code is a sample YAML for a Deployment at the `shared_cores` level.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: cpu-qos-shared-demo  # The Deployment name.
     namespace: default  # The namespace where the Deployment resides.
   spec:
     replicas: 1  # The number of Deployment replicas.
     selector:
       matchLabels:
         app: cpu-qos-shared-demo
     template:
       metadata:
         labels:
           app: cpu-qos-shared-demo
         annotations:
           katalyst.kubewharf.io/qos_level: "shared_cores"  # CPU QoS level of the workload. In this example, the value is shared_cores, which means that Pods in this workload share the same group of CPU resources with Pods of other workloads at the same QoS level.
       spec:
         containers:
           - name: nginx
             image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
             resources:
               requests:
                 cpu: "2"
                 memory: 2Gi
               limits:
                 cpu: "4"
                 memory: 4Gi
   ```

   **reclaimed_cores**

The following code is a sample YAML for a Deployment at the `reclaimed_cores` level.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: cpu-qos-reclaimed-demo  # The Deployment name.
     namespace: default  # The namespace where the Deployment resides.
   spec:
     replicas: 1  # The number of Deployment replicas.
     selector:
       matchLabels:
         app: cpu-qos-reclaimed-demo
     template:
       metadata:
         labels:
           app: cpu-qos-reclaimed-demo
         annotations:
           katalyst.kubewharf.io/qos_level: "reclaimed_cores"  # CPU QoS level of the workload. In this example, the value is reclaimed_cores, which means that Pods in this workload use the idle CPU resources in the shared pool.
       spec:
         containers:
           - name: worker
             image: doc-cn-beijing.cr.volces.com/vke/stress-ng:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
             resources:
               requests:
                 cpu: "1"
                 memory: 1Gi
               limits:
                 cpu: "2"
                 memory: 2Gi
   ```

   **dedicated_cores**

The following code is a sample YAML for a Deployment at the `dedicated_cores` level.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: cpu-qos-dedicated-demo  # The Deployment name.
     namespace: default  # The namespace where the Deployment resides.
   spec:
     replicas: 1  # The number of Deployment replicas.
     selector:
       matchLabels:
         app: cpu-qos-dedicated-demo
     template:
       metadata:
         labels:
           app: cpu-qos-dedicated-demo
         annotations:
           katalyst.kubewharf.io/qos_level: "dedicated_cores"  # CPU QoS level of the workload. In this example, the value is dedicated_cores, which means that Pods in this workload have dedicated CPUs.
           katalyst.kubewharf.io/memory_enhancement: '{"numa_binding":"true"}'  # Extended configuration. Here, it represents the NUMA enhancement configuration, including numa_binding (the NUMA binding configuration, which is required for the dedicated_cores level). For more information about the parameter, see the extended configuration table below.
       spec:
         containers:
           - name: worker
             image: doc-cn-beijing.cr.volces.com/vke/stress-ng:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
             resources:
               requests:
                 cpu: "1"
                 memory: 1Gi
               limits:
                 cpu: "2"
                 memory: 2Gi
   ```

   **system_cores**

The following code is a sample YAML for a Deployment at the `system_cores` level.

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: cpu-qos-system-demo  # The Deployment name.
     namespace: default  # The namespace where the Deployment resides.
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: cpu-qos-system-demo
     template:
       metadata:
         labels:
           app: cpu-qos-system-demo
         annotations:
           katalyst.kubewharf.io/qos_level: "system_cores"  # CPU QoS level of the workload. In this example, the value is system_cores, which means that Pods in this workload use CPU resources from the system-reserved resource pool.
           katalyst.kubewharf.io/cpu_enhancement: '{"cpuset_pool": "reserve"}'  # Extended configuration. Here, it represents the CPUSet resource pool configuration. For more information about the parameter, see the extended configuration table below.
       spec:
         containers:
           - name: worker
             image: doc-cn-beijing.cr.volces.com/vke/stress-ng:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
             resources:
               requests:
                 cpu: "1"
                 memory: 1Gi
               limits:
                 cpu: "2"
                 memory: 2Gi
   ```

   For some QoS levels, you can add the following extended settings to the Pod annotations.

   |**Annotation key** |**JSON Key** |**Type** |**Default value** |**Description and value** |
   |---|---|---|---|---|
   |katalyst.kubewharf.io/memory_enhancement |numa_binding<br><br> |string<br><br> |false |Whether the Pod needs to be bound to a NUMA node. Valid values:<br><br><br>* **false**: The Pod is not bound to a NUMA node.<br><br>* **true**: The Pod is bound to a NUMA node.<br><br><br>> **warning**<br><br><br>> Support for this parameter varies by CPU QoS level:<br><br><br><br>* > `dedicated_cores`: NUMA node binding is required. Configure this annotation and set `numa_binding` to `true`.<br><br><br>* > `shared_cores`: Binding is optional.<br><br><br>* > `reclaimed_cores`: Binding is not supported.<br><br><br>* > `system_cores`: Binding is not needed.<br> |
   |katalyst.kubewharf.io/cpu_enhancement |cpuset_pool |string |reserve |Whether to specify a CPUSet resource pool. Valid values:<br><br><br>* **reserve**: Reserves a CPUSet resource pool with the number of CPU cores via the katalyst\-agent startup parameter `--cpu-resource-plugin-reserve`.<br><br><br>> **warning**<br><br><br>> Configure this only when using the system_cores QoS level and you need to bind the Pod to the reserved pool. This setting is not required for general workloads.<br> |

3. Run the following command to create the Deployment.

   ```bash
   kubectl apply -f cpu-qos-demo.yaml
   ```

4. (Optional) Configure CPU reservation for system_cores

   If you need to run critical system components such as log collectors and monitoring agents at the system_cores level, reserve CPU cores for these system components through the katalyst\-agent startup parameter `--cpu-resource-plugin-reserve`. Without the reservation, system_cores Pods have no cores available.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation pane, click **Cluster**. On the page that appears, click the name of the target cluster.

   3. In the left navigation bar of the cluster management page, click **Workload** \> **DaemonSet**.

   4. In the **katalyst\-system** namespace, find **katalyst\-agent** and click **Update** in the **Actions** column.

   5. In the **Container configuration** step, go to the **Run parameter** section in **Start command** to add a startup parameter `--cpu-resource-plugin-reserve` to specify the number of CPU cores to reserve.

      > **tip**

      * > We recommend setting the number of reserved cores based on the actual usage of system components on the node. An excessively small value restricts system components, while an excessively large value takes resources away from workloads.

      * > This parameter takes effect only for newly scheduled Pods. Pods that are already running are not rebound to cores automatically.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_97ce51dab9a7969ff398d2eddd01f48d.png)

   6. After you complete the configuration as instructed by the wizard, save the changes and wait until the katalyst\-agent pod restarts.

### Step 4: Configure the pressure eviction policy

To prioritize the stability of high\-priority workloads when a node or node pool is under pressure, explicitly enable the eviction policy through AdminQoSConfiguration.

> **tip**

> In the sample YAML below, commented\-out parameters are optional. Apply them as needed by referring to the comments. We recommend keeping the default values for parameters without comments.

1. Create or edit an AdminQoSConfiguration object. The following YAML file `katalyst-config.yaml` serves as an example.

   > **tip**

   * > If an AdminQoSConfiguration object already exists in the cluster, you do not need to create another one. Edit the CPU QoS settings in the existing AdminQoSConfiguration YAML instead.

   * > Multiple eviction policies are provided below, and all of them can be added to the same AdminQoSConfiguration YAML file.

   **System-wide CPU pressure-based eviction**

The example below shows a minimal system\-wide CPU pressure eviction configuration.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: AdminQoSConfiguration
   metadata:
     name: katalyst-config  # This field has a fixed value: the name of the AdminQoSConfiguration object.
     namespace: katalyst-system  # This field has a fixed value: the namespace of the AdminQoSConfiguration object.
     labels:
       vke.node.katalyst.deploy: "true" # The label related to the fine-grained resource management feature of node pool configuration. This feature applies only to nodes with this label.
   spec:
     config:
       evictionConfig:
         cpuSystemPressureEvictionConfig:
           enableCPUSystemPressureEviction: true # Whether to enable the system CPU pressure awareness and eviction policy. Valid values: true (enabled) and false (disabled).
           usageUpperBoundRatio: 0.8 # Eviction threshold for node CPU utilization. Value range: 0 to 1. A value of 0.8 corresponds to 80%.
    #       usageLowerBoundRatio: 0.8 # Taint threshold for node CPU utilization. Value range: 0 to 1. A value of 0.8 corresponds to 80%.
    #       evictionWorkloadScope: declaredEvictable # Indicates that AdminQoSConfiguration selects Pods for eviction only from those with the annotation katalyst.kubewharf.io/evictable=true.
    #       evictionCoolDownTime: 300s # Eviction cooldown period, in seconds.
   ```

   **Shared pool CPU utilization-based eviction**

To enable shared pool CPU utilization eviction, add the following settings to the same AQC.

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
       evictionConfig:
         cpuPressureEvictionConfig:
           enableCPUUsageEviction: true  # Whether to enable eviction based on shared pool CPU utilization. Valid values: true (enabled) and false (disabled).
    #       usageUpperBoundRatio: 0.9 # Eviction threshold for shared pool CPU utilization. Value range: 0 to 1. A value of 0.9 corresponds to 90%.
    #       usageLowerBoundRatio: 0.8 # Taint threshold for shared pool CPU utilization. Value range: 0 to 1. A value of 0.8 corresponds to 80%.
    #       usageEvictionCoolDownTime: 300s # Eviction cooldown period, in seconds.
   ```

   **Reclaim pool suppression ratio-based eviction**

To enable eviction based on the reclaimed pool's suppression ratio, add the following settings to the same object.

   > **tip**

   > The reclaimed pool's suppression ratio equals the sum of requests from reclaimed_cores pods divided by the number of available CPU cores in the reclaimed pool.

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
       evictionConfig:
         cpuPressureEvictionConfig:
           enableSuppressionEviction: true  # Whether to enable eviction based on the reclaimed pool's suppression ratio. Valid values: true (enabled) and false (disabled).
    #       maxSuppressionToleranceRate: 5  # Maximum suppression tolerance ratio that a Pod can declare, which is also the default suppression tolerance ratio.
   ```

   For reclaimed_cores Pods, you can also declare a separate suppression tolerance threshold using the annotation `katalyst.kubewharf.io/cpu_enhancement`. The following code shows the YAML content of a sample Pod.

   ```YAML
   apiVersion: v1
   kind: Pod
   metadata:
     name: hello-pod  # Pod Name.
     namespace: namespace-a  # Namespace to which the pods belong.
     annotations:
       katalyst.kubewharf.io/qos_level: "reclaimed_cores"
       katalyst.kubewharf.io/cpu_enhancement: |  # Extended configuration. The value is a JSON string.
         {
           "suppression_tolerance_rate": "2.0" # Suppression tolerance threshold. The value is a string in the range (0, maxSuppressionToleranceRate].
         }
   spec:
     containers:
       - name:    hello-pod # The container name.
         image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0  # The container image address and tag. Replace them with your actual information. If a public image is used, ensure that the cluster has access to the Internet.
         ports:
           - containerPort: 8080 # The container port.
   ```

2. (Optional) Create a KatalystCustomConfig (KCC) object. KCC provides resource management and hot reloading for AdminQoSConfiguration.

   > **tip**

   > If the KCC object was created in Step 2, skip this step. If the KCC object was not created in Step 2, you need to create one here.

   ```YAML
   apiVersion: config.katalyst.kubewharf.io/v1alpha1
   kind: KatalystCustomConfig
   metadata:
     name: katalyst-config  # This field has a fixed value: the name of the KatalystCustomConfig object.
     namespace: katalyst-system  # This field has a fixed value: the namespace of the KatalystCustomConfig object.
     labels:
       vke.node.katalyst.deploy: "true"  # This field has a fixed value. The label related to the fine-grained resource management feature of node pool configuration.
   spec:
     targetType:  # Fixed values, indicating the GVR information of AdminQoSConfiguration.
       group: config.katalyst.kubewharf.io
       resource: adminQoSconfigurations
       version: v1alpha1
   ```

## Validate results

### Verify the Pod QoS annotation

1. Obtain the name of the Pod that belongs to the Deployment.

   ```Bash
   # Replace <deployment-name> below with the actual Deployment name, and replace <namespace> with the namespace of the Deployment.
   kubectl get pods -l app=<deployment-name> -n <namespace>
   ```

2. Confirm that the annotation on the target workload is correctly applied.

   ```Bash
   # Replace <pod_name> below with the actual pod name.
   kubectl get pod <pod-name> -o jsonpath='{.metadata.annotations}'
   ```

   The expected result is` dedicated_cores`, `shared_cores`, `reclaimed_cores`, or `system_cores`, which indicates that the annotation is correctly applied.

### Verify that the CPUSet resource pool settings take effect

1. Run the following command to obtain the Pod's UID.

   ```Bash
   # Replace <pod_name> below with the actual Pod name.
   kubectl get pod <pod-name> -o jsonpath='{.metadata.uid}'
   ```

2. Run the following command to view the container ID of the Pod.

   ```Bash
   # Replace <pod_uid> below with the actual pod UID.
   kubectl get pod <pod_uid> -o jsonpath='{.status.containerStatuses[*].containerID}'
   ```

4. Log in to the node where the Pod resides. For the login method, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

5. View the value of `cpuset.cpus` in the container cgroup directory.

   **cgroup v1**

```Bash
   # Replace <container-id> and <pod_uid> below with the actual container ID and pod UID.
   # Guaranteed pod
   cat /sys/fs/cgroup/cpu/kubepods/pod<pod-uid>/<container-id>/cpuset.cpus
   
   # Burstable pod
   cat /sys/fs/cgroup/cpu/kubepods/burstable/pod<pod-uid>/<container-id>/cpuset.cpus
   
   # Besteffort pod
   cat /sys/fs/cgroup/cpu/kubepods/besteffort/pod<pod-uid>/<container-id>/cpuset.cpus
   ```

   **cgroup v2**

```Bash
   # Replace <container-id> or <pod_uid> below with the actual container ID or Pod UID.
   # Guaranteed pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpuset.cpus
   
   # Burstable pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpuset.cpus
   
   # Besteffort pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-besteffort.slice/kubepods-besteffort-pod<pod-uid>.slice/cri-containerd-<container-id>.scope/cpuset.cpus
   ```

   After CPU QoS takes effect, the CPUSet resource pool settings take effect differently for Pods of different QoS levels:

   * The CPUSet of each dedicated_cores Pod consists of dedicated cores.

   * The CPUSet of all shared_cores and reclaimed_cores Pods depends on whether Overlap is enabled:

      * Overlap is disabled: shared_cores and reclaimed_cores use separate, non\-overlapping CPUSet resource pools, and neither pool includes the CPU resources dedicated to dedicated_cores.

      * Overlap is enabled: The Pods of shared_cores and reclaimed_cores use the same (overlapping) CPUSet resource pool, which does not include the CPU resources dedicated to dedicated_cores. Compare the `cpuset.cpus` values of a shared_cores Pod and a reclaimed_cores Pod on the same node. The two values should be the same.

### Verify that CPU Idle takes effect

> **tip**

> If only the Overlap capability is enabled, verify that CPU Idle takes effect as follows.

1. Log in to the node where the Pod resides. For the login method, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. View the value of `cpuset.cpus` in the container cgroup directory.

   **cgroup v1**

```Bash
   # Replace <container-id> or <pod_uid> below with the actual container ID or Pod UID.
   # Guaranteed pod
   cat /sys/fs/cgroup/cpu/kubepods/pod<pod-uid>/cpu.idle
   
   # Burstable pod
   cat /sys/fs/cgroup/cpu/kubepods/burstable/pod<pod-uid>/cpu.idle
   
   # Besteffort pod
   cat /sys/fs/cgroup/cpu/kubepods/besteffort/pod<pod-uid>/cpu.idle
   ```

   **cgroup v2**

```Bash
   # Replace <container-id> or <pod_uid> below with the actual container ID or Pod UID.
   # Guaranteed pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable-pod<pod-uid>.slice/cpu.idle
   
   # Burstable pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-burstable.slice/kubepods-burstable-pod<pod-uid>.slice/cpu.idle
   
   # Besteffort pod
   cat /sys/fs/cgroup/kubepods.slice/kubepods-besteffort.slice/kubepods-besteffort-pod<pod-uid>.slice/cpu.idle
   ```

   After Overlap is enabled, the `cpu.idle` value differs by Pod QoS level:

   * reclaimed_cores pods: The value should be 1.

   * dedicated_cores pods: The value should be 0.

   * shared_cores pods: The value should be 0.

   * system_cores pods: The value should be 0.

## Monitoring metrics

The following table describes the CPU QoS metrics. To monitor this feature, [enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability), configure [container service observability](https://docs.byteplus.com/en/docs/vke/VKE-observability), and select the CPU QoS\-related metrics of the katalyst add\-on listed in the following table. After you enable metric observability, you can view the metrics in the [preset dashboard](https://console.byteplus.com/observe/dashboard/dashboard/2927/view?type=builtin).

> **tip**

> Enabling the following metrics incurs VMP fees. For detailed billing information, see [Product billing](https://docs.byteplus.com/en/docs/vmp/billing-overview).

To observe how CPU QoS performs, we recommend focusing on the following metrics:

|Metric name |Metric type |Tags |Meaning |
|---|---|---|---|
|metaserver_update_config |Counter |instance,status |The status of dynamic configuration loading in the metaserver. |
|cpu_advisor_update_duration |Gauge(ms) |instance |The time taken for a single Advisor calculation. A sudden spike indicates an anomaly in policy computation. |
|cpu_advisor_pool_size |Gauge |instance,name |The target pool size (in cores) finally calculated by Advisor. |
|cpu_pool_size |Gauge |instance,poolName |The pool size (in cores) actually written to CPUSet by QRM. |
|cpu_pool_usage_cores |Gauge |instance,pool_name |Actual CPU usage of the resource pool (in cores). |
| <br><br>cpu_advisor_indicator_observed |Gauge |instance,owner_pool_name,indicator<br><br> |Metrics for calculating shared pool CPU resource demand:<br><br><br>* Scheduling latency: `indicator="cpu_sched_wait"`<br><br>* CPU utilization: `indicator="cpu_usage_ratio"` |
|cpu_advisor_indicator_target<br><br> |Gauge |instance,owner_pool_name,indicator |Metric thresholds for the estimated shared pool CPU resource demand. Exceeding a threshold indicates that scale\-out is required:<br><br><br>* Scheduling latency: `indicator="cpu_sched_wait"`<br><br>* CPU utilization: `indicator="cpu_usage_ratio"` |
|cpu_reclaimed_requests_cores |Gauge |instance |Sum of the CPU requests of all Pods in the reclaimed pool. |
|eviction_kill_pod_total<br><br> |Counter |instance,name,state<br><br> |Total number of Pods actually evicted.  `name` indicates the eviction add\-on name:<br><br><br>* **cpu\-pressure\-shared\-usage\-plugin**: Shared pool CPU utilization eviction add\-on<br><br>* **system\-cpu\-pressure\-eviction\-plugin**: System\-wide pressure eviction add\-on<br><br>* **cpu\-pressure\-suppression\-plugin**: Reclaim pool suppression rate eviction add\-on |
|cpu_idle_enabled |Gauge |node |Whether the CPU Idle feature is enabled successfully. |
|cpu_idle_kernel_supported |Gauge |node |Whether the node supports the CPU Idle feature. |
|cpu_idle_operation_total |Counter |node,operation,status,reason |The number of operations of different types performed by the CPU Idle feature. |
|cpu_idle_managed_targets |Gauge |node,target_type,state |Number of Pods managed by CPU Idle. |
|cpu_idle_reconcile_duration_seconds |Gauge |node |The time taken for the update process during the CPU Idle phase. |
|cpu_reconcile_failed |Gauge |node |Number of failed CPU QoS reconcile events. |
|cpu_container_sched_wait_seconds |Counter |node,pool_name,pod,container |Average waiting time (in seconds) before a container is scheduled.<br><br> |
|cpu_container_sched_run_timeslices |Counter |node,pool_name,pod,container |The number of times the container is scheduled to run. |

## Related documentation

[CPU QoS FAQ](https://docs.byteplus.com/en/docs/vke/CPU_QoS_scheduling_FAQs)
