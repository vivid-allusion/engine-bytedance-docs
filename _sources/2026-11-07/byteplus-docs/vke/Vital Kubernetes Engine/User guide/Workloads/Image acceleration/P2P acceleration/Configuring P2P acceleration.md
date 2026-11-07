---
title: "Configuring P2P acceleration"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/P2P-acceleration-solution"
---

This topic introduces how VKE, in combination with BytePlus CR, provides P2P acceleration capabilities by utilizing internal node network bandwidth to distribute images between nodes.

<span id="AbUjm3YA"></span>
## Recommendations

P2P acceleration speeds up pulling gigabyte\-sized container images in large\-scale clusters, supporting concurrent pulls from hundreds to thousands of nodes. Note the following recommendations:


* When you select a P2P cache disk type, we **recommend** **using local disks first**. If the region or ECS instance type does not support local disks, prioritize ESSD cloud disks. For performance information about different storage types, see [P2P acceleration performance reference](https://docs.byteplus.com/en/docs/vke/P2P_Performance_Testing?lang=en).

* We recommend creating a dedicated P2P cache node pool to isolate scheduling and seed caching capabilities from business workloads. This prevents the acceleration add\-on and business workloads from competing for resources such as nodes and networks, which may affect normal business operations. For details, see [Overview of P2P image acceleration](https://docs.byteplus.com/en/docs/vke/Overview-of-P2P-acceleration?lang=en).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For better image acceleration performance, we recommend using the image warm\-up feature to pre\-warm images on Seed Peer nodes. This allows P2P nodes to cache image data in advance, and you can then gradually expand the scale of image pulls.</div>


<span id="oRe8Ut1q"></span>
## Limits

When using cloud disks as P2P image cache disks, consider the following factors:


* Cloud disk specifications: The cloud disk type and capacity affect the throughput of an individual disk. For details, see [ESSD FlexPL](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume?lang=en) and [ESSD PL0](https://docs.byteplus.com/en/docs/ecs/esd_pl0_volume?lang=en).

* Total throughput of a cloud disk cluster: Confirm that the total throughput of the cloud disk cluster in the target region and availability zone meets the expected concurrent image pull requirements.

* Pressure on disks from workloads within the cluster: Avoid excessive read and write load on cloud disks during image pulling, as this may interrupt production workloads in the cluster and even affect other users in the region. If P2P acceleration causes excessive disk pressure, contact VKE support to configure an appropriate speed limit and then restart the p2p\-accelerator add\-on.


<span id="JM5uzhW0"></span>
## Prerequisites


* CR has been enabled. For details, see [What is CR?](https://docs.byteplus.com/en/docs/cr/what-is-cr?lang=en)

* A CR Standard Edition instance has been created and initialized. For details, see [Creating a standard instance](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only CR <strong>Standard Edition</strong> instances support P2P acceleration.   </div>
   

<span id="582ye9wN"></span>
## Procedure

<span id="zhuA3Wxi"></span>
### Step 1: Add cache disks to an existing node pool

<div data-tips="true" data-tips-type="warning">Note</div>


<div data-tips="true" data-tips-type="warning">The cache disk settings apply only to new nodes added to the node pool later. Cache disks are not automatically attached to existing nodes. To apply the settings to existing nodes, choose one of the following methods:</div>



* <div data-tips="true" data-tips-type="warning">Rotate existing nodes: Gradually replace existing nodes with new nodes. Cache disks are automatically attached to new nodes.</div>


* <div data-tips="true" data-tips-type="warning">Attach disks manually: Attach cache disks to existing nodes separately and configure the corresponding label without replacing the nodes. For details, see <a href="https://docs.byteplus.com/en/docs/90/21482#MtsTwkUb">Attaching cache disks to the existing node pool</a>.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the name of the target cluster to go to the management page of this cluster.

3. In the left navigation pane, choose **Image acceleration** to open the image acceleration configuration page.

4. On the image acceleration configuration page, select the target node pool, then click **Configure cache disk** in the **Actions** column.

5. In the pop\-up configuration page, add a new P2P cache disk for nodes.

6. Click **Confirm** to finish.

7. After configuration is complete, check the configuration of the corresponding node pool. You can see the newly added P2P cache disk mounted to the `/mnt/p2pcache` directory.


<span id="iYlUUdpT"></span>
### Step 2: (Optional) Create a dedicated cache node pool


1. On the image acceleration configuration page, click **Create a dedicated cache node pool** to go to the managed node pool configuration page.

2. The system automatically configures some parameters of the dedicated P2P cache node pool, as shown in the table below. For information about other parameters, see [Creating a managed node pool](https://docs.byteplus.com/en/docs/vke/Creating-a-managed-NodePool?lang=en).

   
   |Parameter |Description |
   |---|---|
   |**Node pool setting** ||
   |Name |The default is **p2p\-cachepool**. The node pool name must be unique within the cluster and can be modified as needed. Modifications do not affect the P2P cache feature. |
   |Billing methods |The default is **Pay\-as\-you\-go**. |
   |Enable management |The managed mode is enabled by default. In a managed node pool, the system manages the lifecycle of nodes, including node initialization, health checks, and fault replacement, eliminating the need for manual O&M. We recommend keeping the default setting. If you disable the managed mode, you need to handle node anomalies manually, which may affect the availability of the P2P cache service. |
   |Instance type |The system selects the **Local\-SSD** instance type by default and lists ECS instance specifications with 8 vCPUs and 16 GiB of memory or above. Local SSDs offer higher I/O performance and are suitable for high\-frequency read/write cache scenarios. We recommend prioritizing them. Select an appropriate instance type based on your cluster scale and expected volume of cached data.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If no Local\-SSD instance specifications are available in the current region, the system displays all instance types. Manually select the instance types that meet your requirements.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The instance specification of the selected instance type must have at least 8 vCPUs and 16 GiB of memory. Instances below this specification may result in insufficient cache performance.</div><br> |
   |Number of nodes |The default is 3, which means three dedicated P2P cache nodes are created. The number of nodes determines the number of cache replicas available in the cluster. We recommend keeping the default to ensure high availability of the cache service. |
   |**System configuration** ||
   |Storage |The system automatically creates a P2P cache disk for the node and mounts it to `/mnt/p2pcache` to persist P2P image cache data. If a single data volume does not provide sufficient cache capacity, click **Add data volume** to attach additional cache disks to the node. |
   |**Advanced settings** ||
   |Node labels |By default, the node pool is labeled with `vke.volcengine.com/p2p-cache-enabled=true`, indicating that this node pool is dedicated to P2P caching. The P2P components (Seed Peer and Scheduler) schedule cache data to the corresponding nodes based on this label. Other nodes in the cluster can obtain image data from these cache nodes through the P2P protocol, avoiding repeated back\-to\-origin pulls. |
   |Node taints |The taint `vke.volcengine.com/p2p-cache-enabled=true:NoSchedule` is added to the node pool by default. This isolates nodes dedicated to P2P caching, prevents business Pods from being scheduled to cache nodes, and avoids resource competition with the cache service. The P2P components (Seed Peer and Scheduler) are configured with corresponding toleration rules and can be scheduled to this node pool normally. |
   

3. After configuring other required parameters (such as the availability zone, subnet, and login password) and optional parameters, click **Confirm** to complete the configuration.


<span id="08JP4Z1f"></span>
### Step 3: Configure kubelet and containerd parameters


1. On the image acceleration configuration page, select the target node pool and click **Configure Kubelet/Containerd parameters** in the **Actions** column.

2. On the page that appears, configure the kubelet and containerd parameters for the node pool.

   
   |Parameter |Description |
   |---|---|
   | Sync data for existing nodes |Whether to synchronize custom kubelet and containerd parameters to existing nodes.<br><br><br>* Enabled: (Default) Custom kubelet and containerd parameters are synchronized to existing nodes, and custom parameters apply to all nodes in the node pool.<br><br>* Disabled: Custom kubelet and containerd parameters are not synchronized to existing nodes. Custom parameters apply only to new nodes, not to existing nodes. |
   |Kubelet parameters |Configure P2P acceleration\-related kubelet parameters, such as `image-gc-high-threshold-percent`, `image-gc-low-threshold-percent`, `image-maximum-gc-age`, `image-minimum-gc-age`, `registry-qps`, and `registry-burst`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The default parameter values displayed in the console may differ from those in the community, and pre\-filled values in the console do not indicate that the values have taken effect.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Confirm that the pre\-filled value of each parameter matches your actual environment. If necessary, modify them based on your actual needs. For detailed parameter descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool?lang=en">Configuring kubelet parameters for a node pool</a>.</div><br> |
   |Containerd parameters |Configure containerd parameters related to P2P acceleration. The parameters include `max_concurrent_downloads`, `max_concurrent_unpacks`, `concurrent_layer_fetch_buffer`, and `use_local_image_pull`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The containerd parameters that can be configured vary with the containerd version.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The default parameter values displayed in the console may differ from those in the community, and pre\-filled values in the console do not indicate that the values have taken effect.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Confirm that the pre\-filled value of each parameter matches your actual environment. If necessary, modify them based on your actual needs. For detailed parameter descriptions, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool?lang=en">Configuring kubelet parameters for a node pool</a>.</div><br> |
   

3. Click **Confirm** to finish.


<span id="Z1cTY7TF"></span>
### Step 4: Install the P2P acceleration add\-on

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If the p2p\-accelerator add\-on is already installed in your cluster, upgrade it to v2.0.0 or later.</div>



1. In the add\-on installation section of the image acceleration configuration page, click **Install**.

2. On the page that appears, configure and install the p2p\-accelerator add\-on. For detailed parameter descriptions, see [p2p-accelerator](https://docs.byteplus.com/en/docs/vke/p2p-accelerator-add-on?lang=en).


<span id="ic83vWZw"></span>
## Validate results

<span id="EQHRD81z"></span>
### Confirming configurations


1. After the configuration is complete, verify on the image acceleration configuration page that cache disks are configured for the cluster nodes, the dedicated P2P node pool exists, and the p2p\-accelerator add\-on is installed and running properly.

2. View the node details in the cluster. On the **Label** tab, confirm that the P2P acceleration\-related labels are effective.

   * For nodes in the dedicated P2P node pool, the label `vke.volcengine.com/p2p-cache-enabled=true` should exist.

   * For new nodes in the existing node pool, the label `vke.volcengine.com/p2p-cache-disk=true` should exist.


<span id="iYp9P5Sg"></span>
### Feature verification

After configuration is complete, create a workload in the cluster to pull images, then use the image acceleration dashboard in cloud\-native observability to confirm that the feature works properly.


1. Enable the image acceleration observability feature. For details, see [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability?lang=en).

2. Create a workload to trigger an image pull. For this example, a Deployment is created. For details, see [Creating a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment?lang=en).

3. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

4. In the left dashboard list, select **Image acceleration service monitoring** \> **Image acceleration monitoring** to view the P2P image acceleration monitoring dashboard. For details about the dashboard, see [Image acceleration observability](https://docs.byteplus.com/en/docs/vke/Image-acceleration-observability).


<span id="j2S1UV2H"></span>
## Other configurations

<span id="MtsTwkUb"></span>
### Mounting cache disks to existing nodes

Attaching cache disks to an existing node pool takes effect only for new nodes. For existing nodes, you need to configure this manually. Procedure:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">We recommend testing on a single node before performing batch operations.</div>



1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation pane, click **Storage** \> **Volumes**, then click **Create volume** to create a data volume.

3. Find the target volume and in the **Actions** column, click `...` \> **Attach** to attach the data volume to the corresponding VKE node. For details, see [Attaching volumes](https://docs.byteplus.com/en/docs/ecs/Attach-a-volume?lang=en).

4. After the volume is attached, [log in to the VKE node](https://docs.byteplus.com/en/docs/vke/Managing-nodes?lang=en#ecs-terminal) and run the following command to confirm the storage device name on the node.

   ```Bash
   lsblk -f
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">This topic uses the newly attached data volume <code>/dev/vdc</code> as an example. In your scenario, note the actual device name.   </div>
   

   The expected result is as follows:

   ```Bash
   NAME   FSTYPE LABEL UUID                             FSAVAIL FSUSE% MOUNTPOINT
   vda                                                                     
   ├─vda1 vfat         8038-E872                        184.1M     2% /boot/efi
   └─vda2 ext4         9fe1e649-af91-4241-ac59-a6f***   34.1G     9% /
   vdb    ext4         60396815-6cbd-42d7-9877-f97***   87.8G     5% /mnt/vdb
   vdc 
   ```
   

5. Run the following command to format the filesystem.

   ```Bash
   sudo mkfs.xfs /dev/vdc
   ```
   

   Expected output shows that formatting was successful.

   ```Bash
   meta-data=/dev/vdc               isize=512    agcount=4, agsize=655360 blks
            =                       sectsz=512   attr=2, projid32bit=1
            =                       crc=1        finobt=1, sparse=1, rmapbt=0
            =                       reflink=0
   data     =                       bsize=4096   blocks=2621440, imaxpct=25
            =                       sunit=0      swidth=0 blks
   naming   =version 2              bsize=4096   ascii-ci=0, ftype=1
   log      =internal log           bsize=4096   blocks=2560, version=2
            =                       sectsz=512   sunit=0 blks, lazy-count=1
   realtime =none                   extsz=4096   blocks=0, rtextents=0
   ```
   

6. Run the following command to create a cache directory and mount the data volume to this directory.

   ```Bash
   sudo mkdir -p /mnt/p2pcache
   sudo mount /dev/vdc /mnt/p2pcache
   df -hT /mnt/p2pcache
   ```
   

   After mounting is complete, check whether the mount is correct.

   ```Bash
   findmnt /mnt/p2pcache
   ```
   

   The expected output shows that the data volume is correctly mounted to the specified directory.

   ```Bash
   TARGET        SOURCE   FSTYPE OPTIONS
   /mnt/p2pcache /dev/vdc xfs    rw,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota
   ```
   

7. Configure automatic mounting of the data volume on system startup.

   1. Run the following command to obtain the filesystem UUID of the data volume.

   ```Bash
   sudo blkid /dev/vdc
   ```
   

   2. Run the following command to add the configuration item to `/etc/fstab`. You need to replace `<UUID>` with your actual value.

   ```Bash
   sudo echo "UUID=<UUID>  /mnt/p2pcache  xfs  defaults,nofail  0  2" >> /etc/fstab
   ```
   

   After configuration is complete, check whether the mount is correct.

   ```Bash
   findmnt /mnt/p2pcache
   ```
   

   The expected output shows that the data volume is correctly mounted to the specified directory.

   ```Bash
   TARGET        SOURCE   FSTYPE OPTIONS
   /mnt/p2pcache /dev/vdc xfs    rw,relatime,attr2,inode64,logbufs=8,logbsize=32k,noquota
   ```
   

8. Run the following command to configure the node label. In the command, `<node_name>` is the node name, for example, `192.168.1.10`.

   ```Bash
   kubectl label node <node_name> vke.volcengine.com/p2p-cache-disk=true --overwrite
   ```
   

   Confirm that the label is correctly configured and effective. In the command, `<node_name>` is the node name, for example, `192.168.1.10`.

   ```Bash
   kubectl get node <node_name> -L vke.volcengine.com/p2p-cache-disk
   ```
   

   The expected result is as follows:

   ```Bash
   NAME           STATUS                     ROLES    AGE   VERSION          P2P-CACHE-DISK
   192.168.1.10   Ready,SchedulingDisabled   <none>   22h   v1.34.6-vke.12   true
   ```
   

9. Run the following command to check whether the mount point is normal. In the command, `<node_name>` is the node name, for example, `192.168.1.10`.

   ```Bash
   kubectl debug node/<node_name> -it --image=doc-cn-beijing.cr.volces.com/vke/nginx-demo:v1.0 -- chroot /host df -h /mnt/p2pcache
   ```
   

   The following expected output indicates that the mount point on the node is normal.

   ```Bash
   Creating debugging pod node-debugger-192.168.1.10-kfz8z with container debugger on node 192.168.1.10.
   Warning: metadata.name: this is used in the Pod's hostname, which can result in surprising behavior; a DNS label is recommended: [must not contain dots]
   Filesystem      Size  Used Avail Use% Mounted on
   /dev/vdc        10G   43M   10G   1% /mnt/p2pcache
   ```
   


&nbsp;
