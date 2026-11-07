---
title: "Basic monitoring"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/Basic_monitoring"
---

Infrastructure monitoring is the platform's most basic monitoring feature, including monitoring of metrics such as CPU, disk, IO, iNode, memory, and GPU for hosts, containers, and processes.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Non\-container environment: The Agent needs to be connected on the host

* k8s: The Agent needs to be integrated via DaemonSet

* Other container environments: The Agent must be integrated on the host.


<span id=".5Li75py655uR5o6n"></span>
## host monitoring

<span id=".5Li75py65YiX6KGo"></span>
### Host list

The host list displays the hosts integrated with Monitoring, along with their status, CPU utilization, IO, and load information.

All metrics support sorting, selecting a time range, filtering data by hostname, and filtering data by tag. You can quickly select hosts according to business needs.

<span id=".5Li75py66K-m5oOF"></span>
### Host details

Click the hostname to display trend charts for the host's metrics, including CPU, load, memory, and other metrics.

The description of host monitoring metrics is shown in the following table:


|**Metric name** |**Metric** |**DescriptionS** |**Units** |
|---|---|---|---|
|CPU idle ratio |host.cpu.idl_ratio |Host CPU idle ratio: the proportion of CPU time spent in the idle state (excluding iowait). The ratio calculation method is idle time divided by total CPU time. |% |
|CPU total usage percentage |host.cpu.total_used_ratio |The total CPU usage ratio of the host is the sum of the user usage ratio and the operating system usage ratio. |% |
|CPU user percentage |host.cpu.user_ratio |Host CPU user utilization ratio, percentage of CPU time consumed in user space. |% |
|Cpu system usage ratio |host.cpu.system_ratio |Host CPU kernel mode usage ratio, percentage of CPU time spent in kernel space. |% |
|CPU iowait ratio |host.cpu.iowait_ratio |Host CPU iowait ratio: the proportion of CPU time spent in the idle (iowait) state. |% |
|CPU stolen percentage |host.cpu.stolen_ratio |The host CPU steal ratio. Relevant only in virtualization environments, this refers to the proportion of time during which the CPU is unavailable to the current virtual machine because the hypervisor has taken the CPU away from this VM. If "Steal Time" is high on a specific virtual machine, this indicates that the virtual machine is running on an overloaded or heavily loaded physical host. |% |
|The CPU guest ratio |host.cpu.guest_ratio |Host CPU guest ratio Indicates the proportion of CPU time used by the virtual machine. |% |
|CPU nice ratio |host.cpu.nice_ratio |The host CPU nice ratio Represents the proportion of CPU usage by user\-mode processes with a positive nice value (low priority). |% |
|Available memory |host.memory.available |Host available memory |Byte |
|Memory usage |host.memory.used |Host memory usage. |Byte |
|Memory availability ratio |host.memory.available_ratio |The proportion of available host memory. The calculation method is the ratio of available host memory to total host memory. |% |
|Memory usage ratio |host.memory.used_ratio |Host memory usage ratios. The calculation method is host memory usage divided by host total memory. |% |
|1\-minute average load |host.load.1m |Average load over the past 1 minute. Average number of processes running or waiting to run on the CPU in the past minute. |\- |
|Average load over the past 5 minutes |host.load.5m |Average load over the past 5 minutes. Average number of processes running or waiting to run on the CPU over the past five minutes. |\- |
|The average load over the past 15 minutes |host.load.15m |The average load over the past 15 minutes. The average number of processes running or waiting to run on the CPU over the past 15 minutes. |\- |
|Disk space usage ratio |host.disk.bytes_used_ratio |Disk usage ratio. Method: disk space usage divided by total disk capacity. |% |
|Available disk space percentage |host.disk.bytes_free_ratio |Available disk space ratio. The calculation method is available host space divided by total disk capacity. |% |
|Disk space usage |host.disk.bytes_used |Disk space usage. |Byte |
|Disk space available |host.disk.bytes_free |Available host space. |Byte |
|I/O latency |host.disk.io.lantency |Disk read/write average latency. |ms |
|Read IO latency |host.disk.io.read_latency |Average disk read latency. |ms |
|Write IO latency |host.disk.io.write_latency |Average disk write latency. |ms |
|Read IOPS |host.disk.io.read_qps |Disk reads per second. |/s |
|Write IOPS |host.disk.io.write_qps |Disk writes per second. |/s |
|Merged disk read |host.disk.io.read_merged_qps |Merged disk reads per second. |/s |
|Disk write merging |host.disk.io.write_merged_qps |Number of merged disk writes per second. |/s |
|Read IO throughput |host.disk.io.read_bytes_rate |Number of bytes read from disk per second. |Byte/s |
|Write IO throughput |host.disk.io.write_bytes_rate |Bytes written to disk per second. |Byte/s |
|Space usage ratio of disk mount points |host.disk_mount.bytes_used_ratio |Space usage ratio of disk mount points. |% |
|Available space ratio of mount point |host.disk_mount.bytes_free_ratio |Available space ratio at disk mount points |% |
|Disk mount point space usage |host.disk_mount.bytes_used |Disk mount point space usage. |Byte |
|Disk mount point space available |host.disk_mount.bytes_free |Available space at disk mount points. |Byte |
|Disk mount point INODE usage ratio |host.disk_mount.inode_used_ratio |Disk mount point inode usage |% |
|Disk mount point inode availability ratio |host.disk_mount.inode_free_ratio |Disk mount point inode availability ratio |% |
|Disk mount point inode usage |host.disk_mount.inode_used |Disk mount point INODE usage. |\- |
|The disk mount point inode is available |host.disk_mount.inode_free |Inode availability at disk mount points. |\- |
|Bytes received (network card) |host.network.bytes_recv |Number of bytes received by the network card. |Byte |
|Network card sent bytes |host.network.bytes_sent |Bytes sent by network card |Byte |
|Network card receiving data packets |host.network.packets_recv |Number of packets received by the network card. |p/s |
|Network card sends data packets |host.network.packets_sent |Number of packets sent by the network card. |p/s |
|GPU graphics memory idle |host.nvidia.memory_free |Idle graphics memory on the GPU. |Byte |
|GPU graphics memory usage |host.nvidia.memory_used |GPU graphics memory usage. |Byte |
|Total graphics memory |host.nvidia.memory_total |Total GPU graphics memory capacity |Byte |
|Gpu graphics memory utilization |host.nvidia.memory_used_ratio |GPU graphics memory utilization rate. The calculation method is GPU graphics memory usage divided by the total GPU graphics memory. |% |
|GPU utilization |host.nvidia.gpu_utilization |GPU usage rate. |% |
|GPU graphics memory utilization |host.nvidia.mem_copy_utilization |Percentage of time graphics memory is read or written. |% |
|GPU temperature |host.nvidia.temperature |The GPU temperature. |℃ |
|GPU power |host.nvidia.power |GPU power. |mW |


<span id=".RG9ja2Vy55uR5o6n"></span>
## Docker monitoring

<span id=".RG9ja2Vy6LaL5Yq_"></span>
### Docker trends

Docker Trend displays the list of monitored containers, including their status, host name, image, CPU utilization, memory usage rate, startup time, creation time, and other information.

All metrics support sorting, selection of a time range, filtering by hostname, searching by Docker container, and filtering by tag. Containers can be quickly filtered according to business requirements.

<span id=".RG9ja2Vy6K-m5oOF"></span>
### Docker details

Click the container name to display container details, including CPU and memory usage trend charts and more.

Descriptions of container monitoring metrics are shown in the following table:


|**Metric name** |**Metric** |**DescriptionS** |**Unit** |
|---|---|---|---|
|CPU system ratio |docker.cpu.system_ratio |CPU utilization in the container's kernel space. |% |
|CPU user percentage |docker.cpu.user_ratio |CPU utilization in the container user space. |% |
|cpu shares |docker.cpu.shares_ratio |The container's CPU share. The share controls the proportion of CPU usage by processes in a container. |% |
|Overall CPU usage percentage |docker.cpu.total_ratio |Total CPU utilization rate of the container. |% |
|Thread count |docker.cpu.thread_num |Container thread count. |\- |
|Memory usage (RSS) |docker.memory.rss |Container memory usage. |Byte |
|Memory usage (RSS) ratio |docker.memory.rss_ratio |Container memory usage ratio. The calculation method is memory RSS divided by container memory limit. |% |
|Read IOPS |docker.io.read_qps |Container disk read operations per second. |/s |
|Write IOPS |docker.io.write_qps |Container disk write operations per second. |/s |
|Read I/O throughput |docker.io.read_bytes_rate |Number of bytes written to disk by the container per second. |Byte/s |
|Write IO throughput |docker.io.write_bytes_rate |Container disk bytes read per second |Byte/s |


<span id=".6L-b56iL55uR5o6n"></span>
## process monitoring

<span id=".6L-b56iL6LaL5Yq_"></span>
### Process trends

The process list displays processes integrated with Monitoring, along with information such as the start user, host name, CPU usage rate, memory usage rate, creation time, end time, and other information.

All metrics support sorting, time range selection, hostname filtering, process search, and tag filtering, enabling you to quickly filter processes according to business needs.

<span id=".6L-b56iL6K-m5oOF"></span>
### Process details

Click the process name to display process details, including process metrics, Runtime metrics, RED metrics, and logs. Process metrics display information such as CPU and memory usage trend charts, and other information.

The description of process monitoring metrics is shown in the following table:


|**Metric name** |**Metric** |**DescriptionS** |**Unit** |
|---|---|---|---|
|Total number of CPU cores |process.cpu.cpu_limit |The limit on the number of CPU cores a process can use. |\- |
|Overall CPU usage ratio (relative to a single core) |process.cpu.total_ratio |The process CPU utilization. For example, when two cores are used, CPU utilization is 200%. |% |
|CPU system ratio (relative to single core) |process.cpu.system_ratio |CPU utilization in kernel space. |% |
|CPU user percentage (relative to single core) |process.cpu.user_ratio |CPU utilization in user space. |% |
|Total number of CPU cores in use |process.cpu.total_used |Number of CPU cores used. For example, when using 2 cores, set the number of cores to 2. |\- |
|Cpu system core usage |process.cpu.system_used |Number of CPU cores used by kernel space. |\- |
|CPU user mode core count |process.cpu.user_used |Number of CPU cores used in user space. |\- |
|Thread count |process.cpu.thread_num |Number of Operating System threads in a process. |\- |
|Total memory |process.memory.limit |CPU limit available to the process. |Byte |
|Memory usage (RSS) |process.memory.rss |Memory usage |Byte |
|The memory usage (RSS) ratio |process.memory.rss_ratio |Memory usage percentage. The calculation method is memory RSS divided by memory limit. |% |
|Virtual memory size |process.memory.vms |The virtual memory size. |Byte |
|Read IOPS |process.io.read_qps |Number of disk reads per second by the process. |/s |
|Write IOPS |process.io.write_qps |Number of times the process writes to disk per second. |/s |
|Read I/O throughput |process.io.read_bytes_rate |Process disk read bytes per second. |Byte/s |
|Write I/O throughput |process.io.write_bytes_rate |Number of bytes written to disk per second by the process. |Byte/s |
|Number of open files |process.open_fd_count |Number of open files for the process. |\- |
|Number of voluntary context switches (voluntary_ctx_switches) |process.voluntary_ctx_switches |Number of voluntary context switches. |\- |
|Involuntary context switch count (involuntary_ctx_switches) |process.involuntary_ctx_switches |Number of forced context switches. |\- |


JVM metrics for process monitoring


|**Metric** |**DescriptionS** |
|---|---|
|jvm.clazz.loaded_class_count |Number of classes currently loaded by the JVM |
|jvm.clazz.total_unloaded_class_count |Total number of unloaded JVM classes |
|jvm.clazz.total_loaded_class_count |Total number of loaded classes in the JVM |
|jvm.gc.gc_count_old |The number of JVM GC events in OldGen |
|jvm.gc.gc_time_old |JVM GC time – OldGen |
|jvm.gc.gc_count_new |JVM GC count for NewGen |
|jvm.gc.gc_time_new |Jvm GC time for NewGen |
|jvm.memory.init_heap |Initial JVM heap memory |
|jvm.memory.max_heap |The maximum JVM heap memory |
|jvm.memory.used_heap |Used heap memory (JVM) |
|jvm.memory.committed_heap |JVM committed heap memory |
|jvm.memory.init_noheap |The initial JVM non\-heap memory |
|jvm.memory.max_noheap |The maximum JVM non\-heap memory |
|jvm.memory.used_noheap |JVM has used non\-heap memory |
|jvm.memory.committed_noheap |Committed non\-heap memory (JVM) |
|jvm.memory_pool.init_newgen |JVM memory pool \- initial NewGen |
|jvm.memory_pool.max_newgen |JVM memory pool – maximum NewGen memory pool size |
|jvm.memory_pool.used_newgen |JVM memory pool – NewGen used |
|jvm.memory_pool.committed_newgen |JVM memory pool \- committed NewGen |
|jvm.memory_pool.init_oldgen |The initial OldGen JVM memory pool |
|jvm.memory_pool.max_oldgen |JVM memory pool \- maximum OldGen |
|jvm.memory_pool.used_oldgen |Used OldGen memory |
|jvm.memory_pool.committed_oldgen |JVM memory pool \- committed OldGen |
|jvm.memory_pool.init_code_cache |JVM memory pool \- initial CodeCache |
|jvm.memory_pool.max_code_cache |JVM memory pool – maximum CodeCache size |
|jvm.memory_pool.used_code_cache |CodeCache usage |
|jvm.memory_pool.committed_code_cache |JVM memory pool \- committed CodeCache |
|jvm.memory_pool.init_survivor |JVM memory pool \- initial Survivor space |
|jvm.memory_pool.max_survivor |Maximum size of Survivor space in the JVM memory pool |
|jvm.memory_pool.used_survivor |JVM memory pool \- Survivor space used |
|jvm.memory_pool.committed_survivor |JVM memory pool \- committed Survivor |
|jvm.memory_pool.init_meta_space |JVM memory pool \- initial MetaSpace |
|jvm.memory_pool.max_meta_space |JVM memory pool \- maximum MetaSpace |
|jvm.memory_pool.used_meta_space |JVM memory pool \- Used MetaSpace |
|jvm.memory_pool.committed_meta_space |JVM memory pool \- committed MetaSpace |
|jvm.memory_pool.init_perm_gen |JVM memory pool \- the initial PermGen |
|jvm.memory_pool.max_perm_gen |JVM memory pool – maximum PermGen |
|jvm.memory_pool.used_perm_gen |JVM memory pool – PermGen used |
|jvm.memory_pool.committed_perm_gen |JVM memory pool \- submitted PermGen |
|jvm.thread.live_count |JVM live thread count |
|jvm.thread.daemon_count |JVM daemon thread count |
|jvm.thread.peak_count |JVM peak thread count |
|jvm.thread.runnable_state_thread_count |Number of runnable threads in the JVM |
|jvm.thread.blocked_state_thread_count |Number of blocked JVM threads |
|jvm.thread.waiting_state_thread_count |JVM waiting thread count |
|jvm.thread.timed_waiting_state_thread_count |JVM timed waiting thread count |
