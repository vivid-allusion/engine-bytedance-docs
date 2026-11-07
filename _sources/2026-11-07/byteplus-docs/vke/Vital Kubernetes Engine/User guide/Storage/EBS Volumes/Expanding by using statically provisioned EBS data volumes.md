---
title: "Expanding by using statically provisioned EBS data volumes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Statically-expanding-EBS-Volumes"
---

As your business grows and application data expands, you can increase the Elastic Block Storage (EBS) volume capacity to meet increased storage demands. This topic describes the steps of expanding EBS capacity as statically provisioned PersistentVolumes (PV).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The csi\-ebs add\-on has already been upgraded to the latest version.

* EBS has been used as a statically provisioned PV. For details, see [Using statically provisioned EBS PV](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes).

*  Obtained the target volume ID to be expanded by using the `volumeHandle` value (for example, `volumeHandle: vol-k10sii****`) in the PV's YAML file for the pod.

* To avoid data loss caused by expansion failure, we recommend that you back up data in advance. For details, see [Using EBS snapshots](https://docs.byteplus.com/en/docs/vke/Using-EBS-volume-snapshots).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

This topic provides two volume expansion methods: expansion without application interruption and manual expansion with application interruption. You can select one that suits your scenario. The following are detailed descriptions and steps:

<span id=".5pa55byP5LiA77ya5LiN5pqC5YGc5bqU55So5a6e546w5Zyo57q_5omp5a65"></span>
### Method 1: Expansion without application interruption

This method does not restart the application during the storage expansion process, which ensures business continuity. However, if the I/O traffic of the file system is relatively high during expansion, there may be a risk of I/O errors in the file system.

<span id=".5q2l6aqk5LiA77ya5LqR55uY5pWw5o2u5Y235omp5a65"></span>
#### Step 1: Expand the EBS data volume


1. Log in to the [Elastic Compute Service (ECS) console](https://console.byteplus.com/ecs/instance). In the left navigation bar, click **Storage \> Volumes**. In the top menu bar, select the region of the target EBS volume.

2. On the volume management page, find the target volume and click **Extend** in the Actions column. Follow the steps of the volume expansion wizard to expand the volume.

3. In the Adjust capacity step, configure the **New capacity** field. Then, click **Extend volume**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The new capacity cannot be less than the current capacity.</div>


In this example, the volume `vol-k10sii****` is expanded from 100 GiB to 120 GiB.


4. In the Attach to Instance step, attach the volume to the instance and click **Next step**.

5. Click **Return to the volume list** to check the new capacity of the volume. This skips the Partition Disk and Create and Mount File Systems step. 


<span id=".5q2l6aqk5LqM77ya5paH5Lu257O757uf5omp5a65"></span>
#### Step 2: Expand the file system


1. Log in to the ECS instance where the target EBS volume is located. For details, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. (Optional) Run the `lsblk -f` command as the root user to check whether the target EBS volume has a file system created and a mount point assigned. As shown in the figure below, the `vdb` has a file system and mount point. If no `vdc` information is displayed, it does not have a file system.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_571588a014ccf37f3f1917bbf6835b5d.png) </span>

If the target EBS volume already has a file system, this step can be skipped. If the target EBS volume does not have a file system, run the following commands in sequence to create a file system for the EBS volume and mount it to a directory.

```bash
mkfs.ext4  /dev/vdc         # Create an ext4 file system for the EBS volume. /dev/vdc is the EBS device identifier.
mkdir /mnt/vdc              # Create a mount point.
mount /dev/vdc /mnt/vdc/    # Mount the EBS volume /dev/vdc to the /mnt/vdc/ folder.
```



3. Run the following command as the root user to view the status of the EBS volume.


```bash
fdisk -l                 # /dev/vda is the system volume. Volumes like /dev/vdb or /dev/vdc are data volumes. In this example, the target volume to be expanded is a data volume.
```


As shown in the figure below, the device identifier of the EBS volume expanded to 120 GiB in Step 1 is `/dev/vdb`. At this time, if you run the `df -Th` command, the file system is still 100 GiB.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9ee77e92a4b278168a23c73d7bd42bc.png) </span>


4. For example, if the `vdb` uses the ext4 file system, run the following command to expand the file system capacity.


```bash
resize2fs /dev/vdb       # /dev/vdb is the device identifier of the target data volume.
```


As shown in the figure below, the output matches expectations and no error is reported, indicating that the file system expansion was successful.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb816026583e496dd09f6407ac4b458d.png) </span>


4. Run the following command to view the result of the file system expansion.


```bash
df -Th 
```


As shown in the figure below, the `/dev/vdb` file system has been expanded to 120 GiB. Now the volume and file system are ready for use.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_231528420f3fa2fabaa9c296884a131f.png) </span>

<span id=".5pa55byP5LqM77ya5pqC5YGc5bqU55So5a6e546w5omL5Yqo5omp5a65"></span>
### Method 2: Manual expansion with application interruption

This method suspends disk I/O and makes file system expansion more secure. However, your application will experience a short downtime. Therefore, evaluate whether your business can tolerate this downtime before you perform this type of expansion.

<span id=".5q2l6aqk5LiA77ya5Yig6Zmk5bqU55SoLXBvZA=="></span>
#### Step 1: Delete the application pod


1. Suspend the application by deleting the StatefulSet or setting the number of replicas to 0. This scenario uses a MySQL application as an example. You can execute the following command to adjust the pod replica count to 0.


```bash
kubectl scale sts mysql --replicas=0
```


Expected output:

```bash
statefulset.apps/mysql scaled
```



2. Run the following command to check whether the pod has been deleted. No output indicates that the MySQL application has been deleted.


```bash
kubectl get pod | grep mysql
```


<span id=".5q2l6aqk5LqM77ya5LqR55uY5pWw5o2u5Y235omp5a65"></span>
#### Step 2: Expand the EBS data volume


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). In the left navigation bar, click **Storage \> Volumes**. In the top menu bar, select the region of the target EBS volume.

2. On the volume management page, find the target volume and click **Extend** in the Actions column. Follow the steps of the volume expansion wizard to expand the volume.

3. In the Adjust capacity step, configure the **New capacity** field. Then, click **Extend volume**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The new capacity cannot be less than the current capacity.</div>


In this example, the volume `vol-k10sii****` is expanded from 100 GiB to 120 GiB.


4. In the Attach to Instance step, attach the volume to the instance and click **Next step**.

5. Click **Return to the volume list** to check the new capacity of the volume. This skips the Partition Disk and Create and Mount File Systems step. 


<span id=".5q2l6aqk5LiJ77ya5paH5Lu257O757uf5omp5a65"></span>
#### Step 3: Expand the file system


1. Log in to the ECS instance where the target EBS volume is located. For details, see [Logging in to Linux instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. (Optional) Run the `lsblk -f` command as the root user to check whether the target EBS volume has a file system created and a mount point assigned. As shown in the figure below, the `vdb` has a file system and mount point. If no `vdc` information is displayed, it does not have a file system.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_571588a014ccf37f3f1917bbf6835b5d.png) </span>

If the target EBS volume already has a file system, this step can be skipped. If the target EBS volume does not have a file system, run the following commands in sequence to create a file system for the EBS volume and mount it to a directory.

```bash
mkfs.ext4  /dev/vdc         # Create an ext4 file system for the EBS volume. /dev/vdc is the EBS device identifier.
mkdir /mnt/vdc              # Create a mount point.
mount /dev/vdc /mnt/vdc/    # Mount the EBS volume /dev/vdc to the /mnt/vdc/ folder.
```



3. Run the following command as the root user to view the status of the EBS volume.


```bash
fdisk -l                 # /dev/vda is the system volume. Volumes like /dev/vdb or /dev/vdc are data volumes. In this example, the target volume to be expanded is a data volume.
```


As shown in the figure below, the device identifier of the EBS volume expanded to 120 GiB in Step 1 is `/dev/vdb`. At this time, if you run the `df -Th` command, the file system is still 100 GiB.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9ee77e92a4b278168a23c73d7bd42bc.png) </span>


4. For example, if the `vdb` uses the ext4 file system, run the following command to expand the file system capacity.


```bash
resize2fs /dev/vdb       # /dev/vdb is the device identifier of the target data volume.
```


As shown in the figure below, the output matches expectations and no error is reported, indicating that the file system expansion was successful.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cb816026583e496dd09f6407ac4b458d.png) </span>


4. Run the following command to view the result of the file system expansion.


```bash
df -Th 
```


As shown in the figure below, the `/dev/vdb` file system has been expanded to 120 GiB. Now the volume and file system are ready for use.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_231528420f3fa2fabaa9c296884a131f.png) </span>

<span id=".5q2l6aqk5Zub77ya6YeN5ZCv5bqU55So"></span>
#### Step 4: Restart the application


1. Run the following command to adjust the pod replica count to 2.


```bash
kubectl scale sts mysql --replicas=2
```


Expected output:

```bash
statefulset.apps/mysql scaled
```



2. Run the following command to check whether the pod has been restored. The following expected output shows that the MySQL application has been restored.


```bash
kubectl get pod | grep mysql
```


Expected output:

```bash
NAME           READY   STATUS    RESTARTS   AGE
mysql-0        1/1     Running   0          74s
mysql-1        1/1     Running   0          42s
```



3. Execute the following command to view the file system size. The following expected output shows that the storage capacity of the `/dev/vdb` file system is 120 GiB.


```bash
kubectl exec mysql-0 -- df /data
```


Expected output:

```bash
Filesystem      1K-blocks  Used     Available   Use%   Mounted on
/dev/vdb        12330192   180114   123084512   1%     /data
```


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

For more information on EBS volume expansion, see [Expanding EBS capacity](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux).
