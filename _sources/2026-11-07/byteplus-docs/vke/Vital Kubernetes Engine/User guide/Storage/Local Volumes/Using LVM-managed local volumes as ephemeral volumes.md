---
title: "Using LVM-managed local volumes as ephemeral volumes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using_local_storage_LVM_through_the_temporary_volume"
---

Vital Kubernetes Engine (VKE) supports local storage through the Container Storage Interface (CSI). This topic describes how to use local storage volumes managed by Local Volume Manager (LVM) as ephemeral volumes.

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

* LVM\-managed local storage volumes do not support cross\-node data migration and are not applicable to high availability scenarios.


<span id="Co9KUi59"></span>
## Prerequisites


* A cluster that uses a compliant Kubernetes version has been created. For details, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

* The kubectl tool has been installed in the local environment. For details, see [Installing and setting up kubectl](https://kubernetes.io/docs/tasks/tools/).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5a6J6KOF5ZKM6YWN572u5L6d6LWW57uE5Lu2"></span>
### Step 1: Install and configure add\-ons

To use local storage, you need to install and set up the following add\-ons in the order described below.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">The csi\-local add\-on depends on the snapshot\-controller add\-on. Before installing the csi\-local add\-on, confirm that the snapshot\-controller add\-on is installed.</div>


* <div data-tips="true" data-tips-type="danger">The csi\-local add\-on must be used with the storage\-aware scheduling feature of the scheduler\-plugin add\-on. Before enabling the storage\-aware scheduling feature, ensure that both the snapshot\-controller and csi\-local add\-ons are installed.</div>


* <div data-tips="true" data-tips-type="danger">Before you uninstall the csi\-local add\-on, disable the storage\-aware scheduling feature in the scheduler\-plugin add\-on to avoid affecting scheduling capabilities.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the cluster that you need to configure.

3. On the cluster management page, click **Addons** in the left navigation bar.

4. Click the **Storage** tab, move the pointer over the snapshot\-controller add\-on card, and then click **Deploy** to install the snapshot\-controller add\-on. Then, install the csi\-local add\-on in the same way.

5. Click the **Scheduling** tab, move the pointer over the scheduler\-plugin add\-on card, and then click **Configuration**. In the configuration dialog box, select **Local storage** for the **Storage\-aware scheduling** parameter.

   
   |**Parameter** |**Description** |
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


<span id="oGzGLL0W"></span>
### Step 3: Initialize local disks

After the csi\-local add\-on is installed, local storage\-related CRDs will be automatically created, including


* NodeLocalStorageInitConfig: Initialize the NodeLocalStorage resources for each node. If NodeLocalStorageInitConfig exists when the csi\-local add\-on creates NodeLocalStorage resources, the configurations in NodeLocalStorageInitConfig will be populated into the spec of the created NodeLocalStorage resources.

* NodeLocalStorage: Report storage device information for each node. You can edit the Spec field of the NodeLocalStorage resource as needed.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e117d189131aefd4f41ee7c2bff33cfe.png) </span>

This scenario uses an ecs.i4ag.12xlarge instance with a 3.5 TB SSD `/dev/nvme0n1` and `csi-local: "i4ag"` as the node label.


1. In the left navigation bar, click **Workload \> Resource Explorer**. On the page that appears, click **Create with Yaml**. On the Create with Yaml page, configure the CR to initialize the local disk.

   * Select **Custom** from the **Type** drop\-down list.

   * Enter the following sample YAML configurations in the **Yaml** code editor.

   ```Yaml
   apiVersion: csi.volcengine.com/v1alpha1
   kind: NodeLocalStorageInitConfig
   metadata:
     name: csi-local
   spec:
     globalConfig:  # The global default node configuration.
       listConfig:
         devices: {}
         mountPoints: {}
         vgs: {}
       resourceToBeInited: {}
       spdkConfig: {}
     nodesConfig: # The node pool-level configuration filtered by label.
       - selector: # The filter rule.
           matchLabels:
             csi-local: "i4ag" # Label for filtering nodes
         listConfig: # The list of storage devices that can be allocated by csi-local.
           mountPoints: {}
           vgs: # The LVM (shared disk) blocklist and allowlist. In this context, the shared disk name is the VolumeGroup (VG) name.
             include:
               - csi-local-pool-[0-9]+
         resourceToBeInited: # The device initialization list.
           vgs:  # LVM (shared disk) initialization.
             - devices: # Initialize the device /dev/nvme0n1 as a VG named csi-local-pool-0. Caution: If the node contains a VG with the same name, csi-local does not perform any operation.
                 - /dev/nvme0n1
               name: csi-local-pool-0
         spdkConfig: {}
   ```
   

1. Wait for about one minute, and then run the following command to view the NodeLocalStorage configuration for the corresponding node. `192.168.2.6` is the IP address of the node.

   ```Bash
   kubectl get nls 192.168.2.6 -oyaml
   ```
   

   The expected result is as follows: You can query VG information, which indicates that the local disk has been initialized.

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
       volumeGroups: # VolumeGroup is initialized. You can view information about VolumeGroup.
       - allocatable: 3840753532928
         available: 3840753532928
         condition: DiskReady
         name: csi-local-pool-0
         physicalVolumes:
         - /dev/nvme0n1
         total: 3840753532928
   ```
   


<span id=".5q2l6aqk5Zub77ya6YCa6L-H5Li05pe25Y235pa55byP5L2_55SoLWx2bS3ljbc="></span>
### Step 4: Use LVM\-managed volumes as ephemeral volumes

This example uses Deployment creation to demonstrate how to use LVM\-managed volumes as ephemeral volumes.


1. Create a YAML file for the Deployment. The code of the sample file `deployment-demo.yaml` is as follows:

   ```YAML
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: deployment-demo
   spec:
     replicas: 1
     selector:
       matchLabels:
         app: deployment-demo
     template:
       metadata:
         labels:
           app: deployment-demo
       spec:
         containers:
         - name: demo
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           volumeMounts:
             - mountPath: /srv
               name: webroot
         volumes:
           - name: webroot
             csi:
               driver: local.csi.volcengine.com
               fsType: ext4  # Specify the file system. Valid values: ext4 and xfs.
               volumeAttributes:
                 vgName: csi-local-pool-0 # Required. The VG used by the ephemeral volume.
                 size: 10Gi # Optional. The size of the ephemeral volume. If you do not specify this parameter, the default value 1Gi is used.
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl create -f deployment-demo.yaml
   ```
   


<span id=".5ZCO57ut5pON5L2c"></span>
## Result validation

<span id="HapsRZ5s"></span>
### Volume mounting

After the workload is created, log in to the node and view the details of local storage on the node.


1. Use **ECS Terminal** to log in to the node. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to view the block device information on the node.

   ```Bash
   lsblk
   ```
   

   The expected result is as follows: You can see the initialized local storage block.

   ```Bash
   NAME                                                                                        MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   vda                                                                                         254:0    0   40G  0 disk 
   ├─vda1                                                                                      254:1    0  190M  0 part /boot/efi
   └─vda2                                                                                      254:2    0 39.8G  0 part /
   vdb                                                                                         254:16   0  100G  0 disk /mnt/vdb
   nvme0n1                                                                                     259:0    0  3.5T  0 disk 
   └─csi--local--pool--0-csi--c77b8485df5eae495f6b2d902772697a7d9c9364fc4d8bb4750da62c89abba49 253:0    0   10G  0 lvm  /mnt/vdb/kubelet/pods/7e9fd2a9-d9a0-4ba4-b80a-6682a8a202a9/volumes/kubernetes.io~csi/webroot/mount
   ```
   

3. Run the following command to view the logical volume (LV) on the node.

   ```Bash
   lvs
   ```
   

   The expected result is as follows: The LV has been created and mounted.

   ```Bash
     LV                                                                   VG               Attr       LSize  Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
     csi-c77b8485df5eae495f6b2d902772697a7d9c9364fc4d8bb4750da62c89abba49 csi-local-pool-0 -wi-ao---- 10.00g   
   ```
   


<span id="PruHNorB"></span>
### PV reclaim


1. Delete the workload. After the pod has been deleted,

2. run the `lsblk` and `lvs` commands again. You can find that the LV has been reclaimed.

   ```Bash
   root@iv-yebwt6xkhsqb***:~# lsblk
   NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
   vda     254:0    0   40G  0 disk 
   ├─vda1  254:1    0  190M  0 part /boot/efi
   └─vda2  254:2    0 39.8G  0 part /
   vdb     254:16   0  100G  0 disk /mnt/vdb
   nvme0n1 259:0    0  3.5T  0 disk 
   root@iv-yebwt6xkhsqb***:~#
   root@iv-yebwt6xkhsqb***:~#
   root@iv-yebwt6xkhsqb***:~# lvs
   root@iv-yebwt6xkhsqb***:~#
   ```
   


&nbsp;
