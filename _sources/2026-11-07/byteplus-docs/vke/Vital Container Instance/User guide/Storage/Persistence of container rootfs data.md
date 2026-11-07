---
title: "Persistence of container rootfs data"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Persistence-of-container-rootfs"
---

VCI supports mounting the read\-write layer of VCI pods to cloud disks (persistent volumes) based on user\-defined configurations. This support enables persistence of container rootfs data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"> [<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently at the beta stage. Submit an application if you need to use it.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Only EBS cloud disks can be used to persist rootfs data. Other storage types are not supported.

* We recommend using an empty disk when using EBS to persist rootfs data for the first time. If the disk is not empty, it is recommended to specify a separate directory. If no directory is specified, the root directory is used by default. In this case, ensure that the root directory does not contain the `upper` or `work` directory .


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A cluster for VCI applications has been created. For details, see [Using VCI in VPC-CNI network model cluster ](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine), [using VCI in Flannel network model cluster ](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Flannel-cluster).

* The csi\-ebs add\-on has been installed in the cluster. For details, see [csi-ebs](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.Y3NpLWVicy3nu4Tku7Y=).

* An ESSD has been created. For details, see [Creating cloud disks](https://docs.byteplus.com/en/docs/ecs/Create-a-volume).


<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

Specify a volume used for the read\-write layer of containers by adding a specific annotation to VCI pods.


|Annotation Key |Annotation sample value |Description |
|---|---|---|
|vci.volcengine.com/overlay\-rw\-layer\-spec |[] |Whether to persistently store container rootfs data. To achieve persistent storage, configure the following fields:<br><br><br>* **name**: The name of the target container.<br><br>* **volumeName**: The name of the volume. The name set here must be consistent with the value of `spec.volumes.name` in the pod YAML manifest.<br><br>* **Path**: The storage path for container rootfs data within the volume. By default, the field is left empty to indicate that the root directory of the volume is used as the storage path for container rootfs data.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When multiple containers use the same volume as the storage path for container rootfs data, they must be distinguished by <code>path</code>.   </div><br>    |


The following YAML sample provides an example of the pod annotation:

```yaml
vci.volcengine.com/overlay-rw-layer-spec: |-
  [
     {
         "name": "$Container_name", 
         "volumeName": "$Volume_name",
         "path": "$Volume_path"
     }, 
     {
         "name": "my_container",
         "volumeName": "ebs-volume",
         "path": "final/rootfs-dir1"
     }
  ]
```


<span id=".5L2_55So5pa55rOV"></span>
## Procedure

The following example demonstrates how to create a VCI pod that uses a statically provisioned EBS PersistentVolume (PV) for rootfs data persistence. For more information about using EBS PVs, see [EBS PVs](https://docs.byteplus.com/en/docs/vke/EBS-Volumes).


1. Connect to the VCI cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a PV of type EBS.

   1. Create a YAML file for the PV. The following `vci-ebs-pv.yaml` file serves as an example:

      ```yaml
      apiVersion: v1
      kind: PersistentVolume
      metadata:
        name: vci-ebs-pv  # The name of the PV.
      spec:
        accessModes:
        - ReadWriteOnce
        capacity:
          storage: 20Gi # EBS storage capacity.
        csi:
          driver: ebs.csi.volcengine.com
          fsType: ext4
          volumeAttributes:
            ChargeType: PostPaid
            type: ESSD_PL0    # Cloud disk type. The cloud disk name must be in uppercase.
            zone: cn-beijing-a  # The availability zone where your application resides.
          volumeHandle: vol-cmukmy9yi5bi254b****  # Specify the ID of an existing ESSD.
        volumeMode: Filesystem
      ```
      

   2. Run the following command to create the PV.

      ```bash
      kubectl create -f vci-ebs-pv.yaml
      ```
      

3. Create a PersistentVolumeClaim (PVC).

   1. Create a YAML file for the PVC. The following `vci-ebs-pvc.yaml` file serves as an example:

      ```yaml
      apiVersion: v1
      kind: PersistentVolumeClaim
      metadata:
        name: vci-ebs-pvc  # The name of the PVC.
        namespace: default  # The namespace where the PVC is located.
      spec:
        accessModes:
        - ReadWriteOnce
        resources:
          requests:
            storage: 20Gi
        volumeMode: Filesystem
        volumeName: vci-ebs-pv  # The name of the PV bound to this PVC (the PV created in Step 2).
      ```
      

   2. Run the following command to create the PVC.

      ```bash
      kubectl create -f vci-ebs-pvc.yaml
      ```
      

4. Create a VCI and configure parameters related to persistence of container rootfs data. For detailed instructions on creating a VCI instance, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

   1. Create a YAML file for the VCI pod. The following `vci-pod-ebs-rootfs.yaml` file serves as an example:

      ```yaml
      apiVersion: v1
      kind: Pod
      metadata:
        name: vci-pod-ebs-rootfs  # Pod Name.
        namespace: default  # Namespace to which the pods belong.
        annotations:
          vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
          vci.volcengine.com/overlay-rw-layer-spec: |-
            [
                    {
                      "name": "c1",
                      "volumeName": "rootfs",
                      "path": "final/rootfs-dir1"
                    },
                    {
                      "name": "c2",
                      "volumeName": "rootfs",
                      "path": "final/rootfs-dir2"
                    }
            ]
        labels:
          app: vci-pod-ebs-rootfs
      spec:
        containers:
          name: c1  # The container name.
          image: nginx:1.14.2  # The container image address and tag of the pod. Replace the values with those used in your business scenario.
          imagePullPolicy: Always
          name: c2  # The container name.
          image: nginx:1.14.2  # The container image address and tag of the pod. Replace the values with those used in your business scenario.
          imagePullPolicy: Always
        tolerations:
        - effect: NoSchedule
          key: vci.vke.volcengine.com/node-type
          operator: Equal
          value: vci
        volumes:
        - name: rootfs  # Keep it consistent with the volumeName specified in the annotation.
          persistentVolumeClaim:
            claimName: vci-ebs-pvc  # Keep it consistent with the name of the PVC associated with EBS volume created in Step 3.
      ```
      

   2. Run the following command to create the VCI pod.

      ```bash
      kubectl create -f vci-pod-ebs-rootfs.yaml
      ```
      


<span id=".6aqM6K-B5q2l6aqk"></span>
## Validation steps

This example shows how to verify the result by installing the vim add\-on in the pod. This verification method requires that **public network access** is enabled for the cluster.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If public network access is not enabled when the cluster is created, manually configure public network access for each node pool in every subnet of the cluster. For details, see <a href="https://docs.byteplus.com/en/docs/vke/How-do-I-manually-enable-internet-facing-access-for-a-cluster">FAQ</a>.</div>



1. Log in to the VCI pod and install the vim add\-on in the pod.

   ```Bash
   vim --version  # vim is not installed.
   apt-get update
   apt-get install vim -y
   vim --version  # vim is installed.
   ```
   

2. Delete the pod and then use the same pod YAML manifest to create the pod again.

   ```Bash
   kubectl delete pod vci-pod-ebs-rootfs -n default
   kubectl create -f vci-pod-ebs-rootfs.yaml
   ```
   

3. Log in to the newly created pod and use the `vim --version` command to verify that the previously installed vim add\-on is retained.
