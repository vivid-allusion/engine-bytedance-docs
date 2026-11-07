---
title: "Configuring NVIDIA GPU scheduling"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NVIDIA-GPU-scheduling"
---

NVIDIA GPU scheduling is the basic scheduling mode in VKE that allows a container to occupy one or more entire GPUs with full access to all computing power and video memory of these GPUs. This topic describes how to configure NVIDIA GPU scheduling for a cluster.

<span id="AyxUhsaW"></span>
## Prerequisites

The nvidia\-device\-plugin add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<span id="jdMkguAQ"></span>
## Procedure

<span id=".5q2l6aqk5LqM77ya5Yib5bu6LWdwdS3orqHnrpflnovoioLngrnmsaA="></span>
### Step 1: Create a GPU node pool


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the cluster list, click the name of the target cluster to open the cluster management page.

3. In the left navigation bar, click **Node pool**.

4. On the Node pool page, click **Create node pool** to create a node pool that meets your requirements. For parameter details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * For **Instance type**, select **GPU Accelerated** to add nodes with GPUs to the cluster.

   * (Optional) In the **Advanced settings** section, click **Add new** to add a GPU scheduling label to the node pool. In this example, set the key to `vke.node.gpu.schedule` and the value to `nvidia`. This setting enables NVIDIA GPU scheduling for nodes in this node pool.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more information about the tag for GPU scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/GPU-scheduling-labels">GPU scheduling overview</a>.      </div>
      

5. After configuring other parameters, click **Confirm** to create the node pool.


<span id="Xf3tlRjb"></span>
### Step 2: Configure a workload

This topic uses the creation of a stateless workload (Deployment) as an example. For detailed steps, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

<span id="W090DIxr"></span>
#### Creating through the console


1. In the left navigation bar of the cluster management page, click **Workload** \> **Deployment**.

2. Create a Deployment or update an existing Deployment. In the **ResourceQuota** section of the **Container configuration** step, configure GPU resources ** as needed.** 

   
   |**Parameter** |**Description** |
   |---|---|
   |GPU resource type |In this example, select **Nvidia**. |
   |GPU computing power |Configure the number of whole GPUs requested by the Pod. The value must be a positive integer. For example, if the value is 1, it means requesting one whole GPU. |
   |Graphics card type |Configure the GPU nodes to which the pod is to be scheduled. By default, the GPU model is not limited. After you specify the GPU model, GPU nodes will be specified based on the selected model. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The parameters displayed in the console vary based on whether the mgpu add\-on is installed in the cluster where the workload resides.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the mgpu add\-on is not installed, the <strong>GPU computing power</strong> and <strong>Graphics card type</strong> parameters are displayed. Specify the parameters based on your business requirements.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the mgpu add\-on is installed, the <strong>GPU computing power</strong> and <strong>GPU memory</strong> parameters are displayed. In the NVIDIA GPU scheduling scenario, you need to set the <strong>GPU computing power</strong> parameter to an integer greater than or equal to 1. In this case, <strong>GPU memory</strong> will change to <strong>Graphics card type</strong>, and the system will display <strong>Enable NVIDIA scheduling</strong>.   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the NVIDIA GPU scheduling scenario, you need to select <strong>Enable NVIDIA Scheduling</strong>. If you do not select this option, NVIDIA GPU scheduling will not be used, and mGPU scheduling will be used instead. Both mGPU scheduling and the mGPU add\-on are public beta features.   </div>
   


<span id="h5Itxz2q"></span>
#### Creating through kubectl

Use YAML to create a workload that applies NVIDIA GPU scheduling:

```YAML
apiVersion: apps/v1
kind: Deployment
metadata:
  name: gpu-demo
  namespace: default
spec: 
  replicas: 1
  selector: 
    matchLabels: 
      app: demo
  template: 
    metadata: 
      labels: 
        app: demo
    spec:
      affinity: # (Optional) Use affinity configuration to specify a GPU type.
        nodeAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
            nodeSelectorTerms:
            - matchExpressions:
              - key: machine.cluster.vke.volcengine.com/gpu-name
                operator: In
                values:
                - Tesla-V100 # Specify the specific GPU type.
      containers:
      - name: demo
        image: doc-cn-beijing.cr.volces.com/vke/gpu-burn:1.0
        command: ["/bin/sh"]
        args: ["-c", "sleep infinity"]
        ports:
        - containerPort: 80
        resources:
          limits:
            nvidia.com/gpu: "1" # Number of GPU graphics cards
```


<span id="APvP0U2N"></span>
## Validating results

<span id="608XPeVo"></span>
### Checking GPU status

Run the following command to log in to the container and view the total allocated video memory.

```Bash
kubectl exec -it gpu-demo nvidia-smi
```


The expected result is as follows. You can see information such as the GPU type and driver used by the Pod.

```Bash
Tue Mar  3 08:18:08 2026       
+---------------------------------------------------------------------------------------+
| NVIDIA-SMI 535.129.03             Driver Version: 535.129.03   CUDA Version: 12.2     |
|-----------------------------------------+----------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |         Memory-Usage | GPU-Util  Compute M. |
|                                         |                      |               MIG M. |
|=========================================+======================+======================|
|   0  NVIDIA A10                     On  | 00000000:65:01.0 Off |                    0 |
|  0%   31C    P8              20W / 150W |      4MiB / 23028MiB |      0%      Default |
|                                         |                      |                  N/A |
+-----------------------------------------+----------------------+----------------------+
                                                                                         
+---------------------------------------------------------------------------------------+
| Processes:                                                                            |
|  GPU   GI   CI        PID   Type   Process name                            GPU Memory |
|        ID   ID                                                             Usage      |
|=======================================================================================|
|  No running processes found                                                           |
+---------------------------------------------------------------------------------------+
```


<span id="ct0hEfTE"></span>
### Viewing GPU monitoring data

After NVIDIA GPU scheduling is enabled, you can view the GPU resource dashboard in the AI resource observability module of cloud\-native observability. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc30ceb776354440babbf31c0e675e30.png) </span>

&nbsp;

&nbsp;

&nbsp;
