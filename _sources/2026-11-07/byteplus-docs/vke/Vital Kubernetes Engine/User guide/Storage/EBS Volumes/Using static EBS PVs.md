---
title: "Using static EBS PVs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes"
---

EBS is a high\-availability, high\-reliability, high\-performance, and elastically scalable block storage device that can be used as additional storage for VKE. EBS devices can be used as additional storage for VKE. This topic describes how to create a static PersistentVolume (PV) of the EBS type, as well as how a workload mounts and uses it.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-ebs add\-on has been installed. For details, see [Installing the add-on](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A volume that is not mounted to an ECS instance has been created. For details, see [Creating volumes](https://docs.byteplus.com/en/docs/ecs/Create-a-volume).

* To specify volume formatting parameters, the csi\-ebs add\-on must be upgraded to v1.3.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* (Optional) To configure the certificate via YAML, install kubectl in your local environment and connect it to the target cluster. For details, see [Connecting to a cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* You cannot mount and unmount volumes that use the subscription billing method. Do not change the volume billing method to subscription. For details, see [Volume FAQ](https://docs.byteplus.com/en/docs/ecs/Volume-faqs).

* You cannot mount a volume to multiple instances.

* Volumes are non\-shared storage devices and only support the ReadWriteOnce mode. This means that a volume can only be mounted by one pod in read\-write mode.

   * Each pod managed by a StatefulSet requires exclusive access to a volume. A manually created PersistentVolumeClaim (PVC) cannot be shared by all pods under a StatefulSet.

   * To mount a volume in a Deployment, the number of `replicas` must be set to 1. You cannot configure an independent PV for each pod. The priority order of mounting and unmounting operations cannot be guaranteed.

   * According to the upgrade policy for Deployments, when a pod is restarted, the pod may be unable to mount a volume for an extended period of time. Therefore, we recommend that you mount volumes only to StatefulSets.

* Volumes are categorized into multiple types and subject to the following usage limits:

   * Volumes can be mounted only if the volume type and the ECS instance specification match. For details, see [Instance specification introduction](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

   * A volume can only be mounted to an ECS instance in the same availability zone.

   * The maximum number of mountable EBS volumes per node is determined by the ECS instance specifications and the csi\-ebs add\-on configuration. To modify the number of node\-reserved volumes, adjust the csi\-ebs add\-on configuration.

      * When the **Node reserve volumes count** setting in the csi\-ebs add\-on configuration is empty, the system reserves 30% of the volumes for the system volume and data volumes. For example, if an ECS instance can be mounted to up to 16 volumes, VKE allows up to 12 volumes to be mounted, which is calculated by using the following formula: 16 × (1 \- 0.3).

      * When the **Node reserve volumes count** setting in the csi\-ebs add\-on configuration is explicitly configured, the system reserves data volumes according to the specified value. For example, if an ECS instance allows a maximum of 16 volumes, and the **Node reserve volumes count** is set to 1 in the csi\-ebs add\-on configuration, VKE allows mounting up to 15 volumes (16 \- 1).

* A csi\-ebs version that is earlier than v1.1.2 does not support third\-generation machines, such as g3i, c3i, or r3i. We recommend that you regularly upgrade the add\-on to the latest version. For details, see [Release notes of the csi-ebs add-on](https://docs.byteplus.com/en/docs/vke/csi-ebs).

* When you use EBS PVs, configuring `securityContext.fsGroup` in the application template causes kubelet to execute `chmod` and `chown` after PV mounting. This extends the time required for mounting.

* When you use a PV of the EBS type, if an unformatted disk is larger than 2 TiB, it will be formatted, extending the mounting time.


<span id=".6YCa6L-H5o6n5Yi25Y-w5L2_55So"></span>
## Configure through the console

<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5Y2377yIcHbvvIk="></span>
### Step 1: Create a PV


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |Creation method |Select a method for creating the PV. Currently, only **static creation** (manually created by the administrator) is supported. |
   |Name |Specify a name for the PV based on the system prompts. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **EBS**. |
   |Access mode |Select a PV access mode. You can select **ReadWriteOnce**, which allows read and write access by a single node. |
   |Cloud disk type |Select the volume type and performance level. Available volume types include:<br><br><br>* **ESSD**: Highly available, reliable, and scalable block storage devices. For a detailed description and a comparison of EBS volume types, see [EBS volume types](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* **Remote Elastic Disk**: Volumes that deliver high throughput, IOPS, and cost\-effectiveness. This type is suitable for storing temporary data.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Available volume types may vary by region. Select one from those displayed in the console.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Different ESSD performance levels provide varying specifications for metrics including maximum IOPS, maximum throughput, and latency.</div><br> |
   |Service\-side encryption |Whether to enable the server\-side encryption feature. If this feature is enabled, the system encrypts files during upload and decrypts files during download to protect data. |
   |EBS |Select an EBS volume, which should be in the same region and availability zone as the cluster, and is ready for mounting.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Ensure that the number of mounted EBS volumes on the node where the selected EBS volume is located does not exceed 10. Otherwise, after the PV is mounted to the workload, the pod cannot start successfully.</div><br> |
   |File system type |Choose the data type for storing data in EBS. Available options include **EXT4** and **XFS**. |
   |**Advanced settings** ||
   |Formatting parameters |Specify volume formatting parameters. The parameters take effect only if the volume is formatted for the first time. Dynamic modification is not supported. For details, see [Specifying formatting parameters](https://docs.byteplus.com/en/docs/vke/Configuring_formatting_parameters). |
   |Mount parameters |Specify volume mount parameters, which support dynamic modification and only take effect on newly mounted volumes instead of those already mounted. For details, see [Specifying mount parameters](https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters). |
   

5. Click **Confirm** to finish.


<span id=".5q2l6aqk5LiJ77ya5Yib5bu65a2Y5YKo5Y235aOw5piO77yIcHZj77yJ"></span>
### Step 2: Create a PVC


1. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolumeClaim**.

2. Click **Create PersistentVolumeClaim** and configure parameters on the page that appears.

   
   |**Parameter** |**Description** |
   |---|---|
   |Namespace |Select the namespace to which the PVC belongs. We recommend selecting a custom namespace or the system\-created **default** namespace. For details about namespaces, see [Namespace overview](https://docs.byteplus.com/en/docs/vke/Namespace-overview). |
   |Name |Specify a name for the PVC. The name must be unique within the cluster. |
   |StorageClass type |Select the storage type. In this scenario, select **EBS**. |
   |Access mode |Select a PVC access mode. You can select **ReadWriteOnce**, which allows read and write access by a single node. |
   |Billing type |Select a resource billing type as needed. Currently, pay\-as\-you\-go is supported. |
   |Cloud disk type |Select the volume type and performance level. Available volume types include:<br><br><br>* **ESSD**: Highly available, reliable, and scalable block storage devices. For a detailed description and a comparison of EBS volume types, see [EBS volume types](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br>* **Remote Elastic Disk**: Volumes that deliver high throughput, IOPS, and cost\-effectiveness. This type is suitable for storing temporary data.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Available volume types may vary by region. Select one from those displayed in the console.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Different ESSD performance levels provide varying specifications for metrics including maximum IOPS, maximum throughput, and latency.</div><br> |
   |Creation method |You can use one of the following methods to create a PVC: **Create based on StorageClass** and **Use an existing PersistentVolume**. For this example, select **Use an existing PersistentVolume**. |
   |PersistentVolume |Select the PV created in the previous step. |
   

3. Click **Confirm** to finish.


<span id=".5q2l6aqk5Zub77ya5bel5L2c6LSf6L295re75Yqg5Y23"></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet.

You can add a PV to a workload when creating it or updating it. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workload-overview).

<span id=".6YCa6L-HLWt1YmVjdGwt5ZG95Luk6KGM5L2_55So"></span>
## Use kubectl

If you have [connected to the cluster](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster), you can use the command\-line tool kubectl to configure static EBS PVs.

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LXB2"></span>
### Step 1: Create a PV


1. Create a YAML file for the PV. The following `pv-ebs-static.yaml` file serves as an example:

   
   <Tabs>
   <Tab zoneid="LOhaDLOv" title="Volumes of the ESSD type">
   <TabTitle>Volumes of the ESSD type</TabTitle>
   
   The following example demonstrates how to create a PV of type ESSD.
   
   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pv-ebs-static
   spec:
     accessModes:  # Required. The PV access mode. Only ReadWriteOnce is supported, which indicates read and write access from a single node.
     - ReadWriteOnce 
     capacity:
       storage: 20Gi # Required. The PV capacity. Unit: Gi. The value must be consistent with the capacity of the created volume.
     csi:
       driver: ebs.csi.volcengine.com # Required. The driver required for storage mount.
       fsType: ext4 # Required. The file system type. Valid values: ext4 and xfs.
       volumeAttributes:
         ChargeType: PostPaid # Required. The billing type. Only PostPaid is supported, which indicates pay-as-you-go.
         type: ESSD_FlexPL   # Required. The EBS volume type and performance level. For ESSD, performance levels ESSD_PL0 and ESSD_FlexPL are supported.
         extraPerformanceTypeId: IOPS # Optional. The extra performance type. Valid values: IOPS, Balance, and Throughput. This parameter takes effect only if the volume type is ESSD_FlexPL and the volume capacity is greater than or equal to 500 GB.
         extraPerformanceIOPS: "1000" # Optional. IOPS in the extra performance configurations. This parameter takes effect only if the extra performance type is IOPS or Balance. The value range is 1 to 50000.
         extraPerformanceThroughputMB: "100" # Optional. Throughput in the extra performance configurations. This parameter takes effect only if the extra performance type is Throughput.
         mkfsOptions: "-O bigalloc -C 16384" # Optional. The volume formatting parameters take effect if the volume is formatted for the first time. Dynamic modification is not supported.
         zone: cn-shanghai-a # Required. The availability zone of the created volume.
         encrypted: "true" # (Optional) Whether to enable cloud disk encryption. Value: true (enabled) or false (disabled, default value).
         kmsKeyId: fe98c63e-84ca-46e8-8301-4ffb1b****** # This parameter takes effect only when encrypted is set to true. The parameter is required when a custom key is used and must be set to the actual key ID configured for the cloud disk. If you do not specify this parameter, the default key is used.
       volumeHandle: vol-cmukmy9yi5bi254b**** # Required. The ID of the created volume.
     mountOptions: # Optional. The volume mount parameters, which support dynamic modification and only take effect on newly mounted disks, instead of those already mounted.
     - noatime
     - nodiratime
     - discard
     - nobarrier
     volumeMode: Filesystem # Required. The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="iJHhmwiO" title="Volumes of the TSSD type">
   <TabTitle>Volumes of the TSSD type</TabTitle>
   
   The following example demonstrates how to create a PV of type TSSD.
   
   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pv-ebs-static
   spec:
     accessModes:   # Required. The PV access mode. Only ReadWriteOnce is supported, which allows read and write access by a single node.
     - ReadWriteOnce
     capacity:
       storage: 20Gi  # Required. The capacity of the PV. Unit: Gi. The value must be consistent with the capacity of the created volume.
     csi:
       driver: ebs.csi.volcengine.com  # Required. The driver required for storage mount.
       fsType: ext4  # Required. The file system type. Currently, only ext4 and xfs are supported.
       volumeAttributes:
         ChargeType: PostPaid  # Required. The billing type. Only PostPaid is supported, which indicates pay-as-you-go.
         type: TSSD_TL0  # Required. The EBS volume type and performance level. For TSSD, only TSSD_TL0 is supported.
         extraPerformanceTypeId: Throughput # Optional. The extra performance type. TSSD volumes only support Throughput. This parameter takes effect if the volume capacity is greater than or equal to 100 GB.
         extraPerformanceThroughputMB: "20" # Optional. Throughput in the extra performance configurations.
         mkfsOptions: "-O bigalloc -C 16384" # Optional. The volume formatting parameters take effect if the volume is formatted for the first time. Dynamic modification is not supported.
         zone: cn-beijing-a # Required. The availability zone of the created volume.
       volumeHandle: vol-cmukmy9yi5bi254b****  # Required. The ID of the created volume.
     mountOptions: # Optional. The volume mount parameters, which support dynamic modification and only take effect on newly mounted disks, instead of those already mounted.
     - noatime
     - nodiratime
     - discard
     - nobarrier
     volumeMode: Filesystem  # Optional. The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="jlTPef82kf" title="RSSD volumes">
   <TabTitle>RSSD volumes</TabTitle>
   
   The following example demonstrates how to create a PV of type RSSD.
   
   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pv-ebs-static
   spec:
     accessModes:   # Required. The PV access mode. Only ReadWriteOnce is supported, which allows read and write access by a single node.
     - ReadWriteOnce
     capacity:
       storage: 20Gi  # Required. The capacity of the PV. Unit: Gi. The value must be consistent with the capacity of the created volume.
     csi:
       driver: ebs.csi.volcengine.com  # Required. The driver required for storage mount.
       fsType: ext4  # Required. The file system type. Currently, only ext4 and xfs are supported.
       volumeAttributes:
         ChargeType: PostPaid  # Required. The billing type. Only PostPaid is supported, which indicates pay-as-you-go.
         type: RSSD_RL0  # Required. The EBS volume type and performance level. For RSSD, only RSSD_RL0 is supported.
         mkfsOptions: "-O bigalloc -C 16384" # Optional. The volume formatting parameters take effect if the volume is formatted for the first time. Dynamic modification is not supported.
         zone: cn-beijing-a # Required. The availability zone of the created volume.
       volumeHandle: vol-cmukmy9yi5bi254b****  # Required. The ID of the created volume.
     mountOptions: # Optional. The volume mount parameters, which support dynamic modification and only take effect on newly mounted disks, instead of those already mounted.
     - noatime
     - nodiratime
     - discard
     - nobarrier
     volumeMode: Filesystem  # Optional. The PV type. Valid values: Filesystem (using the volume as a file system) or Block (using the volume as a block device).
   ```
   
   
   
   </Tab>
   </Tabs>
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteOnce is supported, which allows read and write access by a single node. |
   |storage |The capacity of the PV. Unit: Gi. The value must be consistent with the capacity of the created volume. |
   |driver |The driver required for PV mount. In this topic, you need to set the value to ebs.csi.volcengine.com, which indicates the csi\-ebs add\-on. |
   |fsType |The file system type. Only ext4 and xfs are supported. |
   |ChargeType |The billing type. It supports only PostPaid, which means pay\-as\-you\-go. |
   |type |The volume type. For a detailed description and a comparison of EBS volume types, see [EBS volume types](https://docs.byteplus.com/en/docs/ecs/Volume-specifications).<br><br><br>* For ESSD volumes, ESSD_PL0 and ESSD_FlexPL are supported.<br><br>* For TSSD volumes, TSSD_TL0 is supported.<br><br>* RSSD volumes support RSSD_RL0. |
   |extraPerformanceTypeId |The extra performance type. You can increase volume performance without increasing volume capacity.<br><br><br>* For ESSD volumes, IOPS, Balance, and Throughput are supported. This field takes effect only when the type is ESSD_FlexPL and the EBS capacity is greater than or equal to 500G. For different types of extra performance, see [ESSD FlexPL volumes](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume).<br><br>* For TSSD volumes, Throughput is supported. This parameter takes effect only if the volume capacity is greater than or equal to 100 GB.<br><br>* For RSSD volumes, this parameter is not supported. |
   |extraPerformanceIOPS |IOPS in the extra performance configurations. This parameter takes effect only if the extra performance type is IOPS or Balance. The value is an integer. Unit: operations per second. The value range is from 1 to 50000. |
   |extraPerformanceThroughputMB |The throughput of the extra performance configurations. This parameter takes effect only if the extra performance type is Throughput. The value is an integer. Unit: MB/s. Valid values: 0 to 650. |
   |mkfsOptions |The volume formatting parameters. For details, see [Specifying formatting parameters](https://docs.byteplus.com/en/docs/vke/Configuring_formatting_parameters).<br><br><br>* The parameters take effect only if the volume is formatted for the first time. Dynamic modification is not supported.<br><br>* You can specify multiple formatting parameters and need to separate them with spaces. For example, `"-O bigalloc -C 16384"`. |
   |zone |The ID of the availability zone for the volume. For details, see [Regions and availability zones](https://docs.byteplus.com/en/docs/ecs/Regions-and-Availability-Zones). |
   |encrypted |Whether to enable the cloud disk encryption feature. Valid values:<br><br><br>* **true**: Enable cloud disk encryption. After this feature is enabled, files on the data disk are stored in encrypted form, preventing unauthorized access to data at the storage layer and meeting data security compliance requirements.<br><br>* **false** (default): Disable cloud disk encryption. |
   |kmsKeyId |Configure the KMS key ID used for cloud disk encryption. This parameter must be set to the actual key ID configured for the cloud disk.<br><br><br>* This parameter takes effect only when `encrypted` is set to `true`.<br><br>* This parameter is required when you use a custom key. In this case, you need to specify the KMS key ID for encryption.<br><br>* If you do not specify this parameter, the default key is used. |
   |volumeHandle |The ID of the created volume. |
   |mountOptions |Volume mount parameters, which support dynamic modification and only take effect on newly mounted volumes instead of those already mounted. For details, see [Specifying mount parameters](https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters). |
   |volumeMode |The PV types. Valid values:<br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the PV as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   

2. Run the following command to create the PV.

   ```Bash
   kubectl apply -f pv-ebs-static.yaml
   ```
   


<span id=".5q2l6aqk5LqM77ya5Yib5bu6LXB2Yw=="></span>
### Step 2: Create a PVC


1. Create a YAML file for the PVC. The following `pvc-ebs-static.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: PersistentVolumeClaim
   metadata:
     name: pvc-ebs-static
     namespace: default
   spec:
     accessModes:  # PV access modes. You can specify only ReadWriteOnce, which allows read-write access by a single node. Keep it consistent with that in the PV configuration.
     - ReadWriteOnce
     resources:
       requests:
         storage: 20Gi # The declared storage capacity. Unit: Gi. The value must be consistent with the capacity of the created volume.
     volumeMode: Filesystem # The PV type. Valid values: Filesystem (using the PV as a filesystem) and Block (using the PV as a block device). The value must be consistent with the type configured in the PV.
     volumeName: pv-ebs-static # The name of the created PV.
   ```
   

   The key parameters are described in the following table.

   
   |Parameter |Description |
   |---|---|
   |accessModes |The PV access mode. Only ReadWriteOnce is supported, which allows read and write access by a single node. Keep it consistent with that in the PV configuration. |
   |storage |The declared storage capacity. Unit: Gi. The value must be consistent with the capacity of the created volume. |
   |volumeMode |The PV type. It must be consistent with the type configured for the PV.  <br><br><br>* **Filesystem**: (Default) Use the PV as a file system. The PV will be formatted and mounted to a file system (such as ext4 and xfs), and the file system will be mounted to a specified path in the container. You can use the `ls` command (such as `ls /data`) in the container to view the mounted directories or files, and directly read and write files.<br><br>* **Block**: Use the volume as a block device. It is directly exposed to the container without being formatted or mounted to a file system. You can perform operations on the block device by using paths such as `/dev/block/xxx`, and applications must support read and write operations on the raw block device. |
   |volumeName |The name of the PV, which must be consistent with the name configured for the PV. |
   

2. Run the following command to create the PVC.

   ```Bash
   kubectl apply -f pvc-ebs-static.yaml
   ```
   


<span id=".5q2l6aqk5LiJ77ya5Yib5bu6LWRlcGxveW1lbnQ="></span>
### Step 3: Create an application and mount the PV

After the PV is created, add it to a workload that will use it. Supported workloads include Deployment, StatefulSet, Job, CronJob, and DaemonSet. The following example uses a StatefulSet.


1. Create a YAML file for the StatefulSet. The following `statefulset-nginx-static.yaml` file serves as an example:

   ```YAML
   apiVersion: v1
   kind: Service
   metadata:
     name: statefulset-demo  # The headless service name.
     labels:
       app: demo
   spec:
     ports:
     - port: 80
       name: web
     clusterIP: None # When you configure a headless service, you need to set the value to None.
     selector:
       app: demo
   ---
   apiVersion: apps/v1
   kind: StatefulSet
   metadata:
     name: statefulset-demo
     namespace: default
   spec:
     replicas: 1 # When you mount a PV of the EBS type, the number of replicas for the workload must be 1.
     serviceName: statefulset-demo # The headless service name.
     selector:
       matchLabels:
         app: demo
     template:
       metadata:
         labels:
           app: demo
       spec:
         containers:
         - name: pod-demo # The container name.
           image: doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0
           ports:
           - containerPort: 80
             name: port
           volumeMounts:
           - name: pod-volume0 # The PV name, which must be consistent with the value of the volumes.name field.
             mountPath: /data # The mount location of the PV in the container.
         volumes:
           - name: pod-volume0 # The PV name. You can specify a custom name.
             persistentVolumeClaim:
               claimName: pvc-ebs-static  # The name of the created PVC.
         affinity:
           nodeAffinity:
             requiredDuringSchedulingIgnoredDuringExecution:
               nodeSelectorTerms:
               - matchExpressions:
                 - key: topology.kubernetes.io/zone
                   operator: In
                   values:
                   - cn-beijing-a # (Optional) Use affinity configurations. Specify the availability zone of the volume. You need to make sure that the pod and volume are in the same availability zone.
   ```
   

2. Run the following command to create the workload.

   ```Bash
   kubectl apply -f statefulset-nginx-static.yaml
   ```
   


<span id="Z0rJRxwJ"></span>
## Result validation

After creating a workload and mounting it to a PV as described in the preceding steps, you can verify the mounting status and persistent storage of the volume via the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec pod-demo-0 -- df | grep data
   ```
   

   The expected response is as follows.

   ```Bash
   /dev/vdc        20466256      24  20449848   1% /data
   ```
   

2. Check the mount path in the pod to view the data in the PV.

   ```Bash
   kubectl exec statefulset-demo-0 -- ls /data
   ```
   

   The expected response is as follows.

   ```Bash
   lost+found
   ```
   

3. Write a file to the PV.

   ```Bash
   kubectl exec statefulset-demo-0 -- touch /data/test
   ```
   

4. Delete the pod.

   ```Bash
   kubectl delete pod statefulset-demo-0
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After you delete the pod in the workload, the system will automatically create a pod. The name remains unchanged.   </div>
   

5. Check the mount path of the PV in the newly created pod.

   ```Bash
   kubectl exec statefulset-demo-0 -- ls /data
   ```
   

   The expected result is as follows. You can see that the file written to the PV still exists and is not deleted along with the pod. This indicates that persistent storage of data is achieved.

   ```Bash
   lost+found  
   test
   ```
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment)

* [Creating a StatefulSet](https://docs.byteplus.com/en/docs/vke/Creating-a-StatefulSet)

* [Creating a Job](https://docs.byteplus.com/en/docs/vke/Creating-a-Job)

* [Creating a CronJob](https://docs.byteplus.com/en/docs/vke/Creating-a-CronJob)

* [Creating a DaemonSet](https://docs.byteplus.com/en/docs/vke/Creating-a-DaemonSet)
