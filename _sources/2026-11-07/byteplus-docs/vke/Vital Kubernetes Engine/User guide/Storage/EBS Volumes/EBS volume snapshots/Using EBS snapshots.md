---
title: "Using EBS snapshots"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-EBS-volume-snapshots"
---

This topic describes how to statically and dynamically create Elastic Block Storage (EBS) snapshots.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features">Beta · Apply for Trial</a>]: The EBS snapshot feature is currently in the beta stage. We recommend that you test this feature in non\-production environments first and exercise caution when using it in production.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Limits

EBS snapshots support the instant availability feature. After enabling this feature, you do not need to wait for the snapshot creation progress to reach 100% before using the snapshot to create a new EBS volume. This feature provides a faster and more convenient snapshot service. For details, see [Instant snapshot availability](https://docs.byteplus.com/en/docs/ecs/Instant-access).

The following limitations apply to the instant availability feature:


1. Instant availability supports only ESSD_PL0 and ESSD_FlexPL EBS types.

2. The available traffic bandwidth during lazy loading is limited to 15\-40 MB/s per volume.

3. Snapshot size cannot exceed 300 GB.

4. During lazy loading when you use an instant snapshot to create a PersistentVolume (PV), the snapshot cannot be deleted.

5. A single account in a single region can have up to 10 instant snapshots in the lazy loading state.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-ebs add\-on has been installed. For details, see [csi-ebs](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.Y3NpLWVicy3nu4Tku7Y=).

* The snapshot\-controller add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A StorageClass (SC) and PersistentVolumeClaim (PVC) have been created. In this topic, the PVC is named pvc\-ebs. For details, see [Using EBS as dynamic PersistentVolumes](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes).

* The cluster has been connected using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

* To use the instant snapshot availability feature, ensure that the csi\-ebs add\-on has been upgraded to version 1.2.13 or later.


<span id=".5Yqo5oCB5Yib5bu65b-r54Wn"></span>
## Dynamically creating snapshots

<span id="UTpMQNy2"></span>
### Step 1: Create a VolumeSnapshotClass


1. Create a YAML file for the VolumeSnapshotClass. The following `vke-volumesnapshotclass.yaml` file serves as an example:

   ```YAML
   apiVersion: snapshot.storage.k8s.io/v1
   kind: VolumeSnapshotClass
   metadata:
     name: vke-volumesnapshotclass   # The name of the VolumeSnapshotClass.
   parameters:
     instantAccess: "false" # Whether to enable the EBS instant snapshot availability feature. The valid value is false or true. By default, this feature is disabled.
   driver: ebs.csi.volcengine.com   # The driver type. This example uses ebs.csi.volcengine.com, which indicates the csi-ebs add-on.
   deletionPolicy: Delete   # Snapshot reclaim policy. Supported policies include Delete (deleting VolumeSnapshot also deletes VolumeSnapshotContent and related resources) and Retain (deleting VolumeSnapshot does not automatically delete VolumeSnapshotContent and related resources).
   ```
   

2. Run the following command to create the VolumeSnapshotClass.

   ```Bash
   kubectl apply -f vke-volumesnapshotclass.yaml
   ```
   


<span id="KAd9BXZo"></span>
### Step 2: Create a workload and write data

Create a workload (application) and write data. This topic uses a stateless workload (Deployment) as an example.


1. Create a YAML file for the Deployment. The following `deployment-nginx.yaml` file serves as an example. For details, see [Using dynamic EBS PersistentVolumes](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes#.6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So). For information about how to configure other types of workload, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads).

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-nginx
   spec:
     selector:
       matchLabels:
         app: nginx
     template:
       metadata:
         labels:
           app: nginx
       spec:
         containers:
         - name: nginx
           image: cr-cn-beijing.volces.com/****/vci-demo-nginx:latest # The image file to deploy.
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - name: ebs-essd-volume0
             mountPath: /data
         volumes:
           - name: ebs-essd-volume0
             persistentVolumeClaim:
               claimName: pvc-ebs # The name of the PVC.
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f deployment-nginx.yaml
   ```
   

3. Write data to the pod.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>deployment-nginx-6fcb64f6cd-qcxkt</code> with your own pod name.   </div>
   

   ```Bash
   kubectl exec deployment-nginx-6fcb64f6cd-qcxkt -- touch /data/test   
   ```
   

   Check whether the data has been written.

   ```Bash
   kubectl exec deployment-nginx-6fcb64f6cd-qcxkt -- ls /data   
   ```
   

   The expected output is as follows:

   ```Bash
   lost+found
   test  
   ```
   


<span id="rCWUnLai"></span>
### Step 3: Create a snapshot


1. Create a VolumeSnapshot YAML file. The following `vke-snapshot.yaml` file serves as an example:

   ```YAML
   apiVersion: snapshot.storage.k8s.io/v1
   kind: VolumeSnapshot
   metadata:
     name: vke-snapshot  # The custom VolumeSnapshot name, which will be used when you restore data from the snapshot.
     namespace: default  # The namespace of the VolumeSnapshot.
   spec:
     volumeSnapshotClassName: vke-volumesnapshotclass  # The VolumeSnapshotClass created in Step 1.
     source:
       persistentVolumeClaimName: pvc-ebs  # It must be consistent with the PVC name used by the workload in Step 2.
   ```
   

2. Run the following command to create the VolumeSnapshot.

   ```Bash
   kubectl apply -f vke-snapshot.yaml
   ```
   


<span id="wBOHQh7o"></span>
### Step 4: Validate the result


1. Run the following command to check whether the snapshot was created successfully.

   ```Bash
   kubectl get VolumeSnapshot
   ```
   

   The expected output is as follows. You can view the status and source of the EBS snapshot.

   ```Bash
   NAME           READYTOUSE   SOURCEPVC   SOURCESNAPSHOTCONTENT   RESTORESIZE   SNAPSHOTCLASS             SNAPSHOTCONTENT                  CREATIONTIME   AGE
   vke-snapshot   true         pvc-ebs                             20Gi          vke-volumesnapshotclass   snapcontent-b863c082-ad70-4***   2m29s          2m29s
   ```
   

2. Run the following command to view the details of the EBS snapshot.

   ```Bash
   kubectl get VolumeSnapshotContent
   ```
   

   The expected output is as follows:

   ```Bash
   NAME                             READYTOUSE   RESTORESIZE   DELETIONPOLICY   DRIVER                   VOLUMESNAPSHOTCLASS       VOLUMESNAPSHOT   VOLUMESNAPSHOTNAMESPACE   AGE
   snapcontent-b863c082-ad70-4***   true         21474836480   Delete           ebs.csi.volcengine.com   vke-volumesnapshotclass   vke-snapshot     default                   3m12s
   ```
   


<span id=".6Z2Z5oCB5Yib5bu65b-r54Wn"></span>
## Statically creating snapshots


1. In the [ECS console](https://console.byteplus.com/ecs/instance)  ** ** create a snapshot. For details, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).

2. (Optional) To use the instant snapshot feature, add the following label to the snapshot configuration.

   
   |Label key |Label value |
   |---|---|
   |ebs.csi.volcengine.com/use\-instant\-access |true |
   

3. Create a VolumeSnapshotContent YAML file. The following `vke-snapshotcontent.yaml` file serves as an example:

   ```YAML
   apiVersion: snapshot.storage.k8s.io/v1
   kind: VolumeSnapshotContent
   metadata:
     name: vke-snapshotcontent
   spec:
     deletionPolicy: Retain   # Snapshot reclaim policy. Supported policies include Delete (deleting VolumeSnapshot also deletes VolumeSnapshotContent and related resources) and Retain (deleting VolumeSnapshot does not automatically delete VolumeSnapshotContent and related resources).
     driver: ebs.csi.volcengine.com   # The driver type. This example uses ebs.csi.volcengine.com, which indicates the csi-ebs add-on.
     source:
       snapshotHandle: snap-f1ksxj7k1d********   # The ID of the created snapshot in ECS.
     volumeSnapshotRef:
       name: vke-snapshot   # The name of the VolumeSnapshot.
       namespace: default   # The namespace of the VolumeSnapshot.
   ```
   

4. Run the following command to create a VolumeSnapshotContent.

   ```Bash
   kubectl apply -f vke-snapshotcontent.yaml
   ```
   

5. Create a VolumeSnapshot YAML file. The following `vke-snapshot.yaml` file serves as an example:

   ```YAML
   apiVersion: snapshot.storage.k8s.io/v1
   kind: VolumeSnapshot
   metadata:
     name: vke-snapshot   # The name of the VolumeSnapshot. The name must be consistent with the custom snapshot name specified in Step 2. This name will be used for restoring data from the snapshot.
     namespace: default   # The namespace of the VolumeSnapshot. It must be consistent with the namespace selected in Step 2.
   spec:
     source:
       volumeSnapshotContentName: vke-snapshotcontent   # The name of the VolumeSnapshotContent created in Step 2.
   ```
   

6. Run the following command to create the VolumeSnapshot.

   ```Bash
   kubectl apply -f vke-snapshot.yaml
   ```
   


<span id=".5oGi5aSN5b-r54Wn"></span>
## Restoring data from snapshots

After a snapshot is created, you can restore data from the snapshot to a new PVC. The following YAML file serves as an example. For details, see [Using EBS as dynamic PersistentVolumes](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes#.6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So).

```YAML
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: restore-test
  namespace: default
spec:
  storageClassName: ebs-ssd
  dataSource:
    name: vke-snapshot # The name of the snapshot from which you want to restore data. It is the name that you specified when you created the VolumeSnapshot. Make sure that you specify the name of the target snapshot.
    kind: VolumeSnapshot
    apiGroup: snapshot.storage.k8s.io
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi    # The storage needs to be greater than or equal to the size of the snapshot (original EBS volume)
```
