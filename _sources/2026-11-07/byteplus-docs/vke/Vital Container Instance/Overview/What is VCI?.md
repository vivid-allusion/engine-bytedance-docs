---
title: "What is VCI?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance"
---

Vital Container Instance (VCI) is a serverless and containerized computing service. VCI can seamlessly integrate with VKE to provide Kubernetes orchestration capabilities.

<span id=".5Lqn5ZOB5qaC6L-w"></span>
## Product overview

Traditional Kubernetes architectures are generally node\-centric and require clusters to be built on resource nodes such as cloud servers with operations and management centered around these nodes. As the business scale expands and the number of nodes increases, this architecture often faces limitations in deploying and running container applications, including complex node operations, low resource utilization, and slow resource scaling.

VCI is a new cloud\-native solution developed to address these challenges. It is a serverless and containerized computing service abstracted from years of internal cloud\-native technology accumulation of ByteDance.


* VCI is seamlessly integrated with VKE via Virtual Kubelet and provides elastic computing and Kubernetes orchestration capabilities. It supports second\-level startup, high\-concurrency creation, and secure isolation with sandbox containers.

* By combining the advantages of serverless and containerization, VCI offers enterprises an efficient, reliable, and secure environment. It allows you to focus on developing and running cloud\-native applications without worrying about the management and maintenance of underlying infrastructure. Additionally, VCI can optimize your cloud costs because you only pay for the resources you use.


<span id=".5Lqn5ZOB5Yqf6IO9"></span>
## Features


|**Feature** |**Description** |
|---|---|
|Serverless |The serverless architecture eliminates the need to purchase underlying infrastructure and subsequent efforts such as management, maintenance, or capacity planning during runtime. It provides a fully managed, zero operations and maintenance (O&M), and securely isolated serverless environment for your container applications. |
|Multiple instance specifications |Based on differences in underlying hardware capabilities, instance types are categorized into distinct instance families. Each family uses different processors, CPU/memory ratios, cloud disk types, and network card virtualization methods to provide differentiated computing, storage, and network performance. VCI offers two instance families, each with multiple specifications:<br><br><br>* [General-purpose](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose): A general\-purpose instance family that offers various vCPU and memory configurations. |
|Pay\-as\-you\-go by second |You can manage VCIs throughout their lifecycles. You pay for the actual uptime of VCIs. The billing cycle is accurate down to seconds, and bills are settled on an hourly basis. |
|Second\-level autoscaling |VCI supports second\-level pod startup, which enables rapid autoscaling in response to sudden traffic surges to meet real\-time business requirements. |
|Efficient isolation |Based on MicroVM technology, it provides VM\-level security and efficient isolation. These factors contribute to lower resource consumption and higher efficiency. |
|Bursting on\-premises workloads to the cloud |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VCI provides the ability to burst workloads from self\-built Kubernetes clusters to the cloud. By registering and managing virtual nodes on the cloud, it elastically schedules business workloads from Kubernetes clusters to cloud resources. This fully expands the computing resource capacity of on\-premises clusters. |
|Global configuration |It provides the vci\-profile configuration file to support unified configuration of VCI resources at the cluster or namespace level, as well as global fixed allocation capabilities. This capability reduces the need to modify workload YAML files, enables more convenient, efficient, and non\-intrusive use of VCI, and avoids confusion between operation management and business management. |
|Image cache acceleration. |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VCI provides an image caching solution that allows pre\-downloading images to data disks and creating cache snapshots. Based on these snapshots, VCI instance creation can be accelerated. This solution enables direct mounting at container startup, thereby reducing or avoiding image layer downloads. This solution eventually reduces the read and write pressure on image repositories and cloud disks, significantly shortens the image download duration, and greatly reduces instance startup time. |
|Comprehensive monitoring of VCI status |VCI supports monitoring of VCI instances in all aspects based on Volcengine VMP, including usage of CPU, memory,, network throughput performance indicators, and status of control plane and data plane components. This allows you to track the status of container applications in real time. |


<span id=".5Lqn5ZOB5p625p6E"></span>
## Service architecture

VCI seamlessly integrates with VKE via Virtual Kubelet, delivering security, isolation, high performance, and ease of use to support your container services.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c1f2965e27200f5efa857f2276ece34.png) </span>

<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios


* Highly elastic businesses

   Applications with significant peaks and troughs, such as live streaming, e\-commerce, and social networking.

* Task\-oriented applications

   * Data processing types: big data computing, machine learning, and scientific computing.

   * Event\-driven types: video recording, transcoding, and IoT.

   * CI/CD, GitLab Runner, and Jenkins.

* Online business hosting
