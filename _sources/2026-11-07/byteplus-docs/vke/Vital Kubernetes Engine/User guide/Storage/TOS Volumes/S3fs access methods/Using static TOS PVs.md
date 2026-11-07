---
title: "Using static TOS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-static-TOS-Volumes"
---

This topic describes how to create a static PersistentVolume (PV) and PersistentVolumeClaim (PVC) based on Torch Object Storage (TOS), and how a workload uses the PV.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-tos add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A bucket has been created. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* A valid key has been created in the target namespace.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits

StatefulSets require exclusive access to a volume, and do not support a manually created PVC.

<span id=".6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Creating through the console

<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select Static creation. |
   |Name |Specify a name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **TOS**. |
   |Access type |Select an access type for the PV. In this scenario, select **S3FS**.<br><br><br>* **FSX**: A unified file access client for unstructured data storage. It supports standard POSIX semantics.<br><br>* **S3FS**: A FUSE\-based file system that allows S3\-compatible object storage services to be used as a local file system through mounting.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">FSX\-based access currently supports only Elastic Compute Service (ECS). It does not support VCI.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">FSX\-based access delivers better performance and higher availability, and will gradually replace S3fs. For a detailed description, see <a href="https://docs.byteplus.com/en/docs/vke/Description_of_the_TOS_CSI_capability_upgrade">Upgrading CSI for TOS</a>.</div><br> |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Access key |Select a key for accessing TOS. VKE uses this specified key to access TOS.<br><br>If no access key is available, click **Create key** and configure the key name, associated namespace, and the AK and SK of the account. |
   |Storage bucket |Choose an existing TOS bucket. |
   |Subdirectory |Specify the bucket subdirectory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend an existing directory. If you specify a directory that does not exist, it is automatically created.</div><br> |
   

5. Click **Confirm**.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 2: Create a PVC


1. On the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. In the upper left corner of the PVC list, click **Create PersistentVolumeClaim**.

3. On the **Create PersistentVolumeClaim** page, configure the parameters. Note that you should select **TOS** for StorageClass type.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **TOS**. |
   |Access mode |Select a PVC access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, only Pay\-as\-you\-go is supported. |
   |PersistentVolume |Select the created PV for mounting. |
   

4. Click **Confirm**.


<span id=".5q2l6aqk5Zub77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Add the PV to a workload

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Creating through kubectl

<span id=".5YeG5aSH5bel5L2c"></span>
### Preparation


* Install the kubectl tool locally. For details, see [Installing and configuring kubectl](https://kubernetes.io/docs/tasks/tools/).

* Connect to the target cluster. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXNlY3JldA=="></span>
### Step 1: Create a Secret


1. Create a YAML file for the Secret. The following `vke-tos-secret.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: Secret
   metadata:
     name: tos-key # Secret name. If the cluster version is 1.26.x, the name cannot contain the . character. Other cluster versions do not have this limit.
     namespace: default # Namespace of the Secret.
   type: Opaque # Secret type. In this example, select it to Opaque to store arbitrary key-value pairs.
   data:
     akId: ${AK} # The Base64-encoded account AK. Replace the value with your actual information.
     akSecret: ${AK} # The Base64-encoded SK that matches with the AK. Replace the value with your actual information.
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <code>echo -n "${ak}" | base64</code> command to perform Base64 encoding on items such as the AK and SK. Note that you need to replace <code>${ak}</code> with your actual value. For example, if <code>${ak}</code> is <code>demo</code>, the encoding command is <code>echo -n "demo" | base64</code>, which produces the encoded result <code>ZGVtbw==</code>.   </div>
   

2. Run the following command to create the Secret.

   ```Bash
   kubectl create -f vke-tos-secret.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXB2"></span>
### Step 2: Create a PV


1. Create a YAML file for the PV. The following `vke-tos-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-tos-static-pv  # PV name.
     namespace: default # Namespace to which the PV belongs.
   spec:
     capacity:
       storage: 20Gi   # Declared PV capacity. This field is required by Kubernetes. The value has no actual meaning and is only for validation.
     accessModes:  # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     - ReadWriteMany
     csi:
       driver: tos.csi.volcengine.com # Driver required for storage mount.
       nodePublishSecretRef:
         name: tos-key # Secret name.
         namespace: default # Namespace where the configured Secret resides.
       nodeStageSecretRef:    # Starting from csi-tos v0.2.2, the NodeStageSecretRef parameter is required. Its content is the same as nodePublishSecretRef. Additionally, v0.2.2 is compatible only with existing PVs identified by volumeHandle or name. v0.2.3 is compatible with all existing PVs.
         name: tos-key # Secret name.
         namespace: default # Namespace where the configured Secret resides.
       volumeAttributes:
         bucket: vke-tos # The name of the created TOS bucket.
         path: /tmp # Specify the root directory of the TOS bucket. Make sure that the directory exists. Otherwise, the mount will fail.
         url: http://tos-s3-cn-beijing.ivolces.com # The domain name of the created TOS bucket.
         fuse_pod_cpu_request: "100m" # Fuse Pod CPU requests. It defaults to 100m.
         fuse_pod_cpu_limit: "2" # Fuse Pod CPU limit. It defaults to 6.
         fuse_pod_memory_request: 100Mi # Fuse Pod memory requests. It defaults to 200Mi.
         fuse_pod_memory_limit: "2Gi" # Fuse Pod memory limit. It defaults to 6Gi.
         additional_args: -oparallel_count=20 -oallow_other    # S3FS mount parameters. For details, see the S3FS help documentation. Starting from csi-tos v0.2.8, -oparallel_count=20 is added by default.
         dbglevel: err # S3FS log level. The default is err.
       volumeHandle: vke-tos-static-pv  # The unique identifier of the PV. Keep it consistent with the PV name. volumeHandle should uniquely correspond to <url>:<bucket><path>. Do not map the same volumeHandle to different <url>:<bucket><path> items. Otherwise, this may result in unexpected mounting.
     persistentVolumeReclaimPolicy: Retain # The reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |storage |Declared PV capacity. Unit: Gi. This is a required field in Kubernetes. However, the capacity value set here does not limit the actual usage by the application. The actual capacity depends only on the TOS capacity. |
   |driver |The driver for mounting a PV. In this example, you need to set the value to tos.csi.volcengine.com, which indicates the csi\-tos add\-on. |
   |nodePublishSecretRef |TOS bucket authentication configuration, including the created Secret name and namespace. |
   |nodeStageSecretRef |TOS bucket authentication configuration, including the created Secret name and namespace.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the csi\-tos add\-on is v0.2.2 or later, you need to configure this parameter and set its content to the same as that of <code>nodePublishSecretRef</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The csi\-tos v0.2.2 is only compatible with existing PVs using a volumeHandle and PV name. Version 0.2.3 and later are compatible with all existing PVs.</div><br> |
   |bucket |The name of the created TOS bucket. |
   |path |Specify the root directory of the TOS bucket. Ensure that the directory exists. Otherwise, the mount will fail. |
   |url |The domain name of the created TOS bucket.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can view the domain name of the created TOS bucket in the TOS console. For details, see <a href="https://docs.byteplus.com/en/docs/tos/docs-exporting-bucket-information">Viewing bucket information</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the VKE cluster and TOS bucket are deployed in the same region, we recommend <strong>using a private domain name for access</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the VKE cluster and TOS bucket are deployed in different regions, you can <strong>use a public domain name for access</strong>. In this case, make sure that the public access feature is enabled for the VKE cluster.</div><br> |
   |fuse_pod_cpu_request |Fuse Pod CPU requests. It defaults to 100m. |
   |fuse_pod_cpu_limit |Fuse Pod CPU limit. It defaults to 6. |
   |fuse_pod_memory_request |Fuse Pod memory requests. It defaults to 200Mi. |
   |fuse_pod_memory_limit |Fuse Pod memory limit. It defaults to 6Gi. |
   |additional_args |The mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. For details, see the [S3FS documentation](https://manpages.org/s3fs). |
   |dbglevel |S3FS log level. The default is err. |
   |volumeHandle |Keep the value consistent with the PV name. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-tos-static-pv.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LXB2Yw=="></span>
### Step 3: Create a PVC


1. Create a YAML file for the PVC. The following `vke-tos-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-tos-static-pvc  # The name of the PVC.
     namespace: default # Namespace of the PVC.
   spec:
     accessModes:  # PV access mode. You can select only ReadWriteMany, which allows read-write access by multiple nodes. Keep it consistent with that in the PV configuration.
     - ReadWriteMany
     resources:
       requests:
         storage: 20Gi  # Declared storage usage. The unit is Gi. Ensure it is consistent with the capacity of the created PV.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the PV as a filesystem) and Block (using the PV as a block device). The value must be consistent with the type configured in the PV.
     volumeName: vke-tos-static-pv  # The name of the created PV.
   
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. Keep it consistent with that in the PV configuration. |
   |storage |The declared storage capacity. Unit: Gi. It must be consistent with the capacity of the created PV. |
   |volumeMode |The PV type. It must be consistent with the type configured for the PV. The following information is included:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the volume as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   |volumeName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-tos-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                 STATUS   VOLUME              CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-tos-static-pvc   Bound    vke-tos-static-pv    20Gi       RWX                          2m36s         
   ```
   


<span id=".5q2l6aqk5Zub77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 4: Create an application and mount the PV


1. Create a YAML file for the Deployment. The following `vke-tos-static-deployment.yaml` file serves as an example:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To use Vital Container Instance (VCI), you need to add <code>vke.volcengine.com/burst-to-vci: enforce</code> to <code>spec.template.metadata.annotations</code>. VCI offers advantages including fully managed maintenance\-free operation, pay\-as\-you\-go pricing, and secure sandboxed container isolation. For details, see <a href="https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance">What is VCI?</a>   </div>
   

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vke-static-tos-deploy
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: vke-static-tos-deploy
     template:
       metadata:
         labels:
           app: vke-static-tos-deploy
       spec:
         containers:
         - image: nginx
           imagePullPolicy: IfNotPresent
           name: nginx
           volumeMounts:
           - mountPath: /tmp # The mount location of the PV in the container.
             name: tos-pv # The PV name, which must be consistent with the value of the volumes.name field.
         volumes:
         - name: tos-pv # The PV name. You can specify a custom name.
           persistentVolumeClaim:
             claimName: vke-tos-static-pvc  # Name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-tos-static-deployment.yaml
   ```
   


<span id="UqWLPmRl"></span>
## Validating results

After you create a workload and mount it to a PV as described in the preceding steps, verify whether the TOS volume is mounted and whether shared storage and persistent storage are achieved by using the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-static-tos-deploy-5f55*** -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   /dev/vdc        20466256      24  20449848   1% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-static-tos-deploy-5f55*** -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Log in to the [TOS console ](https://console.byteplus.com/tos). Upload a file to the specified path. For details, see [Uploading files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

4. View the PV mount path in the pod again.

   ```Bash
   kubectl exec vke-static-tos-deploy-5f55*** -- ls /tmp
   ```
   

   The expected response is as follows. You can see the uploaded file, which indicates that the data volume is mounted and persistent storage is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id="y3tbRlUD"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
