---
title: "Accessing static PFS PV through the FSX client"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_static_PFS_Volumes_through_FSX_client"
---

FSX can be integrated with the PFS file system and provides a file system client based on the FUSE framework. You only need to create a FUSE protocol service for the PFS file system, and then you can mount it through FSX. This topic introduces how to use static PFS PersistentVolumes (PVs) by using the FSX client.

<span id="Io6LdMIW"></span>
## Prerequisites


* The csi\-fsx and fsx\-service add\-ons have been installed and upgraded to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* The FSX client has been enabled for PFS (including Performance edition and Intelligent Computing edition), and an access point has been created.

* (Optional) You have obtained the AK/SK required for creating a key.

* (Optional) The kubectl tool has already been installed locally, and the target cluster has been connected by using kubectl. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="cJdHecs3"></span>
## Usage limits


* The FSX client only supports PFS instances of the Performance edition or Intelligent Computing edition.

* To use a temporary token for authentication, you need to implement the logic for refreshing tokens.

* StatefulSets require exclusive access to a volume, and do not support a manually created PersistentVolumeClaim (PVC).

* This feature is unavailable in clusters running on Kubernetes v1.20 and earlier.

* If you use clusters running on Kubernetes v1.26.x, you cannot use Secrets whose names contain periods (`.`). Otherwise, the PV will fail to be created.


<span id="o5XvrKuw"></span>
## Creating through the console

<span id="51Qsrau9"></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolume**. Click **Create PersistentVolume** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |How to create |Select a method for creating the PV. Currently, you can select **Static creation**. |
   |Name |Specify a name for the PV. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Access type |Select an access type for the PV. In this scenario, select **FSX**. The FSX access type delivers higher performance and more enterprise features. For detailed information on access type selection, see [Method selection description](https://docs.byteplus.com/en/docs/vke/Model_selection_description).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">FSX\-based access currently supports only Elastic Compute Service (ECS). It does not support VCI.</div><br> |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Project |Assign the PV to a project so that you can perform operations such as maintenance and authorization at the project level. By default, the **default** project is selected.  |
   |File system |Select a created PFS file system and access point based on your business requirements. |
   |Access key |Select a vePFS access key. Use the access key specified here to authorize VKE to access vePFS.<br><br>If no access key is available, click **Create key** and configure the key name, associated namespace, and the AK and SK of the IAM user.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The Secret names containing dots (<code>.</code>) are not allowed in v1.26.x clusters as they will cause PV creation failures.</div><br> |
   |Subdirectory |Configure an existing path in the file system based on your business requirements. The default directory is the root directory (represented by "/").<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that the configured subdirectory already exists in the file system. Otherwise, mounting will fail.</div><br> |
   

4. Click **Confirm**.


<span id="SvfzHnoU"></span>
### Step 2: Create a PVC


1. In the left navigation bar of the cluster management page, click **Storage \> PersistentVolumeClaim**. Click **Create PersistentVolumeClaim** to configure a PVC.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend that you select a custom namespace or the **default** namespace created by the system. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select a storage type. In this scenario, select **PFS**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteMany**, which enables read and write access by multiple nodes. |
   |Billing type |Select a resource billing type as needed. Currently, only **Pay\-as\-you\-go** is supported. |
   |Instance type |Select the filesystem specifications for creating a PV. 100 MB/s/TiB and Performance edition are supported. For more details, see [Service specifications](https://docs.byteplus.com/en/docs/pfs/Product-specifications).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta \- apply for trial</strong></a>]: The Intelligent Computing edition is currently in beta. To use it, submit an application.</div><br> |
   |How to create |The method of creating a PVC. Available methods include **Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Use an existing PersistentVolume**. |
   |PersistentVolume |Specify the PFS PV. |
   

2. Click **Confirm**.


<span id="33LwXoFo"></span>
### Step 3: Create an application and mount the PV

After the static PV of the PFS type is created, add the PV to a workload that will use the PV. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id="sSsZS4os"></span>
## Creating through kubectl

If you [connect to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can use a static PFS PV by using kubectl.

<span id="r7PyHoEC"></span>
### Step 1: (Optional) Create a policy

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you use the AK and SK of the root user, you can skip this step.</div>


* <div data-tips="true" data-tips-type="tip">To dynamically refresh temporary tokens, see the AssumeRole API document.</div>



For the procedure of creating a policy, see Creating custom policies. The following code is a JSON sample for creating a vePFS policy:

```JSON
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "vepfs:ClientMount",
                "vepfs:ClientWrite"
            ],
            "Resource": ["trn:vepfs:cn-beijing:xxxx:filesystem/vepfs-cngl86xxxxxab461"],
            "Condition": {
                "StringEquals": {
                    "volc:RequestTag/accesspoint": "<accesspoint ID>"
                }
            }
        },
        {
            "Effect": "Allow",
            "Action": [
                "vepfs:VerifyAccessPoint",
                "vepfs:DescribeAccessPoints",
                "vepfs:CreateAccessPoint",
                "vepfs:ModifyAccessPoint",
                "vepfs:DeleteAccessPoint"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
  }
```


<span id="xyUxa6Ty"></span>
### Step 2: Create a Secret


1. Create a YAML document for the Secret. The following `vke-pfs-fsx-secret.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   data:
     AccessKeyId: ${ak} # The Base64-encoded account AK. Replace the value with your actual information.
     SecretAccessKey: ${sk} # The Base64-encoded SK that matches the AK. Replace the value with your actual information.
     ExpiredTime: ${Temporary Token expiration time}  # The Base64-encoded expiration time of the temporary token. If you use an AK and SK, do not specify this field.
     SessionToken: ${Temporary Token content} # The Base64-encoded content of the temporary token. If you use an AK and SK, do not specify this field.
   kind: Secret
   metadata:
     name: pfs-fsx-key  # The name of the Secret. If the cluster version is 1.26.x, the name cannot contain the . character. Other cluster versions do not have this limit.
     namespace: default
   type: Opaque
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <code>echo -n "${ak}" | base64</code> command to perform Base64 encoding on items such as the AK and SK. Note that you need to replace <code>${ak}</code> with your actual value. For example, if <code>${ak}</code> is <code>demo</code>, the encoding command is <code>echo -n "demo" | base64</code>, which produces the encoded result <code>ZGVtbw==</code>.   </div>
   

2. Run the following command to create the Secret.

   ```Bash
   kubectl create -f vke-pfs-fsx-secret.yaml
   ```
   


<span id="5kujIQC4"></span>
### Step 3: Create a PV


1. Create a YAML document for the PV. The following `vke-pfs-fsx-static-pv.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-pfs-fsx-static-pv
   spec:
     capacity:
       storage: 20Gi
     accessModes:
     - ReadWriteMany
     persistentVolumeReclaimPolicy: Delete
     csi:
       driver: fsx.csi.volcengine.com # The driver that the storage mount depends on.
       volumeHandle: vke-pfs-fsx-static-pv # The unique identifier of the PV. Keep it consistent with the PV name. To use multiple PVs simultaneously, the value for each PV must be different.
       volumeAttributes:
         type: vePFS # PersistentVolume type. Set it to vePFS.
         server: ap-55xxxxbd.cnbxxxxxx40305xx.rrmjxxxxxxxxxxx58q09xxx.cn-beijing.vepfs-ivolces.com # The domain name in the PFS mount command. It is concatenated from the ID and the domain of the access point.
         path: / # The mount directory. Ensure  that the path exists. Otherwise the mount will fail.
         secretName: pfs-fsx-key  # The Secret created.
         secretNamespace: default  # Namespace where the Secret resides.
   ```
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-pfs-fsx-static-pv.yaml
   ```
   


<span id="Gif54Z3n"></span>
### Step 4: Create a PVC


1. Create a YAML document for the PVC. The following `vke-pfs-fsx-static-pvc.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-pfs-fsx-static-pvc # The name of the PVC.
     namespace: default
   spec:
     accessModes:  # PVC access mode. Only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     - ReadWriteMany
     resources:
       requests:
         storage: 20Gi # The declared storage usage.
     volumeMode: Filesystem
     volumeName: vke-pfs-fsx-static-pv  # The name of the PV bound to this PVC.
   ```
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl create -f vke-pfs-fsx-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                       STATUS   VOLUME                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-pfs-fsx-static-pvc     Bound    vke-pfs-fsx-static-pv      20Gi       RWX                          2m36s
   ```
   


<span id="fRUA7x4a"></span>
### Step 5: Create an application and mount the PV


1. Create a YAML document for the Deployment. The following `vke-pfs-fsx-static-deployment.yaml` file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vke-static-pfs-fsx-deploy
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: vke-static-vepfs-fsx-deploy
     template:
       metadata:
         labels:
           app: vke-static-vepfs-fsx-deploy
       spec:
         containers:
         - image: nginx
           imagePullPolicy: IfNotPresent
           name: nginx
           volumeMounts:
           - mountPath: /tmp  # Mount location of the PV in the container.
             name: pfs-fsx-pv
         volumes:
         - name: pfs-fsx-pv
           persistentVolumeClaim:
             claimName: vke-pfs-fsx-static-pvc  # The name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-pfs-fsx-static-deployment.yaml
   ```
