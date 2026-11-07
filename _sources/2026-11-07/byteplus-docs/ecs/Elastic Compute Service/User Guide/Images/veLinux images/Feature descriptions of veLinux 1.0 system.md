---
title: "Feature descriptions of veLinux 1.0 system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Introduction-to-veLinux-features"
---

This topic mainly describes the key features of the veLinux 1.0 operating system, such as the kernel, system components, system configurations, and optimizations.

<span id=".5YaF5qC4"></span>
## Kernel

The veLinux kernel is customized based on version 5.4 of the long\-term support (LTS) kernel from the kernel community. It fixes bugs and improves the performance of kernel modules such as memory, networking, I/O, and file systems, and introduces new features for cloud applications, for example:


* Optimized redundant HugeTLB to reduce memory overhead.

* Added generic helper functions of eBPF. Therefore, you can extend eBPF capabilities via modules.

* Optimized cgroup slab memory controller.

* VDUSE device emulation framework.

* PSI feature: introduced FULL mode for CPU stall at the cgroup level, and optimized implementation of FULL mode for memory stall and for switching overhead due to process blocking.


<span id=".57O757uf57uE5Lu2"></span>
## System components

Self\-developed software packages of the BytePlus platform are as follows:

<span id="atop"></span>
### Atop

Atop is a performance monitoring tool from the open\-source community. BytePlus platform further customizes Atop based on the community version. New features include:


* Supported Top N thread filtering in monitoring data records.

* Supported output of monitoring data in JSON format with various display options.

* Prevented invalid writes that are caused by continuous writes to the old file after a crash.

* Custom log retention days.


<span id="kdump-tools"></span>
### kdump\-tools

kdump\-tools are designed to work with the veLinux 5.4.56 kernel. If a kernel panic occurs due to hardware failure or a kernel software issue, the first kernel switches to the second kernel via kdump\-tools to handle the panic scene and record key information. When used with the kernel dbg package, kdump\-tools can also support gdb debugging and tracing. Besides, kdump\-tools support reporting to the server and integrate with monitoring services to provide near\-real\-time monitors and alerts for kernel panics.

<span id="systemd"></span>
### systemd

The issue where logs are lost during journald restart is fixed.

<span id="pciutils"></span>
### pciutils

It provides support for the correct reading and display of PCI Gen 4 16GT/s rate.

<span id="zlib"></span>
### zlib

zlib is a foundational lossless compression library from the open\-source community. BytePlus platform further optimizes zlib based on the community version madler/zlib.


* zlib supports vectorized instructions for hash functions during compression and refactors the string matching process.

* The efficiency of copying long strings during decompression is enhanced.

* Vectorized instructions are supported for crc32, adler32, and other checksums.


Comparison of compression and decompression performance:

<span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/b52c3bc539e34acb8193a543e12b2a92.png) </span>

<span id=".6YWN572u5LyY5YyW"></span>
## Configuration optimizations

Based on the massive business scenarios of the BytePlus platform, system configurations undergo in\-depth optimizations in aspects like memory, file systems, networks, and security. This can better meet business requirements such as high concurrency and low latency.

<span id=".572R57uc"></span>
### Network


* High concurrency

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |net.core.netdev_max_backlog |16384 |Maximum number of backlogged packets |
   |net.core.somaxconn |16384 |Maximum number of pending listen sockets |
   |net.ipv4.tcp_max_syn_backlog |16384 |Maximum number of backlogged SYN packets |
   |net.ipv4.ip_local_port_range |10000 65535 |Restrictions on local minimum and maximum ports |
   |net.ipv4.tcp_max_orphans |2097152 |Maximum number of isolated connections |
   |net.ipv4.tcp_max_tw_buckets |1048576 |Total TIME_WAIT count |
   

* Low latency

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |net.core.rmem_max |16777216 |Maximum socket read buffer |
   |net.core.wmem_max |16777216 |Maximum socket write buffer |
   |net.ipv4.tcp_rmem |4096 87380 33554432 |Minimum, default, and maximum values of the TCP read buffer |
   |net.ipv4.tcp_wmem |4096 65536 33554432 |Minimum, default, and maximum values of the TCP read buffer |
   |net.ipv4.tcp_slow_start_after_idle |0 |TCP connections do not enter slow start after idling |
   |net.ipv4.tcp_fastopen |3 |Both the client and server enable TCP Fast Open |
   |net.ipv4.tcp_fin_timeout |15 |Maximum duration of the FIN_WAIT_2 status |
   

* Network security

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |net.ipv4.ip_forward |0 |IP forwarding between network ports is disabled |
   |net.ipv6.conf.all.forwarding |0 |IPv6 forwarding between network ports is disabled |
   |net.ipv4.tcp_syncookies |1 |The SYN Cookie feature is enabled to prevent SYN attacks |
   |net.ipv4.conf.all.route_localnet |0 |Cross\-machine loopback access is prevented |
   

* Improved resource utilization

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |net.ipv4.tcp_tw_recycle |0 |Fast recycling of TIME\-WAIT sockets is disabled |
   |net.ipv4.tcp_tw_reuse |1 |Reuse of TIME\-WAIT sockets is allowed |
   |net.ipv4.tcp_orphan_retries |2 |Number of RTO retries |
   |net.ipv4.tcp_synack_retries |2 |SYNACK retry count |
   |net.ipv4.tcp_syn_retries |3 |SYN retry count |
   |net.ipv4.tcp_thin_linear_timeouts |1 |Linear timeout retransmission is enabled |
   


<span id=".5a6J5YWo"></span>
### Security


* The difficulty of exploiting vulnerabilities is enhanced

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |kernel.dmesg_restrict |1 |Ordinary users are not allowed to read dmesg |
   |kernel.randomize_va_space |2 |Address Space Layout Randomization is enabled |
   |vm.unprivileged_userfaultfd |0 |Ordinary users are not allowed to use userfaultfd system calls |
   |kernel.kptr_restrict |1 |Only those with the CAP_SYSLOG permission and where euid equals ruid can read kernel addresses printed via %pK (that is, by reading /proc/kallsyms to obtain the addresses of kernel exported symbols). |
   

* The attack surface is reduced

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |kernel.yama.ptrace_scope |1 |PTRACE_ATTACH feature is disabled |
   |kernel.unprivileged_bpf_disabled |1 |Ordinary users are not allowed to use eBPF system calls |
   |fs.protected_hardlinks |1 |Any user is restricted from creating hard links to arbitrary files |
   |fs.protected_symlinks |1 |Symbolic links are verified |
   |fs.suid_dumpable |0 |SUID_DUMP_DISABLE prevents malicious exploitation of coredumps of protected or tainted processes |
   |kernel.perf_event_paranoid |2 |Ordinary users access to perf events is restricted. When the CAP_SYS_ADMIN privilege is not held, they are blocked to use kernel profiling, CPU events, ftrace function tracepoints, and raw tracepoints. |
   


<span id=".5YW25LuW"></span>
### Other optimizations


* High performance

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |vm.swappiness |0 |Maximum utilization of physical memory |
   |vm.max_map_count |2097152 |Maximum memory space available to a single process |
   

* Debugging

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |kernel.sched_schedstats |1 |Enable scheduler statistics to add debugging and statistical information. |
   |net.core.bpf_jit_enable |1 |eBPF is enabled |
   

* High concurrency

   
   |**Configuration item** |**Value** |**Description** |
   |---|---|---|
   |kernel.pid_max |4194303 |Maximum PID |
   |fs.file\-max |12288000 |Maximum File Descriptors |
   |net.unix.max_dgram_qlen |512 |Unix socket queue length |
