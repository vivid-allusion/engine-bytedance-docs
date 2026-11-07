---
title: "Configuring mGPU scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-mGPU"
---

This topic mainly describes how to use the mGPU feature in Vital Kubernetes Engine (VKE) to enable multiple containers to share a GPU.

<span id="e8Z2lbrr"></span>
## Limits


* A pod cannot use mGPU and RDMA add\-ons simultaneously.

* mGPU cannot be used together with privileged containers. Otherwise, the containers will fail to be created or deleted.

* When you use the mGPU feature, take note of the following environment requirements and usage limits on clusters and GPUs.



|Project |Requirement |
|---|---|
|Kubernetes version |The version must be v1.20.15\-vke.4 or later.<br><br>For the method of viewing the Kubernetes version of a cluster, refer to [FAQs](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster). |
|Operating system |When you create a cluster, if you specify a **public image** provided by VKE as the **operating system**, the system will automatically configure an operating system of the corresponding version. Currently supported operating systems include veLinux 1.0, veLinux 1.0 CentOS Compatible, Ubuntu 20.04, and Ubuntu 22.04. |
|Kernel Version |When you create a cluster, if you specify a **public image** provided by VKE as **the operating system**, the system will automatically configure an operating system kernel of the corresponding version. Currently, kernel version 5.4 is supported. |
|NVIDIA driver version |Use v470 or v535. The officially supported minor versions shall prevail. For more details, refer to [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).<br><br>When you create a GPU\-accelerated node pool, the system will automatically configure an NVIDIA driver of the corresponding version. |
|GPU |VKE supports mainstream NVIDIA GPU types such as Turing, Volta, Ampere, Hopper, and Ada Lovelace. If you have requirements for other types of GPUs, consult official pre\-sales or technical support.<br><br>For node instance types supported by different types of GPUs, refer to [Specifications of GPU cloud computing instances](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types). |
|Number of mGPUs (corresponding to the number of containers) |Up to 16 mGPUs can be created for one GPU. Computing performance deteriorates as the number of mGPUs increases. It is recommended that you plan the number of mGPUs that are deployed on a single GPU based on the resource size requested by containers. |
|Number of containers |When you use mGPU, it is recommended that the number of containers in a single pod does not exceed 5. |


<span id="0isY8hz2"></span>
## Scheduler description

mGPU must be used together with the scheduler\-plugin add\-on to achieve shared GPU scheduling among containers. The scheduler\-plugin add\-on extends the scheduling capability and policy of the native kube\-scheduler, which allows you to configure Binpack or Spread policies for GPU nodes and GPU memory. For the detailed introduction of the add\-on and scheduling policy configuration descriptions, refer to the [scheduler-plugin](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.c2NoZWR1bGVyLXBsdWdpbi3nu4Tku7Y=) section of the Installing an add\-on topic.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In this topic, you need to install the scheduler\-plugin add\-on when you create a cluster, and cannot modify the configurations of the add\-on after it is configured for the first time. Therefore, when you configure the <strong>add\-on</strong> during the creation of the cluster, configure the Binpack or Spread scheduling policy based on your business requirements.</div>


If you do not modify the scheduling policy of the scheduler\-plugin add\-on when you create the cluster, mGPU will adopt the following default scheduling policy:


|GPU node scheduling policy |GPU card scheduling policy |Scheduling mode |Application scenarios |
|---|---|---|---|
|Spread |Binpack |* Pods are spread to nodes with low GPU allocation rate.<br><br>* Containers are preferentially scheduled to GPUs with high packing rates on nodes. |High fault isolation performance is achieved among nodes and a small number of fragmented resources exist. |


<span id="UPScbDXJ"></span>
## Prerequisites

The mgpu addon has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you need to use an mGPU computing power allocation policy, make sure that the version of the mgpu add\-on is v0.0.3 or later. For detailed description, refer to <a href="https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies">Configuring an mGPU computing power allocation policy</a>.</div>


<span id="grHeyzAJ"></span>
## Procedure

<span id="AD3yWpSy"></span>
### Step 1: Create a GPU node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list, click the name of the target cluster name to open the cluster management page.

3. In the left navigation bar, click **Node pool**.

4. On the Node pool page, click **Create node pool** to create a node pool that meets your requirements. For parameter details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * For **Instance type**, select **GPU Accelerated** to add nodes with GPUs to the cluster.

   * In the **Advanced settings** section, click **Add new** to add a GPU scheduling label to the node pool.

      * Set the key to `vke.node.gpu.schedule` and the value to `mgpu`. This setting enables mGPU scheduling and GPU video memory isolation for nodes in this node pool.

         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="3">warning         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">For details and considerations for using the GPU scheduling label, see <a href="https://docs.byteplus.com/en/docs/vke/GPU-scheduling-labels">GPU scheduling overview</a>.         </div>
         

         * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="3">You can select or deselect <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool">Enable auto renew for node labels and taints</a> to determine whether to synchronously add new labels to existing nodes in the pool. If you disable this feature, the GPU scheduling capability on existing nodes may not meet your expectations. Proceed with caution.         </div>
         

      * Set the label key to `vke.volcengine.com/mgpu-compute-policy` and the label value to `fixed-share`, `guaranteed-burst-share`, or `native-burst-share`. This sets a computing power allocation strategy for nodes in the node pool.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">For details on computing power allocation, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies">Allocating mGPU computing power</a>.         </div>
         

<span id="dIJv7GAN"></span>
### Step 2: Configure a workload

This topic provides an example of how to enable the multi\-card sharing feature when you create a Deployment. For a detailed procedure for creating a Deployment, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<span id="TsXrITwO"></span>
#### Creating through the console


1. In the left navigation bar of the cluster management page, click **Workload \> Deployment**.

2. On the **Deployment** page, create a Deployment or update an existing Deployment. In the **ResourceQuota** section of the **Container configuration** step, configure GPU resources based on your business requirements.

   
   |**Parameter** |**Description** |
   |---|---|
   |GPU resource type |In this scenario, select **mGPU**. |
   |Multi\-card sharing configuration |The mGPU multi\-card sharing feature allows a single container to use computing power and GPU video memory resources jointly provided by multiple GPU cards on the same node. In this example, keep it off. For information about how to configure multi\-card sharing, see [Using mGPUs for multi-card sharing](https://docs.byteplus.com/en/docs/vke/Multiple-GPU-sharing). |
   |GPU computing power |Configure the GPU computing power of the container. You can set it to a value between 0.01 and 1 with two decimal places or to a positive integer greater than 1. For example, set it to 0.01 or 2.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The recommended minimum GPU computing power for mGPUs is 0.05 with a step size of 0.05 (when fewer than 1 card), and the minimum GPU video memory is 1 GiB. The recommended value can improve your user experience in GPU sharing among containers.</div><br> |
   |GPU memory |Specify the GPU video memory of the container, which is provided by multiple GPUs in equal shares.<br><br><br>* If you set the GPU computing power parameter to a value between 0.01 and 1 with two decimal places, set the GPU memory parameter to a value that is greater than or equal to 256 MiB with a step of 1.<br><br>* If you set the GPU computing power to an integer that is greater than or equal to 1, the entire computing power of the GPU is used. Also, all the GPU video memory is used. |
   |Graphics card type |Configure the GPU model of nodes that the Pod can be scheduled to. By default, no GPU model restriction applies. If you specify a model, the Pod will be scheduled to nodes using that GPU model. |
   

3. After configuring other parameters, click **Confirm**.


<span id="GpfmZQlV"></span>
#### Creating through kubectl

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In mGPU use scenarios, the value of the <strong>requests</strong> field must be consistent with that of the <strong>limits</strong> field.</div>


Use YAML to create a workload that applies mGPU scheduling:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mgpu-demo # The name of the Deployment.
  namespace: default # The namespace of the Deployment.
spec:
  replicas: 1 # Number of pod instances
  selector:
    matchLabels:
      app: mgpu-deployment
  template:
    metadata:
      labels:
        app: mgpu-deployment
    spec:
      containers:
      - name: mgpu-container # The container name.
        image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0 # Container image address
        command: ["/bin/sh"]
        args: ["-c", "sleep infinity"]
        resources:
         requests:   # Keep the values of the requests field the same as those of the limits field.
           vke.volcengine.com/mgpu-memory: 4096
           vke.volcengine.com/mgpu-core: 30
         limits:
           vke.volcengine.com/mgpu-memory: 4096   # GPU memory, measured in MiB. In this example, the GPU memory is 4 GiB.
           vke.volcengine.com/mgpu-core: 30      # GPU computing power percentage. In this example, it is 30%.
        ports:
        - containerPort: 80
```


<span id="mHugHcTD"></span>
## Validating results

<span id="wUzNWNVR"></span>
### Viewing GPU card information

You can use the mGPU Client (`mgpu-cli`) to view mGPU\-related information in the terminal.


3. Log in to the node where the pod is located. You can log in to the node through ECS Terminal. For detailed operations, refer to the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) section of the Managing nodes topic.

4. Run the following command to view graphics card information.

   ```shell
   mgpu-cli device info -a
   ```
   

   The system returns a response similar to the following one. You can view information about the graphics card, such as the percentage of its unassigned computing power and its scheduling policy.

   ```Bash
   +-----------------------------------+-------------+
   |             device_id             |      0      |
   +-----------------------------------+-------------+
   |        compute_free_weight        |     100     |
   +-----------------------------------+-------------+
   |    compute_free_weight_online     |     70      |
   +-----------------------------------+-------------+
   |     compute_load_balance_mode     |      0      |
   +-----------------------------------+-------------+
   |          compute_policy           |      0      |
   +-----------------------------------+-------------+
   |        compute_qos_enabled        |      1      |
   +-----------------------------------+-------------+
   | compute_qos_enabled_native_burst  |      1      |
   +-----------------------------------+-------------+
   |         compute_timeslice         |     200     |
   +-----------------------------------+-------------+
   |  compute_timeslice_native_burst   |    4096     |
   +-----------------------------------+-------------+
   | compute_total_weight_native_burst |     30      |
   +-----------------------------------+-------------+
   |           device_major            |     510     |
   +-----------------------------------+-------------+
   |       instance_deploy_mode        |      1      |
   +-----------------------------------+-------------+
   |          instance_major           |     509     |
   +-----------------------------------+-------------+
   |       online_offline_switch       |      2      |
   +-----------------------------------+-------------+
   |        user_instance_major        |     511     |
   +-----------------------------------+-------------+
   |          vmem_free_bytes          | 23359324160 |
   +-----------------------------------+-------------+
   |            vmem_limit             |  4096 MiB   |
   +-----------------------------------+-------------+
   ```
   

   
   |Metric name |Metric meaning |
   |---|---|
   |compute_free_weight_online |The percentage of unassigned computing power of the device (70% in this example). |
   |compute_load_balance_mode |The load balancing mode among containers when the containers use the device. |
   |compute_policy |Specify a computing power scheduling policy. Valid values:<br><br><br>* 0: `fixed-share`<br><br>* 1: `guaranteed-burst-share`<br><br>* 2: `native-burst-share` |
   |compute_timeslice |The percentage of the computing power time slice. |
   |device_major |`/dev/mgpuX` is the major device number. |
   |instance_major |`/dev/mgpuXinstY` and `/dev/mgpuXctl-$(container_id)` are the major device numbers. |
   |vmem_free_bytes |The remaining GPU memory capacity of the device. Unit: byte. |
   


<span id="sy8R7cRW"></span>
### Viewing container\-level mGPU information


1. Log in to the node where the pod is located. You can log in to the node through ECS Terminal. For detailed operations, refer to the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) section of the Managing nodes topic.

2. Run the following command to view mGPU information at the container level.

   ```shell
   mgpu-cli container info
   ```
   

   The system returns a response similar to the following one. You can view container\-level mGPU video memory allocation details.

   ```Bash
   +--------------+-----------+-------------+---------+------------------+---------------------+----------------+-----------------------------+-----------------------+-------+--------------------------+--------+----------+-------+----------------+------------+---------------+------------------+
   | container_id | device_id | instance_id | pod_uid | compute_priority | compute_qos_enabled | compute_weight | compute_weight_native_burst | compute_weight_online | minor | nvidia/compute_timeslice | online | position | tasks |   vmem_info    | vmem_limit | vmem_priority | vmem_qos_enabled |
   +--------------+-----------+-------------+---------+------------------+---------------------+----------------+-----------------------------+-----------------------+-------+--------------------------+--------+----------+-------+----------------+------------+---------------+------------------+
   | 7b0622290a6e | 0         | 0           | N/A     | 0                | 1                   | 0              | 30                          | 30                    | 0     | 0                        | 1      | normal   | N/A   | Free: 4096 MiB | 4096 MiB   | 0             | 1                |
   +--------------+-----------+-------------+---------+------------------+---------------------+----------------+-----------------------------+-----------------------+-------+--------------------------+--------+----------+-------+----------------+------------+---------------+------------------+
   ```
   

   
   |Metric name |Metric meaning |
   |---|---|
   |container_id |The container ID. |
   |device_id |The device ID that corresponds to the instance. |
   |instance_id |The instance ID. |
   |compute_weight |The percentage of offline computing power allocated to the instance. |
   |compute_weight_native_burst |The percentage of computing power allocated to this instance under the `native burst` policy. |
   |compute_weight_online |The percentage of online computing power allocated to the instance. |
   |online |Whether it is an online container. |
   |vmem_info |Information about the video memory requested by a container, including free video memory, PID, and used video memory. |
   |vmem_limit |The upper limit on the video memory requested by a container. |
   


<span id="09JNB46r"></span>
### Viewing mGPU monitoring data

You can monitor various mGPU metrics by using cloud\-native observability. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a1bec3ac602e2a2082f6c5797929448.png) </span>

<span id="MIpPjpUM"></span>
## Related documentation


* [Allocating mGPU computing power](https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies)

* [Using mGPU to implement multi-card sharing](https://docs.byteplus.com/en/docs/vke/Multiple-GPU-sharing)

* [Implementing online-offline hybrid deployment based on mGPUs](https://docs.byteplus.com/en/docs/vke/Using_mGPU_for_online-offline_hybrid_deployment)
