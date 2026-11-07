---
title: "Using static CloudFS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-static-CFS-Volumes"
---

Cloud File System (abbreviated as CloudFS) is a file storage and acceleration service designed for big data and machine learning. It supports standard Hadoop Distributed File System (HDFS) access and transparent data lake access, providing you with low\-cost, high\-performance, high\-throughput, and highly available big data file access.

Vital Kubernetes Engine (VKE) supports CloudFS storage through the Container Storage Interface (CSI). This topic describes how to create CloudFS PersistentVolumes (PVs) and PersistentVolumeClaims (PVCs), and how workloads can use static CloudFS PVs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: This feature is currently in the beta stage. Submit an application if you need to use it.[Beta \- apply for trial]</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-cloudfs add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A CloudFS instance for data lakes has already been created. .

* A TOS bucket has been created. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* (Optional) To use the kubectl command line tool, ensure that kubectl is installed locally. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Currently, VKE supports only data lake access of CloudFS, not file storage access.


<span id=".5pa55byP5LiA77ya6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LiA77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane of the cluster management page, click **Storage \> PersistentVolume**. Click **Create PersistentVolume** and complete the PersistentVolume configuration.

   
   |**Parameter** |**Description** |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select **Static creation**. |
   |Name |Specify a name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **CloudFS**. |
   |Access mode |Select a PV access mode. You can select only **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Application scenarios |Select an application scenario of CloudFS. Currently, only the **Data lake scenario** is supported. |
   |File system |Choose an existing CloudFS resource to store frequently accessed data and enable intelligent dynamic updates. |
   |TOS |Select the TOS bucket associated with the file system for data storage. |
   

4. Click **Confirm**.


<span id="llAWTZAv"></span>
### Step 2: Create a PVC


1. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. Click **Create PersistentVolumeClaim** to configure a PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **CloudFS**. |
   |Access mode |PVC access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |The billing method for resources. Only **pay\-as\-you\-go** is supported. |
   |PersistentVolume |Select the created CloudFS PV for mounting. |
   

3. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".5pa55byP5LqM77ya6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

If you have completed [cluster connection](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can configure static CloudFS PVs via kubectl.

<span id="SA8ozwvZ"></span>
### Step 1: Create a PV


1. Create a YAML file for the PV. The following `vke-cfs-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: cfs-static-pv # PV name.
     labels:
       cloudfs-name: cfs-static-fs
   spec:
     capacity:
       storage: 10Pi  # The PV capacity. This field is required by Kubernetes only for validation. It does not impose an actual capacity limit.
     accessModes: 
       - ReadWriteMany # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     csi:
       driver: cfs.csi.volcengine.com # The driver required for storage mounting. In this example, it is set to cfs.csi.volcengine.com, which indicates the cloudfs add-on.
       fsType: cloudfs
       volumeAttributes:
          cloudfsConf/cfs.filesystem.fs-mode: ACC # Application scenarios. Values include ACC (for data lake scenarios) and HDFS ( for file storage scenarios). Currently, only ACC is supported.
          cloudfsConf/cfs.filesystem.ns-id: "540431955***" # Instance list. You can obtain this namespace ID from TOS.
          cloudfsConf/cfs.filesystem.ufs-path: tos://tos-doc-demo/   # The namespace mount path in the format tos://<TOS bucket name>/<TOS prefix>/. If the TOS prefix is empty, all objects in the bucket are included.
          cloudfsConf/cfs.filesystem.uri: cfs://demo.cfs-cn-shanghai.cfs.ivolces.com   # The mount address of the CloudFS instance.
          cloudfsConf/cfs.client.network.segment: "192.168.2.0/24" # The subnet segment where the CloudFS instance is located.
       volumeHandle: cfs-static-pv # The unique identifier of the PV. Keep it consistent with the PV name.
     persistentVolumeReclaimPolicy: Retain # PV reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem # The PV type. Value: Filesystem (using the volume as a filesystem. It will be mounted by the pod to a directory) or Block (using the volume as a block device).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |storage |Declared PV capacity. Unit: Gi. This field is required by Kubernetes. The value has no actual meaning and is only for validation. The actual capacity is subject to the created storage capacity. |
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |driver |The driver for mounting a PV. In this example, you need to set the value to nas.csi.volcengine.com, which indicates the cloudfs add\-on. |
   |fsType |PV type. In this example, set it to cloudfs. |
   |cloudfsConf/cfs.filesystem.fs\-mode |CloudFS application scenarios include:<br><br><br>* **ACC**: Data lake scenarios.<br><br>* **HDFS**: File storage scenarios.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Currently, only ACC is supported.</div><br> |
   |cloudfsConf/cfs.filesystem.ns\-id |A list of instances. The namespace ID can be obtained from TOS. |
   |cloudfsConf/cfs.filesystem.ufs\-path |The namespace mount path in the format `tos://<TOS bucket name>/<TOS prefix>/`. If the TOS prefix is empty, all objects in the bucket are included. |
   |cloudfsConf/cfs.filesystem.uri |The mount address of the CloudFS instance. You can obtain it from the CloudFS instance details page. |
   |cloudfsConf/cfs.client.network.segment |The subnet segment where the CloudFS instance is located. |
   |persistentVolumeReclaimPolicy |The PV reclaim policy. The following information is included:<br><br><br>* **Retain**: The Retain policy. When the PVC bound to the PV is deleted, the PV is retained.<br><br>* **Delete**: The Delete policy. When the PVC bound to the PV is deleted, the PV is deleted synchronously. |
   |volumeMode |The PV types. Valid values:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the PV as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-cfs-static-pv.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `vke-cfs-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: cfs-static-pvc # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes:
       - ReadWriteMany # PV access mode. Only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     resources:
       requests:
         storage: 10Pi # Declared storage usage. Ensure it is consistent with the capacity of the created PV. This field is required by Kubernetes.
     volumeName: cfs-static-pv  # Name of the created PV.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. |
   |storage |The declared storage capacity. It must be consistent with the capacity of the created PV. |
   |volumeName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-cfs-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                 STATUS   VOLUME              CAPACITY   ACCESS MODES   STORAGECLASS  AGE
   vke-cfs-static-pvc   Bound    vke-cfs-static-pv   10Pi       RWX                          2m36s
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 3: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `deployment-nginx-static.yaml` file serves as an example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">csi\-cloudfs provides mount\-level fault recovery capabilities. If the Mount Pod fails (causing a restart or recreation), application containers can still continue operating. To achieve this, in the <code>volumeMounts</code> of your application Pod, set <code>mountPropagation</code> to <strong>HostToContainer</strong> or <strong>Bidirectional</strong>. This propagates the storage mount of the host node to the Pod, enabling mount\-level fault recovery. For more information, see <a href="https://kubernetes.io/zh-cn/docs/concepts/storage/volumes/#mount-propagation">Volume propagation</a>.   </div>
   

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
           - name: cloudfs-pv
             mountPath: /tmp  # The location where CloudFS is mounted in the container.
             mountPropagation: HostToContainer # The propagation of the mounted volume. Valid values include None, HostToContainer, and Bidirectional.
         volumes:
           - name: cloudfs-pv
             persistentVolumeClaim:
               claimName: cfs-static-pvc # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl apply -f deployment-nginx-static.yaml
   ```
   


<span id="6AXthDmr"></span>
## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec deployment-nginx-static-xxx -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   demo.cfs-***.cfs.ivolces.com:/ 10995116277760       0 10995116277760   0% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec deployment-nginx-static-xxx -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Write a file to the PV.

   ```Bash
   kubectl exec deployment-nginx-static-xxx -- touch /tmp/test
   ```
   

4. Delete the pod.

   ```Bash
   kubectl delete pod deployment-nginx-static-xxx
   ```
   

5. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec deployment-nginx-static-xxx -- ls /tmp
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id="8Ag8VieY"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
