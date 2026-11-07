---
title: "Using static FileNAS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-static-NAS-Volumes"
---

This topic describes how to create a static PersistentVolume (PV) and PersistentVolumeClaim (PVC) based on FileNAS storage, and how a workload uses the PV.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-nas add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A FileNAS filesystem and mount point have been created. 

* (Optional) The kubectl tool has already been installed locally, and the target cluster has been connected by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

StatefulSets require exclusive access to a volume and do not currently support manually created PVCs.

<span id=".6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LiA77ya55m75b2V6ZuG576k566h55CG6aG16Z2i"></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**. Click **Create PersistentVolume** to configure a PV.

   
   |**Parameter** |**Description** |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select **Static creation**, in which the administrator creates one. |
   |Name |Specify a valid name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **FileNAS**. |
   |Access type |Select an access type for the PV. In this scenario, select **NFS**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |File system type |Select a file system type.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br>* **Cache type**: [Beta] This type is applicable to scenarios where workloads use high\-speed filesystem interfaces for data access, such as machine learning and high\-performance computing (HPC).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache\-type FileNAS storage supported by VKE is a beta feature that does not require additional permissions for use. On the FileNAS side, cache\-type storage is a beta feature that requires a trial application. To use this type of file system, you need to request permission to use FileNAS.</div><br> |
   |Project |Assign the PV to a project so that you can perform operations such as maintenance and authorization at the project level. By default, the **default** project is selected. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Mount point |Select a mount point that exists under an existing FileNAS file system and is in the same VPC as the cluster. |
   |Subdirectory |Enter a valid subdirectory that complies with the on\-screen rules. The default directory is the root directory, which is represented by `/`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Ensure that the subdirectory already exists in the NFS file system.</div><br> |
   |NFS version |Select an NFS version for the PV.<br><br><br>* If you select **Extreme speed** for **File system type**, only **NFSv3** is supported.<br><br>* If you select **Capacity type** for **File system type**, only **NFSv3** is supported.<br><br>* If you select **Cache type** for **File system type**, only **NFSv4.1** is supported. |
   |**Advanced settings** ||
   |Mount parameters |Configure PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. For details, see [PV mount parameters](https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters). |
   

4. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 2: Create a PVC


1. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolumeClaim**. Click **Create PersistentVolumeClaim** to configure a PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **FileNAS**. |
   |Access mode |Select a PVC access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, Pay\-as\-you\-go is supported. |
   |File system type |Select the same file system type as the one configured for the PV.<br><br><br>* **Extreme speed**: This type is applicable to latency\-sensitive Linux applications, for example, AI for small and medium\-sized scenarios, file sharing, and DevOps code storage.<br><br>* **Capacity type**: This type is applicable to storage of frequently accessed data, for example, database backups, log storage, primary directories, and other general file sharing services.<br><br>* **Cache type**: [Beta] This type is applicable to scenarios where workloads use high\-speed filesystem interfaces for data access, such as machine learning and high\-performance computing (HPC).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cache\-type FileNAS storage supported by VKE is a beta feature that does not require additional permissions for use. On the FileNAS side, cache\-type storage is a beta feature that requires a trial application. To use this type of file system, you need to request permission to use FileNAS.</div><br> |
   |How to create |The method of creating the PVC. Available methods include **Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Use an existing PersistentVolume**. |
   |PersistentVolume |Select the created FileNAS PV. |
   

2. Click **Confirm**.


<span id=".5q2l6aqk5Zub77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXB2"></span>
### Step 1: Create a PV


1. Create a YAML file for the PV. The following `vke-nas-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-nas-static-pv # PV name.
   spec:
     accessModes: 
     - ReadWriteMany # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     capacity:
       storage: 100Gi # Declared volume capacity. This field is only for validation, and does not actually impose a capacity limit.
     csi:
       driver: nas.csi.volcengine.com # The driver required for volume mounting. In this example, set the value to nas.csi.volcengine.com, which indicates the csi-nas add-on.
       volumeAttributes:
         fsType: Extreme  # Filesystem type. Value: Extreme, Cache, and Capacity.
         fsId: enas-cnsha0*** # The ID of the FileNAS file system. This parameter is required only if fsType is set to Extreme. For other file system types, it must be left empty or omitted.
         server: cnsha0d51***.vpc-3qda7du***.nas.ivolces.com # The domain of the FileNAS filesystem mount point.
         volumeAs: subpath # Subdirectory type. Value: subpath.
         path: /temp  # The subdirectory of the filesystem to be mounted. It defaults to the root directory ("/").
       volumeHandle: vke-nas-static-pv # The unique identifier of the PV. Keep it consistent with the PV name.
     mountOptions: # The mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted.
     - nolock,proto=tcp,noresvport
     - vers=3  # The NFS protocol version number for mounting PVs. Valid values include 3 and 4.1. The value 3 indicates NFSv3, which is applicable to the Extreme speed and Capacity types. The value 4.1 indicates NFSv4.1, which is the only version supported by the Cache type.
     persistentVolumeReclaimPolicy: Retain  # PV reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem # The volume type. Value: Filesystem (using the volume as a filesystem. It will be mounted by the pod to a directory) or Block (using the volume as a block device).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |storage |Declared PV capacity. Unit: Gi. This field is required by Kubernetes. The value has no actual meaning and is only for validation. The actual capacity is subject to the created storage capacity. |
   |driver |The driver for mounting a PV. In this example, you need to set the value to nas.csi.volcengine.com, which indicates the csi\-nas add\-on. |
   |fsType |# NFS filesystem type. Available values include Extreme, Cache, and Capacity.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For a description of NFS filesystem types, see <a href="https://docs.byteplus.com/en/docs/nas/What-is-FileNAS">Product overview</a>.</div><br> |
   |fsId |The ID of the created NFS filesystem.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view the ID of the created filesystem in the console.</div><br> |
   |server |The domain of the FileNAS filesystem mount point. |
   |path |The subdirectory of the filesystem to be mounted. It defaults to the root directory ("/"). Ensure that the specified directory exists. Otherwise, the mount will fail. |
   |volumeAs |Specify the subdirectory type of NFS storage. Values: subpath. |
   |volumeHandle |The unique identifier of the PV. Keep it consistent with the name of the PV. |
   |mountOptions |Configure PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. You can use the `vers` parameter to specify the NFS version number for mounting the PV. Valid values:<br><br><br>* **3**: Indicates NFSv3, which applies to the Extreme speed and Capacity.<br><br>* **4.1**: Indicates NFSv4.1, which applies only to the Cache type. |
   |persistentVolumeReclaimPolicy |The PV reclaim policy. The following information is included:<br><br><br>* **Retain**: The Retain policy. When the PVC bound to the PV is deleted, the PV is retained.<br><br>* **Delete**: The Delete policy. When the PVC bound to the PV is deleted, the PV is deleted synchronously. |
   |volumeMode |The volume type. The following information is included:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the PV as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-nas-static-pv.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXB2Yw=="></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `vke-nas-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-nas-static-pvc # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes:
     - ReadWriteMany # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     resources:
       requests:
         storage: 100Gi # Declared storage usage. The unit is Gi. Ensure it is consistent with the capacity of the created PV.
     volumeMode: Filesystem  # The PV type. Valid values: Filesystem (using the PV as a filesystem) and Block (using the PV as a block device). The value must be consistent with the type configured in the PV.
     volumeName: vke-nas-static-pv # Name of the created PV.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. |
   |storage |The declared storage capacity. Unit: Gi. It must be consistent with the capacity of the created PV. |
   |volumeMode |The PV type. It must be consistent with the type configured for the PV. The following information is included:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the volume as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   |volumeName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-nas-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                 STATUS   VOLUME                CAPACITY   ACCESS MODES   STORAGECLASS  
   vke-nas-static-pvc   Bound    vke-nas-static-pv     100Gi      RWX                        
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 3: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `vke-nas-static-deployment.yaml` file is an example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use Vital Container Instance (VCI), you need to add <code>vke.volcengine.com/burst-to-vci: enforce</code> to <code>spec.template.metadata.annotations</code>. VCI offers advantages including fully managed maintenance\-free operation, pay\-as\-you\-go pricing, and secure sandboxed container isolation. For details, see <a href="https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance">What is VCI?</a>   </div>
   

   ```YAML
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
         - image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           name: nginx
           volumeMounts:
           - mountPath: /tmp  # The location where the FileNAS storage is mounted in the container.
             name: nas-pv
         volumes:
         - name: nas-pv
           persistentVolumeClaim:
             claimName: vke-nas-static-pvc  # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-nas-static-deployment.yaml 
   ```
   


<span id="95giBWjq"></span>
## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   cnshbb5***.3qda7du***.nas.ivolces.com:/temp 10995116277760       0 10995116277760   0% /tmp
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
   


<span id="V3TI5wqm"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
