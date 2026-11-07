---
title: "Using PFS PVs via NFS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_PFS_through_the_NFS_Service"
---

VKE supports PFS access over the Network File System (NFS) protocol. This topic describes how to access PFS over NFS by using the kubectl command\-line tool.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[Beta] The protocol service NFS is at the beta stage. To use this service, contact your account manager.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* PFS protocol support has been enabled, and an NFS PFS filesystem has been created.

* The kubectl tool has already been installed locally, and the target cluster has been connected by using kubectl. For details, see[ Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5pa55byP5LiA77ya5L2_55SoLXZlcGZzLemdmeaAgeWtmOWCqOWNtw=="></span>
## Using statically provisioned PFS PVs

<span id="tRFZksWR"></span>
### Step 1: Create a PV


1. Create a YAML file for the PV. The following `vke-pfs-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pfs-static-pv # PV name. The name must be unique within the cluster.
   spec:
     accessModes: # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     - ReadWriteMany
     capacity:
       storage: 20Gi # The PV capacity. This is a required field in Kubernetes, but meaningless for PFS. It is only required as a validation parameter.
     csi:
       driver: nas.csi.volcengine.com # Driver required for storage mount.
       volumeAttributes:
         fsId: vepfs             
         fsType: vepfs  # Filesystem type. Value: Extreme, Cache, Capacity, or Vepfs (indicating PFS)
         path: /vepfs/temp # Mount subdirectory on the filesystem. It must start with the /vepfs prefix.
         server: export-6535d79e.cnbxxxxxbbd50f.rrazxxxxxxx7g.vepfs.ivolces.com  # Mount point of the target export directory for PFS.
         volumeAs: subpath   # The type of the subdirectory. Value: subpath (indicating a subpath) or filesystem (indicating a filesystem).
       volumeHandle: pfs-static-pv  # The unique identifier of the PV. Keep it consistent with the PV name. To use multiple PVs simultaneously, the value for each PV must be different.
     mountOptions:
     - nolock,proto=tcp,noresvport
     - vers=3                      # PFS supports only v3.
     persistentVolumeReclaimPolicy: Retain # The PV reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem
   ```
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-pfs-static-pv.yaml
   ```
   


<span id="vklu0KxM"></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `vke-pfs-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pfs-static-pvc
     namespace: default
   spec:
     accessModes:  # PVC access method. Only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
       - ReadWriteMany
     resources:
       requests:
         storage: 20Gi # The declared storage capacity. This is a required field in Kubernetes, but meaningless for PFS. It is only required as a validation parameter.
     volumeName: pfs-static-pv # The name of the PV bound to this PVC.
   ```
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-pfs-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                   STATUS   VOLUME                 CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-pfs-static-pvc     Bound    vke-pfs-static-pv      20Gi       RWX                           2m36s
   ```
   


<span id="X33m0gXQ"></span>
### Step 3: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `deployment-nginx-static.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-nginx-static
     namespace: default
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
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
             name: nginx
           volumeMounts:
           - name: pfs
             mountPath: /tmp # Mount location of the PV in the container.
         volumes:
           - name: pfs
             persistentVolumeClaim:
               claimName: pfs-static-pvc # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f deployment-nginx-static.yaml
   ```
   


<span id=".5pa55byP5LqM77ya5L2_55SoLXZlcGZzLeWKqOaAgeWtmOWCqOWNtw=="></span>
## Using dynamically provisioned PFS PVs

<span id="rgeHpM5Q"></span>
### Step 1: Create a StorageClass


1. Create a YAML file for the SC. The following `vke-pfs-sc.yaml` file serves as an example:

   ```YAML
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: pfs-nas-sc # Name of the StorageClass.
   mountOptions:
   - nolock,proto=tcp,noresvport,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2
   - vers=3 # Protocol version for mounting the data volume. Value: 3 (indicating NFSv3)
   parameters:
     ChargeType: PostPaid # Billing type. It supports only PostPaid, which means pay-as-you-go.
     fsId: vepfs # Filesystem ID. Value: vepfs
     fsType: vepfs # Filesystem type. Value: vepfs
     server: cngl327ffxxxxx78.3rei7p0lzu1xxxxx2j48kqtl.vepfs.ivolces.com
     subPath: /test # The subdirectory after subPath mounting. The system will create directories within this subdirectory as the backend storage for dynamically provisioned volumes.
     volumeAs: subpath # The type of the subdirectory. Value: subpath (indicating a subpath) or filesystem (indicating a filesystem).
   provisioner: nas.csi.volcengine.com # Driver required for storage mount.
   reclaimPolicy: Retain # The reclaim policy. Value: Retain or Delete.
   volumeBindingMode: Immediate # Volume binding mode. Values include Immediate (indicating immediate binding and allocation) and WaitForFirstConsumer (indicating delayed binding and allocation).
   ```
   

2. Run the following command to create the StorageClass.

   ```Bash
   kubectl create -f vke-pfs-sc.yaml
   ```
   


<span id="pR7ajBYg"></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `vke-pfs-dynamic-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pfs-dynamic-pvc
     namespace: default
   spec:
     accessModes: # PVC access method. Only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     - ReadWriteMany
     resources:
       requests:
         storage: 20Gi # The declared storage capacity. This is a required field in Kubernetes, but meaningless for PFS. It is only required as a validation parameter.
     storageClassName: pfs-nas-sc  # Name of the created StorageClass.
   ```
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-pfs-dynamic-pvc.yaml
   ```
   

3. Run the following command to view the result of the dynamic binding between the PVC and StorageClass.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, it indicates that the PVC and the PV are dynamically bound through the StorageClass configured by PFS.

   ```Bash
   NAME                 STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   
   pfs-dynamic-pvc      Bound    pvc-6e8c646b-e3e9-4d02-836e-3b66********   20Gi       RWX            pfs-nas-sc      
   ```
   


<span id="SUs0iV0L"></span>
### Step 3: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `deployment-nginx-dynamic.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-nginx-dynamic
     namespace: default
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
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
             name: nginx
           volumeMounts:
           - name: pfs
             mountPath: /tmp # Mount location of the PV in the container.
         volumes:
           - name: pfs
             persistentVolumeClaim:
               claimName: pfs-dynamic-pvc # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f deployment-nginx-dynamic.yaml
   ```
   

   <span id="70LodUeP"></span>
   ## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-efs-static-deployment-xxx -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   fs_vepfs-cnsh67*** 6442450944 27478016 6414972928   1% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Write a file to the PV.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- touch /tmp/test
   ```
   

4. Delete the pod.

   ```Bash
   kubectl delete pod vke-nas-static-deployment-xxx
   ```
   

5. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- ls /tmp
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   

   <span id="hmu6SAYP"></span>
   ## Related documentation

* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
