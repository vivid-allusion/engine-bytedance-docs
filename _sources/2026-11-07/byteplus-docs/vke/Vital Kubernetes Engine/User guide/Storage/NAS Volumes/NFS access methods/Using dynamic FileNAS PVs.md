---
title: "Using dynamic FileNAS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-dynamic-NAS-Volumes"
---

This topic describes how to create a dynamic PersistentVolume (PV) and PersistentVolumeClaim (PVC) based on FileNAS storage, and how a workload uses the PV.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-nas add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A FileNAS file system and mount point have been created. 

* (Optional) The kubectl tool has already been installed locally, and the target cluster has been connected by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

StatefulSets require exclusive access to a volume and do not currently support manually created PVCs.

<span id=".6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo57G777yIc3RvcmFnZWNsYXNz77yJ"></span>
### Step 1: Create an SC


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> StorageClass**.

4. Click **Create StorageClass** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify a name for the StorageClass. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **FileNAS**. |
   |Availability zone |Availability Zones (AZs) are physically isolated infrastructure units within a single region, featuring independent power and networking systems. AZs communicate with each other over internal networks. |
   |Billing type |Select a resource billing type as needed. Currently, pay\-as\-you\-go is supported. |
   |File system type |Choose a file system type.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br>* **Cache type**: [Beta] This type is applicable to scenarios where workloads use high\-speed filesystem interfaces for data access, such as machine learning and high\-performance computing (HPC).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache\-type FileNAS storage supported by VKE is a beta feature that does not require additional permissions for use. On the FileNAS side, cache\-type storage is a beta feature that requires a trial application. To use this type of file system, you need to request permission to use FileNAS.</div><br> |
   |Project |Assign the StorageClass to a project so that you can perform operations such as maintenance and authorization at the project level. By default, the **default** project is selected.  |
   |Mount point |Select an existing mount point in the FileNAS file system. |
   |Subdirectory |Enter a valid subdirectory that complies with the on\-screen rules. By default, the root directory (`/`) is used.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Ensure that the subdirectory already exists in FileNAS.</div><br> |
   |NFS version |Select an NFS version for the PV.<br><br><br>* If the file system type is Extreme speed, only the **NFSv3** version is supported.<br><br>* If the file system type is Capacity, only the **NFSv3** version is supported.<br><br>* If the file system type is Cache, only the **NFSv4.1** version is supported. |
   |Reclaim policy |The reclaim policy. Available options include:<br><br><br>* **Delete**: When you delete the PVC, the specified **Delete policy** applies.<br><br>   * When the **Delete policy** is set to **Delayed deletion**, the PV and FileNAS data will be archived and will not be permanently deleted.<br><br>   * When **Delete policy** is set to **Delete now**, the PV and FileNAS data will be actually deleted.<br><br>* **Retain**: When you delete the PVC, the PV and FileNAS data will not be deleted. If necessary, you can manually delete them.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend that you select Retain to prevent accidental data deletions.</div><br> |
   |PersistentVolume binding mode |The binding mode. The following information is included:<br><br><br>* **Immediate**: Performs PV binding and allocation when the PVC is created.<br><br>* **WaitForFirstConsumer**: Delays PV binding and allocation until a pod that uses the PVC is created. |
   

5. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 2: Create a PVC


1. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. Click **Create PersistentVolumeClaim** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **FileNAS**. |
   |Access mode |Select a PVC access mode. Currently, you can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, pay\-as\-you\-go is supported. |
   |File system type |Select the same file system type as the one configured in the StorageClass.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br>* **Cache type**: [Beta] This type is applicable to scenarios where workloads use high\-speed filesystem interfaces for data access, such as machine learning and high\-performance computing (HPC).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache\-type FileNAS storage supported by VKE is a beta feature that does not require additional permissions for use. On the FileNAS side, cache\-type storage is a beta feature that requires a trial application. To use this type of file system, you need to request permission to use FileNAS.</div><br> |
   |How to create |The method of creating a PVC. Available methods include **Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Create based on StorageClass**. |
   |StorageClass |Select a StorageClass. The system automatically binds a PV that has the same StorageClass and a capacity greater than or equal to the capacity size defined in the PVC. |
   |Capacity |Configure the capacity of the PV.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This is a required field in Kubernetes. However, the capacity value set here does not limit the actual usage by the application. The actual capacity depends only on the filesystem capacity.</div><br> |
   

3. Click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the system dynamically creates a PV according to the resource declaration in the PVC, it will create a subdirectory at the associated FileNAS mount point. Subsequently, when a pod uses the PV, it will mount the subdirectory.   </div>
   

<span id=".5q2l6aqk5Zub77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXN0b3JhZ2VjbGFzcw=="></span>
### Step 1: Create an SC


1. Create a YAML file for the SC. The following `vke-nas-sc.yaml` file serves as an example:

   ```YAML
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: vke-nas-sc # StorageClass name.
   provisioner: nas.csi.volcengine.com  # (Required) The driver required for volume mounting. In this example, set the value to nas.csi.volcengine.com, which indicates the csi-nas add-on.
   parameters:
     fsType: Extreme # (Required) Filesystem type. Value: Extreme, Cache, and Capacity.
     fsId: enas-cnbj1b9f32****** # (Optional) The ID of the FileNAS filesystem. This parameter is required only if fsType is set to Extreme. For other file system types, it must be left empty or omitted.
     volumeAs: subpath  # (Required) Subdirectory type. Value: subpath.
     server: cnshbb***.3qda7dut***.nas.ivolces.com  # (Required) The domain of the FileNAS file system mount point when you create a PV as a subdirectory.
     subPath: /tmp  # (Required) The subdirectory of the subpath-type FileNAS system after the mount operation. The csi-nas add-on creates directories in the subdirectory as the back-end storage of the dynamic PV.
     archiveOnDelete: "true" # (Required) Whether to enable the delayed deletion policy. Valid values include true and false. true indicates that the PV and FileNAS data will be archived and not deleted. false indicates that the PV and FileNAS data will be deleted.
   mountOptions:
   - nolock,proto=tcp,noresvport
   - vers=3   # Protocol version for mounting the data volume. Valid values include 3 and 4.1. The value 3 indicates NFSv3, which is applicable to the Extreme speed and Capacity types. The value 4.1 indicates NFSv4.1, which is the only version supported by the Cache type.
   reclaimPolicy: Delete  # PV reclaim policy. Value: Retain or Delete.
   volumeBindingMode: Immediate # Volume binding mode. Values include Immediate (indicating immediate binding and allocation) and WaitForFirstConsumer (indicating delayed binding and allocation).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |provisioner |The driver for mounting a PV. In this example, you need to set the value to nas.csi.volcengine.com, which indicates the csi\-nas add\-on. |
   |archiveOnDelete |Whether to synchronously delete PVs when the PVC is deleted. Valid values include:<br><br><br>* **true**: Delayed PV deletion. When the PVC is deleted, the FileNAS data will not be deleted synchronously.<br><br>* **false**: Immediate deletion. When the PVC is deleted, the FileNAS data will be deleted synchronously. |
   |fsId |The ID of the created NFS filesystem.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view the ID of the created filesystem in the console.</div><br> |
   |fsType |NFS filesystem type. Available values include Extreme, Cache, and Capacity.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For a description of NFS filesystem types, see <a href="https://docs.byteplus.com/en/docs/nas/What-is-FileNAS">Product overview</a>.</div><br> |
   |volumeAs |Specify the subdirectory type for NFS storage, including: subpath. |
   |server |The domain of the FileNAS filesystem mount point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When <code>volumeAs</code> is set to <code>subpath</code> (creating a subdirectory in an existing filesystem), this field is required.</div><br> |
   |subpath |The subdirectory after FileNAS mounting. The system will create directories within this subdirectory as the backend storage for dynamically provisioned volumes. |
   |volumeHandle |The unique identifier of the PV. Keep it consistent with the name of the PV. |
   |mountOptions |Configure PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. You can use the `vers` parameter to specify the NFS version number for mounting the PV. Valid values:<br><br><br>* **3**: Indicates NFSv3, which applies to the Extreme speed and Capacity.<br><br>* **4.1**: Indicates NFSv4.1, which applies only to the Cache type. |
   |reclaimPolicy |The PV reclaim policy. Valid values:<br><br><br>* **Delete**: When you delete the PVC, the PV and the data in the PV will be simultaneously deleted.<br><br>* **Retain**: When you delete the PVC, the PV and the data in the PV will not be simultaneously deleted. You need to manually delete them.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend that you select <strong>Retain</strong> to prevent accidental data deletions.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Under the <strong>Delete</strong> policy, deleted data cannot be restored. Proceed with prudence when selecting the Delete policy.</div><br> |
   |volumeBindingMode |The binding mode of the PV. Values:<br><br><br>* **Immediate**: Performs PV binding and allocation when the PVC is created.<br><br>* **WaitForFirstConsumer**: Delays PV binding and allocation until a pod that uses the PVC is created. |
   

2. Run the following command to create the StorageClass.

   ```Bash
   kubectl create -f vke-nas-sc.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXB2Yw=="></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `vke-nas-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-nas-pvc # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes: # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     - ReadWriteMany
     resources:
       requests:
         storage: 100Gi # The declared storage capacity. Unit: Gi.
     storageClassName: vke-nas-sc # StorageClass name.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. |
   |storage |The declared storage capacity. Unit: Gi. |
   |storageClassName |The name of the created SC. |
   |volumeMode |The PV types. Valid values:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the volume as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-nas-pvc.yaml
   ```
   

3. Run the following command to check whether the dynamic volume declared by the PVC has been created.

   ```Bash
   kubectl get pvc
   ```
   

   The expected result is as follows:

   ```Bash
   NAME          STATUS   VOLUME                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-nas-pvc   Bound    pvc-6318***-3d355a768220   100Gi      RWX            vke-nas-sc     5s  
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 3: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `vke-dynamic-nas-deployment.yaml` file serves as an example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use Vital Container Instance (VCI), you need to add <code>vke.volcengine.com/burst-to-vci: enforce</code> to <code>spec.template.metadata.annotations</code>. VCI offers advantages including fully managed maintenance\-free operation, pay\-as\-you\-go pricing, and secure sandboxed container isolation. For a detailed introduction, see <a href="https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance">What is VCI?</a>   </div>
   

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: dynamic-nas-deploy
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: dynamic-nas-deploy
     template:
       metadata:
         labels:
           app: dynamic-nas-deploy
       spec:
         containers:
         - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           name: nginx
           volumeMounts:
           - mountPath: /tmp # The location where the FileNAS storage is mounted in the container.
             name: nas-pv
         volumes:
         - name: nas-pv
           persistentVolumeClaim:
             claimName: vke-nas-pvc  # The name of the created PVC.
   
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-dynamic-nas-deployment.yaml
   ```
   


<span id="2jKazYuL"></span>
## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec dynamic-nas-deploy-5fcd*** -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   cnshb***.3qda7dut***.nas.ivolces.com:/tmp/pvc-6318d*** 10995116277760       0 10995116277760   0% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec dynamic-nas-deploy-5fcd*** -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Write a file to the PV.

   ```Bash
   kubectl exec dynamic-nas-deploy-5fcd*** -- touch /tmp/test
   ```
   

4. Delete the pod.

   ```Bash
   kubectl delete pod dynamic-nas-deploy-5fcd***
   ```
   

5. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec dynamic-nas-deploy-5fcd*** -- ls /tmp
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id="N9lDRPkU"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
