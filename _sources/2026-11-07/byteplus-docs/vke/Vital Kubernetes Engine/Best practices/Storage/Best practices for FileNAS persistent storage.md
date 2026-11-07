---
title: "Best practices for FileNAS persistent storage"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NAS-persistent-storage-best-practices"
---

FileNAS provides shared and persistent storage services, which allow multiple pods to share data. This topic describes how to use FileNAS for shared and persistent storage by statically creating PVs.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenario

FileNAS can be mounted by multiple pods at the same time. In this case, multiple pods may modify the same data at the same time. Therefore, applications need to automatically achieve data synchronization.

<span id=".5pyJ54q25oCB5pyN5YqhLW5hcy3nmoTkvb_nlKjlnLrmma8="></span>
### Usage scenarios for stateful FileNAS service


* Applications with high disk I/O requirements.

* Read/write performance is higher than that of TOS.

* It can achieve cross\-host file sharing. For example, it can function as a file server.


<span id=".5pyJ54q25oCB5pyN5YqhLW5hcy3nmoTkvb_nlKjmlrnlvI8="></span>
### Usage methods for stateful FileNAS service


1. Manually create a file system and add mount points.

2. Manually create PVs and PVCs.


<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

The following content introduces the proven practices of VKE. To achieve the expected results and conform to the [limits of VKE](https://docs.byteplus.com/en/docs/vke/Limits), you need to perform operations by following the solution described in this topic or on the recommended resources. If you want to use another solution, consult your account manager.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An account has been created, and real name authentication has been completed.

* The project to which the file system belongs has been created. 

* A VPC has been created. For detailed operations, see [Creating VPCs](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC). The VPC used for mounting the file system must be consistent with the VPC where your Kubernetes cluster is located.

* A file system and a mount point have been created in the FileNAS console. If not, create a file system and a mount point based on the instructions in Step 1. The created file system must be in the same availability zone as your Kubernetes cluster.

* Pods that use the file system must run on the same node, and the node and the created file system must be deployed in the same availability zone.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65paH5Lu25a2Y5YKo5ZKM5oyC6L2954K5"></span>
### Step 1: Create a file system and a mount point


1. Log in to the [FileNAS console ](https://console.byteplus.com/filenas/), and select the target region from the top navigation bar.

2. In the left navigation bar, click **File System \> File System list** to create a file system. For more details, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/Creating-a-file-system).

3. In the left navigation bar, click **File System \> Permission groups** to create a permission group and configure an authorization management rule. For more details, see [Creating groups and rules](https://docs.byteplus.com/en/docs/nas/Managing-permission-groups).

4. In the left navigation bar, click **File system \> Instance list**. On the page that appears, click the name of the file system for which you want to create a mount point, and create a mount point. For more details, see [Creating mount points](https://docs.byteplus.com/en/docs/nas/Managing-mount-points).


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 2: Create a PV


<Tabs>
<Tab zoneid="MGjrxe3qQ0" title="Creating through the console">
<TabTitle>Creating through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar of VKE console, click **Cluster**.

3. Click the name of the target cluster to go to the cluster management page.

4. On the cluster management page, click **Storage \> PersistentVolume**.

5. In the upper left corner of the PV list, click **Create PersistentVolume**.

6. On the **Create PersistentVolume** page, configure the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |how to create |Select a method for creating the PV. Currently, you can select **Static creation**, in which the administrator creates one. |
   |Name |Specify a valid name for the PV. The name must be unique within the cluster. |
   |PersistentVolume type |Select a PV type. In this scenario, select **NAS**. |
   |Access mode |Select a PV access mode. Currently, you can select ReadWriteMany, which enables read and write access by multiple nodes. |
   |File system type |Select a file system type.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Capacity\-type file storage is currently in beta in both VKE and FileNAS. To use this feature, you must apply for a trial of both VKE and FileNAS.</div><br> |
   |Mount point |Select a mount point that exists under an existing FileNAS file system and is in the same VPC as the cluster. |
   |Subpath |Enter a valid subdirectory that complies with the on\-screen rules. The default directory is the root directory, which is represented by `/`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Ensure that the subdirectory already exists in FileNFS.</div><br> |
   |NFS version |Select an NFS version for the PV.<br><br><br>* If the file system type is Extreme speed, it supports the **NFSv3** version.<br><br>* If the file system type is Capacity type, it supports the **NFSv3** version. |
   

7. Click **Confirm**.


</Tab>
<Tab zoneid="Za9dVHKFtw" title="Configure resource quotas through YAML">
<TabTitle>Configure resource quotas through YAML</TabTitle>

The following sample code shows how to create a PV by using YAML:

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: vke-nas-static-pv  # The name of the PV.
spec:
  accessModes:  # PV access mode. Currently, only ReadWriteMany is supported.
  - ReadWriteMany
  capacity:
    storage: 100Gi # FileNAS storage capacity.
  csi:
    driver: nas.csi.volcengine.com  # The driver type. This example uses nas.csi.volcengine.com, which indicates the csi-nas add-on.
    volumeAttributes:
      fsId: enas-cnbj1b9f********  # The ID of the FileNAS file system. This parameter needs to be specified only if the file system type is Extreme speed.
      fsType: Extreme   # The file system type. Valid values include Extreme and Capacity.
      path: /enas-cnbj1b9f********/temp  # The subdirectory of the FileNAS file system for mounting.
      server: cnbj1b9f********.r*********.nas.ivolces.com  # The mount point of the FileNAS file system.
      volumeAs: subpath  # The subdirectory type. Valid values include subpath and filesystem.
    volumeHandle: vke-nas-static-pv  # The unique identifier of the PV. Keep it consistent with the PV name. To use multiple PVs simultaneously, the value for each PV must be different.
  mountOptions:
  - nolock,proto=tcp,noresvport
  - vers=3  # The NFS version. 3: NFSv3. 4: NFSv4. 4.1: NFSv4.1.
  persistentVolumeReclaimPolicy: Retain  # The PV reclaim policy. "Retain" indicates a retain policy, and "Delete" indicates a delete policy.
  volumeMode: Filesystem  # The PV type. Filesystem: Uses the volume as a file system. When a volume is set to Filesystem, the pod mounts it to a directory. Block: Uses the volume as a block device.
```



</Tab>
</Tabs>


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 3: Create a PVC


<Tabs>
<Tab zoneid="OLLKoCRFER" title="Creating through the console">
<TabTitle>Creating through the console</TabTitle>

1. On the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. In the upper left corner of the PVC list, click **Create PersistentVolumeClaim**.

3. On the **Create PersistentVolumeClaim** page, configure the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Storage types include EBS, NAS, and TOS. In this scenario, select **NAS**. |
   |Access mode |Select a PVC access mode. Currently, you can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, pay\-as\-you\-go is supported. |
   |File system type |Select a file system type.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Capacity\-type file storage is currently in beta in both VKE and FileNAS. To use this feature, you must apply for a trial of both VKE and FileNAS.</div><br> |
   |how to create |Methods for creating a PVC include Create based on StorageClass and Use an existing PersistentVolume. For this example, select **Use an existing PersistentVolume**. |
   |PersistentVolume |This parameter must be configured if an existing PV is used. Select a FileNAS PV for binding. |
   

4. Click **Confirm**.


</Tab>
<Tab zoneid="uepgE54J9S" title="Configure resource quotas through YAML">
<TabTitle>Configure resource quotas through YAML</TabTitle>

The following sample code shows how to create a PVC by using YAML:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: vke-nas-static-pvc  # The name of the PVC.
spec:
  accessModes:
  - ReadWriteMany  # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
  resources:
    requests:
      storage: 100Gi  # Declared storage usage.
  volumeMode: Filesystem  # The PV type. In this example,  enter "Filesystem", which indicates file storage.
  volumeName: vke-nas-static-pv  # The name of the PV bound to this PVC.
```



</Tab>
</Tabs>


<span id=".5q2l6aqk5Zub77ya5Yib5bu65bqU55So5bm25re75Yqg5Y23"></span>
### Step 4: Create an application and add a volume

After the static PV of the FileNAS type is created, add the PV to a workload that will use the PV. Supported workloads include Deployments, Jobs, CronJobs, and DaemonSets.

You can add a PV to a workload when you create or update the workload. This topic provides an example of how to create a Deployment. For detailed operations, see [Creating Deployments](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment).

The following sample code shows how to create a Deployment by using YAML:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: vke-nas-static-deployment  # The name of the Deployment.
  namespace: default
  labels:
  app: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: vke-nas-static-deployment
  template:
    metadata:
      labels:
        app: vke-nas-static-deployment
    spec:
      containers:
      - image: nginx
        imagePullPolicy: IfNotPresent
        name: nginx
        volumeMounts:
        - mountPath: /tmp  # The location where the FileNAS storage is mounted.
          name: nas-pv
      volumes:
      - name: nas-pv
        persistentVolumeClaim:
          claimName: vke-nas-static-pvc  # The name of the PVC created in Step 2.
```


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

<span id=".6aqM6K-BLW5hcy3nmoTlhbHkuqvlrZjlgqg="></span>
### Verify FileNAS shared storage


1. Run the following command in kubectl to view the created application.

   ```bash
   kubectl get pod
   ```
   

   Expected output:

   ```bash
   NAME                                     READY   STATUS    RESTARTS   AGE
   web-5c4d7f****-8f9qx                     1/1     Running   0          2m53s
   web-5c4d7f****-brvch                     1/1     Running   0          2m53s
   web-5c4d7f****-xltnr                     1/1     Running   0          2m53s
   ```
   

2. Run the following command to view the files under the `/test` path.

   ```bash
   kubectl exec web-5c4d7f****-8f9qx ls /test
   ```
   

   Expected output:

   ```bash
   kubectl exec web-5c4d7f****-8f9qx ls /test
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>/test</code> path contains no files.   </div>
   

3. Run the following command to create a file named `nas` under the `/test` path.

   ```bash
   kubectl exec web-5c4d7f****-8f9qx touch /test/nas
   ```
   

4. Run the following command to view the files under the `/test` path.

   ```bash
   kubectl exec web-5c4d7f****-8f9qx ls /test
   ```
   

   Expected output:

   ```bash
   nas
   ```
   

5. Run the following command to view the files under the `/test` path on other pods.

   ```bash
   kubectl exec web-5c4d7f****-brvch ls /test
   ```
   

   Expected output:

   ```bash
   nas
   ```
   

6. A file created under the `/test` path of any pod exists under the `/test` path of both pods, which indicates that the two pods share the same FileNAS.


<span id=".6aqM6K-BLW5hcy3lrZjlgqjmjIHkuYXljJY="></span>
### Verify FileNAS persistence storage


1. Run the following command to delete all pods of the application.

   ```bash
   kubectl delete pod web-5c4d7f****-8f9qx web-5c4d7f****-brvch web-5c4d7f****-xltnr
   ```
   

   Expected output:

   ```bash
   pod "web-5c4d7f****-8f9qx" deleted
   pod "web-5c4d7f****-brvch" deleted
   pod "web-5c4d7f****-xltnr" deleted
   ```
   

2. Run the following command to view the names of pods recreated by Kubernetes.

   ```bash
   kubectl get pod
   ```
   

   Expected output:

   ```bash
   NAME                                     READY   STATUS    RESTARTS   AGE
   web-5c4d7f****-8l78w                     1/1     Running   0          53s
   web-5c4d7f****-r5282                     1/1     Running   0          53s
   web-5c4d7f****-vbswz                     1/1     Running   0          53s
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can see that the pod is automatically recreated and its name is different from the original.   </div>
   

3. Run the following command to view the files under the recreated `Pod/test` path.

   ```bash
   kubectl exec web-5c4d7f****-8l78w ls /test
   ```
   

   Expected output:

   ```bash
   nas
   ```
   

4. Run the following command to view the files under another `Pod/test` path.

   ```bash
   kubectl exec web-5c4d7f****-vbswz ls /test
   ```
   

   Expected output:

   ```bash
   nas
   ```
   

5. The created file `nas` is not deleted when the pod is deleted, which indicates that FileNAS data can be persistently stored.
