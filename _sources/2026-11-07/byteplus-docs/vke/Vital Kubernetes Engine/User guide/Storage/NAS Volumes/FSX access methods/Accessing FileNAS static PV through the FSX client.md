---
title: "Accessing FileNAS static PV through the FSX client"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Use_a_static_NAS_PersistentVolume_through_the_FSX_client"
---

FSX can access FileNAS file systems based on unified policies for access, authentication, and management. This topic describes how to access a static FileNAS PersistentVolume (PV) through the FSX client.

<span id="zly4aLo0"></span>
## Prerequisites


* The csi\-fsx and fsx\-service add\-ons have been installed and upgraded to the latest version. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* A FileNAS file system and access point have already been created. Currently only cache\-type FileNAS supports access points.

* A valid key has been created in the target namespace. . To use a temporary token for authentication, you need to implement the logic for refreshing tokens.

* The kubectl tool has already been installed locally, and the target cluster has been connected by using kubectl. For details, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id="k4xhUVFr"></span>
## Usage limits


* Currently, only cache\-type FileNAS supports access points. This support is in the beta stage. To request access, contact your account manager to get trial permissions.

* To use a temporary token for authentication, you need to implement the logic for refreshing tokens.

* Stateful workloads require exclusive access to a volume and do not support a manually created PersistentVolumeClaim (PVC).

* This feature is unavailable in clusters running on Kubernetes v1.20 and earlier.


<span id="5mXDUZvG"></span>
## Procedure

<span id="R5WrqI2E"></span>
### Step 1: (Optional) Create a policy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If you use the AK and SK of the root user, you can skip this step.</div>


* <div data-tips="true" data-tips-type="default">To dynamically refresh temporary tokens, see the AssumeRole API document.</div>



For detailed instructions on creating a policy, see Creating custom policies. The following is an example of creating a FileNAS policy:


<Tabs>
<Tab zoneid="Z108VX4MDg" title="Read-only configuration example">
<TabTitle>Read-only configuration example</TabTitle>

The following configuration example grants read\-only access to an access point.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "filenas:ClientMount"
      ],
      "Resource": ["trn:filenas:cn-beijing:2100xxxxxx:filesystem/anas-sw07xxxxxx9caxxx"],
      "Condition": {
        "StringEquals": {
          "volc:RequestTag/accesspoint": "ap-8dcxxxxx"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "filenas:VerifyAccessPoint",
        "filenas:DescribeAccessPoints",
        "filenas:CreateAccessPoint",
        "filenas:ModifyAccessPoint",
        "filenas:DeleteAccessPoint"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```



</Tab>
<Tab zoneid="fCTVp99GVP" title="Read and write access configuration example">
<TabTitle>Read and write access configuration example</TabTitle>

The following configuration example grants read and write access to an access point.

```JSON
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "filenas:ClientMount",
        "filenas:ClientWrite",
        "filenas:ClientRootAccess"
      ],
      "Resource": ["trn:filenas:cn-beijing:2100xxxxxx:filesystem/anas-sw07xxxxxx9caxxx"],
      "Condition": {
        "StringEquals": {
          "volc:RequestTag/accesspoint": "ap-8dcxxxxx"
        }
      }
    },
    {
      "Effect": "Allow",
      "Action": [
        "filenas:VerifyAccessPoint",
        "filenas:DescribeAccessPoints",
        "filenas:CreateAccessPoint",
        "filenas:ModifyAccessPoint",
        "filenas:DeleteAccessPoint"
      ],
      "Resource": [
        "*"
      ]
    }
  ]
}
```



</Tab>
</Tabs>


<span id="9oxrF5wO"></span>
### Step 2: Create a Secret


1. Create a YAML document for the Secret. The following vke\-nas\-fsx\-secret.yaml file serves as an example:

   ```YAML
   apiVersion: v1
   kind: Secret
   metadata:
     name: nas-fsx-key # Secret name. If the cluster version is 1.26.x, the name cannot contain the . character. Other cluster versions do not have this limit.
     namespace: default # Namespace of the Secret.
   type: Opaque # Secret type. In this example, select it to Opaque to store arbitrary key-value pairs.
   data:
     akId: ${AK} # The Base64-encoded account AK. Replace the value with your actual information.
     akSecret: ${AK} # The Base64-encoded SK that matches with the AK. Replace the value with your actual information.
     ExpiredTime: ${Temporary Token expiration time}      # The Base64-encoded expiration time of the temporary token. If you use an AK and SK, do not specify this field.
     SessionToken: ${Temporary Token content}        # The Base64-encoded content of the temporary token. If you use an AK and SK, do not specify this field.
   ```
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can use the <code>echo -n "${ak}" | base64</code> command to perform Base64 encoding on items such as the AK and SK. Note that you need to replace <code>${ak}</code> with your actual value. For example, if <code>${ak}</code> is <code>demo</code>, the encoding command is <code>echo -n "demo" | base64</code>, which produces the encoded result <code>ZGVtbw==</code>.   </div>
   

2. Run the following command to create the Secret.

   ```Bash
   kubectl create -f vke-nas-fsx-secret.yaml
   ```
   


<span id="M4sdJCAi"></span>
### Step 3: Create a PV


1. Create a YAML document for the PV. The following vke\-nas\-fsx\-static\-pv.yaml file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: vke-nas-fsx-static-pv # PV name.
   spec:
     capacity:
       storage: 100Gi # Declared PV capacity.
     accessModes: # PV access mode. The only supported mode is ReadWriteMany, which allows read and write access by multiple nodes.
     - ReadWriteMany
     csi:
       driver: fsx.csi.volcengine.com # Driver required for storage mount.
       volumeAttributes:
         type: nas # The PV type. In this example, it needs to be set to efs.
         server: ap-69xxxxxx.swxxxxxxb9ceaxxx.xxxxxx8013xxx2dxxxxxx19ew.cn-beijing.nas.ivolces.com # The ID and domain of the filesystem access point.
         path: / # The root directory of the filesystem. Ensure that the directory exists. Otherwise, the mount will fail.
         secretName: nas-fsx-key # The created Secret. It is required for AK/SK-based authentication.
         secretNamespace: default # Namespace of the created Secret. It is required for AK/SK-based authentication.
       volumeHandle: vke-nas-fsx-static-pv # The unique identifier of the PV. Keep it consistent with the PV name.
     persistentVolumeReclaimPolicy: Delete # PV reclaim policy. Value: Retain or Delete.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When you use the FSX client to mount FileNAS storage, you can configure only basic parameters.   </div>
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteMany is supported, which allows the PV to be read and written by multiple pods. |
   |storage |Declared PV capacity. Unit: Gi. This field is required by Kubernetes. The value has no actual meaning and is only for validation. The actual capacity is subject to the created storage capacity. |
   |driver |The driver required for PV mount. In this topic, you need to set the value to fsx.csi.volcengine.com, which indicates the csi\-fsx add\-on. |
   |type |The storage type. In this example, it is set to `nas`, indicating FileNAS. |
   |server |The ID and domain of the created NFS filesystem access point. They are concatenated in the `accessPointID.accessPointDomain` format. An example is `ap-69xxxxxx.swxxxxxxb9ceaxxx.xxxxxx8013xxx2dxxxxxx19ew.cn-beijing.nas.ivolces.com`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can view the ID and domain name of a filesystem access point in the console.</div><br> |
   |path |Specify the root directory of the NFS storage. Ensure that the directory exists. Otherwise, the mount will fail. |
   |secretName |The name of the created Secret when you use AK/SK authentication. |
   |secretNamespace |The namespace to which the created Secret belongs when you use AK/SK authentication. |
   |volumeHandle |The unique identifier of the PV. Keep it consistent with the name of the PV. |
   |persistentVolumeReclaimPolicy |The PV reclaim policy. The following information is included:<br><br><br>* **Retain**: The Retain policy. When the PVC bound to the PV is deleted, the PV is retained.<br><br>* **Delete**: The Delete policy. When the PVC bound to the PV is deleted, the PV is deleted synchronously. |
   |volumeMode |The PV types. Valid values:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the PV as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl create -f vke-nas-fsx-static-pv.yaml
   ```
   


<span id="b0pCFLbL"></span>
### Step 4: Create a PVC


1. Create a YAML document for the PVC. The following vke\-nas\-fsx\-static\-pvc.yaml file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: vke-nas-fsx-static-pvc  # PVC name.
     namespace: default # Namespace to which the PVC belongs.
   spec:
     accessModes:  # PVC access mode. Currently, only ReadWriteMany is supported. ReadWriteMany allows read and write access from multiple nodes.
     - ReadWriteMany
     resources:
       requests:
         storage: 20Gi # Declared storage usage. The unit is Gi. Ensure it is consistent with the capacity of the created PV.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the PV as a filesystem) and Block (using the PV as a block device). The value must be consistent with the type configured in the PV.
     volumeName: vke-nas-fsx-static-pv # Name of the created PV.
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
   kubectl create -f vke-nas-fsx-static-pvc.yaml
   ```
   

3. Run the following command to view the result of the static association between the PVC and PV.

   ```Bash
   kubectl get pvc
   ```
   

   If the response is similar to the following one, the binding is successful.

   ```Bash
   NAME                       STATUS   VOLUME                     CAPACITY   ACCESS MODES   STORAGECLASS   AGE
   vke-nas-fsx-static-pvc     Bound    vke-nas-fsx-static-pv      20Gi       RWX                          2m36s
   ```
   


<span id="Kia1mvHP"></span>
### Step 5: Create an application and mount the PV


1. Create a YAML document for the Deployment. The following vke\-nas\-fsx\-static\-deployment.yaml file serves as an example:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vke-static-nas-fsx-deploy
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: vke-static-nas-fsx-deploy
     template:
       metadata:
         labels:
           app: vke-static-nas-fsx-deploy
       spec:
         containers:
         - image: nginx
           name: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           volumeMounts:
           - mountPath: /tmp # The mount location of the PV in the container.
             name: nas-fsx-pv # The PV name, which must be consistent with the value of the volumes.name field.
         volumes:
         - name: nas-fsx-pv # The PV name. You can specify a custom name.
           persistentVolumeClaim:
             claimName: vke-nas-fsx-static-pvc # Name of the created PVC.
   ```
   

2. Run the following command to create the Deployment.

   ```Bash
   kubectl create -f vke-nas-fsx-static-deployment.yaml
   ```
   


<span id="iYu58TVp"></span>
## Validating results

After creating a workload and mounting a PV to it as described in the preceding steps, you can verify the volume mounting status and persistent storage via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec vke-static-nas-fsx-deploy-xxx -- df | grep tmp
   ```
   

   The expected response is as follows.

   ```Bash
   cnshbb5***.3qda7du***.nas.ivolces.com:/temp 10995116277760       0 10995116277760   0% /tmp
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec vke-static-nas-fsx-deploy-xxx -- ls /tmp
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Write a file to the PV.

   ```Bash
   kubectl exec vke-static-nas-fsx-deploy-xxx -- touch /tmp/test
   ```
   

4. Delete the pod.

   ```Bash
   kubectl delete pod vke-static-nas-fsx-deploy-xxx
   ```
   

5. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec vke-static-nas-fsx-deploy-xxx -- ls /tmp
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id="bQBwTQyh"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
