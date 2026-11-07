---
title: "Ray on VKE product introduction"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Ray_on_VKE_product_introduction"
---

The EMR on VKE product provides a deployment method for Ray under Volcano Container Engine (VKE). Deploy Ray on VKE using the KubeRay Operator. This Operator offers a Kubernetes\-native approach to managing Ray clusters. KubeRay supports heterogeneous compute nodes (including GPUs), as well as running multiple Ray clusters within the same VKE cluster. Refer to the official website [Ray on Kubernetes](https://docs.ray.io/en/master/cluster/kubernetes/index.html).

<span id="部署架构"></span>
## Deployment architecture

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f4a3805642a4b1281f006f3d35c71e7.png) </span>


* KubeRay: An open\-source Kubernetes Operator designed to simplify the deployment and management of Ray applications on Kubernetes.

* CRD: KubeRay introduces three Kubernetes Custom Resource Definitions (CRDs): RayCluster, RayJob, and RayService, which help users efficiently manage Ray clusters for different use cases.

   * **RayCluster**: KubeRay fully manages the lifecycle of RayCluster, including cluster creation/deletion, autoscaling, and ensuring fault tolerance.

   * **RayJob**: With RayJob, KubeRay automatically creates a RayCluster and Submit Job when the cluster is ready. RayJob can also be configured to automatically delete the RayCluster after the Job is completed.

   * **RayService**: Used to manage RayCluster and Ray Serve applications. RayService provides zero\-downtime upgrades and high availability for RayCluster.


Meanwhile, the EMR management console offers cluster management, Job Management, and other capabilities to ensure better user experience and operations. Job Management and Ray HistoryServer functionality are currently under development.

<span id="kuberay介绍"></span>
### KubeRay introduction

With KubeRay, users can leverage the powerful features of Kubernetes to scale and manage Ray applications, making it easier and more efficient to run Ray applications in cloud environments or large\-scale clusters. Main features:


* Simplified deployment: KubeRay provides a suite of tools and YAML configuration templates, making it very easy to deploy Ray on Kubernetes clusters.

* Elastic scaling: KubeRay allows Ray clusters to dynamically scale compute resources based on workload, optimizing resource utilization and cost.

* Tenant isolation: KubeRay supports running multiple Ray clusters within the same Kubernetes cluster, enabling different users or teams to run their applications in isolated environments, thereby improving resource utilization and security.

* Reduced operation and maintenance costs: KubeRay supports integration with Kubernetes monitoring and logging systems, making it convenient for users to monitor and manage Ray applications.

* Seamless integration with the cloud\-native ecosystem: KubeRay is designed to be compatible with the cloud\-native ecosystem, including various cloud service providers and on\-premises Kubernetes installations.


In summary: By combining Ray's powerful distributed computing capabilities with Kubernetes's flexible management features, KubeRay provides developers with an efficient and scalable platform for deploying and managing a wide range of complex distributed applications.

<span id="使用指导"></span>
## User guide

Refer to the [cluster creation](https://docs.byteplus.com/docs/E-MapReduce/109064) section to create a Ray service. At this point, the KubeRay Operator will be present in the cluster. Next, you can create RayCluster and RayJob.

<span id="494d41b7"></span>
### Creating KubeRay

When creating a Ray service, you can configure the KubeRayOperator resource. By default, it is allocated 1 GB of memory and 1 CPU, which in theory can support nearly five thousand PODs. The memory specification of the KubeRay Operator is proportional to the number of PODs it supports. When the total number of PODs in the Ray cluster increases, you also need to increase the memory allocated to KubeRay. You can also refer to the [KubeRay memory and scalability benchmark](https://docs.ray.io/en/latest/cluster/kubernetes/benchmarks/memory-scalability-benchmark.html#kuberay-mem-scalability) for information on their relationship.

<span id="raycluster的使用"></span>
### Using RayCluster

To use RayCluster, you need to create a RayCluster instance. Refer to [Using RayCluster](https://docs.byteplus.com/docs/E-MapReduce/109433#raycluster%E7%9A%84%E4%BD%BF%E7%94%A8).

<span id="rayjob使用"></span>
### Using RayJob

This is done using a YAML file. Refer to the RayJob usage section. The RayCluster section contains examples, and you can also package them using the RayJob YAML template format before executing.
