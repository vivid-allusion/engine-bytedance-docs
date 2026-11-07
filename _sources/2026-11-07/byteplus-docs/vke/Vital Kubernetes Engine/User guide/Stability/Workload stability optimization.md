---
title: "Workload stability optimization"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Workload-stability-optimization"
---

This topic primarily introduces relevant configurations and operational recommendations for workload stability optimization in VKE stability assurance.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

Growing containerized workloads can bring greater pressure and more complex challenges to your business system. Stability optimization helps ensure that the system can adapt to increasing demands and support business expansion. VKE, with workloads and Kubernetes clusters as its core, can help you improve business stability without requiring intrusive modifications.

This topic covers workload stability optimization. For more information on stability optimization, see the following topics:


* [Basic stability capabilities](https://docs.byteplus.com/en/docs/vke/Basic-stability-capability-configuration)

* [Kubernetes cluster stability optimization](https://docs.byteplus.com/en/docs/vke/Kubernetes-cluster-stability-optimization)


<span id=".5L2_55So5o6n5Yi25Zmo"></span>
## Using controllers

In Kubernetes, use workload controllers (such as Deployment, StatefulSet, DaemonSet, Job, and CronJob) to deploy applications instead of directly using pods, for the following reasons:


* Workload controllers, such as Deployment and StatefulSet, support automated rolling updates. During an update, old\-version pods are gradually replaced, and new\-version pods are started incrementally, thereby avoiding service downtime.

* Kubernetes workload controllers have self\-healing capabilities. When a pod failure is detected or the expected number of replicas (pods) is not met, the controller automatically creates new pods to replace the failed ones. This self\-healing mechanism ensures that the application always runs as expected.


<span id=".6YG_5YWN5Y2V54K55pWF6Zqc"></span>
## Preventing single points of failure

Preventing single points of failure for pods in Kubernetes is critical to ensuring high availability. You can implement the following measures to prevent single points of failure:


* Configure workload replicas and restart policies to ensure that there are always pods available.

   Set the number of replicas of core workloads to at least 2 with the restart policy `Always`.

* Associate workloads with a Service to enable automatic pod discovery and load balancing.

* Distribute pods associated with a workload across multiple availability zones using [topology spread constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/).

   * Topology key: `topology.kubernetes.io/zone`.

   * Topology value: You can view the value corresponding to the topology key in the node label in the console.

   * To use multiple availability zones, you need to add subnets from different availability zones to the cluster. For details, see [Changing API Server subnets](https://docs.byteplus.com/en/docs/vke/Modifying-API-server-subnets).

* Distribute multiple pods associated with a workload across multiple nodes using [node anti-affinity scheduling](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#inter-pod-affinity-and-anti-affinity).

* Deploy multiple pods associated with the same workload to a specific node pool with the desired instance specifications using [node affinity scheduling](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#node-affinity).

   * Different application scenarios have varying requirements for node CPU, memory, disk, and bandwidth resources. You can refer to [Best practices for ECS specification selection](https://docs.byteplus.com/en/docs/vke/ECS-selection-best-practices) to configure node specifications in the node pool that match your actual application scenario.

   * Nodes within the same node pool are assigned a specific label with the label key `cluster.vke.volcengine.com/machinepool-name` and the label value being the node pool ID. This label can be used in node affinity scheduling to schedule pods to a particular node pool.

* Pod dispersion across availability zones delivers higher latency than dispersion within the same availability zone. Therefore, distributing pods across multiple availability zones may lead to decreased network performance if frequent communication between pods is required.

   If pods need to connect to a storage service, you also need to confirm whether the storage service is available in all availability zones where the distributed pods are located.


<span id=".6YWN572uLWhwYQ=="></span>
## Configuring HPAs

The Horizontal Pod Autoscaler (HPA) object in Kubernetes scales the number of pod replicas. A properly configured HPA monitors workload metrics, such as CPU and memory, and dynamically adjusts the number of workload replicas based on actual load requirements. This ensures that the application remains stable under varying traffic and usage conditions.


* A managed VKE cluster has Metric Server (metrics\-server in VKE) installed by default. An HPA can directly use CPU and memory metrics to scale the number of workload replicas. For details, see [Creating HPAs](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler).

* After you [enable observability](https://docs.byteplus.com/en/docs/vke/Enabling-cloud-native-observability) in the cluster and install the collector, an HPA monitors workload metrics such as GPU and network and dynamically adjusts the number of replicas accordingly. For details, see [Achieving autoscaling by using GPU and network metrics](https://docs.byteplus.com/en/docs/vke/Using-GPU-metrics-for-autoscaling).

* Considering the risks associated with scale\-in, an HPA supports scaling in pods in a multi\-batch canary\-style approach and restores the number of replicas promptly if related metrics rise. For details, see [Configurable scaling behavior](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#configurable-scaling-behavior).

* Note that an HPA cannot scale out workloads from zero replicas. Therefore, ensure that at least one replica exists for any workload associated with an HPA.


<span id=".5L2_55SoLXZjaS3pg6jnvbLotJ_ovb0="></span>
## Deploying workloads by using VCI

Clusters support scheduling pods using ECS, VCI, or a mix of ECS and VCI. By scheduling pods to virtual nodes and running them on VCI, you can achieve flexible, on\-demand pod scheduling while eliminating the need for capacity planning and node O&M. For details, see [Using VCI with VKE](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine).

<span id=".5Li65qC45b-D6LSf6L296YWN572u5LyY5YWI57qn"></span>
## Configuring priorities for core workloads

VKE supports ResourcePolicy scheduling and pod priority\-based scheduling:


* [ResourcePolicy scheduling](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling) allows you to use custom resource policies (ResourcePolicy) to deploy pods on both ECS and VCI, leveraging rapid VCI elasticity to handle sudden peaks and ensure application stability.

* Pod priority\-based scheduling, also known as pod preemption scheduling, enables higher\-priority pods to preempt resources from lower\-priority pods when cluster resources are insufficient. Pod priority is defined by [PriorityClass](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-priority-preemption/#priorityclass) and specified in workloads after configuration.


Both types of priority scheduling can coexist to jointly enhance business stability.

<span id=".6YWN572u5o6i6ZKI"></span>
## Configuring probes

In Kubernetes, pod probes are a mechanism used to check if containers are running healthily. Probes play a crucial role in maintaining the stability and reliability of clusters. Kubernetes supports three types of probes, each with its specific role and purpose:


* Readiness probe: Determines if a container has started and is ready to accept traffic. A pod is marked as ready and accessible by the Service only when the readiness probe passes.

* Liveness probe: Checks if a container is still alive and running properly. If the liveness probe fails, Kubernetes restarts the container.

* Startup probe: Verifies if the application inside the container is ready to accept traffic. Compared to the readiness probe, it is mainly used to protect processes that require a certain amount of time for initialization. The startup probe is executed after the container starts, and the container is considered ready only when the startup probe succeeds.


For probe configuration and examples, see Kubernetes documentation [Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/).

<span id=".6YWN572u6LWE5rqQ6YWN6aKd"></span>
## Configuring resource quotas

For resources used by a pod, you can configure `request` and `limit`:


* `request` indicates the minimum amount of resources that a node must reserve for the pod.

* `limit` indicates the maximum amount of resources that the pod can use.


If a container uses more memory than the `limit`, the container will be restarted due to an Out of Memory (OOM) error. If the container uses more CPU than the `limit`, the container will have CPU usage throttled.

Additionally, it is recommended to configure limits for ephemeral storage (temporary storage). In Kubernetes, each node has a certain amount of local disk space for storing temporary container data. Ephemeral storage limits restrict the usage of these local disk resources by containers, preventing containers from overusing local disk resources and causing resource contention or insufficient node disk space.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If ephemeral storage usage by pods exceeds the specified limit, it will result in the OOM error.</div>


<span id=".6YWN572u5pyN5Yqh6LSo6YeP562J57qn"></span>
## Configuring QoS levels

Kubernetes divides quality of service (QoS) priorities into three levels based on whether the pod has memory/CPU `request` and `limit` configured:


* **Guaranteed**: All containers in the pod have `request` and `limit` configured. For each container, the two values are equal.

* **Burstable**: At least one container in the pod has `request` configured, but the pod does not meet the requirements for the Guaranteed level (that is, memory/CPU request and limit values are different).

* **BestEffort**: No containers in the pod have `request` or `limit` configured.


When a Kubernetes cluster needs to evict pods, it does so based on QoS priority. Therefore, it is recommended to configure core workloads to use the highest QoS priority. To avoid missing QoS configurations for core workloads due to human error, Kubernetes provides LimitRange as an admission check. If the admission check fails, the pod will fail to be created. For LimitRange configuration details, see [Setting resource limits](https://docs.byteplus.com/en/docs/vke/Setting-LimitRanges).

<span id=".5a655Zmo6ZWc5YOP5Yqg6YCf"></span>
## Configuring container image acceleration

After creating or updating a workload, the speed of container image pulling is critical to the canary release, observability, and rollback of application changes. To address this problem, BytePlus provides [P2P image acceleration](https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution) and [lazy loading](https://docs.byteplus.com/en/docs/vke/Container-image-lazy-loading-solution) capabilities to support smooth application iteration.

<span id=".57K-566A5Z-656GA6ZWc5YOP"></span>
## Using minimal base images

Base images with multi\-architecture support are recommended for building application images. These base images contain only the minimal components required to run the application, reducing the attack surface and resource usage, while enabling smooth migration across multiple architectures.

Common base images include:


* Alpine Linux: A lightweight Linux distribution optimized for security and resource efficiency. Its default package manager (apk) and tiny base image make it an ideal choice for containerized applications. Alpine Linux supports multiple architectures, including `amd64`, `arm64`, `armv6`, and `armv7`.

* Distroless: Developed by Google, it is a minimal base image without a package manager. It eliminates package managers (and their associated security risks) from traditional Linux distributions. Distroless images support multiple architectures and include static binaries that can run without external dependencies.
