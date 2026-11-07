---
title: "How do I obtain node information of a cluster?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How_do_obtain_node_information_of_a_cluster"
---

When an exception occurs in node resources in a VKE cluster, you can use the diagnosis feature provided by the AIOps Suite to locate issues in cluster nodes. For details, see [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis). If the node diagnosis feature does not meet your business requirements, you can use a script on the abnormal node to collect key node information. This facilitates subsequent diagnosis of node failures.

<span id="cglBi3x9"></span>
## Prerequisites


* To save node information in TOS, create a TOS bucket first. For details, see [Creating buckets](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).

* The TOS bucket needs to be in the same region as the cluster.


<span id="T7ci0Wx4"></span>
## Procedure

<span id="k4KD0kDZ"></span>
### Step 1: Obtain the information collection script


1. Use **ECS Terminal** to log in to the node. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to download the information collection script.

   ```Bash
   curl -O https://vke-diagnostics-cn-beijing.tos-cn-beijing.volces.com/node_diagnostics.sh
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The command for obtaining the node information collection script varies based on different regions where your cluster is deployed and public network access statuses.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When your cluster is deployed in the <strong>China (Beijing)</strong> region, you can directly run the preceding command to obtain the script.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When your cluster is deployed in other regions:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If <strong>Public NAT for internet endpoint</strong> is enabled for your cluster, you can directly run the preceding command to obtain the script.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If <strong>Public NAT for internet endpoint</strong> is not enabled for your cluster, replace the public domain name (<code>volces.com</code>) in the preceding command with the private domain name (<code>ivolces.com</code>), and replace RegionID with the RegionID of your cluster. For example, when your cluster is deployed in the <strong>China (Shanghai)</strong> region, you need to modify the command to <code>curl -O https://vke-diagnostics-cn-shanghai.tos-cn-shanghai.ivolces.com/node_diagnostics.sh</code>. For more information about regions where VKE is available, see <a href="https://docs.byteplus.com/en/docs/vke/Regions-and-Availability-Zones">Regions and availability zones</a>.   </div>
   

3. Run the following command to grant execution permissions to the script.

   ```Bash
   chmod +x node_diagnostics.sh
   ```
   


<span id="MBAMmCUm"></span>
### Step 2: Run the information collection script


1. (Optional) Run the following command to configure the modules for information collection. If no modules are configured, all information related to nodes will be collected.

   ```Bash
   bash node_diagnostics.sh --modules ${module-name-1},${module-name-2}
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can run the <code>bash node_diagnostics.sh --modules-list</code> command to view all available modules. For example, to collect only network and memory information, configure the command <code>bash node_diagnostics.sh --modules network,memory</code>.   </div>
   

2. (Optional) Specify the location where the collected results are stored. To save collected results in TOS, run the following command to configure the AK/SK environment variables for your BytePlus account. If you do not specify a location, the collected information will be saved in the local path of the node.

   ```Bash
   export ACCESS_KEY_ID=${your_ak}
   export ACCESS_KEY_SECRET=${your_sk}
   ```
   

   The following table describes the parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |ACCESS_KEY_ID |The AK of your BytePlus root user. For instructions on obtaining the AK, see [Access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
   |ACCESS_KEY_SECRET |The SK of your BytePlus root user. For instructions on obtaining the SK, see [Access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey). |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Make sure that the account to which the AK/SK belongs has write permissions on the TOS bucket. Otherwise, the collected information will fail to be written. For TOS permission descriptions, see <a href="https://docs.byteplus.com/en/docs/tos/docs-overview_6">IAM policy overview</a>.   </div>
   

3. Run the collection script.

   * Use the following command to run the script and save the result locally. The file path is `/tmp/{hostname}_{timestamp}`.

      ```Bash
      bash node_diagnostics.sh
      ```
      

   * Use the following command to run the script and save the result in the TOS bucket.

      ```Bash
      bash node_diagnostics.sh --bucket my-bucket --region cn-beijing
      ```
      

      The following table describes the parameters.

      
      |**Parameter** |**Description** |
      |---|---|
      |\-\-bucket |The TOS bucket name. |
      |\-\-region |The RegionID of the TOS bucket. |
      


<span id="L6K06FiS"></span>
## Validating results


1. After the script is run, the system displays the following example. The name of the generated log file is unique each time the diagnosis script is run. This topic uses `iv-yeheeqetq8ug9cb7s1ki_20260309202204.tar.gz` as an example. The actual result depends on the actual environment.

   ```Bash
   ...
   [Mon Mar  9 14:54:42 2026] intel_pstate: CPU model not supported
   [Mon Mar  9 14:54:42 2026] ledtrig-cpu: registered to indicate activity on CPUs
   [Mon Mar  9 14:54:42 2026] drop_monitor: Initializing network drop monitor service
   [Mon Mar  9 14:54:42 2026] NET: Registered protocol family 10
   [Mon Mar  9 14:54:42 2026] Segment Routing with IPv6
   [Mon Mar  9 14:54:42 2026] mip6: Mobile IPv6
   [Mon Mar  9 14:54:42 2026] NET: Registered protocol family 17
   [Mon Mar  9 14:54:42 2026] mpls_gso: MPLS GSO support
   [Mon Mar  9 14:54:42 2026] IPI shorthand broadcast: enabled
   [Mon Mar  9 14:54:42 2026] sched_clock: Marking stable (1154488504, 106307620)->(1374330680, -113534556)
   [Mon Mar  9 14:54:42 2026] registered taskstats version 1
   [Mon Mar  9 14:54:42 2026] Loading compiled-in X.509 certificates
   [Mon Mar  9 14:54:42 2026] zswap: loaded using pool lzo/zbud
   [Mon Mar  9 14:54:42 2026] page_owner is disabled
   ...
   ```
   

2. Run the following command to access the node information folder and view the information collected from different modules.

   ```Bash
   cd iv-yeheeqetq8ug9cb7s1ki_20260309202204/
   ls -l
   ```
   

   The expected result is as follows:

   ```Bash
   total 60
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 cloud_init
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 disk
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 dmesg
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 gpu
   -rw-r--r-- 1 root root  128 Mar  9 20:22 instance
   drwxr-xr-x 5 root root 4096 Mar  9 20:22 kubernetes
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 memory
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 mgpu
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 network
   drwxr-xr-x 3 root root 4096 Mar  9 20:22 process
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 service
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 syslog
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 system_info
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 throttling
   drwxr-xr-x 2 root root 4096 Mar  9 20:22 top
   ```
   

3. View the detailed information collected by the specified module. This topic uses disk information as an example.

   ```Bash
   cat disk/df
   ```
   

   The expected result is as follows:

   ```Bash
   -----------------run df -Th------------------
   Filesystem     Type      Size  Used Avail Use% Mounted on
   udev           devtmpfs  7.7G     0  7.7G   0% /dev
   tmpfs          tmpfs     1.6G   43M  1.5G   3% /run
   /dev/vda2      ext4       40G  3.1G   35G   9% /
   tmpfs          tmpfs     7.7G     0  7.7G   0% /dev/shm
   tmpfs          tmpfs     5.0M     0  5.0M   0% /run/lock
   tmpfs          tmpfs     7.7G     0  7.7G   0% /sys/fs/cgroup
   ...
   ```
