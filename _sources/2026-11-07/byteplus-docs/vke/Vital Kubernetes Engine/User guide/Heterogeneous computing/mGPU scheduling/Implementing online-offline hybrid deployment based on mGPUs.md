---
title: "Implementing online-offline hybrid deployment based on mGPUs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_mGPU_for_online-offline_hybrid_deployment"
---

The mGPU online/offline hybrid deployment is applied on the same GPU card within VKE clusters. This maximizes GPU resource utilization and effectively reduces computing costs. This topic provides a detailed introduction to the technical principles and implementation steps of the scheduling solution for mGPU online/offline hybrid deployment.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

<span id=".5Yqf6IO95qaC6L-w"></span>
### Feature overview

By default, mGPU employs a fair‑scheduling policy to allocate GPU resources. Its kernel driver assigns equal GPU time slices to different types of tasks. However, different GPU computing tasks exhibit significant variations in their operation characteristics and priorities, leading to correspondingly diverse resource requirements. At this point, online/offline hybrid deployment technology can be leveraged to completely unlock the potential of GPU computing power. For example, real‑time inference tasks are sensitive to GPU resource latency and require quick access to computing power to complete calculations, yet their resource utilization is typically low. On the other hand, model training tasks demand substantial computing resources but are less sensitive to latency and can tolerate a certain degree of computation throttling. By deploying with the hybrid online/offline technology, the overall GPU resource utilization can be effectively improved, maximizing the value of computing power.

The online\-offline hybrid deployment feature of mGPU deploys online tasks and offline tasks on the same GPU. At the kernel and driver level, this feature enables offline tasks to use 100% idle computing power and enables online tasks to preempt offline tasks with absolute priority, which maximizes GPU resource utilization and minimizes GPU costs.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c2ca0071208663d0e28f552c8ac271c5.png) </span>

<span id=".5bqU55So5Zy65pmv"></span>
### Application scenario

For business scenarios where GPU computing demands are complementary, adopting online/offline hybrid deployment can maximize the potential of GPU resources.


|Typical scenario |Scenario description |
|---|---|
|Hybrid deployment of online and offline inference |Search, recommendation, and other real\-time inference tasks require performing logical reasoning based on existing data to generate results, imposing stringent demands on the real\-time capabilities of GPU computing power. In contrast, data preprocessing and other offline inference tasks primarily serve offline data cleaning and processing workflows and have relatively looser requirements regarding the real‑time availability of computing resources. By specifying the two types of jobs as online and offline jobs, and assigning them to a single GPU card, a significant improvement in GPU resource utilization can be achieved. |
|Hybrid deployment of online inference and offline training |Search, recommendation, and other real‑time inference tasks require logical reasoning based on existing data to generate results. Their key characteristic is a high demand for real‑time GPU computing performance, while their actual resource consumption is relatively low. In contrast, model training tasks encompass stages such as data preparation, parameter configuration, model evaluation, and tuning, which demand large‑scale GPU computing resources but are less sensitive to latency. Configuring real‑time inference as high‑priority online tasks and model training as low‑priority offline tasks, then assigning them to a single GPU card, can further enhance GPU resource utilization efficiency. |


<span id=".5oqA5pyv5Y6f55CG"></span>
### Technical principles


1. **100% utilization of idle GPU computing power by offline pods.** 


After an offline pod is scheduled to the GPU of a node, if the GPU computing power is not currently occupied by online pods, the offline pod can fully utilize the entire GPU computing capacity. When multiple offline pods share GPU resources, the allocation of computing power will follow the pre‑defined computing scheduling policy of mGPU.


2. **100% absolute preemption of offline pod computing power by online pods.** 


The mGPU driver layer incorporates a priority\-based absolute preemption mechanism, with the specific implementation logic detailed below:


* Instant resource scheduling: When an online pod submits a computing task that requires GPU resources, the mGPU driver immediately allocates the full GPU computing power to that pod. If multiple online pods sharecomputing resources, the allocation rules also follow the mGPU computing scheduling policy. When no online pod has active tasks running, the driver releases the occupied computing power after 100 ms and reallocates the resources to offline pods.

* Task checkpoint and resume: The mGPU driver supports the suspension and resumption of computing tasks. When an online pod requests computing resources, any offline pod currently occupying GPU resources is immediately suspended and its computing power is released. Once the online pod task is completed, the offline pod is automatically resumed and continues its computation from the point of interruption.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ee989e14ea0e981cda2a43b30f8ec9d7.png) </span>

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* mGPU resource configuration has been completed, including installing the mGPU component and creating GPU nodes. For details, see [How to use mGPU](https://docs.byteplus.com/en/docs/vke/Using-mGPU).

* The mGPU computing power allocation policy has been configured. For the online/offline hybrid deployment scenario, mGPU supports the `fixed‑share` and `guaranteed‑burst‑share` policies. For details, see [Congiuring mGPU computing power allocation policies](https://docs.byteplus.com/en/docs/vke/Configuring-mGPU-computing-power-allocation-policies).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* In the online/offline hybrid deployment scenario, only the `fixed‑share` and `guaranteed‑burst‑share` computing power allocation policies are currently supported. The `native‑burst‑share` policy is not yet available for this use case. To guarantee the maximum performance for online jobs, we recommend using the `guaranteed‑burst‑share` computing power allocation policy.

* Multi\-card sharing mode does not support online\-offline hybrid deployment.

* Preemption between online and offline tasks is exclusively available for computing power but is unavailable for memory.

* Nodes that use the velinux2.0/ubuntu22.04 image do not support online\-offline hybrid deployment.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya6YWN572u6ZuG576k"></span>
### Step 1: Configure a cluster

The mGPU online/offline hybrid deployment feature relies on multiple components within the container cluster. **We recommended deploying it on a newly created cluster and nodes.**  If you want to use existing clusters and nodes, submit a [ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support to upgrade dependency add\-ons. Detailed requirements for each add\-on are as follows:


|**Dependency add\-on** |**Version restrictions** |**View method** |
|---|---|---|
|Kubernetes |* v1.24.17\-vke.38 and later versions of 1.24<br><br>* v1.26.15\-vke.26 and later versions of 1.26<br><br>* v1.28.15\-vke.19 and later versions of 1.28<br><br>* v1.30.4\-vke.3 and later |You can visit the console of the cluster and find the current version of Kubernetes in the cluster basic information page. See [How to find the Kubernetes version of a cluster?](https://docs.byteplus.com/en/docs/vke/How-do-I-view-the-Kubernetes-version-of-a-cluster) for details. |
|mGPU driver |0.07.35.23 and later |Log in to the Elastic Compute Service (ECS) instance associated with mGPU, and run the `mgpu-cli version` command to view the mGPU driver version. |
|mGPU add\-on |v0.6.0 and later |Go to the Addons page in the VKE console. For a detailed procedure, see [Viewing add-ons](https://docs.byteplus.com/en/docs/vke/Add-on-overview). |
|general\-webhook |v1.20.0 and later |The managed add\-on, which is invisible in the console. New clusters already use the add\-on of the latest version. For existing clusters, you need to contact official technical support to check or upgrade the add\-on version. |


<span id=".5q2l6aqk5LqM77ya6YWN572u5Lia5Yqh"></span>
### Step 2: Configure businesses

You can deploy both online and offline pods within the cluster and schedule them to the same GPU card to compete for computing resources, thereby fulfilling the requirement for online/offline hybrid deployment.


<Tabs>
<Tab zoneid="XOm8PwiZRY" title="Offline pod">
<TabTitle>Offline pod</TabTitle>

Supports identifying offline pods via the annotation `katalyst.kubewharf.io/qos_level: reclaimed_cores` and requesting offline computing power using `vke.volcengine.com/reclaimed-mgpu-core`. An example YAML for an offline pod is as follows:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: offline-pod # Pod name
  namespace: default # Namespace to which the pod belongs
  annotations:
    katalyst.kubewharf.io/qos_level: reclaimed_cores # Online/offline job identifier. Value: shared_cores (online job), reclaimed_cores (offline job). If this annotation identifier is not specified, the job is regarded as online.
    vke.volcengine.com/mgpu-compute-policy: guaranteed-burst-share # mGPU computing power allocation policy. In the online/offline hybrid deployment scenario, only guaranteed-burst-share and fixed-share are currently supported.
spec:
  containers:
    - name: offline-container # The container name.
      image: nginx:1.14.2 # Container image address
      resources:
        limits:
          vke.volcengine.com/mgpu-memory: 4096 # GPU memory, measured in MiB. In this example, the GPU memory is 4 GiB.
          vke.volcengine.com/reclaimed-mgpu-core: 30 # Percentage of GPU computing power allocated for offline jobs. In this example, 30% of GPU computing power is configured.
```



</Tab>
<Tab zoneid="NFnWbYoVGL" title="Online pod">
<TabTitle>Online pod</TabTitle>

Supports identifying online pods either via the annotation `katalyst.kubewharf.io/qos_level: shared_cores` or by omitting this annotation, and requests online computing power using `vke.volcengine.com/mgpu-core`. An example YAML for an online pod is as follows:

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: online-pod # Pod name
  namespace: default # Namespace to which the pod belongs
  annotations:
    katalyst.kubewharf.io/qos_level: shared_cores # Online/offline job identifier. Value: shared_cores (online job), reclaimed_cores (offline job). If this annotation identifier is not specified, the job is regarded as online.
    vke.volcengine.com/mgpu-compute-policy: guaranteed-burst-share # mGPU computing power allocation policy. In the online/offline hybrid deployment scenario, only guaranteed-burst-share and fixed-share are currently supported.
spec:
  containers:
    - name: online-container # The container name.
      image: nginx:1.14.2 # Container image address
      resources:
        limits:
          vke.volcengine.com/mgpu-memory: 4096 # GPU memory, measured in MiB. In this example, the GPU memory is 4 GiB.
          vke.volcengine.com/mgpu-core: 30 # Percentage of GPU computing power allocated for online jobs. In this example, 30% of GPU computing power is configured.
```



</Tab>
</Tabs>


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

After configuration is complete, you can observe the resource contention between online and offline jobs based on the scheduling status of the business pods:


* The scenario where only online tasks are running on a single GPU is not considered an online\-offline hybrid deployment scenario. In this case, the original computing power allocation strategy takes effect.

* The scenario where only offline tasks are running on a single GPU is not considered an online\-offline hybrid deployment scenario. In this case, the original computing power allocation strategy takes effect.

* The scenario where both online and offline tasks are running on a single GPU is considered an online\-offline hybrid deployment scenario. In this case, when an online task is running, offline computing power will be completely suppressed, even if the online task does not fully utilize GPU computing power. When the actual GPU usage of the online task is zero, offline tasks can utilize 100% idle computing power.


Therefore, you can check whether online\-offline hybrid deployment takes effect by observing the GPU computing power utilization of online tasks and offline tasks on the GPU. For example, when an online task continuously uses GPU computing power to process requests on the same GPU, the GPU computing power utilization of the offline task will be continuously suppressed to 0%.
