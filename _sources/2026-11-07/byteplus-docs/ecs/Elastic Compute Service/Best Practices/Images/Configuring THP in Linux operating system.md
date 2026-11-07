---
title: "Configuring THP in Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-transparent-huge-pages"
---

This topic describes how to configure transparent huge pages (THP) for an instance running the Linux operating system.

<span id=".5YWz5LqO6YCP5piO5aSn6aG1"></span>
## About THP

THP is a Linux memory management system. It uses larger memory pages to reduce the overhead of Translation Lookaside Buffer (TLB) lookups on machines with large memory.

<span id=".5L2_55So6YCP5piO5aSn6aG155qE5LyY54K5"></span>
### Advantages of using THP

THP reduces TLB misses and page faults, thereby improving performance. Example:

The application requires 2 MB of memory. If the operating system uses 4 KB as the paging unit, 512 pages are required. Consequently, 512 entries are required in the TLB and 512 page table entries are also required. The operating system must experience at least 512 TLB misses and 512 page faults to fully map the 2 MB application space to physical memory.

However, when the operating system adopts 2 MB as the basic paging unit, only 1 TLB miss and 1 page fault are required to establish the virtual mapping for the application space. Moreover, no additional TLB misses or page faults will occur during the operation (assuming no TLB entry replacement or swap takes place).

<span id=".5L2_55So6YCP5piO5aSn6aG155qE57y654K5"></span>
### Disadvantages of using THP


* Internal fragmentation. When a transparent huge page is used, internal fragmentation occurs. For example, if an application requiring only 1 byte of data is allocated a 2 MB huge page, internal fragmentation occurs.

* Increased page fault handling latency. Although THP reduces the number of page faults, larger pages take more time to transfer from the disk. This leads to increased latency in page fault handling. Meanwhile, it also takes longer to zero out huge pages.

* Memory access performance degradation caused by locking in the memory path. When the khugepaged process scans the process memory and merges 4 KB pages into huge pages, various memory allocation activities for the target memory require different memory locks. This directly affects the memory access performance of the program. Additionally, this process is transparent to the application and cannot be controlled at the application level. For programs optimized specifically for 4 KB memory pages, this may cause random performance degradation.

* System resources occupied by background tasks. When the system lacks sufficient contiguous memory, it triggers memory compression and memory reclamation. These operations ultimately lead to a decline in system performance.


<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The impact of THP on system performance varies by scenario. You can decide whether to enable THP based on your scenario.

<span id=".U1BFQ2piYuKTh-WcuuaZrw=="></span>
### SPECjbb<sup>Ⓡ</sup> scenarios

In scenarios such as the Java Server Business Benchmark (SPECjbb), which is developed by the Standard Performance Evaluation Corporation (SPEC), applications require large memory. In such scenarios, using a larger page granularity to map memory helps boost the hit rate in the TLB, making this approach beneficial for performance. For memory\-intensive workloads, enabling THP may yield significant performance gains.

<span id=".5pWw5o2u5bqT5Zy65pmv"></span>
### Database scenarios

Databases typically have sparse rather than contiguous memory access patterns. As a result, their workloads usually perform poorly when THP is enabled. For example, when you run MongoDB on Linux, you should disable THP to achieve optimal performance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YWN572u6YCP5piO5aSn6aG1"></span>
### Enable/disable THP


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. View the status of the THP feature.

   Execute the following command to view the feature status.

   ```Plain Text
   cat /sys/kernel/mm/transparent_hugepage/enabled
   ```
   

   Example:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a8aff6aa10a38324e0043aa27b325310.png) </span>

   Return value description:

   * `[always] madvise never`: THP is enabled.

   * `always [madvise] never`: THP can only be used in memory regions marked with `MADV_HUGEPAGE` through the `madvise()` system call.

   * `always madvise [never]`: THP is disabled.

3. Configure the THP mode.

   
   <Tabs>
   <Tab zoneid="GHV1uETJoP" title="Temporary configuration">
   <TabTitle>Temporary configuration</TabTitle>
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">Settings applied in this way do not require an instance restart, but they take effect only for the current boot session and are lost after a restart.</div>
   
   
   
   * Configure the settings during the instance startup process.
   
      1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance) and restart (forcibly restart) the instance. For more information, see [Restarting instance](https://docs.byteplus.com/en/docs/ecs/Restarting-instances).
   
      2. Use VNC to connect to the instance. For more information, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).
   
      3. When the system boots to the kernel selection screen, press the `↑` or `↓` key to select the target kernel.
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01c99e0f279ce30e61a91ac243f90754.png) </span>
   
      3. Press `e` to enter the page for editing the Grub boot file.
   
      4. Move the cursor to the Linux kernel parameter line and add either `transparent_hugepage=always`, `transparent_hugepage=madvise`, or `transparent_hugepage=never`, as shown in the following figure.
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2bc3ec245b189f5a5bedf8972517b733.png) </span>
   
      5. Press `Ctrl` + `x` to complete the configuration.
   
      6. After logging in to the operating system, you can execute the command in Step 2 to check whether the configuration takes effect.
   
   * Configure the settings after logging in to the instance.
   
      * Enable THP
   
         ```Plain Text
         echo always > /sys/kernel/mm/transparent_hugepage/enabled
         ```
         
   
      * Disable THP
   
         ```Plain Text
         echo never > /sys/kernel/mm/transparent_hugepage/enabled
         ```
         
   
      * Specify that THP can only be used in memory regions marked with `MADV_HUGEPAGE` through the `madvise()` system call.
   
         ```Plain Text
         echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
         ```
         
   
   
   
   
   
   </Tab>
   <Tab zoneid="EATsJ8pmF6" title="Permanent configuration">
   <TabTitle>Permanent configuration</TabTitle>
   
   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>
   
   
   <div data-tips="true" data-tips-type="warning">The settings applied using this method persist permanently, but a restart of the instance is required for the settings to take effect.</div>
   
   
   
   * **veLinux/Debian/Ubuntu**
   
      1. Execute the following command to edit the Grub configuration file.
   
         ```Bash
         sudo vim /etc/default/grub
         ```
         
   
      2. Press `i` to enter edit mode, and add the `transparent_hugepage` THP parameter next to `GRUB_CMDLINE_LINUX`. If this parameter already exists, modify its value as needed.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>never</code> with the required parameter value. Value:      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>always</code>: Enable THP.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>madvise</code>: THP can only be used in memory regions marked with <code>MADV_HUGEPAGE</code> through the <code>madvise()</code> system call.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>never</code>: Disable THP.      </div>
         
   
         ```Plain Text
         transparent_hugepage=never
         ```
         
   
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5af1a7b66a40e0c3bc58aca8f245905.png) </span>
   
      3. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save and exit the file.
   
      4. Execute the following command to generate a new Grub configuration.
   
         ```Bash
         sudo update-grub
         ```
         
   
      5. Execute the following command to restart the instance for the configuration to take effect.
   
         ```Bash
         sudo reboot
         ```
         
   
   * **CentOS/RHEL/Rocky Linux**
   
      1. Execute the following command to add the THP parameter.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>never</code> with the required parameter value. Value:      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>always</code>: Enable THP.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>madvise</code>: THP can only be used in memory regions marked with <code>MADV_HUGEPAGE</code> through the <code>madvise()</code> system call.      </div>
         
   
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>never</code>: Disable THP.      </div>
         
   
         ```Bash
         sudo grubby --args="transparent_hugepage=never" --update-kernel="/boot/vmlinuz-$(uname -r)"
         ```
         
   
      2. Execute the following command to restart the instance for the configuration to take effect.
   
         ```Bash
         sudo reboot
         ```
         
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id=".5p-l55yL6YCP5piO5aSn6aG15L2_55So5oOF5Ya1"></span>
### View the usage of transparent huge pages


1. Execute the following command to view the usage of transparent huge pages at the system level.

   ```Plain Text
   cat /proc/meminfo | grep AnonHugePages
   ```
   

   Example:

   ```Plain Text
   AnonHugePages:  819200 kB
   ```
   

2. Execute the following command to view the usage of transparent huge pages at the process level.

   > Replace `[pid]` with the ID of the target process.   
   

   ```Plain Text
   cat /proc/[pid]/smaps | grep AnonHugePages
   ```
   

   Example:

   ```Plain Text
   AnonHugePages:         0 kB
   AnonHugePages:         0 kB
   AnonHugePages:         0 kB
   AnonHugePages:         0 kB
   AnonHugePages:         0 kB
   ```
   


<span id=".6YCP5piO5aSn6aG156KO54mH5pW055CG6YWN572u"></span>
### Configure THP defragmentation

You can configure the THP defragmentation feature by performing the following steps. When transparent huge pages cannot be allocated, the system automatically performs corresponding operations to defragment huge pages.


1. Execute the following command to complete the configuration.

   When transparent huge pages cannot be allocated, the system pauses the allocation, directly reclaims pages and compresses memory to immediately allocate transparent huge pages.

   ```Plain Text
   echo always >/sys/kernel/mm/transparent_hugepage/defrag
   ```
   

2. Execute the following command to complete the configuration.

   When transparent huge pages cannot be allocated, the system instead allocates 4 KB regular pages. Meanwhile, it wakes up `kswapd` in the background to reclaim pages and `kcompactd` to compress memory. This way, `khugepaged` can merge transparent huge pages when contiguous memory becomes available.

   ```Plain Text
   echo defer >/sys/kernel/mm/transparent_hugepage/defrag
   ```
   

3. Execute the following command to complete the configuration.

   When transparent huge pages cannot be allocated, the `always` mode is only applied to the allocation in memory regions marked with `MADV_HUGEPAGE` through the `madvise()` system call. 4 KB regular pages are allocated for other regions.

   ```Plain Text
   echo madvise >/sys/kernel/mm/transparent_hugepage/defrag
   ```
   

4. Execute the following command to complete the configuration.

   When transparent huge pages cannot be allocated, the `always` mode is applied to the allocation in memory regions marked with MADV_HUGEPAGE through the `madvise()` system call. The `defer` mode is applied to other regions.

   ```Plain Text
   echo defer+madvise >/sys/kernel/mm/transparent_hugepage/defrag
   ```
   

5. You can also execute the following command to disable defragmentation.

   ```Plain Text
   echo never >/sys/kernel/mm/transparent_hugepage/defrag
   ```
   


<span id=".S2h1Z2VwYWdlZOmFjee9rg=="></span>
### Configure Khugepaged

khugepaged is a daemon process for THP. It wakes up periodically and attempts to convert 4 KB regular pages into large pages (such as 2 MB pages) according to the specified configurations, thereby reducing TLB pressure and improving memory usage efficiency. However, khugepaged needs to use various memory locks during processing, which may affect system performance to a certain extent. You can configure khugepaged according to your actual needs.


1. Execute the following command to disable khugepaged defragmentation.

   ```Plain Text
   echo 0 > /sys/kernel/mm/transparent_hugepage/khugepaged/defrag
   ```
   

2. Execute the following command to enable khugepaged defragmentation.

   ```Plain Text
   echo 1 >/sys/kernel/mm/transparent_hugepage/khugepaged/defrag
   ```
   

3. Execute the following command to specify that khugepaged scans 4,096 pages each time (by default, 4,096 pages are scanned).

   ```Plain Text
   echo 4096 > /sys/kernel/mm/transparent_hugepage/khugepaged/pages_to_scan
   ```
   

4. Execute the following command to specify that the wake\-up interval of khugepaged is 10,000 ms (the default wake\-up interval is 10,000 ms).

   ```Plain Text
   echo 10000 > /sys/kernel/mm/transparent_hugepage/khugepaged/scan_sleep_millisecs
   ```
   

5. Execute the following command to specify that the wait time after khugepaged fails to allocate huge pages is 60,000 ms (the default wait time is 60,000 ms). This helps prevent repeated failures in a short period.

   ```Plain Text
   echo 60000 > /sys/kernel/mm/transparent_hugepage/khugepaged/alloc_sleep_millisecs
   ```
   

6. If the system experiences severe lag and khugepaged usage reaches 100%, you can execute the following command to disable khugepaged.

   ```Plain Text
   echo 0 > /sys/kernel/mm/transparent_hugepage/khugepaged/defrag
   ```
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Introduction to Kernel THP](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html?spm=a2c4g.11186623.0.0.1e7237a1Omevtz)

* [Introduction to THP in RHEL 7](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/performance_tuning_guide/sect-red_hat_enterprise_linux-performance_tuning_guide-configuring_transparent_huge_pages?spm=a2c4g.11186623.0.0.1e7237a1Omevtz)
