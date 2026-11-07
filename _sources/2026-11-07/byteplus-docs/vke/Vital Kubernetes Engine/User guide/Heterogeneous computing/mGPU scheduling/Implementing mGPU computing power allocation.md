---
title: "Implementing mGPU computing power allocation"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies"
---

This topic mainly describes how to configure an mGPU computing power allocation policy and use this policy for scheduling in workloads.

<span id="0g35RjS0"></span>
## Usage notes

When you use an mGPU computing power allocation policy, take note of the following requirements and limits on clusters and GPU add\-ons. For more mGPU usage notes, see [Configuring mGPU scheduling](https://docs.byteplus.com/en/docs/vke/Using-mGPU).


|Project |Requirement |
|---|---|
|Kubernetes version |The version must be v1.20.15\-vke.6 or later.<br><br>For the method of viewing the Kubernetes version of a cluster, see [FAQs](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you have a cluster of v1.20.15\-vke.6 or earlier, where mGPU\-related businesses already exist and you want the cluster to use an mGPU computing power allocation policy, submit a <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210">ticket</a> to obtain technical support and upgrade the Kubernetes version.</div><br> |
|mGPU add\-on version |The version must be v0.0.3 or later. For the method of upgrading an add\-on, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on). To view the release records of each add\-on, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/mgpu). |


<span id="iRVEgCIl"></span>
## Description of the computing power allocation policy

mGPU supports the following three computing power allocation policies.


|Value |Description |
|---|---|
|fixed\-share (default) |Fixed quota. Each container has a fixed computing power quota, which cannot be exceeded even if the remaining GPU computing power exists when the containers are running. |
|guaranteed\-burst\-share |Fixed contention. Each container has a minimum computing power quota. However, the containers can use any idle GPU computing power. |
|native\-burst\-share |Contention mode. You can specify a computing power quota. The higher value indicates the higher quota can be contended for, but not all containers can contend for a quota equal to the specified computing power quota. |


<span id="FxPFl52B"></span>
## Prerequisites

The related configuration of mGPU is complete. For details, see [Configuring mGPU scheduling](https://docs.byteplus.com/en/docs/vke/Using-mGPU).

<span id="QSGAb1MK"></span>
## Procedure

<span id="JqxZWmmQ"></span>
### Step 1: Configure a computing power allocation policy for nodes


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target cluster to go to the management page of the cluster.

3. Configure a computing power allocation policy for the mGPU node pool or nodes.

   
   <Tabs>
   <Tab zoneid="rQZV9POBBb" title="Node pools">
   <TabTitle>Node pools</TabTitle>
   
   1. In the left navigation bar on the cluster management page, click **Nodes** \> **Node pool**.
   
   2. On the **Node pool** page, find the node pool where mGPU\-related configuration is complete, and click **Edit** in the **Actions** column.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can also create a mGPU\-related GPU\-accelerated node pool in a cluster and configure a computing power allocation policy. The cluster must meet the environment requirements for configuring mGPU computing power allocation policies. The requirements include the Kubernetes version and the mGPU add\-on version. In this case, you do not need to restart nodes. For detailed operations, see <a href="https://docs.byteplus.com/en/docs/vke/Using-mGPU">mGPU usage methods</a>.   </div>
      
   
   3. In the **Advanced settings** section, set the label key to `vke.volcengine.com/mgpu-compute-policy` and the label value to `fixed-share`, `guaranteed-burst-share`, or `native-burst-share`. This sets a computing power allocation policy for nodes in the node pool.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can select or deselect <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool">Enable auto renew for node labels and taints</a> to determine whether to synchronously add new labels to existing nodes in the pool. If you disable this feature, the GPU computing power allocation policy on existing nodes may not meet your expectations. Proceed with caution.   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you change an mGPU computing power allocation policy for nodes in a node pool, you need to restart all mGPU\-related nodes in the node pool to make the policy take effect.   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not configure a computing power allocation policy, which means that you do not configure the <code>vke.volcengine.com/mgpu-compute-policy</code> node label, the <code>fixed-share</code> policy is used by default to allocate computing power.   </div>
      
   
   
   </Tab>
   <Tab zoneid="yik8IVM7EW" title="Nodes">
   <TabTitle>Nodes</TabTitle>
   
   1. In the left navigation bar on the cluster management page, click **Nodes** \> **Node**.
   
   2. On the **Node** page, find the node where mGPU\-related configuration is complete, and in the **Actions** column, click `...` \> **Label management**.
   
   3. On the **Label** tab, click **Add new**. At the end of the node label list, add a label with the key `vke.volcengine.com/mgpu-compute-policy` and the value as `fixed-share`, `guaranteed-burst-share`, or `native-burst-share`, which indicates that a computing power allocation policy that corresponds to the value is configured for the node.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you change an mGPU computing power allocation policy for a node, you need to restart the node to make the policy take effect. For the method of restarting nodes, see <a href="https://docs.byteplus.com/en/docs/ecs/Restarting-instances">Restarting instances</a>.   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>vke.volcengine.com/mgpu-compute-policy</code> is a system label. After you add the system label on the node, you cannot modify its value.   </div>
      
   
      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you do not add the <code>vke.volcengine.com/mgpu-compute-policy</code> node label, the <code>fixed-share</code> policy is used by default to allocate computing power.   </div>
      
   
   
   </Tab>
   </Tabs>
   


<span id="okx2IZ26"></span>
### Step 2: Configure a workload

This topic provides an example of how to enable the multi\-card sharing feature when you create a Deployment. For a detailed procedure for creating a Deployment, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<span id="fMiRB35X"></span>
#### Creating through the console


1. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. On the **Deployment** page, create a Deployment or update an existing Deployment. In the **Advanced settings** step, go to the **Instance configuration** section to configure a computing power allocation policy for the Pod.

   For **Instance annotation**, add an annotation with its key set to `vke.volcengine.com/mgpu-compute-policy` and its value set to `fixed-share`, `guaranteed-burst-share`, or `native-burst-share`.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If no computing power allocation policy is configured for a workload , it will be scheduled using the <code>fixed-share</code> policy by default.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Ensure that the cluster contains GPU Accelerated nodes with the same policy as the workload. For example, if the scheduling policy of the workload is <code>fixed-share</code>, ensure that the cluster has GPU Accelerated nodes with the <code>fixed-share</code> policy. Otherwise, the workload will fail to be scheduled due to no suitable resources for scheduling.   </div>
   


<span id="nG1W74pU"></span>
#### Creating through kubectl

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the <code>spec.template.metadata</code> section, use the annotation <code>vke.volcengine.com/mgpu-compute-policy</code> to configure a computing power allocation policy for the corresponding Pod.</div>


Use YAML to create a workload that has a computing power allocation policy. The following code is an example:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mgpu-demo
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mgpu-deployment
  template:
    metadata:
      labels:
        app: mgpu-deployment
      annotations:
        vke.volcengine.com/mgpu-compute-policy: guaranteed-burst-share   # The computing power allocation policy for the workload. It defaults to the fixed-share policy.
    spec:
      containers:
      - name: mgpu-container
        image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0
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


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">If no computing power allocation policy is configured for a workload, it will be scheduled using the <code>fixed-share</code> policy by default.</div>


* <div data-tips="true" data-tips-type="warning">Ensure that the cluster contains GPU Accelerated nodes with the same policy as the workload. For example, if the scheduling policy of the workload is <code>fixed-share</code>, ensure that the cluster has GPU Accelerated nodes with the <code>fixed-share</code> policy. Otherwise, the workload will fail to be scheduled due to no suitable resources for scheduling.</div>



<span id="2r7OwqvL"></span>
## Validating results

<span id="5YcVMvjL"></span>
### Viewing GPU card information

You can use the mGPU Client (`mgpu-cli`) to view mGPU\-related information in the terminal.


1. Log in to the node where the pod is located. You can log in to the node through ECS Terminal. For detailed operations, refer to the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) section of the Managing nodes topic.

2. Run the following command to view graphics card information of nodes.

   ```Bash
   mgpu-cli device info -a
   ```
   

   The system returns a response similar to the following one. In this example, the value of `compute_policy` is `1`, which indicates the node\-level computing power allocation policy is `guaranteed-burst-share`.

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
   |          compute_policy           |      1      |
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
   |compute_free_weight_online |The percentage of unassigned computing power of the device (70% in this example) . |
   |compute_load_balance_mode |The load balancing mode among containers when the containers use the device. |
   |compute_policy |Specify a computing power scheduling policy. Valid values:<br><br><br>* 0: `fixed-share`<br><br>* 1: indicates `guaranteed-burst-share`<br><br>* 2: indicates `native-burst-share` |
   |compute_timeslice |The percentage of the computing power time slice. |
   |device_major |`/dev/mgpuX` is the major device number. |
   |instance_major |`/dev/mgpuXinstY` and `/dev/mgpuXctl-$(container_id)` are the major device numbers. |
   |vmem_free_bytes |The remaining GPU memory capacity of the device. Unit: byte. |
   


<span id="aBjT3onv"></span>
### Viewing mGPU monitoring data

You can monitor various mGPU metrics by using cloud\-native observability. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a1bec3ac602e2a2082f6c5797929448.png) </span>
