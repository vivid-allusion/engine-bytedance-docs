---
title: "Using mGPU to implement multi-card sharing"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Multiple-GPU-sharing"
---

Vital Kubernetes Engine (VKE) provides the mGPU multi\-card sharing feature. Based on two\-tier scheduling, each container can use the computing power and memory resources of multiple GPUs on the same node. The computing power and memory that a container can use are no longer limited to one GPU. This feature improves the utilization of GPU fragments. This topic describes how to use the mGPU multi\-card sharing feature in detail.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster has been created, and mGPU\-related basic resource configurations have been completed, including installing the mGPU add\-on and creating GPU nodes. For a detailed introduction, see [mGPU usage methods](https://docs.byteplus.com/en/docs/vke/Using-mGPU).

* One of the following mGPU computing power allocation policies has been specified as needed: `native-burst-share`, `fixed-share`, and `guaranteed-burst-share`. For details, see [Allocating mGPU computing power](https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

Multiple required add\-ons have version restrictions. We recommend that you use the latest add\-ons when you create a cluster and nodes. If you want to use an existing cluster and nodes, submit[ a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain  support and upgrade the add\-on versions. The detailed restrictions are as follows:


|**Dependency add\-on** |**Version restrictions** |**View method** |
|---|---|---|
|Kubernetes version |* Other later [Kubernetes versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes) released by VKE<br><br>* [Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32): v1.32.3\-vke.5 and later<br><br>* [Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30): v1.30.4\-vke.10 and later<br><br>* [Kubernetes v1.28](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28): v1.28.15\-vke.25 and later<br><br>* [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.15\-vke.32 and later |* You can visit the console of the cluster and find the current version of Kubernetes in the cluster basic information page. See [How to find the Kubernetes version of a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster) for details.<br><br>* If the cluster version is outdated, upgrade the version first. For details, see [Upgrading clusters](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster). |
|mGPU driver |07.34.4 and later |Log in to the ECS instance where mGPU is located and run the `mgpu-cli version` command to view the mGPU driver version. |
|mGPU add\-on |v0.2.0 and later |View add\-on information on the Add\-ons page in the VKE console. For details, see [Viewing add-ons](https://docs.byteplus.com/en/docs/vke/Add-on-overview) |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This topic provides an example of how to enable the multi\-card sharing feature when you create a Deployment. For a detailed procedure for creating a Deployment, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<span id=".5pa55byP5LiA77ya6YCa6L-H5o6n5Yi25Y-w6YWN572u"></span>
### Creating through the console


1. In the Container configuration step for the Deployment, enable **Multi\-card sharing configuration** for mGPU in the ResourceQuota section, and specify the GPU computing power, GPU memory, and Number of GPU cards parameters based on your business requirements.

   
   |**Parameter** |**Description** |
   |---|---|
   |GPU resource type |The multi\-card sharing feature only takes effect on mGPU resources. In this scenario, **mGPU ** is selected. |
   |Multi\-card sharing configuration |This feature is disabled by default. In this scenario, you need to **enable** this feature. After this option is enabled, the mGPU multi\-card scheduling capability will be provided for the workload, which means a single container can use computing power and GPU memory provided by multiple GPUs. |
   |GPU computing power |Specify the GPU computing power of the container, which is provided by multiple GPUs in equal shares.<br><br><br>* You can enter a value only in the following formats: two\-decimal\-place values from 0.01 to 1, single\-decimal\-place values greater than 1, or positive integers. Example: 0.01, 1.2, or 2.<br><br>* Single GPU computing power = GPU computing power/Number of GPUs. The accuracy of the calculation result must not exceed 0.01. |
   |GPU memory |Specify the GPU video memory of the container, which is provided by multiple GPUs in equal shares.<br><br>Configuration requirement: Single GPU memory = GPU memory/Number of GPUs. After you convert the result unit to MiB, the value must be an integer from 1024 to 81920. |
   |Number of GPU cards |The number of GPUs that are used to jointly provide computing power and GPU memory when the multi\-card sharing feature is enabled. The value can only be set to an integer from 1 to 8. |
   |Graphics card type |Configure the GPU model of nodes that the Pod can be scheduled to. By default, no GPU model restriction applies. If you specify a model, the Pod will be scheduled to nodes using that GPU model. |
   

2. After you complete the container configuration, click **Next: Advanced configuration** to proceed to the Advanced configurations step. The system adds two annotations by default. Do not manually delete or modify them. Otherwise, multi\-card scheduling cannot be achieved.

   * `vke.volcengine.com/multiple-mgpu-<container-name>: "number"`: indicates the number of GPUs. `<container-name>` indicates the container name, which must be consistent with the configuration of `spec.containers.name`. `"number"` indicates the number of cards, such as `vke.volcengine.com/multiple-mgpu-pod-demo: "2"`.

   * `vke.volcengine.com/mgpu-compute-policy: <policy>`: indicates the GPU computing power allocation strategy. `<policy>` indicates the allocation policy, such as `vke.volcengine.com/mgpu-compute-policy: native-burst-share`.

3. After you complete all configurations, click **Confirm** to create the Deployment.


<span id=".5pa55byP5LqM77ya6YCa6L-HLXlhbWwt6YWN572u"></span>
### Creating through kubectl

VKE allows you to achieve the mGPU multi\-card sharing feature for pods by using instance annotations. When you create a workload, you need to add the following two annotations in addition to the required configurations:


* `vke.volcengine.com/multiple-mgpu-<container-name>: "number"`: indicates the number of GPUs. `<container-name>` indicates the container name, which must be consistent with the configuration of `spec.containers.name`. `"number"` indicates the number of cards, such as `vke.volcengine.com/multiple-mgpu-pod-demo: "2"`.

* `vke.volcengine.com/mgpu-compute-policy: <policy>`: indicates the GPU computing power allocation strategy. `<policy>` indicates the allocation policy, such as `vke.volcengine.com/mgpu-compute-policy: native-burst-share`.


The following content describes the sample code and annotation descriptions when you create a Deployment.

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mgpu-deployment
  namespace: default
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mgpu-deployment
  template:
    metadata:
      annotations:
        vke.volcengine.com/multiple-mgpu-pod-demo: "2" # The number of GPUs.
        vke.volcengine.com/mgpu-compute-policy: native-burst-share # The GPU computing power allocation policy.
      labels:
        app: mgpu-deployment
    spec:
      containers:
      - name: pod-demo
        image: nginx:1.14.2
        resources:
         requests:   # Keep the values of the requests field the same as those of the limits field.
           vke.volcengine.com/mgpu-memory: 2048
           vke.volcengine.com/mgpu-core: 120
         limits:
           vke.volcengine.com/mgpu-memory: 2048   # The GPU video memory. Unit: MiB. The value 2048 indicates that 2 GiB of GPU video memory is applied.
           vke.volcengine.com/mgpu-core: 120      # The GPU computing power percentage. The value 120 indicates that 120% of GPU computing power is applied.
        ports:
        - containerPort: 80
```


<span id="GnjSTbpA"></span>
## Validating results

After the mGPU multi\-card sharing feature is configured, you can log in to the GPU node to view the GPU resource allocation for the corresponding container.


1. Log in to the node where the pod is located. You can log in to the node through ECS Terminal. For detailed operations, refer to the [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal) section of the Managing nodes topic.

2. Run the following command to view mGPU information at the container level.

   ```Bash
   mgpu-cli container info
   ```
   

   The system returns the following result, which can be used to check whether the configuration has taken effect. The following information is included:

   * This container occupies two GPUs at the same time (`device_id` is `0` and `1`). This indicates that multi\-card sharing is achieved, which is consistent with the configuration.

   * `compute_weight_native_burst` and `compute_weight_online` are both `60` on the two GPUs, which indicates that 60% of computing power is allocated to each card. This is consistent with the configuration.

   * `vmem_limit` is 1024 MiB on both cards. This is consistent with the configuration.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a49404b69132fb1a28a964566a664d6c.png) </span>

   
   |**Metric name** |**Metric meaning** |
   |---|---|
   |container_id |The container ID. |
   |device_id |The device ID that corresponds to the instance. |
   |instance_id |The instance ID. |
   |pod_uid |The container UID, which is often left empty. |
   |compute_priority |The CUDA priority. |
   |compute_qos_enable |Whether to enable computing power Quality of Service (QoS). |
   |compute_weight |The percentage of offline computing power allocated to the instance. |
   |compute_weight_native_burst |The percentage of computing power allocated to the instance when the computing power allocation strategy is `native-burst-share`. |
   |compute_weight_online |The percentage of online computing power allocated to the instance. |
   |minor |The `/dev/mgpuXinstY` minor device number. |
   |online |Whether it is an online container. |
   |tasks |The PID of the process that is using the device. |
   |vmem_info |Video memory information, including free memory, PID, and used memory. |
   |vmem_limit |The GPU video memory limit requested by the container. |
   


&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;
