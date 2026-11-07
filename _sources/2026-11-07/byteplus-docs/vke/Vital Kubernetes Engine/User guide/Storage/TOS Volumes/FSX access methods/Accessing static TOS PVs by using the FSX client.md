---
title: "Accessing static TOS PVs by using the FSX client"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client"
---

FSX is a client used to access the high\-availability POSIX\-compliant file system of TOS. Through this client, TOS buckets can be mounted to a Linux system, enabling the buckets to function as a local Linux file system for data storage and management. This topic introduces how to use static TOS PersistentVolumes (PVs) through the FSX client.

<span id="2oLDeysQ"></span>
## Prerequisites


* The csi\-fsx and fsx\-service add\-ons have been installed and upgraded to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* A TOS bucket has been created. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* The PV mount authentication configuration has been completed. For details, see [FSX authentication methods](https://docs.byteplus.com/en/docs/vke/FSX_authentication_method).

   * AK/SK authentication: You have created the AK/SK, which will be used to mount TOS storage. To use a temporary token for authentication, you need to implement the logic for refreshing tokens.

   * IRSA authentication: IRSA authentication for the csi\-fsx add\-on has been enabled. For details, see [Using IRSA to implement authentication for storage mounting](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx).

* (Optional) If you perform configuration by using YAML, make sure that the kubectl tool has been installed in the local environment and is connected to the target cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="6JPALjjM"></span>
## Usage limits


* StatefulSets require exclusive access to a volume, and do not support a manually created PVC.

* The FSX client currently supports only the x86_64 architecture. The client is currently not available on Windows and macOS. For details about supported environments, see [Supported environments](https://docs.byteplus.com/en/docs/tos/Overview).

* This feature is unavailable in clusters running on Kubernetes v1.20 and earlier.

* If you use clusters running on Kubernetes v1.26.x, you cannot use Secrets whose names contain periods (`.`). Otherwise, the PV will fail to be created.


<span id="KEVJ4ZxG"></span>
## Creating through the console

<span id="z2edeapu"></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** to create a TOS PV with the FSX access type.

   
   |**Parameter** |**Description** |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select Static creation. |
   |Name |Specify a name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **TOS**. |
   |Access type |Select an access type for the PV. In this scenario, select **FSX**.<br><br><br>* **FSX**: A unified file access client for unstructured data storage. It supports standard POSIX semantics.<br><br>* **S3FS**: A FUSE\-based file system that allows S3\-compatible object storage services to be used as a local file system through mounting.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">FSX\-based access currently supports only Elastic Compute Service (ECS). It does not support VCI.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">FSX\-based access delivers better performance and higher availability, and will gradually replace S3fs. For a detailed description, see <a href="https://docs.byteplus.com/en/docs/vke/Description_of_the_TOS_CSI_capability_upgrade">Upgrading CSI for TOS</a>.</div><br> |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Access key |Select a TOS access key.<br><br><br>* When IRSA authentication is enabled for the csi\-fsx add\-on in the cluster (for details, see [Use IRSA to implement authentication for mounting storage](https://docs.byteplus.com/en/docs/vke/Create_an_IAM_role_and_bind_it_to_csi-fsx)), the access key is not required.<br><br>   * When this parameter is empty, the IAM role associated with the csi\-fsx add\-on is used for authentication.<br><br>   * After this parameter is provided, the authentication priority follows this order: PV\-level Secret (if available) \> addon\-level IRSA (if available). If neither is available, authentication will fail.<br><br>* When IRSA authentication is not enabled for the csi\-fsx add\-on in the cluster, the access key is required.<br><br>   * Use the access key specified here to authorize VKE to access TOS.<br><br>   * If no access key is available, click **Create key** and configure the key name, associated namespace, and the AK and SK of the IAM user.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you use clusters running on Kubernetes v1.26.x, you cannot use Secrets whose names contain dots (<code>.</code>). Otherwise, the PV will fail to be created.</div><br> |
   |Service\-side encryption |Select **Enable** to enable server\-side encryption for the TOS PV. This allows encryption and decryption during data writing or reading. For details, see [Encrypting data for TOS PVs](https://docs.byteplus.com/en/docs/vke/Encrypting_data_for_TOS_PVs). |
   |Storage bucket |Select a created TOS bucket in TOS. |
   |Subdirectory |Specify the bucket subdirectory.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend an existing directory. If you specify a directory that does not exist, it is automatically created.</div><br> |
   |**Advanced settings** ||
   |Mount parameters |TOS PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. For details, see [PV mount parameters](https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters). |
   

5. Click **Confirm**.


<span id="3yuD837I"></span>
### Step 2: Create a PVC


1. Click the name of the target cluster. On the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. On the page that appears, click **Create PersistentVolumeClaim** to configure a TOS PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **TOS**. |
   |Access mode |Select a PVC access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, only Pay\-as\-you\-go is supported. |
   |PersistentVolume |Select the PV created in the previous step. |
   

3. Click **Confirm**.


<span id="smy9QntC"></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id="yDTvU7Kr"></span>
## Creating through kubectl

If you [connect to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can use a static TOS PV by using kubectl.

<span id="LiTpvCwa"></span>
### Step 1: (Optional) Create a policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use the AK and SK of the root user, you can skip this step.</div>


* <div data-tips="true" data-tips-type="tip">To dynamically refresh temporary tokens, see the AssumeRole API document.</div>



For the steps of creating a policy, see Creating custom policies. An Identity and Access Management (IAM) user must have the required permissions to mount a bucket. For a list of required permissions, see [Permissions required for mounting a bucket](https://docs.byteplus.com/en/docs/tos/FSX-configuration-and-mounting#b5294119).

The following is a JSON example for creating a TOS policy:

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:Get*",
        "tos:ListBucket",
        "tos:Put*",
        "tos:Head*",
        "tos:DeleteObject",
        "tos:AbortMultipartUpload"
      ],
      "Resource": [
        "trn:tos:::<TOS bucket name>",
        "trn:tos:::<TOS bucket name>/*"
      ]
    }
  ]
}
```


<span id="Lu9dVHd2"></span>
### Step 2: (Optional) Create a Secret

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If IRSA authentication is enabled for the csi\-fsx add\-on, you can skip this step.</div>



1. Create a YAML document for the Secret. The following `vke-tos-fsx-secret.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: Secret
   metadata:
     name: tos-fsx-key # Secret name. If the cluster version is 1.26.x, the name cannot contain the . character. Other cluster versions do not have this limit.
     namespace: default # Namespace of the Secret.
   type: Opaque # Secret type. In this example, select it to Opaque to store arbitrary key-value pairs.
   data:
     AccessKeyId: ${ak}  # The Base64-encoded account AK. Replace the value with your actual information.
     SecretAccessKey: ${sk}  # The Base64-encoded SK that matches the AK. Replace the value with your actual information.
     ExpiredTime: ${Temporary Token expiration time} # The Base64-encoded expiration time of the temporary token. If you use an AK and SK, do not specify this field.
     SessionToken: ${Temporary Token content} # The Base64-encoded content of the temporary token. If you use an AK and SK, do not specify this field.
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <code>echo -n "${ak}" | base64</code> command to perform Base64 encoding on items such as the AK and SK. Note that you need to replace <code>${ak}</code> with your actual value. For example, if <code>${ak}</code> is <code>demo</code>, the encoding command is <code>echo -n "demo" | base64</code>, which produces the encoded result <code>ZGVtbw==</code>.   </div>
   

   2. Run the following command to create the Secret.

   ```Bash
   kubectl create -f vke-tos-fsx-secret.yaml
   ```
   


<span id="cQAU1RTi"></span>
### Step 3: Create a PV


1. Create a YAML document for the PV. The following `vke-tos-fsx-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-tos-fsx-static-pv
   spec:
     accessModes: # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     - ReadWriteMany
     capacity:
       storage: 20Gi # The PV capacity. Unit: Gi.
     csi:
       driver: fsx.csi.volcengine.com # Driver required for storage mount.
       volumeAttributes:
         type: TOS # The PV type. In this topic, select TOS.
         server: tos-cn-shanghai.ivolces.com # The domain name of the created TOS bucket.
         region: cn-shanghai # The region where the created TOS bucket is located. If the TOS bucket is deployed in the same region as the cluster, this parameter can be omitted.
         bucket: doc-tos-demo # The name of the created TOS bucket.
         path: /   # Specify the root directory of the TOS bucket. Make sure that the directory exists. Otherwise, the mount will fail.
         secretName: tos-fsx-key # Make sure that the name of the Secret is consistent with that in Step 2. If you use IRSA authentication, this parameter can be omitted.
         secretNamespace: default # Specify the same namespace as the one of the Secret in Step 2. If you use IRSA authentication, this parameter can be ignored.
       volumeHandle: vke-tos-fsx-static-pv # Keep the value consistent with the PV name.
     persistentVolumeReclaimPolicy: Delete # The reclaim policy. Value: Retain or Delete.
     mountOptions:  # TOS PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. For details on mount parameters, see PV mount parameters.
     - no_writeback_cache
     - tos_allow_delete=true
     - num_meta_threads=64
     - num_io_threads=1024
     - num_bg_threads=128
     - num_prefetch_threads=64
     - tos_enable_cto=false
     - tos_symlink_mode=1
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |storage |The PV capacity. Unit: Gi. |
   |driver |The driver required for PV mount. In this topic, you need to set the value to fsx.csi.volcengine.com, which indicates the csi\-fsx add\-on. |
   |type |The PV type. In this topic, select TOS. |
   |server |The domain name of the created TOS bucket.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">You can view the domain name of the created TOS bucket in the TOS console. For details, see <a href="https://docs.byteplus.com/en/docs/tos/docs-exporting-bucket-information">Viewing bucket information</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the VKE cluster and TOS bucket are deployed in the same region, we recommend <strong>using a private domain name for access</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">When the VKE cluster and TOS bucket are deployed in different regions, you can<strong> use a public domain name for access</strong>. In this case, make sure that the public access feature is enabled for the VKE cluster.</div><br> |
   |region |The region where the created TOS bucket is located. For example, `cn-shanghai`. If the TOS bucket and the cluster are deployed in the same region, this parameter can be omitted. |
   |bucket |The name of the created TOS bucket. |
   |path |Specify the root directory of the TOS bucket. Ensure that the directory exists. Otherwise, the mount will fail. |
   |secretName |The name of the created Secret when you use AK/SK authentication. If you use IRSA authentication, this parameter can be omitted. |
   |secretNamespace |The namespace to which the created Secret belongs when you use AK/SK authentication. If you use IRSA authentication, this parameter can be omitted. |
   |volumeHandle |Keep the value consistent with the PV name. |
   |mountOptions |TOS PV mount parameters, which support dynamic modification and only take effect on newly mounted PVs instead of those already mounted. For details, see [PV mount parameters](https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters). |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-tos-fsx-static-pv.yaml
   ```
   


<span id="F2jjKcsO"></span>
### Step 4: Create a PVC


1. Create a YAML document for the PVC. The following `vke-tos-fsx-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-tos-fsx-static-pvc # The name of the PVC.
     namespace: default
   spec:
     accessModes: # PVC access mode. You can select only ReadWriteMany, which allows read-write access by multiple nodes. Keep it consistent with that in the PV configuration.
     - ReadWriteMany
     resources:
       requests:
         storage: 20Gi # The declared storage usage.
     volumeMode: Filesystem
     volumeName: vke-tos-fsx-static-pv # The name of the PV bound to this PVC.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PVC access mode. You can only select ReadWriteMany, which enables read and write access by multiple nodes. Keep it consistent with that in the PV configuration. |
   |storage |The declared storage capacity. Unit: Gi. |
   |volumeMode |The PV type. It must be consistent with the type configured for the PV. The following information is included:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the volume as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   |volumeName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-tos-fsx-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                       STATUS   VOLUME                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-tos-fsx-static-pvc     Bound    vke-tos-fsx-static-pv      20Gi       RWX                          2m36s
   ```
   


<span id="2jGQ57T1"></span>
### Step 5: Create an application and mount the PV


1. Create a YAML document for the Deployment. The following `vke-tos-fsx-static-deployment.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vke-static-tos-fsx-deploy
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: vke-static-tos-fsx-deploy
     template:
       metadata:
         labels:
           app: vke-static-tos-fsx-deploy
       spec:
         containers:
         - name: nginx # The container name.
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
             name: web
           volumeMounts:
           - mountPath: /tmp # The location where the FSX file system is mounted in the container.
             name: tos-fsx-pv
         volumes:
         - name: tos-fsx-pv
           persistentVolumeClaim:
             claimName: vke-tos-fsx-static-pvc  # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-tos-fsx-static-deployment.yaml
   ```
   


<span id="pBBr8Dbq"></span>
## Validating results

After you create a workload and mount it to a PV as described in the preceding steps, verify whether the TOS volume is mounted and whether shared storage and persistent storage are achieved by using the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   /dev/vdc        20466256      24  20449848   1% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Log in to the [TOS console ](https://console.byteplus.com/tos). Upload a file to the specified path. For details, see [Uploading files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).

4. View the PV mount path in the pod again.

   ```Bash
   kubectl exec vke-static-tos-fsx-deploy-5f55*** -- ls /tmp
   ```
   

   The expected response is as follows. You can see the uploaded file, which indicates that the data volume is mounted and persistent storage is achieved.

   ```Bash
   lost+found  
   test
   ```
