---
title: "Storage basics"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Storage_basics"
---

This topic details common Kubernetes storage concepts, such as access modes, binding modes, and reclaim policies, to help you better understand the basics of storage before using storage solutions.

<span id="JFOPA87F"></span>
## Volume

<span id="OdYNGAmK"></span>
### Volume overview

In a Kubernetes cluster, files inside containers are stored temporarily on disks. This temporary data storage causes the following issues for mission\-critical applications:


* When a container crashes or is rebuilt, its internal files are lost, making data persistence impossible.

* When multiple containers in the same Pod run collaboratively, file sharing or data exchange cannot be implemented efficiently and securely.


To address these issues, Kubernetes provides volume abstraction. Volumes are subordinate to Pods and are not independently creatable resource objects. They must be defined and declared in the spec section of Pod manifests. All containers within a Pod can use the volumes, but the volumes must be mounted to specified directories inside the containers.

<span id="85dQAtAL"></span>
### Basic volume usage principles


* A Pod can mount multiple volumes. However, to ensure stability and maintainability, avoid mounting an excessive number of volumes in a single Pod.

* A Pod supports mounting volumes of different types at the same time to meet diverse data storage requirements.

* Volumes in a Pod can be shared among multiple containers to enable data exchange between containers.

* In Kubernetes production environments, the recommended solution to mounting and managing volumes is the PersistentVolumeClaim (PVC) or PersistentVolume (PV) resource.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information about volumes, see the <a href="https://kubernetes.io/zh-cn/docs/concepts/storage/volumes/">official Kubernetes documentation</a>.</div>


<span id="9Ppiah15"></span>
## Volume access modes

Volume access modes (accessModes) are standard constraints defined by Kubernetes to describe how a volume can be mounted and used by cluster nodes. They define the concurrent access capability and permission scope of a volume.

Kubernetes defines three standard access modes, which are followed by all CSI (Container Storage Interface)\-compatible storage services:


* ReadWriteOnce (RWO): Single\-node read/write access. The volume can be mounted as read\-write by a single node simultaneously.

* ReadOnlyMany (ROX): Multi\-node read\-only access. The volume can be mounted as read\-only by many nodes.

* ReadWriteMany (RWX): Multi\-node read/write access. The volume can be mounted as read\-write by many nodes.


The following table lists the access modes supported by different volume types.


|Storage type |ReadWriteOnce |ReadWriteMany |
|---|---|---|
|EBS |✅ |❌ |
|TOS |❌ |✅ |
|NAS |❌ |✅ |
|EFS |❌ |✅ |
|vePFS |❌ |✅ |
|CloudFS |❌ |✅ |


<span id="WouzdDKA"></span>
## Volume binding mode

The volume binding mode (volumeBindingMode) is a core StorageClass configuration field that controls when a PV is bound to a PVC and when a PV is dynamically provisioned in Kubernetes. It determines the timing of storage resource allocation, which directly affects the Pod scheduling success rate and stability in multi\-availability\-zone scenarios. Kubernetes supports two binding modes: Immediate and WaitForFirstConsumer. If no binding mode is explicitly configured, Immediate is used by default.

<span id="ZFzeCKae"></span>
### Immediate

In Immediate binding mode, when a PVC is created, the cluster searches for a matching PV to bind to it. If no matching PV is found, the automatic provisioning process is initiated:


1. If the newly created PVC specifies a StorageClass name, the provisioner plug\-in that corresponds to the StorageClass will automatically create a PV.

2. The provisioner plug\-in creates a PV based on the parameters defined in the PVC and the StorageClass.

3. The provisioner plug\-in creates a data volume in the storage resource pool and then creates a PV by using the data volume information.

4. After the PV is created, it is bound to the PVC.


In summary, if a StorageClass defines the immediate binding mode for binding PVs and PVCs, when a PVC is created, it will be immediately bound to an existing suitable PV. If no suitable PV is available, a new suitable PV will be immediately created for binding.

<span id="PRqfWJW0"></span>
### WaitForFirstConsumer

The WaitForFirstConsumer mode is a delayed binding mode. In this mode, when a PVC is created, the system does not immediately bind a PV to it, but waits until the PVC is consumed by a Pod. The binding process is as follows:


1. When a pod is created and consumes this PVC, the system detects that the PVC uses delayed binding.

2. The scheduler continues scheduling and synchronizes the scheduling result to the metadata of the PVC.

3. The provisioner detects that scheduling information has been written to the PVC. It then uses the scheduling information to determine target storage attributes, such as the node and availability zone.

4. PV creation is triggered.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When you mount a cloud disk, a restriction exists based on the availability zone. Only cloud disks and nodes in the same availability zone can be mounted. This restriction may lead to the following issues during use.</div>



* <div data-tips="true" data-tips-type="tip">A cloud disk is created in Availability Zone A. However, node resources in Availability Zone A are insufficient. In this case, pods starting on nodes in Availability Zone B cannot mount the cloud disk.</div>


* <div data-tips="true" data-tips-type="tip">When multiple availability zones exist, users find it hard to assess and plan the appropriate number of PVs for each availability zone in advance.</div>



When multiple availability zones exist, you can use the WaitForFirstConsumer binding mode to prevent the preceding issues. When a user creates a PVC, the provisioner plug\-in will no longer immediately bind it to a PV or create a PV. Instead, it will wait until the PVC is consumed by a pod before performing the creation process. In this mode, when a pod is started, it is first scheduled to a node. After the location of the pod is confirmed, a PV and cloud disk are created based on the availability zone information of the pod. This ensures that both the node running the pod and the cloud disk are in the same availability zone. Therefore, in a cluster environment with multiple availability zones, we recommend that you use the WaitForFirstConsumer binding mode.

<span id="71YnQwA8"></span>
### Binding mode comparison

The following table compares the binding modes.


|Item |**Immediate (immediate binding)**  |**WaitForFirstConsumer (delayed binding)**  |
|---|---|---|
|Binding timing |Immediately when the PVC is created |After a pod that uses the PVC has been scheduled |
|Topology\-aware |No (Pod scheduling constraints are ignored) |Yes (fully matching nodes and availability zones) |
|Multi\-availability\-zone performance |Poor (scheduling easily fails) |Excellent (recommended in production) |
|Pod startup speed |Fast (volumes are ready) |Slightly slower (volume provisioning occurs during scheduling) |
|Resource utilization |Potential resource waste (pre\-allocation) |High (on\-demand allocation) |


<span id="AsxTcGM1"></span>
## PersistentVolume reclaim policy

A reclaim policy (persistentVolumeReclaimPolicy) is a core PV and StorageClass configuration field that controls how a PV and its data are processed when its bound PVC is deleted. It is a critical setting for persistent storage lifecycle management. Two reclaim policies are available: Delete and Retain.


|Item |Delete |Retain |
|---|---|---|
|Behavior |When the PVC is deleted, the PV and the underlying storage volume are automatically deleted, along with the data. |When the PVC is deleted, neither the PV nor the underlying storage resources are deleted. Manual deletion and reclamation are needed.  After the PVC is deleted, the PV enters the `Released` state, and cannot be directly bound to a PVC again. |
|Features |Resources are automatically released. However, data cannot be restored after deletion. |It provides maximum data security with no risk of accidental deletion. Administrators need to manually clean up PVs and underlying storage resources. |
|Application scenario |Test environments, temporary data, caches, stateless applications, and non\-critical data (such as logs). |Databases, core business data, and other high\-value data requiring long\-term retention. |
