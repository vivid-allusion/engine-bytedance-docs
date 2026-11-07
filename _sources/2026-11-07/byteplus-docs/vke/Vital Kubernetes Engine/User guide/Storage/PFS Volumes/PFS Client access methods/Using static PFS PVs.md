---
title: "Using static PFS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-static-PFS-volumes"
---

VKE supports the use of PFS through Container Storage Interface (CSI). This topic describes how to create a PersistentVolume (PV) and PersistentVolumeClaim (PVC) based on PFS and how workloads use statically provisioned PFS PVs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]<strong>: The static PFS PV </strong>and the <strong>Intelligent Computing edition</strong> are in the beta stage. Submit an application if you need to use these features.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-vepfs add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A PFS filesystem and mount service have been created, and the mount service has been bound to the filesystem. For details, see [Creating a filesystem](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system), [Creating a mount service](https://docs.byteplus.com/en/docs/pfs/Creating-a-mount-service), and [Binding filesystems](https://docs.byteplus.com/en/docs/pfs/Binding-a-file-system).

* (Optional) The kubectl tool has been installed locally. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

When you use PFS, take note of the following limitations or impacts related to deployment compatibility, add\-on uninstallation, service mounting, and operational performance.

<span id=".6YOo572y5YW85a655oCn55u45YWz6ZmQ5Yi2"></span>
### Restrictions on deployment compatibility


* One PFS mount service cannot be used for both the PFS CSI solution and the solution where PFS is pre\-mounted to the host at the same time. For a PFS file system instance, if you have used a VKE node to pre\-mount PFS and supplied it to pods through hostpath, you need to create an additional PFS mount service and configure the new PFS mount service for use by PFS CSI.

* You can use PFS file storage through either CSI or the PFS\-manager add\-on, but not both. We recommend using the CSI solution for new clusters. To apply the latest CSI solution to existing resources, [submit a ticket](https://console.byteplus.com/workorder/create) to the technical support.

* PFS CSI controller will be preferentially scheduled to nodes that have the label `vepfs.csi.volcengine.com/controller=preferred`. If you plan to frequently scale the VKE cluster node pool, we recommend preferentially scheduling the CSI controller to resident nodes (not affected by scaling). This ensures vePFS CSI can process member consistency between the VKE cluster and the vePFS cluster more quickly. Otherwise, when nodes running the PFS CSI controller are scaled in and deleted, the PFS CSI controller may be unable to maintain member consistency between the VKE cluster and the PFS cluster, resulting in slow PFS CSI operations.

* Nodes that have already been added to the PFS cluster through the Virtual Private Cloud (VPC) network will not be able to use the RDMA network. To switch to the RDMA network, remove the VKE node from the PFS file system cluster.


<span id=".57uE5Lu25Y246L2955u45YWz6ZmQ5Yi2"></span>
### Restrictions on add\-on uninstallation


* If the csi\-vepfs add\-on is uninstalled, running pods can continue to access PFS storage until they finish running. However, if csi\-vepfs has already been uninstalled, pod deletion is blocked, and the pods can then be successfully deleted after csi\-vepfs is reinstalled. Therefore, we do not recommend that you uninstall the csi\-vepfs add\-on when pods are running.

* csi\-vepfs enables the file system client to run in a dedicated container, and the PFS client will occupy the computing resources of the Kubernetes node where the container is located. By default, the client uses 4 CPUs and 4 GiB of memory. If node resources are insufficient, both the csi\-vepfs client container and the pod will fail to start.

* If you delete the PFS mount service in advance, the PFS CSI add\-on cannot be uninstalled.

* After you delete the PFS CSI add\-on, you cannot confirm whether some resources can be deleted, which may result in residual resources.

   * **PFS mount service secret**: When you create a PFS PV, VKE will also create a Secret that stores the addresses and login keys of the three management nodes of the PFS mount service. You can run the following command to query the preceding Secret in the VKE cluster.

   ```Bash
   kubectl get -n kube-system secrets | grep "^vepfs-secret-mount-[0-9a-z]*"
   ```
   

   * **Security groups on the VKE node**: To ensure that the VKE node can communicate with the PFS file system cluster, PFS CSI will also add the security group of the management service ECS instance to the security group list of the VKE node. However, when CSI is being uninstalled, whether the security group is still being used by the user cannot be confirmed. Therefore, you cannot unbind the security group from the VKE node. You can view or delete the security group bound to the ECS node to which the PFS mount service belongs in the ECS console.


<span id=".5pyN5Yqh5oyC6L2955u45YWz6ZmQ5Yi2"></span>
### Restrictions on service mounting


* A single PFS instance can be bound to multiple mount services. A single mount service can also be bound to multiple PFS instances.

* A single ECS instance can be added to only one PFS mount service, which is equivalent to a client cluster. One mount service can be bound to multiple file system storage instances.

* A node can be bound to only one mount service. We recommend binding one PFS mount service to a VKE cluster.

* PFS does not support the use of images of Ubuntu and veLinux CentOS Compatible Edition. 


<span id=".6L-Q6KGM5oCn6IO955u45YWz6ZmQ5Yi2"></span>
### Restrictions on operational performance


* The initial startup of a container that uses PFS on a node is approximately 15 seconds slower than subsequent startups. This is because PFS CSI needs to compile the kernel driver for PFS on the node. This process consumes more time. However, this situation only occurs when a container that uses a PFS PV is created for the first time.


<span id=".5pa55byP5LiA77ya6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolume**. Click **Create PersistentVolume** to configure a PV.

   
   |Parameter |Description |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select **Static creation**. |
   |Name |Specify a name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Access type |Select an access type for the PV. In this scenario, select **PFS Client**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Instance type |Select the file system specifications for creating a PV. Performance metrics vary based on different specifications. For more information about product specifications, see [Product specifications](https://docs.byteplus.com/en/docs/pfs/Product-specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: The Intelligent Computing edition is currently in beta. To use it, submit an application.</div><br> |
   |Project |Assign the StorageClass to a project so that you can perform operations such as maintenance and authorization at the project level. By default, the **default** project is selected.  |
   |File system |Sequentially select the created PFS file system, mount service, and security group, and then configure the advanced settings of the mount service based on your business requirements. |
   ||**Mount service**: Select the mount service bound to the file system based on your business requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only mount services in the running state are supported, which need to be in the <strong>same VPC as the cluster</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The PFS mount service will occupy 2 GiB of resources on the mount node. Ensure the proper planning of cluster resources.</div><br> |
   ||**Advanced configurations**: Configure advanced settings related to the mount service. You can view and specify the following parameters.<br><br><br>* Reserved memory: The reserved memory of the PFS mount service occupies 2 GiB of resources on the mount node and cannot be modified.<br><br>* Access key: The default generated secret. This key stores the initial password for PFS client node access. If the initial password has been changed, replace it with the corresponding node password.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the password is incorrect, PFS will fail to be mounted. Make sure that the password is correct.</div><br> |
   |Security group |Select the security group of the mount service client based on your business requirements. The security group will be automatically added to the main NIC of the user node through cross\-service authorization. This adds the user node to the mount service cluster and connects the user cluster to the PFS server. |
   

4. Click **Confirm**.


<span id="i9eLfwtE"></span>
### Step 2: Create a PVC


1. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolumeClaim**. Click **Create PersistentVolumeClaim** to configure a PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, only **Pay\-as\-you\-go** is supported. |
   |How to create |The method of creating a PVC. Available methods **include Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Use an existing PersistentVolume**. |
   |PersistentVolume |Specify the PFS PV. |
   

2. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the static PV of the PFS type is created, add the PV to a workload that will use the PV. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".5pa55byP5LqM77ya6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

If you [connect to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can use a static PFS PV by using kubectl.

<span id=".5q2l6aqk5LiA77ya6L-e5o6l6Ym05p2D"></span>
### Step 1: Configure connection authentication

Run the following commands in sequence to store the SSH connection authentication information of the PFS management node in a Secret.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The addresses, passwords, and hostnames in the following example are for demonstration purposes only. Replace them with actual configurations based on your business requirements.</div>


```Bash
echo -n '[
    {
        "address":"192.168.1.210",
        "password":"bK8C8B5@4T6x9***",
        "hostname":"client-mount-demo-1"
    },
    {
        "address":"192.168.1.209",
        "password":"bK8C8B5@4T6x9***",
        "hostname":"client-mount-demo-2"
    },
    {
        "address":"192.168.1.208",
        "password":"bK8C8B5@4T6x9***",
        "hostname":"client-mount-demo-3"
    }
]' > /tmp/vepfs-hots.json


kubectl create secret generic pfs-secret --namespace kube-system --from-file=vepfsHosts=/tmp/vepfs-hots.json
```


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 2: Create a PV


1. Create a YAML document for the PV. The following `vke-pfs-static-pv.yaml` file serves as an example: You can mount the entire file system or a file system subdirectory based on your business requirements.

   
   <Tabs>
   <Tab zoneid="GB0zDYucR7" title="Mounting the entire file system">
   <TabTitle>Mounting the entire file system</TabTitle>
   
   The following YAML example demonstrates how to mount the entire PFS filesystem:
   
   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pfs-static-pv # PV name. The name must be unique within the cluster.
     namespace: default
     annotations:
       pv.kubernetes.io/provisioned-by: vepfs.csi.volcengine.com
   spec:
     accessModes: 
       - ReadWriteMany # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     capacity:
       storage: 20Gi # Declared PV capacity. This field is required by Kubernetes only for validation. It does not impose an actual capacity limit.
     csi:
       driver: vepfs.csi.volcengine.com # Driver required for storage mount.
       readOnly: false
       nodeStageSecretRef: # The name of the Secret that stores authentication information. The authentication information in the Secret must be consistent with that of the mount service.
         name: pfs-secret # Secret name.
         namespace: kube-system # The namespace of the Secret.
       controllerPublishSecretRef:
         name: pfs-secret
         namespace: kube-system
       volumeAttributes:
         fsid: vepfs-cnsh67*** # Filesystem ID.
         hpcClusterID: vepfs-cluster-id-*** # The ID of the HPC cluster. Binding to an HPC cluster is required only when the Intelligent Computing edition is used.
         mountServiceID: mount-6de0*** # Mount service ID.
         securityGroupID: sg-3679xag6w*** # Security group for mount point clients.
         mountpoint: /vepfs-cnsh67*** # Mount point specified for binding the mount service to the filesystem.
       volumeHandle: vepfs-cnsh67***  # The unique identifier of the PV. Keep it consistent with fsid.
     persistentVolumeReclaimPolicy: Retain # PV reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem # PV type. Value: Filesystem (using the volume as a filesystem. It will be mounted by the pod to a directory) or Block (using the volume as a block device).
   ```
   
   
   
   </Tab>
   <Tab zoneid="yzp14osFfi" title="Mounting a subdirectory of the filesystem">
   <TabTitle>Mounting a subdirectory of the filesystem</TabTitle>
   
   The YAML example for mounting a PFS file system subdirectory is as follows:
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   
   * <div data-tips="true" data-tips-type="warning">You can mount PFS file system subdirectories only when you statically create a PFS PV by using YAML.</div>
   
   
   * <div data-tips="true" data-tips-type="warning">When you create a PV, you need to use a created PFS file system subdirectory. Otherwise, volume cannot be mounted during pod creation.</div>
   
   
   
   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pfs-static-pv # PV name. The name must be unique within the cluster.
     namespace: default
     annotations:
       pv.kubernetes.io/provisioned-by: vepfs.csi.volcengine.com
   spec:
     volumeMode: Filesystem
     accessModes:   # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
       - ReadWriteMany
     capacity:
       storage: 20Gi  # Declared PV capacity. This field is required by Kubernetes only for validation. It does not impose an actual capacity limit.
     persistentVolumeReclaimPolicy: Retain # PV reclaim policy. Value: Retain or Delete.
     csi:
       driver: vepfs.csi.volcengine.com  # The driver required for volume mounting. In this example, set the value to vepfs.csi.volcengine.com, which indicates the csi-vepfs add-on.
       readOnly: false
       nodeStageSecretRef: # The Secret corresponding to the PFS mount service.
         name: pfs-secret
         namespace: kube-system
       controllerPublishSecretRef:
         name: pfs-secret
         namespace: kube-system
       volumeAttributes:
         fsid: vepfs-cnbjexxxxac6e7b3  # Filesystem ID.
         hpcClusterID: vepfs-cluster-id-xxx # The ID of the HPC cluster. You need to bind an HPC cluster only when fsid uses the Intelligent Computing edition.
         mountServiceID: mount-ff0b**** # Mount service.
         securityGroupID: msadgh-14332 # Security group for PFS mount point clients.
         mountpoint: /vepfs-cnbjexxxxac6e7b3 # The mount point, which corresponds to the ID of the filesystem.
         subpath: /l1.dir1/l2.dir1 # The subdirectory of the filesystem for mounting. You need to use a created PFS filesystem subdirectory.
       volumeHandle: vepfs-cnbjexxxxac6e7b3 # Filesystem ID.
   ```
   
   
   
   </Tab>
   </Tabs>
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |storage |Declared PV capacity. Unit: Gi. This field is required by Kubernetes. The value has no actual meaning and is only for validation. |
   |driver |The driver for mounting a PV. In this example, you need to set the value to vepfs.csi.volcengine.com, which indicates the csi\-vepfs add\-on. |
   |nodeStageSecretRef |The name and namespace of the Secret for authentication. The authentication information in the Secret must be consistent with that of the mount service. |
   |controllerPublishSecretRef |The name and namespace of the Secret for authentication. The authentication information in the Secret must be consistent with that of the mount service. |
   |fsid |The ID of the filesystem.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view the ID of the created filesystem in the console. For details, see <a href="https://docs.byteplus.com/en/docs/pfs/Viewing-file-system-details">Viewing filesystem details</a>.</div><br> |
   |hpcClusterID |ID of the HPC cluster. Binding to an HPC cluster is required only when the Intelligent Computing edition is used. |
   |mountServiceID |The ID of the mount service. |
   |securityGroupID |The security group for mount point clients. |
   |mountpoint |The mount point specified for binding the mount service to the filesystem. For details, see [Binding a filesystem](https://docs.byteplus.com/en/docs/pfs/Binding-a-file-system). |
   |volumeHandle |The unique identifier of the PV. Keep it consistent with the name of the PV. |
   |persistentVolumeReclaimPolicy |The PV reclaim policy. The following information is included:<br><br><br>* **Retain**: The Retain policy. When the PVC bound to the PV is deleted, the PV is retained.<br><br>* **Delete**: The Delete policy. When the PVC bound to the PV is deleted, the PV is deleted synchronously. |
   |volumeMode |The PV type. The following information is included:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the PV as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-vepfs-static-pv.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 3: Create a PVC


1. Create a YAML file for the PVC. The following `vke-pfs-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pfs-static-pvc # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes:
       - ReadWriteMany # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     resources:
       requests:
         storage: 20Gi # Declared PV capacity. This field is required by Kubernetes only for validation. It does not impose an actual capacity limit.
     volumeMode: Filesystem  # The PV type. Valid values: Filesystem (using the PV as a filesystem) and Block (using the PV as a block device). The value must be consistent with the type configured in the PV.
     volumeName: pfs-static-pv # Name of the created PV.
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
   kubectl create -f vke-pfs-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                   STATUS   VOLUME                 CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-pfs-static-pvc     Bound    vke-pfs-static-pv      10Pi       RWX                           2m36s
   ```
   


<span id=".5q2l6aqk5Zub77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 4: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `deployment-nginx-static.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-nginx-static
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
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 # Specify the image file to be deployed.
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
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When a workload is being created, a dedicated container for mounting the PFS client is started first on the node. The PFS client will occupy the computing resources of the Kubernetes node where the container is located. By default, the client uses 4 CPUs and 4 GiB of memory. If node resources are insufficient, both the csi\-vepfs client container and the pod will fail to start.   </div>
   

   <span id="5o76ywoa"></span>
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
   

   <span id="E1CZaEVd"></span>
   ## Related documentation

* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
