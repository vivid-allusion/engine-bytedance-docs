---
title: "Storage overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Storage-overview"
---

VKE is integrated with BytePlus cloud storage services, such as EBS, FileNAS, CloudFS, and TOS, to deliver diversified storage capabilities for containers in clusters. This topic describes and compares the storage types supported by VKE.

<span id="7zk4vU6J"></span>
## Storage overview

The Kubernetes Container Storage Interface (CSI) is a standardized storage plug\-in framework launched by the Cloud Native Computing Foundation (CNCF) to enable deep decoupling between storage systems and Kubernetes. CSI allows various storage services to be flexibly integrated into Kubernetes clusters independently in a pluggable manner. Storage vendors can implement storage integration without modifying the core source code of Kubernetes. This greatly improves the flexibility, security, and iteration efficiency of storage extensions.

VKE leverages the CSI standard to deliver robust storage capabilities. It provides deep integration with mainstream cloud storage forms (block storage, file storage, and object storage) and also tailored storage solutions for typical business scenarios, including auto\-scaling of stateless applications, data persistence for stateful applications, and data sharing and isolation. This comprehensive approach meets diverse workload demands for storage performance, reliability, and scalability. Meanwhile, VKE container storage is fully compatible with the native storage system of Kubernetes, with seamless support for cloud\-native storage types including EmptyDir, HostPath, Secret, and ConfigMap. This dual focus on cloud\-native standardization and business compatibility delivers unified, stable, and user\-friendly container data management capabilities.

From the perspective of the storage source, the storage types supported by VKE can be divided into cloud storage, local storage, and Kubernetes resource objects.


|StorageClass type |**Description** |**Application scenarios** |
|---|---|---|
|Cloud storage |BytePlus cloud storage services. They allow data to be stored in the cloud for centralized management and elastic expansion. When creating a Pod, you only need to declare storage requirements and capacity via a PersistentVolumeClaim (PVC) or PersistentVolume (PV), and the CSI plugin will automatically connect to the cloud storage. This eliminates the need for manual configuration of underlying resources. |Suitable for data that needs to be highly available or shared. For example, logs and media resources. |
|Local storage |Local storage media (local disks, SSDs, and node memory). Data is not accessed over the network, but is read from and written directly to the local disks or node memory. The data access path is short, offering low latency and high performance. |Suitable for scenarios where high IO and low latency are critical, and data availability is not a priority. |
|Kubernetes resource object |Kubernetes\-native resource objects, such as ConfigMaps and Secrets. |ConfigMaps are mainly used to mount configuration files for Pods. Secrets are mainly used to deliver sensitive information to Pods, such as account credentials, certificates, or environment variables. |


<span id="RKRXWV5b"></span>
## StorageClass type

<span id="437LY3rd"></span>
### Cloud storage

Appropriate cloud storage types vary with business scenarios. The following table compares supported cloud storage services.


|StorageClass type |Service overview |Usage methods |Capacity and performance |Static PVs |Dynamic PVs |Application scenarios |
|---|---|---|---|---|---|---|
|EBS |EBS offers highly available, highly reliable, high\-performance, elastically scalable block storage devices. These block devices can serve as extended storage for Pods.  For more information, see [EBS](https://docs.byteplus.com/en/docs/ecs/Overview-of-elastic-block-storage). |It supports direct mounting. Volumes can be mapped to local directories of Pods for data storage and access. |GiB level. For details, see [Volume specifications](https://docs.byteplus.com/en/docs/ecs/Volume-specifications). |Supported. See [Using static EBS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes). |Supported. See [Using dynamic EBS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes). |I/O\-intensive applications, relational databases, NoSQL databases, development and testing, and more. |
|Torch Object Storage (TOS) |A large\-capacity, secure, cost\-effective, easy\-to\-use, highly reliable, and highly available distributed cloud storage service. Data stored on TOS is accessible and manageable over the network from any application, anywhere, and anytime. For more information, see [TOS](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos). |Data can be accessed over HTTPS by using multiple access methods, such as RESTful APIs, SDKs, and tools. |N/A. |Supported. See [Using static TOS PVs via the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client) and [Using static TOS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-TOS-Volumes). |Not supported. |Origin sites for VoD, audio and video live streaming, video monitoring, machine learning, autonomous driving, and more. |
|NAS |A high\-performance, cost\-effective cloud file storage service with shared access, continuous online availability, elastic scalability, and cross\-region access for elastic computing, containers, and AI applications. For more information, see [FileNAS](https://docs.byteplus.com/en/docs/nas/What-is-FileNAS). |It can be mounted via different network protocols (FSX and NFS), and allows data access after volumes are mapped to the local directories of Pods. |TiB level. For details, see [Product specifications](https://docs.byteplus.com/en/docs/nas/Product-specifications). |Supported. See [Using static FileNAS PVs via the FSX client](https://docs.byteplus.com/en/docs/vke/Use_a_static_NAS_PersistentVolume_through_the_FSX_client) and [Using static FileNAS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-NAS-Volumes). |Supported. See [Use dynamic FileNAS volumes](https://docs.byteplus.com/en/docs/vke/Using-dynamic-NAS-Volumes). |High\-performance computing, AI\-driven data processing, container storage, and more. |
|PFS |A high\-throughput, low\-latency, scalable parallel file system service that meets read/write throughput and latency requirements in high\-performance computing scenarios. For details, see [vePFS](https://docs.byteplus.com/en/docs/pfs/What-is-PFS). |It can be mounted via different network protocols (FSX, PFS Client, and NFS), and allows data access after volumes are mapped to the local directories of Pods. |TiB level. For details, see [Product specifications](https://docs.byteplus.com/en/docs/pfs/Product-specifications). |Supported. See [Using static vePFS PVs via the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_PFS_Volumes_through_FSX_client) and [Using static vePFS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-PFS-volumes). |Supported. See [Use dynamic vePFS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-PFS-volumes). |Large model training, autonomous driving, high\-performance computing, and AI\-driven data processing. |
|CloudFS |A file storage and acceleration service designed for the big data and machine learning ecosystem. It supports standard HDFS access and transparent data lake access. It provides low\-cost, high\-performance, high\-throughput, and highly available big data access.<br><br> |It supports direct mounting. Volumes can be mapped to local directories of Pods for data storage and access. |N/A. |Supported. See [Use static CloudFS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-CFS-Volumes). |Not supported. |Traditional Hadoop ecosystem, data lake analysis, machine learning training, and more. |


<span id="kJJz3i4o"></span>
### Local storage


|**Comparison dimension** |**Local volumes** |**Temporary path (EmptyDir)**  |**Host path (HostPath)**  |
|---|---|---|---|
|Basic knowledge |The local data disks of nodes are formed into a storage pool (VolumeGroup) by the Logical Volume Manager (LVM), and then logical volumes (LVs) are mounted to container instances. |It is the native EmptyDir type of Kubernetes, whose lifecycle is consistent with that of a container instance. It supports specifying memory as the storage medium. When the container instance is deleted, the EmptyDir is deleted synchronously, and the data stored in it is permanently deleted. |It mounts the file directory of the host machine where the container runs to the specified mount point inside the container. |
|Main characteristics |Persistent volumes that deliver low latency and high IO, but not high availability. |Local temporary volumes, whose storage space comes from the local kubelet root directory or memory. |It mounts a file or directory from the file system on a node. It supports automatic creation of host directories and allows Pod migration (not bound to nodes). |
|Usage methods |For details, see [Using local storage as dynamic volumes of the LVM type](https://docs.byteplus.com/en/docs/vke/Using_LVM_type_for_dynamic_Local_Volumes), [Using dynamic volumes created from dedicated local storage](https://docs.byteplus.com/en/docs/vke/Using_exclusive_type_for_dynamic_Local_Volumes), and [Using LVM-managed local volumes as ephemeral volumes](https://docs.byteplus.com/en/docs/vke/Using_local_storage_LVM_through_the_temporary_volume). |\- |\- |
|Application scenarios |Suitable for scenarios where high IO and low latency are critical, and data availability is not a priority. |* **Temporary file sharing between containers**: It is suitable for scenarios where multiple containers in the same Pod need to share temporary files and intermediate data, for example, sharing data directories among the main business container, log collection container, and sidecar proxy container.<br><br>* **Temporary cache and disk staging**: It is ideal for storing temporary data generated during application uptime that does not need to be persisted for improved read/write performance. This type of data includes temporary caches, intermediate computing results, temporary indexes, and other data items.<br><br>* **Temporary log buffering**: Container runtime logs are first written to EmptyDir and then asynchronously read and uploaded by the log collection component. This avoids business performance degradation caused by direct writes to remote storage.<br><br>* **Temporary working directories**: One\-off working directories for script execution, data decompression, and temporary file generation, where data does not need to be retained for an extended period. |* **Access to node system directories and system components**: Scenarios where containers need to read or write node OS files, device drivers, system log directories, and more, for example, collecting node system logs and reading node hardware information.<br><br>* **High\-performance temporary storage provided by node\-local disks**: For applications with high IO performance requirements but no need for cross\-node data sharing or high availability,  node\-local disks can be used directly to avoid performance loss caused by network storage.<br><br>* **File transfer and data exchange between containers and nodes**: Scenarios where containers need to read pre\-deployed fixed resources on the node, such as configuration files, installation packages, keys, and certificates, or write specific data to node\-local storage.<br><br>* **Temporary scenarios for data backup and local persistence**: In test environments or non\-critical applications, node\-local directories can be temporarily used to store data to implement data persistence easily.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">HostPath volumes pose many security risks. The best practice is to avoid using HostPath whenever possible. When HostPath volumes are necessary, their scope should be limited to the required files or directories only, and they should be mounted in read\-only mode.</div><br> |


<span id=".5a655Zmo5pyN5Yqh5pSv5oyB55qE5a2Y5YKo57G75Z6L"></span>
## Related documentation


* For information about how to use different types of volumes, see the following topics:

   * [EBS](https://docs.byteplus.com/en/docs/vke/EBS-Volumes)

   * [NAS](https://docs.byteplus.com/en/docs/vke/NAS-Volumes)

   * [PFS](https://docs.byteplus.com/en/docs/vke/Model_selection_description)

   * [CloudFS](https://docs.byteplus.com/en/docs/vke/CFS-Volumes)

   * [Local volumes](https://docs.byteplus.com/en/docs/vke/Using_LVM_type_for_dynamic_Local_Volumes)

* For container storage best practices, see [Storage best practices](https://docs.byteplus.com/en/docs/vke/Best-practices-Storage).

* For container storage FAQs and solutions, see [Storage FAQs](https://docs.byteplus.com/en/docs/vke/Storage-FAQs).
