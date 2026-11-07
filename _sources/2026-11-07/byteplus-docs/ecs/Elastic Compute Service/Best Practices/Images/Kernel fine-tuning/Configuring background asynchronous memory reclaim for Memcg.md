---
title: "Configuring background asynchronous memory reclaim for Memcg"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring_background_asynchronous_memory_reclaim_for_Memcg"
---

Memcg asynchronous memory reclaim is an enhanced feature provided by the veLinux kernel on top of the standard Memory Cgroup. This topic describes the working principle, configuration, and query methods of this feature, helping you reduce the impact of memory reclaim on request latency in latency\-sensitive workloads through background asynchronous reclaim.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Memcg asynchronous memory reclaim does not increase the <code>cgroup</code> memory limit and cannot replace memory management on the application side. If a workload consistently approaches or exceeds its memory limit (<code>memory.limit_in_bytes</code>), you still need to address it through capacity evaluation, cache limit management, memory leak troubleshooting, and <code>cgroup limit</code> adjustment.</div>


<span id="1KhR3hZk"></span>
## Background

Memory Cgroup (Memcg) is the memory subsystem of Linux kernel control groups (cgroups). It isolates the memory behaviors of a group of processes from the rest of the system, and tracks and limits their memory usage. Common use cases include isolating memory\-intensive applications, setting memory quotas for containers or VMs, and preventing a single workload from exhausting the memory of an entire node. [Learn more](https://docs.kernel.org/admin-guide/cgroup-v1/memory.html)


* **Direct memory reclaim**: When Memcg usage reaches its limit, the kernel reclaims memory synchronously on the memory allocation path of the application thread. The thread is blocked during reclaim. Under high memory pressure, this manifests as tail latency jitter, increased memory allocation latency, and occasional service stalls.

* **Asynchronous memory reclaim**: Two memory watermarks, `low` and `high`, are configured for the `cgroup`. When available memory drops to the `low` watermark, Memcg wakes up a background `kworker` thread to reclaim memory asynchronously until available memory recovers to the `high` watermark. The reclaim process does not occupy the memory allocation path of application threads, so threads continue running without being blocked. Memory is freed before usage reaches the limit, **reducing the likelihood of direct memory reclaim being triggered** (though it cannot be guaranteed to be completely avoided) and minimizing request latency jitter.


<span id="FLpxKkZ3"></span>
## Applicable scenario

Memcg asynchronous memory reclaim is suitable when a workload uses Memcg for memory isolation and exhibits any of the following symptoms under high memory pressure:


* Noticeable jitter in request tail latency (P99, P999).

* Increased latency in memory allocation (page fault, malloc).

* Occasional service stalls despite available CPU and I/O headroom on the node.


This feature is especially suitable for workloads that are **latency\-sensitive, experience significant memory allocation bursts, or require memory isolation between containers or process groups**, such as online services, cache services, and real\-time data processing.

<span id="UaitfQA5"></span>
## Usage notes


|Item |Description |
|---|---|
|Kernel version |veLinux kernel versions that support this feature:<br><br><br>* veLinux:<br><br>   * 5.4.250\-1\-velinux1 and later<br><br>   * 5.15.152.ve.7u1 and later<br><br>* veLinux CentOS Compatible:<br><br>   * 5.4.250\-1.ve1 and later<br><br>   * 5.15.152\-7.1.ve2 and later<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the <code>memory.watermark_scale_factor</code> or <code>memory.watermark</code> interface, or the corresponding <code>sysctl</code> parameter does not exist in your instance operating system, the current kernel version does not support or has not enabled this feature.</div><br> |
|Cgroup version |`cgroup v1` and `cgroup v2` are supported.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If your operating system uses <code>cgroup v2</code>, we recommend referring to the <a href="https://engineering.fb.com/2022/06/20/data-infrastructure/transparent-memory-offloading-more-memory-at-a-fraction-of-the-cost-and-power/">Linux community solution</a> first and using the <code>memory.reclaim</code> interface to flexibly control reclaim timing and the amount of memory reclaimed. This helps maximize memory utilization and minimize the impact of memory reclaim.</div><br> |
|Risk warning |The asynchronous reclaim feature is **triggered automatically when memory watermarks reach the configured thresholds**. **It does not evaluate the appropriateness of the current reclaim timing or the amount of memory reclaimed**, and may still have some impact on workload latency. |


<span id="hFOEty6D"></span>
## Procedure

<span id="0kzSa4XI"></span>
### Configuration recommendations

We recommend that you first use the `cgroup` interface to enable asynchronous memory reclaim for the target workload on a canary basis. After verifying the gains and CPU overhead, use `sysctl` (configuration file) to persist the default values for subsequently created `cgroups`. Configure via kernel boot parameters only when the workload requires **default values to be applied automatically at boot time**.


|**Configuration item** |**Recommendation** |
|---|---|
|Watermark ratio |Start with a small value on a canary basis, for example, `100`. If direct memory reclaim remains frequent, gradually increase the ratio. If CPU overhead increases or reclaim becomes too frequent, decrease the ratio. |
|Enablement scope |We recommend enabling the feature individually for **latency\-sensitive Memcgs where memory reclaim jitter has already been observed** (via the `cgroup` interface). Enabling it globally via `sysctl` or kernel boot parameters is not recommended. |
|Reclaim concurrency |Keep the default value of `1`. If you need to increase it, verify the CPU overhead and workload latency in a test environment first. |


<span id="Ridoz8gL"></span>
### Configuration methods


<Tabs>
<Tab zoneid="M2r5a1XjIW" title="Configure via the cgroup interface">
<TabTitle>Configure via the cgroup interface</TabTitle>

This method applies only to **a single existing Memcg**. Changes take effect immediately after configuration and are lost when the system restarts or the `cgroup` is recreated. It is suitable for enabling the feature on a canary basis for individual latency\-sensitive workloads, and then expanding the scope after verifying tail latency gains and CPU overhead.


1. Execute the following command to query the watermark ratio and actual watermark of a single existing Memcg.

   
   <Tabs>
   <Tab zoneid="ikKhb1sq57" title="Cgroup v1">
   <TabTitle>Cgroup v1</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Replace <code><memcg_path></code> with the actual path of the target Memcg.</div>
   
   
   ```Bash
   cat /sys/fs/cgroup/memory/<memcg_path>/memory.watermark_scale_factor
   cat /sys/fs/cgroup/memory/<memcg_path>/memory.watermark
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="QlaCL1fS9K" title="Cgroup v2">
   <TabTitle>Cgroup v2</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Replace <code><cgroup_path></code> with the actual path of the target Cgroup.</div>
   
   
   ```Bash
   cat /sys/fs/cgroup/<cgroup_path>/memory.watermark_scale_factor
   cat /sys/fs/cgroup/<cgroup_path>/memory.watermark
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   

   **Interface description:** 

   
   |**Interface** |**Attribute** |**Default value** |**Description** |
   |---|---|---|---|
   |`memory.watermark_scale_factor` |Read/write |0 |Configure the watermark ratio for the current Memcg. Valid values `range from 0 to 1000`.<br><br><br>* A value of `0` disables asynchronous reclaim for the `cgroup`.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_970ee293df2b892012026adbee789d33.png) </span><br><br>* A value of `1000` sets the `low` watermark to **10%**  of `memory.limit_in_bytes`, and the `high` watermark to **twice** the `low` watermark.<br><br>   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d7d575cdc4e5b9172f2676355d8215c.png) </span> |
   |`memory.watermark` |Read\-only |0 |View the calculated `low` and `high` watermark values for the current `cgroup` to verify that the configuration has taken effect.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_af4328fecb92f45d4cd5ae6b3dd19d64.png) </span> |
   

2. Execute the following command to configure the watermark ratio for the specified Memcg.

   
   <Tabs>
   <Tab zoneid="DEaJfGusUB" title="Cgroup v1">
   <TabTitle>Cgroup v1</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Replace <code><memcg_path></code> with the actual path of the target Memcg, and replace <code>100</code> with the desired value.</div>
   
   
   ```Bash
   echo 100 > /sys/fs/cgroup/memory/<memcg_path>/memory.watermark_scale_factor
   ```
   
   
   
   
   
   </Tab>
   <Tab zoneid="uCYhrlFAKd" title="Cgroup v2">
   <TabTitle>Cgroup v2</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="0">tip</div>
   
   
   <div data-tips="true" data-tips-type="default" data-wrapper-indent="0">Replace <code><cgroup_path></code> with the actual path of the target Cgroup, and replace <code>100</code> with the desired value.</div>
   
   
   ```Bash
   echo 100 > /sys/fs/cgroup/<cgroup_path>/memory.watermark_scale_factor
   ```
   
   
   
   
   
   </Tab>
   </Tabs>
   


</Tab>
<Tab zoneid="hn34A9H8mC" title="Configure global sysctl parameters">
<TabTitle>Configure global sysctl parameters</TabTitle>

This method sets the global default values for subsequently created Memcgs and does not affect existing `cgroups`. It is suitable for applying uniform default values to new workloads after canary validation has passed.


1. Execute the following commands to query the global default watermark ratio and the maximum concurrency of `memcg kworkers` for subsequently created Memcgs.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The sysctl query result represents only the global default values and does not indicate that asynchronous reclaim has been enabled for existing Memcgs. To verify the actual configuration of an existing <code>cgroup</code>, use the <code>cgroup</code> interface to query.   </div>
   

   ```Bash
   cat /proc/sys/vm/memcg_watermark_scale_factor
   cat /proc/sys/vm/memcg_mem_reclaim_wq_max_active
   ```
   

2. Select a configuration method as needed to set the global default values for subsequently created Memcgs.

   
   <Tabs>
   <Tab zoneid="pVgBPIajNR" title="Configuration by using the proc interface">
   <TabTitle>Configuration by using the proc interface</TabTitle>
   
   Execute the following commands on the target Linux instance to configure the `memcg_watermark_scale_factor` and `memcg_mem_reclaim_wq_max_active` parameter values via the proc interface.
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="tip">This method allows configuration changes to be made and applied while the system is running. However, <strong>the configuration will reset after an operating system restart</strong> and must be reconfigured.</div>
   
   
   * <div data-tips="true" data-tips-type="tip">The following commands set the default watermark ratio for subsequently created Memcgs to <code>100</code> and set the maximum concurrency of <code>memcg kworkers</code> per NUMA node to <code>1</code>. Replace the values as needed.</div>
   
   
   
   ```Bash
   echo 100 > /proc/sys/vm/memcg_watermark_scale_factor
   echo 1 > /proc/sys/vm/memcg_mem_reclaim_wq_max_active
   ```
   
   
   **Interface description:** 
   
   
   |**Interface** |**Default value** |**Description** |
   |---|---|---|
   |`/proc/sys/vm/memcg_watermark_scale_factor` |0 |Configure the default watermark ratio for subsequently created Memcgs. Modifying this parameter does not affect existing Memcgs. |
   |`/proc/sys/vm/memcg_mem_reclaim_wq_max_active` |1 |Configure the maximum number of concurrent `memcg kworker` threads. The default value of `1` means that at most one `memcg kworker` runs concurrently per NUMA node. |
   
   
   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_450e041ff63e48660c99dc4cedff99ac.png) </span>
   
   
   </Tab>
   <Tab zoneid="ksmLdAb6vk" title="Configure by using the sysctl file">
   <TabTitle>Configure by using the sysctl file</TabTitle>
   
   1. Configure Memcg watermarks via the `sysctl` configuration file.
   
      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
      
   
      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This method requires an operating system restart for the configuration to take effect.<strong> Once the operating system restarts, the configuration persists</strong> and does not need to be reconfigured.   </div>
      
   
      1. Execute the following command to open the /etc/sysctl.conf file.
   
         ```Bash
         vim /etc/sysctl.conf
         ```
         
   
      2. Press the `i` key to enter edit mode, and add or update the following parameters.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following configurations set the default watermark ratio for subsequently created Memcgs to <code>100</code> and set the maximum concurrency of <code>memcg kworkers</code> per NUMA node to <code>1</code>. Replace the values as needed.      </div>
         
   
         ```Bash
         vm.memcg_watermark_scale_factor = 100
         vm.memcg_mem_reclaim_wq_max_active = 1
         ```
         
   
      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.
   
   2. Execute the following command to make the configuration take effect.
   
      ```Bash
      sudo sysctl -p
      ```
      
   
      ### <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c9fa9b31cffb02b95230ba68428824df.png) </span>    <span id="oQAUCtQ6"></span>
   
   
   </Tab>
   </Tabs>
   


</Tab>
<Tab zoneid="F9xWpFjihC" title="Configure kernel boot parameters">
<TabTitle>Configure kernel boot parameters</TabTitle>

This method sets the global default watermark ratio during system boot, applying it to subsequently created Memcgs. It takes effect after the instance is restarted and persists across restarts. It is suitable for scenarios where default configuration should be applied automatically at system boot.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying the GRUB configuration file is a <strong>high\-risk</strong> operation. Incorrect configuration may prevent the system from starting normally. Back up the original configuration file before proceeding, and verify the changes in a test environment before applying them to a production environment.</div>



1. Execute the following command to back up the GRUB configuration file.

   ```Bash
   sudo cp /etc/default/grub /etc/default/grub.bak
   ```
   

2. Execute the following command to check whether the asynchronous memory reclaim parameters already exist in the GRUB configuration file.

   ```Bash
   grep 'memcg_watermark_scale_factor' /etc/default/grub
   ```
   

   **Parameter descriptions:** 

   
   |**Parameter​**  |**Description** |
   |---|---|
   |`memcg_watermark_scale_factor=` |Set the global Memcg watermark ratio at system boot. This is equivalent to calling the `sysctl` interface `/proc/sys/vm/memcg_watermark_scale_factor`, and applies to subsequently created Memcgs. |
   

   * If the output is empty, execute the following command to append the `memcg_watermark_scale_factor` parameter.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>100</code> with the target watermark ratio value.      </div>
      

      ```Bash
      sudo sed -i '/^GRUB_CMDLINE_LINUX=/s/\"$/ memcg_watermark_scale_factor=100\"/' /etc/default/grub
      ```
      

   * If the output is not empty, execute the following command to update the `memcg_watermark_scale_factor` parameter value.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>100</code> with the target watermark ratio value.      </div>
      

      ```Bash
      sudo sed -i 's/memcg_watermark_scale_factor=[^ "]*/memcg_watermark_scale_factor=100/' /etc/default/grub
      ```
      

3. Execute the following command to persist the parameter configuration to the GRUB configuration file.

   
   <Tabs>
   <Tab zoneid="SiaJmQD0QT" title="veLinux">
   <TabTitle>veLinux</TabTitle>
   
   * Legacy boot mode
   
      ```Bash
      grub-mkconfig -o /boot/grub2/grub.cfg
      ```
      
   
   * UEFI boot mode
   
      ```Bash
      grub-mkconfig -o /boot/efi/EFI/debian/grub.cfg
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="J6Lz49u6aF" title="veLinux CentOS Compatible">
   <TabTitle>veLinux CentOS Compatible</TabTitle>
   
   * Legacy boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      
   
   * UEFI boot mode
   
      ```Bash
      grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


</Tab>
</Tabs>
