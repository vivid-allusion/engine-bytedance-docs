---
title: "Using dynamic PersistentVolumes created from dedicated local storage"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_exclusive_type_for_dynamic_Local_Volumes"
---

Vital Kubernetes Engine (VKE) supports local storage through the Container Storage Interface (CSI). This topic describes how to use dynamic PersistentVolumes created from dedicated local storage.

<div data-tips="true" data-tips-type="tip">Description</div>


<div data-tips="true" data-tips-type="tip">[<a href="https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features"><strong>Beta · Apply for trial</strong></a>] The <strong>csi\-local</strong> add\-on for local storage and <strong>storage\-aware scheduling</strong> are currently in the beta stage. To use them, submit an application.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* Use ESSD data volumes to mount to the container and image directories `/var/lib/containerd` and `/var/lib/kubelet`. **Avoid mounting local disks to the container or image directory, as this mounting type is not applicable to local storage scenarios.** 

* The three add\-ons required in this scenario **must be installed or uninstalled in the order described in the following content. If this order is not followed, scheduling will malfunction**.

* The Kubernetes version of the cluster must meet the following requirements:

   * [Kubernetes v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24): v1.24.15\-vke.34 and later

   * [Kubernetes v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26): v1.26.10\-vke.22 and later

   * [Kubernetes v1.28](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28): v1.28.3\-vke.16 and later

   * [Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30): v1.30.4\-vke.13 and later

   * [Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32): v1.32.3\-vke.8 and later

   * [Kubernetes v1.34](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_34): v1.34.1\-vke.2 and later

* Local storage does not offer highly available volumes and is only applicable to temporary data storage or applications that internally implement high availability.


<span id="Xc5yMEvH"></span>
## Prerequisites


* A cluster that uses a compliant Kubernetes version has already been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool has been installed in the local environment. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF5ZKM6YWN572u5L6d6LWW57uE5Lu2"></span>
### Step 1: Install and set up dependent add\-ons

To use local storage, you need to install and set up the following add\-ons in the order described below.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">The csi\-local add\-on depends on the snapshot\-controller add\-on. Before installing the csi\-local add\-on, confirm that the snapshot\-controller add\-on is installed.</div>


* <div data-tips="true" data-tips-type="danger">The csi\-local add\-on must be used with the storage\-aware scheduling feature of the scheduler\-plugin add\-on. Before enabling the storage\-aware scheduling feature, ensure that both the snapshot\-controller and csi\-local add\-ons are installed. Otherwise, normal scheduling will be affected.</div>


* <div data-tips="true" data-tips-type="danger">Before you uninstall the csi\-local add\-on, disable the storage\-aware scheduling feature in the scheduler\-plugin add\-on to avoid affecting scheduling capabilities.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the cluster that you need to configure.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. Click the **Storage** tab, move the pointer over the snapshot\-controller add\-on card, and then click **Deploy** to install the snapshot\-controller add\-on. Then, install the csi\-local add\-on in the same way.

5. Click the **Scheduling** tab, move the pointer over the scheduler\-plugin add\-on card, and then click **Configuration**. In the configuration dialog box, select **Local storage** for the **Storage\-aware scheduling** parameter.

   
   |**Parameters** |**Description** |
   |---|---|
   |Storage\-aware scheduling |**Local storage**: This feature is disabled by default. Selecting the option enables storage\-aware scheduling for local storage. After this feature is enabled, scheduling can be performed according to the storage resources available on each node.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This feature takes effect only if the csi\-local add\-on is installed.</div><br> |
   


<span id=".5q2l6aqk5LqM77ya6YWN572u5pys5Zyw55uY57G75Z6L55qE6IqC54K55rGg"></span>
### Step 2: Configure node pools that use local disks

Configure a node pool that uses a local disk. The following content describes the key configurations involved in this scenario. Specify other parameters based on your business requirements. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool) and [Creating managed node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool).


1. Specify the instance type. Select an ECS instance type that supports local disks. For details, see [Local disks](https://docs.byteplus.com/en/docs/ecs/Local-volumes).

2. Configure a data volume.

   * Specify container and image directories. Use ESSD data volumes to mount to the container and image directories` /var/lib/containerd` and `/var/lib/kubelet`.

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Warning   </div>
   

   <div data-tips="true" data-tips-type="danger" data-wrapper-indent="1">Do not mount local disks to the container or image directory, as this mounting type is not applicable to local storage scenarios.   </div>
   

   * Click **Add data volume** to configure other data volumes by using local disks. Local data volumes support SSD and HDD types. Different ECS types support different data volume types. You can select a local data volume type based on your business requirements.

3. Specify custom node labels, which are used to filter nodes during local disk initialization, such as `csi-local: "i4ag"`.

4. Configure the InitializeScript to install lvm2 on the node. The installation command is `apt-get install -y lvm2`.


<span id=".5q2l6aqk5LiJ77ya5Yid5aeL5YyW5pys5Zyw55uY"></span>
### Step 3: Initialize local disks

After the csi\-local add\-on is installed, local storage\-related CRDs will be automatically created, including


* NodeLocalStorageInitConfig: Initialize the NodeLocalStorage resources for each node. If NodeLocalStorageInitConfig exists when the csi\-local add\-on creates NodeLocalStorage resources, the configurations in NodeLocalStorageInitConfig will be populated into the spec of the created NodeLocalStorage resources.

* NodeLocalStorage: Report storage device information for each node. You can edit the Spec field of the NodeLocalStorage resource as needed.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e117d189131aefd4f41ee7c2bff33cfe.png) </span>

This example scenario uses an ecs.i4ag.12xlarge instance with an Elastic Block Storage (EBS) cloud disk mounted to `/dev/vdc` and the `csi-local: "i4ag"` label attached to the node.


1. In the left navigation bar, click **Workload \> Resource Explorer**. On the page that appears, click **Create with Yaml**. On the Create with Yaml page, configure the CR to initialize the local disk.

   * Select **Custom** from the **Type** drop\-down list.

   * Enter the following sample YAML configurations in the **Yaml** code editor.

   ```Yaml
   apiVersion: csi.volcengine.com/v1alpha1
   kind: NodeLocalStorageInitConfig
   metadata:
     name: csi-local
   spec:
     globalConfig: # The global default node configuration.
       listConfig:
         devices: {}
         mountPoints: {}
         vgs: {}
       resourceToBeInited: {}
       spdkConfig: {}
     nodesConfig: # The node pool-level configuration filtered by label.
       - selector: # The filter rule.
           matchLabels:
             csi-local: "i4ag" # The label used for filtering nodes.
         listConfig: # The list of storage devices that can be allocated by csi-local.
           devices:
             include: # The include regex.
               - /dev/vdc # The data volume that can be allocated for exclusive use. Make sure that the data volume already exists on the ECS instance.
   ```
   

2. Wait for about one minute, and then run the following command to view the NodeLocalStorage configuration for the corresponding node. In this example, `192.168.2.6` is the IP address of the node.

   ```Bash
   kubectl get nls 192.168.2.6 -oyaml
   ```
   

   The expected result is as follows: You can query the information about the dedicated disk, which indicates that the local disk has been initialized.

   ```YAML
   apiVersion: csi.volcengine.com/v1alpha1
   kind: NodeLocalStorage
   metadata:
     creationTimestamp: "2024-07-17T08:52:03Z"
     generation: 1
     name: 192.168.2.6
     resourceVersion: "30819"
     uid: 129012df-d9b2-41f1-bb5f-0d86fc15baf3
   spec:
     listConfig:
       devices:
         include:
         - /dev/vdc
       mountPoints: {}
       vgs:
         include:
         - csi-local-pool-[0-9]+
     nodeName: 192.168.2.6
     resourceToBeInited:
       vgs:
       - devices:
         - /dev/nvme0n1
         name: csi-local-pool-0
     spdkConfig: {}
   status:
     filteredStorageInfo:
       updateStatusInfo:
         lastUpdateTime: "2024-07-17T09:51:24Z"
         updateStatus: accepted
       volumeGroups:
       - csi-local-pool-0
     nodeStorageInfo:
       deviceInfo:                     # After the local disk is initialized, you can view the partitioned dedicated disk.
       - condition: DiskReady
         mediaType: ssd
         name: /dev/nvme0n1
         readOnly: false
         total: 3840755982336
       - condition: DiskReady
         mediaType: hdd
         name: /dev/vda1
         readOnly: false
         total: 199229440
       phase: Running
       state:
         lastHeartbeatTime: "2024-07-17T09:51:24Z"
         status: "True"
         type: DiskRead
   ```
   


<span id=".5q2l6aqk5Zub77ya5L2_55So5pys5Zyw5a2Y5YKo5Yqo5oCB5a2Y5YKo5Y23"></span>
### Step 4: Use a dynamic PersistentVolume based on local storage

Local storage can be used in dynamic provisioning mode. You can select from preset StorageClasses.


|**Built\-in StorageClass** |**Description** |
|---|---|
|csi\-local\-device\-hdd |Preconfigured StorageClass for HDD standalone disks. It uses the ext4 filesystem. |
|csi\-local\-device\-ssd |Preconfigured StorageClass for SSD standalone disks. It uses the ext4 filesystem. |
|csi\-local\-lvm |Preconfigured StorageClass for LVM\-managed shared storage. It uses the ext4 filesystem. |
|csi\-local\-lvm\-xfs |Preconfigured StorageClass for LVM\-managed shared storage. It uses the xfs filesystem. |


This example uses StatefulSet creation to demonstrate how to use a dynamic PersistentVolume created from dedicated local disks.


1. Create a YAML file for the StatefulSet. The following example is a file named `statefulset-demo.yaml`:

   ```YAML
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: nginx-device
   spec:
     selector:
       matchLabels:
         app: nginx-device
     podManagementPolicy: Parallel
     serviceName: "nginx-device"
     replicas: 1
     volumeClaimTemplates:
     - metadata:
         name: html
       spec:
         volumeMode: Filesystem
         accessModes:
           - ReadWriteOnce
         storageClassName: csi-local-device-hdd  # The name of the pre-configured StorageClass. Choose one as needed.
         resources:
           requests:
             storage: 5Gi
     template:
       metadata:
         labels:
           app: nginx-device
       spec:
         containers:
         - name: nginx
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           imagePullPolicy: Always
           volumeMounts:
           - mountPath: "/data"
             name: html
           command:
           - sh
           - "-c"
           - |
               while true; do
                 echo $(hostname) $(date) >> /data/test.txt;
                 sleep 10s
               done;
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl create -f statefulset-demo.yaml
   ```
   


<span id="mZulxVSj"></span>
## Result validation

<span id="qxBWLa4y"></span>
### PV mounting

After you delete the pod and create another one, you can run the `exec` command to enter the new pod to check whether data in the deleted pod exists.

```Bash
❯ kubectl delete pod nginx-device-0
pod "nginx-device-0" deleted

❯ kubectl exec -it nginx-device-0 cat /data/test.txt
kubectl exec [POD] [COMMAND] is DEPRECATED and will be removed in a future version. Use kubectl exec [POD] -- [COMMAND] instead.
nginx-device-0 Thu Jul 18 06:34:51 UTC 2024
nginx-device-0 Thu Jul 18 06:35:01 UTC 2024
nginx-device-0 Thu Jul 18 06:35:11 UTC 2024
nginx-device-0 Thu Jul 18 06:35:21 UTC 2024
nginx-device-0 Thu Jul 18 06:35:31 UTC 2024
nginx-device-0 Thu Jul 18 06:35:41 UTC 2024
nginx-device-0 Thu Jul 18 06:35:51 UTC 2024
nginx-device-0 Thu Jul 18 06:36:01 UTC 2024
nginx-device-0 Thu Jul 18 06:36:11 UTC 2024
```


<span id="ATzUpGK3"></span>
### PV reclaim

Delete the StatefulSet and delete the PVC. The dedicated disk vdc will be reclaimed and formatted, and the file system will be erased.

```Bash
root@iv-yda1sl1t***:~# mount /dev/vdc /tmp2
mount: /tmp2: wrong fs type, bad option, bad superblock on /dev/vdc, missing codepage or helper program, or other error.
```
