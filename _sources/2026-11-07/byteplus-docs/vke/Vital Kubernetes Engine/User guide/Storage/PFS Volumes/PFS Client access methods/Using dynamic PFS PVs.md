---
title: "Using dynamic PFS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-dynamic-PFS-volumes"
---

Vital Kubernetes Engine (VKE) allows you to use PFS through the Container Storage Interface (CSI). This topic describes how to create vePFS PersistentVolumes (PVs) and PersistentVolumeClaims (PVCs) and how workloads use dynamic vePFS PVs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>[</strong><a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a><strong>]: Dynamic PFS PV provisioning</strong> and the <strong>Intelligent Computing edition</strong> are in the beta stage. Submit an application if you need to use these features.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-vepfs add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A PFS filesystem and mount service have been created, and the mount service has been bound to the filesystem. For details, see [Creating a filesystem](https://docs.byteplus.com/en/docs/pfs/Creating-a-file-system), [Creating a mount service](https://docs.byteplus.com/en/docs/pfs/Creating-a-mount-service), and [Binding filesystems](https://docs.byteplus.com/en/docs/pfs/Binding-a-file-system).

* (Optional) The kubectl tool has been installed locally. For detailed steps, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

When you use PFS, take note of the following limitations or impacts related to deployment compatibility, add\-on uninstallation, service mounting, and operational performance.

<span id=".6YOo572y5YW85a655oCn55u45YWz6ZmQ5Yi2"></span>
### Restrictions on deployment compatibility


* One PFS mount service cannot be used for both the PFS CSI solution and the solution where PFS is pre\-mounted to the host at the same time. For a PFS file system instance, if you have used a VKE node to pre\-mount PFS and supplied it to pods through hostpath, you need to create an additional PFS mount service and configure the new PFS mount service for use by PFS CSI.

* You can use PFS file storage through either CSI or the PFS\-manager add\-on, but not both. We recommend using the CSI solution for new clusters. To apply the latest CSI solution to existing resources, [submit a ticket](https://console.byteplus.com/workorder/create) to the technical support.

* PFS CSI controller will be preferentially scheduled to nodes that have the label `vepfs.csi.volcengine.com/controller=preferred`. To frequently scale the VKE cluster node pool, we recommend that you preferentially schedule the CSI controller to resident nodes, which are not affected by scaling. This ensures that PFS CSI can quickly process member consistency between the VKE cluster and the PFS cluster. Otherwise, when nodes running the PFS CSI controller are scaled in and deleted, the PFS CSI controller may be unable to maintain member consistency between the VKE cluster and the PFS cluster, resulting in slow PFS CSI operations.

* Nodes that have already been added to the PFS cluster through the Virtual Private Cloud (VPC) network will not be able to use the RDMA network. To switch to the RDMA network, remove the VKE node from the PFS file system cluster.


<span id=".57uE5Lu25Y246L2955u45YWz6ZmQ5Yi2"></span>
### Restrictions on add\-on uninstallation


* If the csi\-vepfs add\-on is uninstalled, running pods can continue to access PFS storage until they finish running. However, if csi\-vepfs has already been uninstalled, pod deletion will be blocked, and the pods can be deleted again after csi\-vepfs is reinstalled. Therefore, we do not recommend that you uninstall the csi\-vepfs add\-on when pods are running.

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

* A node can be bound to only one mount service. Therefore, we recommend that you bind one VKE cluster to one PFS mount service.

* StorageClasses dynamically provision PVs by using filesets. Therefore, the number of PVs varies based on different types of filesets. For details, see [Considerations on Fileset](https://docs.byteplus.com/en/docs/pfs/Managing-fileset).

* PFS does not support the use of images of Ubuntu and veLinux CentOS Compatible Edition.


<span id=".6L-Q6KGM5oCn6IO955u45YWz6ZmQ5Yi2"></span>
### Restrictions on operational performance


* The creation of dynamic PVs in a PFS filesystem runs in serial mode. If multiple dynamic PVs are created simultaneously, the total creation time will be longer.

* The initial startup of a container that uses PFS on a node is approximately 15 seconds slower than subsequent startups. This is because PFS CSI needs to compile the kernel driver for PFS on the node. This process consumes more time. However, this situation only occurs when a container that uses a PFS PV is created for the first time.


<span id=".5pa55byP5LiA77ya6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a2Y5YKo57G7"></span>
### Step 1: Create an SC


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolume**. Click **Create PersistentVolume** to configure a PV.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify a name for the StorageClass. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Availability zone |Availability Zones (AZs) are physically isolated infrastructure units within a single region, featuring independent power and networking systems. AZs communicate with each other over internal networks. |
   |Billing type |Select a resource billing type as needed. Currently, pay\-as\-you\-go is supported. |
   |Instance type |Select the file system specifications for creating a PV. Performance metrics vary based on different specifications. For more information about product specifications, see [Product specifications](https://docs.byteplus.com/en/docs/pfs/Product-specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: The Intelligent Computing edition is currently in beta. To use it, submit an application.</div><br> |
   |Project |Assign the StorageClass to a project so that you can perform operations such as maintenance and authorization at the project level. By default, the **default** project is selected.  |
   |File system |Sequentially select the created PFS file system, mount service, and security group, and then configure the advanced settings of the mount service based on your business requirements. |
   ||**Mount service**: Select the mount service bound to the file system based on your business requirements.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">You can select a mount service only in the <code>running</code> state and <strong>in the same VPC as the cluster</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The PFS mount service will occupy 2 GiB of resources on the mount node. Ensure the proper planning of cluster resources.</div><br> |
   ||**Advanced configurations**: Configure advanced settings related to the mount service. You can view and specify the following parameters.<br><br><br>* Reserved memory: The reserved memory of the PFS mount service occupies 2 GiB of resources on the mount node and cannot be modified.<br><br>* Access key: The default generated secret. This key stores the initial password for PFS client node access. If the initial password has been changed, replace it with the corresponding node password.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the password is incorrect, PFS will fail to be mounted. Make sure that the password is correct.</div><br> |
   ||**Security group**: Select the security group of the mount service client based on your business requirements. The security group will be automatically added to the main NIC of the user node through cross\-service authorization. This adds the user node to the mount service cluster and connects the user cluster to the PFS server. |
   |Fileset |Configure the required fileset quotas based on your business requirements. This prevents a single fileset from occupying excessive resources, including file quota, bandwidth QoS, and IOPS QoS.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The file quota cannot exceed the upper limit of iNode.</div><br> |
   |Reclaim policy |The reclaim policy. Available options include:<br><br><br>* **Delete**: When you delete the PVC, the data, the backend storage fileset of the PV, and the PV itself will be immediately deleted.<br><br>* **Retain**: When you delete the PVC, the data, the backend storage fileset of the PV, and the PV itself remain intact. You need to manually delete them.<br><br><br><div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div><br><br><br><br>* <div data-tips="true" data-tips-type="danger">The deleted data cannot be restored. Proceed with prudence when selecting the <strong>Delete</strong> policy.</div><br><br><br>* <div data-tips="true" data-tips-type="danger">We recommend that you select Retain to prevent accidental data deletions.</div><br> |
   |PersistentVolume binding mode |The binding mode. The following information is included:<br><br><br>* **Immediate**: Performs PV binding and allocation when the PVC is created.<br><br>* **WaitForFirstConsumer**: Delays PV binding and allocation until a pod that uses the PVC is created. |
   

4. Click **Confirm**.


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y235aOw5piO"></span>
### Step 2: Create a PVC


1. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolumeClaim**. Click **Create PersistentVolumeClaim** to configure a PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, only **Pay\-as\-you\-go** is supported. |
   |How to create |The method of creating a PVC. Available methods include **Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Create based on StorageClass**. |
   |StorageClass |Select an appropriate StorageClass based on your business requirements. When you create an application, it will be automatically bound to a PV that uses the same StorageClass and has a capacity no less than that specified in the PVC. |
   |Capacity |The declared storage usage. |
   

2. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the dynamic PV of the PFS type is created, add the PV to a workload that will use the PV. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When a workload is being created, a dedicated container for mounting the PFS client is started first on the node. The PFS client will occupy the computing resources of the Kubernetes node where the container is located. By default, the client uses 4 CPUs and 4 GiB of memory. If node resources are insufficient, both the csi\-vepfs client container and the pod will fail to start.</div>


<span id=".5pa55byP5LqM77ya6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

If you [connect to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can use a dynamic PFS PV by using kubectl.

<span id="pAD6LZAA"></span>
### Step 1: Configure connection authentication

Run the following commands in sequence to store the SSH connection authentication information of the PFS management node in a Secret.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The addresses, passwords, and hostnames in the following example are for demonstration purposes only. Replace them with actual configurations based on your business requirements.</div>


```Bash
echo -n '[
    {
        "address":"192.168.1.210",
        "password":"bK8C8B5@4T6***",
        "hostname":"client-mount-demo-1"
    },
    {
        "address":"192.168.1.209",
        "password":"bK8C8B5@4T6x***",
        "hostname":"client-mount-demo-2"
    },
    {
        "address":"192.168.1.208",
        "password":"bK8C8B5@4T6x***",
        "hostname":"client-mount-demo-3"
    }
]' > /tmp/vepfs-hots.json


kubectl create secret generic pfs-secret --namespace kube-system --from-file=vepfsHosts=/tmp/vepfs-hots.json
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you have created a PV of type PFS via the console, VKE will synchronously create a Secret that stores the addresses and login credentials of the management nodes for the mount service. You can specify a custom Secret name by using the <code>adminHostsSecretName</code> parameter, or check whether the Secret exists in the cluster by running the <code>kubectl get -n kube-system secrets | grep "^vepfs-secret-mount-[0-9a-z]*"</code> command.</div>


<span id="f8KQT4NW"></span>
### Step 2: Create a StorageClass


1. Create a YAML file for the SC. The following `vke-pfs-sc.yaml` file serves as an example:

   ```YAML
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: vke-pfs-sc  # StorageClass name.
   provisioner: vepfs.csi.volcengine.com # # The driver that the storage mount depends on.
   parameters:
     fsid: vepfs-cnsh672***  # Filesystem ID.
     mountServiceID: mount-6de0***  # Mount service ID.
     fileLimit: "100000" # Fileset file quota.
     maxIOPS: "20" # Fileset IOPS QoS limit.
     maxBandwidth: "30" # Fileset bandwidth QoS limit measured in MB/s.
     mountpoint: /vepfs-cnsh672*** # Mount point specified for binding the mount service to the filesystem.
     securityGroupID: sg-3679xag6w*** # Security group for mount point clients.
     adminHostsSecretName: pfs-secret # Secret name.
     adminHostsSecretNamespace: kube-system # Namespace where the Secret resides.
   reclaimPolicy: Delete # PV reclaim policy. Value: Retain or Delete.
   volumeBindingMode: Immediate # Volume binding mode. Values include Immediate (indicating immediate binding and allocation) and WaitForFirstConsumer (indicating delayed binding and allocation).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |provisioner |The driver for mounting a PV. In this example, you need to set the value to vepfs.csi.volcengine.com, which indicates the csi\-vepfs add\-on. |
   |fsid |The ID of the filesystem.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view the ID of the created filesystem in the console. For details, see <a href="https://docs.byteplus.com/en/docs/pfs/Viewing-file-system-details">Viewing filesystem details</a>.</div><br> |
   |mountServiceID |The ID of the mount service. |
   |fileLimit |Configure the fileset file quota. For details, see [Configuring Fileset quota and QoS settings](https://docs.byteplus.com/en/docs/pfs/Managing-fileset-quota). |
   |maxIOPS |Configure a fileset IOPS QoS limit. For details, see [Configuring Fileset quota and QoS settings](https://docs.byteplus.com/en/docs/pfs/Managing-fileset-quota). |
   |maxBandwidth |Configure a fileset bandwidth QoS limit (measured in MB/s). For details, see [Configuring Fileset quota and QoS settings](https://docs.byteplus.com/en/docs/pfs/Managing-fileset-quota). |
   |mountpoint |The mount point specified for binding the mount service to the filesystem. For details, see [Binding a filesystem](https://docs.byteplus.com/en/docs/pfs/Binding-a-file-system). |
   |securityGroupID |The security group for mount point clients. |
   |adminHostsSecretName |The name of the Secret that stores authentication information. The authentication information in the Secret must be consistent with that of the mount service. |
   |adminHostsSecretNamespace |The namespace of the Secret for authentication. The authentication information in the Secret must be consistent with that of the mount service. |
   |reclaimPolicy |The PV reclaim policy. Valid values:<br><br><br>* **Delete**: When you delete the PVC, the PV and the data in the PV will be simultaneously deleted.<br><br>* **Retain**: When you delete the PVC, the PV and the data in the PV will not be simultaneously deleted. You need to manually delete them.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">We recommend that you select <strong>Retain</strong> to prevent accidental data deletions.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The deleted data cannot be restored. Proceed with prudence when selecting the <strong>Delete</strong> policy.</div><br> |
   |volumeBindingMode |The binding mode of the PV. Values:<br><br><br>* **Immediate**: Performs PV binding and allocation when the PVC is created.<br><br>* **WaitForFirstConsumer**: Delays PV binding and allocation until a pod that uses the PVC is created. |
   

2. Run the following command to create the StorageClass.

   ```Bash
   kubectl create -f vke-pfs-sc.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXB2Yw=="></span>
### Step 3: Create a PVC


1. Create a YAML file for the PVC. The following `vke-pfs-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: csi-pfs-pvc # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes:
     - ReadWriteMany # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     resources:
       requests:
         storage: 20Gi   # Declared storage usage.
     storageClassName: vke-pfs-sc # StorageClass name.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. |
   |storage |The declared storage capacity. Unit: Gi. It must be consistent with the capacity of the created PV. |
   |storageClassName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-pfs-pvc.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 4: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `deployment-nginx-dynamic.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-nginx-dynamic
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
               claimName: csi-pfs-pvc # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f deployment-nginx-dynamic.yaml
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When a workload is being created, a dedicated container for mounting the PFS client is started first on the node. The PFS client will occupy the computing resources of the Kubernetes node where the container is located. By default, the client uses 4 CPUs and 4 GiB of memory. If node resources are insufficient, both the csi\-vepfs client container and the pod will fail to start.   </div>
   

   <span id="W05dKt5f"></span>
   ## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV dynamically provisioned based on the PVC has been created and bound to the PVC.

   ```Bash
   kubectl get pvc
   ```
   

   The expected result is as follows:

   ```Bash
   NAME             STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS   
   csi-pfs-pvc      Pending  pvc-6e8c646b-e3e9-4d02-836e-3b66********   20Gi       RWX            vke-pfs-sc      
   ```
   

2. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-efs-static-deployment-xxx -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   fs_vepfs-cnsh67*** 6442450944 27478016 6414972928   1% /tmp
   ```
   

3. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

4. Write a file to the PV.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- touch /tmp/test
   ```
   

5. Delete the pod.

   ```Bash
   kubectl delete pod vke-nas-static-deployment-xxx
   ```
   

6. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec vke-nas-static-deployment-xxx -- ls /tmp
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id="fIY3etE7"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
