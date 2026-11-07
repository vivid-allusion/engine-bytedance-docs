---
title: "PPO training on the GSM8K dataset with veRL"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/PPO_training_on_the_GSM8K_dataset_with_veRL"
---

<span id=".566A5LuL"></span>
## Introduction

This topic provides the algorithm engineering team with a solution for deploying a multi\-node training environment based on Vital Kubernetes Engine (VKE) clusters by using distributed reinforcement learning (RL) frameworks (veRL+Ray) in RL training scenarios. This topic describes how to configure clusters, create PersistentVolumes (PVs), and deploy KubeRay and Ray clusters in detail. This topic provides the complete workflow of performing Proximal Policy Optimization (PPO) training on the GSM8K dataset, including dataset processing, task submission, and monitoring. For more details, see [Quickstart: PPO training on GSM8K dataset](https://verl.readthedocs.io/en/latest/start/quickstart.html#).

The training framework veRL used in this topic, which is short for BytePlus Reinforcement Learning for large language models (LLMs), is an RL framework designed for LLMs on the cloud platform. It not only provides flexible, efficient, and scalable RL training, but also provides a framework named HybridEngine. This framework separates the control flow, which runs in a single process, from the computation flow, which runs in multiple distributed processes, and supports multiple computation backends, parallel policies for training and inference, and performance optimization technologies.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

<span id=".54mp5paZ5YeG5aSH"></span>
### Prepare materials

Prepare the dataset and model files. For more details, see [Quickstart: PPO training on GSM8K dataset](https://verl.readthedocs.io/en/latest/start/quickstart.html#).


* Download the Qwen2.5\-0.5B\-Instruct model to your on\-premises computer.

   ```bash
   # You need to install git-lfs first, such as apt install git-lfs (Ubuntu), brew install git-lfs (MacOS)
   git lfs install
   git clone https://www.modelscope.cn/Qwen/Qwen2.5-0.5B-Instruct.git
   ```
   

* You need to locally download and preprocess the GSM8k dataset file in the configured veRL environment. For details, see [Installation](https://verl.readthedocs.io/en/latest/start/install.html#).

   ```bash
   git clone https://github.com/volcengine/verl
   cd verl
   python3 examples/data_preprocess/gsm8k.py --local_dir ~/data/gsm8k
   ```
   


<span id=".5LiK5Lyg5qih5Z6L5ZKM5pWw5o2u6ZuG5paH5Lu2"></span>
### Upload the model and dataset files


1. Create a Torch Object Storage (TOS) bucket.

   1. Log in to the [TOS console](https://console.byteplus.com/tos/).

   2. In the left navigation bar, click **Buckets**. On the page that appears, click **Create bucket**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_17cfa98fa830351373a846abd81366aa.png) </span>

   3. Specify the parameters of the TOS bucket and click **Confirm** to create the TOS bucket. For more parameter descriptions, see the [official documentation of TOS](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1#.5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5qG2).

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2665a98d74e178d66643a0de955ae682.png) </span>

2. Upload files. Go to the **Objects** page of the TOS bucket. Click **Upload file** and then click **Select folder** to upload the folders that contain the dataset and model files.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f6d5a6c6ef9def6de75f2c38e934a0c6.png) </span>


<span id=".5Yib5bu6LXZrZS3pm4bnvqQ="></span>
### Creating a VKE cluster

When you create a cluster in VKE, take note of the configurations of the following parameters. For more details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).


|Parameter |Description |
|---|---|
|**Cluster configuration** ||
|Kubernetes version |Select v1.28 or later. |
|Network model |Select VPC\-CNI. |
|**Node pool** ** configuration** ||
|Managed node pool |Select Enable to enable the managed node pool. |
|Instance type |Select the GPU instance specification for the node pool based on task requirements. This topic takes ecs.gni3cl.11xlarge (44 vCPU, 240 GiB, NVIDIA L20\*2) as an example.<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e6d0dc671858110f33e04f90ca57167a.png) </span> |
|Number of nodes |2 |
|Data volume |Select ESSD and 1000 GiB.<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_d27b84517c12d08ae35356fcf0c0158f.png) </span> |
|**Addon configuration** ||
|Platform functional addons |Install the following add\-ons in the cluster:<br><br><br>* **nvidia\-device\-plugin**: required for using GPUs<br><br>* **prometheus\-agent**: the monitoring add\-on of VMP, which collects and sends metrics of Kubernetes clusters to VMP<br><br>* **apmplus\-opentelemetry\-collector**: the add\-on that collects and sends OpenTelemetry data and Prometheus metrics to APMPlus.<br><br>* **apmplus\-server\-agent**: the add\-on that collects monitoring data from services and hosts, and sends the data to APMPlus<br><br>* **csi\-tos**: required for mounting TOS |


<span id=".5Yib5bu65a2Y5YKo5Y23LXB2LeWSjOWtmOWCqOWNt-WjsOaYji1wdmM="></span>
### Create a PV and a PVC


1. Create a static TOS PV in the VKE cluster to achieve the TOS\-based network storage capability for the VKE cluster. For details, see [Using static TOS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-TOS-Volumes).

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_1623b04b702b056cbdf089607d2cff9e.png) </span>

   
   |Parameter |Description |
   |---|---|
   |StorageClass type |Select **TOS**. |
   |Access key |Click **Create key**, and configure the key. Set the AccessKey ID and AccessKey Secret parameters to the AccessKey ID and AccessKey secret of your BytePlus root user. |
   |Storage bucket |Select the created TOS bucket. |
   |Subdirectory |Use the default`/`. |
   

2. Create a PersistentVolumeClaim (PVC) and associate it with the PV created in the previous step.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5c3d6898eb7afdbc3ba9af594d15b752.png) </span>


<span id=".6YOo572y5q2l6aqk"></span>
## Procedure

<span id=".6YOo572yLWt1YmVyYXktb3BlcmF0b3I="></span>
### Deploy the kuberay\-operator application


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Application template**.

3. On the **Application template** page, find the kuberay\-operator application template section and click **Deploy**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ad1d35483419111f26307a653ceaf849.png) </span>

4. On the **Deploy application** page, specify the parameters of kuberay\-operator.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_34d16d8ae7e80c35c7236aec4cac8c0b.png) </span>

   
   |Parameter |Description |
   |---|---|
   |**Orchestration template** ||
   |Application template |Select the Chart version of the application. We recommend that you select the latest version. |
   |Parameter configuration |The configuration method varies based on the `values.yaml` file of each application template. For detailed descriptions, see the annotations in the `values.yaml` file. |
   |Name |Specify the name of the application. The name must be unique within the same namespace. |
   |**Deployment environment** ||
   |Cluster type |Select the cluster type where the application needs to be deployed.  |
   |Cluster |Select the project and cluster where the application needs to be deployed. The project named default is selected by default. For details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Namespace |Select a namespace for the target cluster. |
   

5. Click **Confirm** to deploy the application. The deployed application will be displayed on the **Helm** page. You can go to the details page of the application to view the basic information, associated workloads, services, and other resources of the application.


<span id=".6YOo572yLXJheWNsdXN0ZXI="></span>
### Deploy a Ray cluster


1. Modify the content of the following YAML file based on your business requirements.

   * Modify the `containers.image` mirror addresses in `headGroupSpec` and `workerGroupSpecs` according to the business location.

      
      <Tabs>
      <Tab zoneid="IGLFepaV" title="China (Beijing)">
      <TabTitle>China (Beijing)</TabTitle>
      
      ```Plain Text
      vke-cn-beijing.cr.volces.com/vke/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
      ```
      
      
      
      </Tab>
      <Tab zoneid="EWv1LSGi" title="China (Shanghai)">
      <TabTitle>China (Shanghai)</TabTitle>
      
      ```Plain Text
      vke-cn-shanghai.cr.volces.com/vke/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
      ```
      
      
      
      </Tab>
      <Tab zoneid="6w0VD9Dq" title="China (Guangzhou)">
      <TabTitle>China (Guangzhou)</TabTitle>
      
      ```Plain Text
      vke-cn-guangzhou.cr.volces.com/vke/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
      ```
      
      
      
      </Tab>
      <Tab zoneid="Lr1il57X" title="Asia Pacific (Johor)">
      <TabTitle>Asia Pacific (Johor)</TabTitle>
      
      ```Plain Text
      vke-ap-southeast-1.cr.volces.com/vke/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
      ```
      
      
      
      </Tab>
      </Tabs>
      

   * Modify resource configurations for head and worker instances in the YAML file based on the node specifications. Set the `nvidia.com/gpu` parameter to the number of GPUs on the node. We recommend that you allocate `CPUs` and `memory` as much as possible while reserving some resources for other system add\-ons. For example, allocate 80% of the node resources. Set the `requests` and `limits` parameters to the same values.

   * Set the `persistentVolumeClaim.claimName` parameter to the name of the created PVC.

   * The `tracing-startup-hook` parameter of the `rayStartParams` parameter is required for starting in\-depth observability. The startup script is already provided in `/workspace/verl/tracing/setup_tracing.py`. You only need to perform the following steps to start in\-depth observability. The sample code already includes the following configurations and can be directly used.

      * Add `tracing-startup-hook: "tracing.setup_tracing:setup_tracing"` to the startup command.

      * Configure the environment variable `PYTHONPATH=/workspace/verl` to start in\-depth observability. The data will be automatically reported to APMPlus.

      * Add the annotation `instrumentation.apmplus.volcengine.com/inject-python:"true"` to worker and header instances.

      * To reduce system consumption, you need to configure the environment variable `OTEL_PYTHON_DISABLED_INSTRUMENTATIONS=system_metrics`.

   * For more information about parameters, see [RayCluster Configuration](https://docs.ray.io/en/latest/cluster/kubernetes/user-guides/config.html).


```yaml
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  name: raycluster-kuberay
  namespace: default
spec:
  headGroupSpec:
    serviceType: ClusterIP
    rayStartParams:
      dashboard-host: "0.0.0.0"
      tracing-startup-hook: "tracing.setup_tracing:setup_tracing"
    template:
      metadata:
        annotations:
          instrumentation.apmplus.volcengine.com/inject-python: "true"
      spec:
        containers:
        - name: ray-head
          image: ai-containers-cn-beijing.cr.volces.com/deeplearning/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
          imagePullPolicy: IfNotPresent
          resources:
            limits:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
            requests:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
          volumeMounts:
          - name: log-volume
            mountPath: /tmp/ray
          - name: tos-pv
            mountPath: /data
          env: 
          - name: PYTHONPATH
            value: /workspace/verl
          - name: OTEL_PYTHON_DISABLED_INSTRUMENTATIONS
            value: system_metrics
        volumes:
        - name: log-volume
          emptyDir: {}
        - name: tos-pv
          persistentVolumeClaim:
            claimName: verl-pvc

  workerGroupSpecs:
  - groupName: workergroup
    replicas: 1
    minReplicas: 1
    maxReplicas: 3
    rayStartParams: {}
    template:
      metadata:
        annotations:
          instrumentation.apmplus.volcengine.com/inject-python: "true"
      spec:
        containers:
        - name: ray-worker
          image: ai-containers-cn-beijing.cr.volces.com/deeplearning/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
          imagePullPolicy: IfNotPresent
          resources:
            limits:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
            requests:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
          volumeMounts:
          - name: log-volume
            mountPath: /tmp/ray
          - name: tos-pv
            mountPath: /data
          env: 
          - name: PYTHONPATH
            value: /workspace/verl
          - name: OTEL_PYTHON_DISABLED_INSTRUMENTATIONS
            value: system_metrics
        volumes:
        - name: log-volume
          emptyDir: {}
        - name: tos-pv
          persistentVolumeClaim:
            claimName: verl-pvc

```



2. Log in to the [VKE console](https://console.byteplus.com/vke). Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar, click **Workload \> Resource Explorer**.

4. Click **Create with Yaml**. On the Create with Yaml page, select **Custom** from the **Type** list. Enter the content of the modified YAML file and then click **Confirm**. By default, the resource explorer is deployed in the namespace named **default**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_027b26b93d2ad2bce4a78b4387801baf.png) </span>


<span id=".5qOA5p-l6L-Q6KGM54q25oCB"></span>
### Check running status

In the left navigation bar, click **Workload \> Pod** to view the status of the head and worker pods, which are respectively named `raycluster-kuberay-head-xxxx` and `raycluster-kuberay-workergroup-worker-xxxx`. When `Running` is displayed in the Status column, it indicates that the pods are started, which takes a long period of time.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9d23c647d775735c48e76d30a535f447.png) </span>

<span id=".5omn6KGM6K6t57uD5Lu75Yqh"></span>
## Run a training task

<span id=".5o-Q5Lqk6K6t57uD5Lu75Yqh"></span>
### Submit a training task


1. In the left navigation bar, click **Workload \> Pod**. Click the name of **raycluster\-kuberay\-head\-xxxx**, and then click **Console** in the upper\-right corner to go to the console of the pod.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6bf44eead9f7a1b44a63bb30734ed747.png) </span>

2. Enter the following command in the console to navigate to the verl directory and submit the training task.


```bash
cd /workspace/verl
ray job submit --address="http://127.0.0.1:8265" \
    --runtime-env=verl/trainer/runtime_env.yaml \
    --no-wait \
    -- \
    python3 -m verl.trainer.main_ppo \
    data.train_files=/data/data/gsm8k/train.parquet \
    data.val_files=/data/data/gsm8k/test.parquet \
    data.train_batch_size=256 \
    data.max_prompt_length=512 \
    data.max_response_length=256 \
    actor_rollout_ref.model.path=/data/Qwen2.5-0.5B-Instruct \
    actor_rollout_ref.actor.optim.lr=1e-6 \
    actor_rollout_ref.actor.ppo_mini_batch_size=64 \
    actor_rollout_ref.actor.ppo_micro_batch_size_per_gpu=4 \
    actor_rollout_ref.rollout.log_prob_micro_batch_size_per_gpu=8 \
    actor_rollout_ref.rollout.tensor_model_parallel_size=1 \
    actor_rollout_ref.rollout.gpu_memory_utilization=0.4 \
    actor_rollout_ref.ref.log_prob_micro_batch_size_per_gpu=4 \
    critic.optim.lr=1e-5 \
    critic.model.path=/data/Qwen2.5-0.5B-Instruct \
    critic.ppo_micro_batch_size_per_gpu=4 \
    algorithm.kl_ctrl.kl_coef=0.001 \
    trainer.logger=['console'] \
    trainer.default_hdfs_dir=null \
    trainer.n_gpus_per_node=2 \
    trainer.nnodes=2 \
    trainer.save_freq=10 \
    trainer.test_freq=10 \
    trainer.total_epochs=20 \
    trainer.default_local_dir='/data/checkpoints'
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93f654b279916655ea00991cb6f8a00e.png) </span>

The following figure shows the expected output after the training task is submitted.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dc7ef7793adc325d87014e562613b835.png) </span>

<span id=".5p-l55yL6K6t57uD5Lu75Yqh54q25oCB"></span>
### View training job status

Create an Ingress to expose the Ray dashboard service.


1. In the left navigation bar, click **Services and Ingresses \> Ingress**, and click **Create Ingress** to configure an Ingress.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cc680ab65b2c5d729c89182618e5a623.png) </span>

   Take note of the configurations of the following parameters. For more details, see [Creating an ALB Ingress in the console](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console?lang=zh).

   
   |Parameter |Description |
   |---|---|
   |Ingress type |Select **Application Load Balancer (ALB)** . |
   |Protocol |Select **HTTP**. |
   |Path |Enter`/`. |
   |Service |Select `raycluster-kuberay-head-xxxxxx and 8265`. |
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8ac17cfd5997fb7fe60e9db8143c1345.png) </span>

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6532b68aad506bfbc3ba482ddb887c84.png) </span>

2. After the ALB Ingress is created, enter the virtual IP address (VIP) of the Ingress in the browser address bar to access the dashboard, on which you can view training task logs and cluster status.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba8efa385919bec5c165530bf8d25458.png) </span>

   By default, the trained checkpoints are saved in the `/tmp/ray/session_xxxxx/runtime_resources/working_dir_files/_ray_pkg_xxxxx/checkpoints/verl_examples/gsm8k` directory of the raycluster\-kuberay\-head\-xxxx pod.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_68eb6112fc6ab757aa2100f87a051abf.png) </span>


<span id=".5byA5ZCv6KeC5rWL6YWN572u"></span>
## Enable observability

<span id=".5Z-656GA6KeC5rWL"></span>
### Basic observability

<span id=".5byA5ZCv6KeC5rWL6YWN572u"></span>
#### Enable observability


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of the management page for the target cluster, click **Cloud native observability** \> **Overview**, and then enable cloud native observability and container monitoring based on the **Access guide**. You need to perform the following steps:

   * Enable cloud native observability.

   * Bind a VMP workspace.

   * Install the prometheus\-agent add\-on.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For more configuration details, see <a href="https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability">Enabling observability</a>.      </div>
      

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_9895eb8464bf1cb10d8f7b8ddd14694b.png) </span>

3. Create collection configurations.

   First, check whether Ray PodMonitors are already created in the cluster. If not, create one.

   Confirmation method: In the left navigation bar of the cluster management page, click **Workload** \> **Resource Explorer**. On the page that appears, search for `podmonitor`. Click the name of the target PodMonitor to check whether Ray\-related collection configurations exist.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_956421844fa8d2e1c722984676b847bc.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You still need to verify that the label <code>volcengine.vmp: "true"</code> is added to the preceding two PodMonitors resources even if you created PodMonitors. If the label does not exist, prometheus\-agent cannot identify the resources and thus cannot collect metrics.   </div>
   

If Ray PodMonitors are not created in the cluster, perform the following steps to create Ray PodMonitors.


1. In the left navigation bar of the cluster management page, click **Workload \> Resource Explorer**.

2. Click **Create with Yaml**. Copy the following code to create the corresponding PodMonitor.

   * PodMonitor configuration for collecting head node metrics

      ```yaml
      apiVersion: monitoring.coreos.com/v1
      kind: PodMonitor
      metadata:
        labels:
          volcengine.vmp: "true"
        name: ray-head-monitor
        namespace: default
      spec:
        jobLabel: ray-head
        # Only select Kubernetes Pods in the "default" namespace.
        namespaceSelector:
          matchNames:
            - default
        # Only select Kubernetes Pods with "matchLabels".
        selector:
          matchLabels:
            ray.io/node-type: head
        # A list of endpoints allowed as part of this PodMonitor.
        podMetricsEndpoints:
          - port: metrics
            relabelings:
              - action: replace
                sourceLabels:
                  - __meta_kubernetes_pod_label_ray_io_cluster
                targetLabel: ray_io_cluster
          - port: as-metrics # autoscaler metrics
            relabelings:
              - action: replace
                sourceLabels:
                  - __meta_kubernetes_pod_label_ray_io_cluster
                targetLabel: ray_io_cluster
          - port: dash-metrics # dashboard metrics
            relabelings:
              - action: replace
                sourceLabels:
                  - __meta_kubernetes_pod_label_ray_io_cluster
                targetLabel: ray_io_cluster
      ```
      

   * PodMonitor configuration for collecting worker node metrics

      ```yaml
      apiVersion: monitoring.coreos.com/v1
      kind: PodMonitor
      metadata:
        name: ray-workers-monitor
        namespace: default
        labels:
          volcengine.vmp: "true"
      spec:
        jobLabel: ray-workers
        # Only select Kubernetes Pods in the "default" namespace.
        namespaceSelector:
          matchNames:
            - default
        # Only select Kubernetes Pods with "matchLabels".
        selector:
          matchLabels:
            ray.io/node-type: worker
        # A list of endpoints allowed as part of this PodMonitor.
        podMetricsEndpoints:
        - port: metrics
          relabelings:
          - sourceLabels: [__meta_kubernetes_pod_label_ray_io_cluster]
            targetLabel: ray_io_cluster
      ```
      

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Take note of and modify the following parameters:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><code>namespace</code>: The namespace where the PodMonitor resides. Theoretically, the PodMonitor can be created in any namespace.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2"><code>namespaceSelector</code>: Select a namespace of which Ray cluster pods are to be matched. Enter the namespace where Ray is located.      </div>
      

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_99f2bf04e160d2defa50262b6c784f7c.png) </span>


<span id=".5p-l55yL55uR5o6n6Z2i5p2_"></span>
#### View the monitoring dashboard

After a collection rule is configured, metrics related to Ray will be collected and stored in VMP workspaces. You can use the Explore feature of VMP to query the corresponding metrics.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dac906ecb8848c5892008d33aae5dfd3.png) </span>

You can use the preset dashboard of VMP to view Ray metrics. To view Ray metrics, you need to apply to add your account to the allowlist.


1. Log in to the [VMP console](https://console.byteplus.com/prometheus).

2. Click **Monitor dashboard** in the left navigation bar. Search for ray to view Ray\-related dashboards.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e90a9df9a7b9a2e6d3284d1af8139a2a.png) </span>


You can also install Grafana to view Ray monitoring charts.


1. Install the Grafana service in the VKE cluster. For details, see [Deploying Grafana in a VKE cluster and integrating Grafana with a workspace](https://docs.byteplus.com/en/docs/vmp/deploy-grafana-in-vke-cluster#.5L2_55So6YOo572y6ISa5pys6YOo572yIEdyYWZhbmE=).

2. Log in to your self\-managed Grafana and import the following dashboard.

   <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7fe046516a7586d6cd6c8073fc4b9bcb.json" name="ray_default_dashboard.json">ray_default_dashboard.json</Attachment>
   

3. Select VMP as the data source for importing.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9d5eddd011c523ac84b6bcdcc54a0d71.png) </span>

   The following figure shows the result after importing.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90df3fa9f7b016a5949b380e2c5e9d45.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe1d79089497e58d30444a4a81152fb9.png) </span>


<span id=".5rex5bqm6KeC5rWL"></span>
### In\-depth observability

<span id=".5byA5ZCv6KeC5rWL6YWN572u"></span>
#### Enable observability configuration


1. Deploy the APMPlus observability add\-on.

   In the left navigation bar of the VKE cluster management page, click Addons. On the page that appears, click the Monitoring tab. Find the apmplus\-opentelemetry\-collector and apmplus\-server\-agent add\-ons and install them. The following figure shows the result after the add\-ons are installed. Verify that both add\-ons are installed and that no error messages appear.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_968f808128768cc1262fc2b996c619da.png) </span>

2. Enable in\-depth observability. Add the following annotation to Ray\-related instances.



|key |value |
|---|---|
|instrumentation.apmplus.volcengine.com/inject\-python |true |


In the deployment YAML file of the Ray cluster, add the following configuration. The preceding sample [deployment YAML file of the Ray cluster](https://docs.byteplus.com/en/docs/vke/PPO_training_on_the_GSM8K_dataset_with_veRL#.6YOo572yLXJheWNsdXN0ZXI=) already includes the following configurations and can be directly used.

```yaml
apiVersion: ray.io/v1
kind: RayCluster
metadata:
  creationTimestamp: "2025-05-23T05:23:37Z"
  generation: 2
  name: raycluster-kuberay
  namespace: default
  resourceVersion: "52584"
  uid: cdb81f16-e53d-481f-9426-5db7f93155b5
spec:
  headGroupSpec:
    rayStartParams:
      dashboard-host: 0.0.0.0
      tracing-startup-hook: ray.util.tracing.setup_local_tmp_tracing:setup_tracing
    serviceType: ClusterIP
    template:
      metadata:
        annotations:
          instrumentation.apmplus.volcengine.com/inject-python: "true"
      spec:
        containers:
        - env: 
          - name: OTEL_PYTHON_DISABLED_INSTRUMENTATIONS
            value: system_metrics
        - image: cr-helm-test-cn-beijing.cr.volces.com/cr-helm-test/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
          imagePullPolicy: IfNotPresent
          name: ray-head
          resources:
            limits:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
            requests:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
          volumeMounts:
          - mountPath: /tmp/ray
            name: log-volume
          - mountPath: /data
            name: tos-pv
        volumes:
        - emptyDir: {}
          name: log-volume
        - name: tos-pv
          persistentVolumeClaim:
            claimName: verl-pvc
  workerGroupSpecs:
  - groupName: workergroup
    maxReplicas: 3
    minReplicas: 1
    numOfHosts: 1
    rayStartParams: {}
    replicas: 1
    template:
      metadata:
        annotations:
          instrumentation.apmplus.volcengine.com/inject-python: "true"
      spec:
        containers:
        - env: 
          - name: OTEL_PYTHON_DISABLED_INSTRUMENTATIONS
            value: system_metrics
        - image: cr-helm-test-cn-beijing.cr.volces.com/cr-helm-test/verl:ngc-th2.6.0-cu126-vllm0.8.4-flashinfer0.2.2-cxx11abi0-custom-v1
          imagePullPolicy: IfNotPresent
          name: ray-worker
          resources:
            limits:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
            requests:
              cpu: "30"
              memory: 100Gi
              nvidia.com/gpu: 2
          volumeMounts:
          - mountPath: /tmp/ray
            name: log-volume
          - mountPath: /data
            name: tos-pv
        volumes:
        - emptyDir: {}
          name: log-volume
        - name: tos-pv
          persistentVolumeClaim:
            claimName: verl-pvc
status:
  availableWorkerReplicas: 1
  conditions:
  - lastTransitionTime: "2025-05-23T07:23:08Z"
    message: ""
    reason: HeadPodRunningAndReady
    status: "True"
    type: HeadPodReady
  - lastTransitionTime: "2025-05-23T05:29:39Z"
    message: All Ray Pods are ready for the first time
    reason: AllPodRunningAndReadyFirstTime
    status: "True"
    type: RayClusterProvisioned
  - lastTransitionTime: "2025-05-23T05:23:37Z"
    message: ""
    reason: RayClusterSuspended
    status: "False"
    type: RayClusterSuspended
  - lastTransitionTime: "2025-05-23T05:23:37Z"
    message: ""
    reason: RayClusterSuspending
    status: "False"
    type: RayClusterSuspending
  desiredCPU: "60"
  desiredGPU: "4"
  desiredMemory: 200Gi
  desiredTPU: "0"
  desiredWorkerReplicas: 1
  endpoints:
    client: "10001"
    dashboard: "8265"
    gcs-server: "6379"
    metrics: "8080"
    serve: "8000"
  head:
    podIP: 192.168.5.38
    podName: raycluster-kuberay-head-wcrb7
    serviceIP: 192.168.5.38
    serviceName: raycluster-kuberay-head-svc
  lastUpdateTime: "2025-05-23T07:23:24Z"
  maxWorkerReplicas: 3
  minWorkerReplicas: 1
  observedGeneration: 2
  readyWorkerReplicas: 1
  state: ready
  stateTransitionTimes:
    ready: "2025-05-23T05:29:39Z"

```



3. Configure Ray tracing.

   To enable the tracing feature, you need to provide a tracing startup script that includes a function for configuring the tracing provider and span processor. This function has no input parameters and must be available in the Python environment of all worker processes.

   The following sample code shows how to send tracing data to the server based on environment variable configurations. After the apmplus\-opentelemetry\-collector and apmplus\-server\-agent add\-ons are installed, the environment variable will be set to apmplus\-opentelemetry\-collector. The code is automatically included in the image.


```python
import ray
import logging
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import (
    BatchSpanProcessor,
)
from opentelemetry.exporter.otlp.proto.http.trace_exporter import (
    OTLPSpanExporter as HTTPExporter,
)

def setup_tracing() -> None:
    logging.warning("setup_tracing")
    trace.set_tracer_provider(TracerProvider())
    trace.get_tracer_provider().add_span_processor(
        BatchSpanProcessor(
            HTTPExporter()
        )
    )
```


Add the following parameters to rayStartParams in the YAML file of the Ray cluster.

```yaml
    spec:
      headGroupSpec:
        serviceType: ClusterIP
        rayStartParams:
          dashboard-host: "0.0.0.0"
          tracing-startup-hook: "tracing.setup_tracing:setup_tracing"
        template:
```


<span id=".5p-l55yL6KeC5rWL5pWw5o2u"></span>
#### View observability data

After you enable the observability configuration, the generated tracing data will be sent to APMPlus. In the left\-side navigation bar in the APMPlus console, click **Server level monitoring** to view the ray\-worker and ray\-header services.

Click the service name to go to the observability dashboard page.


* On the **Service overview** tab, you can view the key metrics of the service, such as QPS and request error rate.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_24c5aa9923f6dc467d3828a48367c8e8.png) </span>

* On the **Trace analysis** tab, you can view the reported tracing data. Click the ID of the target trace to go to the details page of the trace. On the List tab, you can view the details of the trace.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_ad7ed8e3b2ee2f5a2fb3c2a80dd15f43.png) </span>


<span id=".d2FuZGIt6YOo572y5LiO5a-55o6l"></span>
## Deploy and connect to wandb

Weights & Biases (wandb) is a platform for tracking and managing machine learning experiments, which is designed to help data scientists and machine learning engineers develop, optimize, and deploy models more efficiently. It provides a set of streamlined tools that automatically record key metrics during experiments, visualize results, manage code versions and datasets, and support team collaboration.

This section describes how to deploy the local version of wandb in the preceding clusters and how to push veRL training metrics to wandb.

<span id=".5YeG5aSH6ZWc5YOP"></span>
### Prepare an image

Prepare a [wandb local image](https://hub.docker.com/r/wandb/local). Two solutions are provided in China's mainland where Docker Hub may be inaccessible.


1. Pull a non\-official Docker image from Docker Hub by using the domain name of a proxy cache registry.

2. First, pull the image to your on\-premises computer. Then, push the image to your Container Registry (CR) instance. For specific steps, see [Pushing and Pulling Images Using Docker](https://docs.byteplus.com/en/docs/cr/push-and-pull-images?lang=zh).


<span id=".5Yib5bu6LW5hcy3mlofku7blrZjlgqg="></span>
### Create a FileNAS file system


1. Log in to [FileNAS console](https://console.byteplus.com/filenas/).

2. In the top navigation bar, select the region for which you want to create a file system.

3. In the left navigation bar, click **File System \> File System list**. On the **File System list** page, click **Create File System**. For detailed parameter descriptions, see [Creating a file system](https://docs.byteplus.com/en/docs/nas/Creating-a-file-system).

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_df66b2834fdf71e119f132a0ff7df183.png) </span>

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_de4a2566ecfd935b34a5c3ba7c6051cd.png) </span>

4. Click the name of the created file system to go to the details page of the file system. Click the Mount Target tab, and then click **Create Mount Target**. Select the Virtual Private Cloud (VPC) where the VKE cluster is located from the **Private network** list.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f786c46e0be3b480469f37ed532e862a.png) </span>

5. Go to the management page of the VKE cluster. Create a PV for the cluster. When you create the PV, select the created FileNAS file system and mount point.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_5b008a882bbf5c1a15cf363c18e2391f.png) </span>

6. Create a PVC and associate it with the created PV.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2996801218d5a31495ce6fa3ce9f9e0f.png) </span>


<span id=".6YOo572yLXdhbmRiLWxvY2Fs"></span>
### Deploy wandb local


1. Deploy wandb local

   1. Modify the content of the following YAML file to modify the wandb local image address and PVC name based on your business requirements.

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: wandb
     labels:
       app: wandb
   spec:
     strategy:
       type: RollingUpdate
     replicas: 1
     selector:
       matchLabels:
         app: wandb
     template:
       metadata:
         labels:
           app: wandb
       spec:
         initContainers:
           - name: init-permissions
             image: cr-helm-test-cn-beijing.cr.volces.com/cr-helm-test/wandb-local:0.68.2
             command: ["sh", "-c", "chmod 777 /vol"]
             securityContext:
               runAsUser: 0
             volumeMounts:
               - name: wandb-pv
                 mountPath: /vol
         containers:
           - name: wandb
             imagePullPolicy: IfNotPresent
             image: cr-helm-test-cn-beijing.cr.volces.com/cr-helm-test/wandb-local:0.68.2
             ports:
               - name: http
                 containerPort: 8080
                 protocol: TCP
             volumeMounts:
               - name: wandb-pv
                 mountPath: /vol
             livenessProbe:
               httpGet:
                 path: /healthz
                 port: http
             readinessProbe:
               httpGet:
                 path: /ready
                 port: http
             resources:
               requests:
                 cpu: "2000m"
                 memory: 4G
               limits:
                 cpu: "4000m"
                 memory: 8G
         volumes:
           - name: wandb-pv
             persistentVolumeClaim:
               claimName: wandb-pvc
   ---
   apiVersion: v1
   kind: Service
   metadata:
     name: wandb-service
   spec:
     type: ClusterIP
     selector:
       app: wandb
     ports:
       - protocol: TCP
         port: 8080
         targetPort: 8080
   ```
   

   3. Log in to the [VKE console](https://console.byteplus.com/vke/region:vke+cn-beijing/cluster?projectName=default). In the left navigation bar, click Cluster. Then, click the name of the target cluster to go to the cluster management page.

   4. In the left navigation bar, click **Workload \> Resource Explorer**.

   5. Click **Create with Yaml**. On the Create with Yaml page, select **Custom** from the **Type** list. Enter the content of the modified YAML file and then click **Confirm** in the lower\-right corner of the page. By default, the resource explorer is deployed in the **default** namespace.

2. Create an Ingress to expose the wandb service.

   1. In the left navigation bar of the cluster management page, click **Services and Ingresses** \> **Ingress**. On the page that appears, click **Create Ingress**.

   2. Take note of the configurations of the following parameters. For more details, see [Creating an ALB Ingress in the console](https://docs.byteplus.com/en/docs/vke/Creating-an-ALB-Ingress-in-the-console?lang=zh).

   
   |Parameter |Description |
   |---|---|
   |Ingress type |Select **Application Load Balancer (ALB)** . |
   |Protocol |Select **HTTP**. |
   |Path |Enter`/`. |
   |Service |Select **wandb\-service and 8080**. |
   

3. After the Ingress is created, enter the VIP of the Ingress in the browser address bar to go to the wandb management page.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8c729dd3c180e5a18cb8890cd21905f4.png) </span>


<span id=".d2FuZGIt6YWN572u"></span>
### wandb configuration


1. Go to the wandb management page and create an account. You will need to use your email and password for login. Please remember them.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4d3d35981ac5383476091f63bcb7d095.png) </span>

2. Configure the license. If you do not have a license, you can apply for a free license based on prompts.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_16f7e7d1fa4bc2a298d81a4951cfc8e2.png) </span>

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b4f286fe926a344fdcc4cdc0233c4ae0.png) </span>

3. Return to the Home page to view the API key.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_7b637206b7fd0936de1e29c75ca520c4.png) </span>

4. Create a project.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_8a51b2d5154c6b3f24c699b223cd1e96.png) </span>


<span id=".dmVybC3phY3nva4="></span>
### veRL configuration


1. Go to the head pod console based on the instructions in the [Submit a training task](https://docs.byteplus.com/en/docs/vke/PPO_training_on_the_GSM8K_dataset_with_veRL#.5o-Q5Lqk6K6t57uD5Lu75Yqh) section of this topic. Edit the content of the `verl/trainer/runtime_env.yaml` file by using vim or nano before you submit the task. Add the `WANDB_BASE_URL` and `WANDB_API_KEY` parameters. Set the `WANDB_API_KEY` parameter to your API key.


```yaml
working_dir: ./
excludes: ["/.git/"]
env_vars:
  TORCH_NCCL_AVOID_RECORD_STREAMS: "1"
  # If you are using vllm<=0.6.3, you might need to set the following environment variable to avoid bugs:
  # VLLM_ATTENTION_BACKEND: "XFORMERS"
  WANDB_BASE_URL: "http://wandb-service:8080"
  WANDB_API_KEY: "local-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
```



2. Add or modify the following content for the task submission command and then submit the task.

   * Add `'wandb'` to `trainer.logger`.

   * Set `trainer.project_name` to the project name that was created in wandb.

   * Set `trainer.experiment_name` to an experiment name.


```javascript
ray job submit --address="http://127.0.0.1:8265" \
    --runtime-env=verl/trainer/runtime_env.yaml \
    --no-wait \
    -- \
    python3 -m verl.trainer.main_ppo \
    data.train_files=/data/data/gsm8k/train.parquet \
    data.val_files=/data/data/gsm8k/test.parquet \
    data.train_batch_size=256 \
    data.max_prompt_length=512 \
    data.max_response_length=256 \
    actor_rollout_ref.model.path=/data/Qwen2.5-0.5B-Instruct \
    actor_rollout_ref.actor.optim.lr=1e-6 \
    actor_rollout_ref.actor.ppo_mini_batch_size=64 \
    actor_rollout_ref.actor.ppo_micro_batch_size_per_gpu=4 \
    actor_rollout_ref.rollout.log_prob_micro_batch_size_per_gpu=8 \
    actor_rollout_ref.rollout.tensor_model_parallel_size=1 \
    actor_rollout_ref.rollout.gpu_memory_utilization=0.4 \
    actor_rollout_ref.ref.log_prob_micro_batch_size_per_gpu=4 \
    critic.optim.lr=1e-5 \
    critic.model.path=/data/Qwen2.5-0.5B-Instruct \
    critic.ppo_micro_batch_size_per_gpu=4 \
    algorithm.kl_ctrl.kl_coef=0.001 \
    trainer.default_hdfs_dir=null \
    trainer.n_gpus_per_node=2 \
    trainer.nnodes=2 \
    trainer.save_freq=10 \
    trainer.test_freq=10 \
    trainer.total_epochs=15 \
    trainer.logger=['console','wandb'] \
    trainer.project_name='verl_example_gsm8k' \
    trainer.experiment_name='experiment1'
```



3. After you complete the preceding configuration, you can view metric data during training on the wandb monitoring page.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_509c681d1e04cc0f307149602f761cc5.png) </span>


&nbsp;
