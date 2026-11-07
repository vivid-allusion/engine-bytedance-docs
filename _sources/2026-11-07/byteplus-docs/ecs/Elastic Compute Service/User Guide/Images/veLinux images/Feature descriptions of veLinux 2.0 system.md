---
title: "Feature descriptions of veLinux 2.0 system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Introduction-to-veLinux-2-features"
---

This topic mainly describes the key features of the veLinux 2.0 operating system, such as the kernel, system components, system configurations, and optimizations.

<span id=".5YaF5qC4"></span>
## Kernel

The veLinux 2.0 kernel is customized based on version 5.15 of the long\-term support (LTS) kernel from the kernel community and will support version 6.6 in the future. It fixes bugs in modules such as memory, network, I/O, and file systems and enhances their performance. veLinux 2.0 also integrates new features tailored to cloud applications.​​

<span id="Kernel 5.15"></span>
### Kernel 5.15


* Added generic helper functions of eBPF (extended Berkeley Packet Filter). Therefore, you can extend eBPF capabilities via modules.

* Added i10mn EDAC drivers for Intel® SPR/EMR processors and EDAC support for HBM memory.

* Added support for features of the EMR platform (such as RAPL, Idle, and Uncore Frequency).

* Added support for fast REP and enhanced Split Lock and P\-state.

* Added support from QAT (QuickAssist Technology) devices for SVM (Secure Virtual Machine).

* Added support from Intel® RDT (Resource Director Technology) for the isolation of SNC (Sub\-NUMA Clustering).

* Added support for TCPDirect (using dma\-buffer), also known as Device Memory TCP. This reduces packet copying and significantly improves packet throughput.

* Added AMD QoS features that include SMBA (Slow Memory Bandwidth Allocation) and BMEC (Bandwidth Monitoring Event Configuration). This provides resource QoS isolation for new types of CXL memory.

* Added PSI (Pressure Stall Information), introduced FULL mode for CPU stall at the cgroup level, and optimized implementation of FULL mode for memory stall and for switching overhead due to process blocking.

* Optimized redundant HugeTLB (Huge Transparent Large Pages) to reduce memory overhead.

* Optimized cgroup slab memory controller.

* Supported VDUSE device emulation framework, which provides a unified I/O virtualization layer for containers and virtual machines.

* Key vulnerabilities fixed, such as CVE\-2023\-5717, CVE\-2023\-2176, CVE\-2023\-35001, CVE\-2023\-31248, and CVE\-2023\-2007.


<span id="Kernel 6.6"></span>
### Kernel 6.6


* Kernel 6.6 supports the EEVDF (Enhanced Virtual Deadline Fairness) scheduler algorithm, which is designed to address certain issues in the Completely Fair Scheduling (CFS), especially the lack of guarantees for task latency. EEVDF considers task latency requirements to enhance latency guarantees for tasks with unaffected overall system throughput.

* The new Folios memory management mechanism is supported to improve memory management performance.

* Intel® Shadow Stack feature in user mode is supported. This ensures that fault protection is triggered if the user mode stack is compromised and also helps the early detection and localization of issues and faults.

* IO_uring Direct I/O performance is significantly improved in I/O scenarios with low queue depth.

* The cachestat syscall is supported to query statistics of the Pagecache for specific files, such as cache, dirty, and writeback.

* Supported Trace Event feature in User Space.

* The Process Big Memory Lock is refined to the VMA (per Virtual Memory Area, per\-VMA) level. This can significantly improve memory management performance and reduce lock contention overhead, especially in concurrent scaling scenarios on large multi\-CPU systems.

* Supported kernel modules that are developed in Rust.

* Supported MGLRU (Most Gapped Least Recently Used) algorithm. This enhances the performance of memory reclamation management.


<span id=".57O757uf57uE5Lu2"></span>
## System components

<span id=".6Ieq56CU57uE5Lu2"></span>
### Self\-developed components

<span id="Atop"></span>
#### Atop

Atop is a performance monitoring tool from the open\-source community. BytePlus platform further customizes Atop based on the community version. In veLinux 2.0, Atop is upgraded to version 2.8.1+velinux2. The key updates are as follows:


* Supported LLC collection.

* Supported pgin & pgout.

* More details about the memory consumption of tcpsock and udpsock.

* Added support for cgroup v2.

* Supplement inflight I/O requests.

* Introduced JSON output via `-J xxx`. This provides the ability to record data in JSON format.

* Two new context switch counters, nvcsw and nivcsw, are added for each process.

* Introduced separate counter for idle threads.

* Added RDELAY/BDELAY to the container.


<span id="kdump-tools"></span>
#### kdump\-tools

kdump\-tools are designed to work with the veLinux 2.0 kernel. If a kernel panic occurs due to hardware failure or a kernel software issue, the first kernel switches to the second kernel via kdump\-tools to handle the panic scene and record key information. When used with the kernel dbg package, kdump\-tools also support gdb debugging and tracing. In velinux 2.0, the version number of kdump\-tools is 2:1.8+velinux2. The main features are as follows:


* kdump\-tools can reduce memory usage in the kdump kernel by filtering out irrelevant kernel cmdline parameters and replacing systemd. This can prevent the instance from out\-of\-memory (OOM) errors during the memory dump process.

* If memory and other hardware faults are detected, kdump\-tools can terminate the dump process early to prevent further kernel panic.

* kdump\-tools can dump dmesg in advance to prevent failure to retrieve dmesg information if the memory dump fails.

* kdump\-tools can implement the crashkernel=auto feature on the kdump side. This feature automatically sets the size of memory reserved for kdump based on machine memory, without custom kernel modifications.


<span id="OpenJDK"></span>
#### OpenJDK

Three versions are supported: openjdk\-velinux\-8, openjdk\-velinux\-11, and openjdk\-velinux\-17. Features are as follows:


* For big data storage compression scenarios, veLinux OpenJDK integrates an optimized zlib implementation. This can effectively improve the performance of GZIP\-based data compression and decompression. For detailed data, refer to the [zlib](https://docs.byteplus.com/en/docs/ecs/Introduction-to-veLinux-2-features#zlib).

* To address the issue of prolonged latency caused by Full GC (Full Garbage Collection), G1 Parallel Full GC (Garbage\-First Parallel Full Garbage Collection) is ported into JDK 8. This effectively mitigates the long delays caused by Full GC.


<span id="LXCFS"></span>
#### LXCFS

LXCFS (Linux Containers Filesystem) is a filesystem proxy for Linux containers. Based on the community version 5.0.4, BytePlus adds per\-cgroup NUMA topology simulation, OOM Killer (Out of Memory Killer) protection, and a remount mechanism.

<span id="zlib"></span>
####  zlib

zlib is a foundational lossless compression library from the open\-source community. BytePlus platform further optimizes zlib based on the community version madler/zlib. In veLinux 2.0, zlib is upgraded to version 1:1.2.11.dfsg\-1+velinux2u. Features are as follows:


* Vectorized instructions are supported for hash functions during compression, and the string matching process is refactored.

* The efficiency of copying long strings during decompression is enhanced.

* Vectorized instructions are supported for crc32, adler32, and other checksums.

* The vulnerability CVE\-2018\-25032 is fixed.


Comparison of compression and decompression performance:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_723ff2bdfc115944a7806e30e5ca87a3.png) </span>

<span id="base-files"></span>
#### base\-files

In veLinux 2.0, base\-files are upgraded to version 12.4+base2u1, which modifies the contents of the /etc/os\-release file to align with the veLinux system identifier.

<span id=".6YeN54K55byA5rqQ57uE5Lu2"></span>
### Key open\-source components

<span id=".5qC45b-D5bel5YW3"></span>
#### Core tools

<span id="glibc"></span>
#### glibc

glibc (GNU C Library) is one of the most fundamental and important C language function libraries in Linux systems. BytePlus platform uses version 2.36, which further improves glibc performance and reliability. Its main features are as follows:


* The AArch64 architecture provides branch protection security enhancement, with BTI (branch target identification) and PAC\-RET (pointer authentication for return addresses) included.

* An upper limit for memory allocation\-related interfaces is set to PTRDIFF_MAX. This prevents potential overflows that cause error requests for excessively large memory and thereby improves reliability.

* The async\-signal\-safe function _Fork, which belongs to the fork family of functions, is newly added to meet the user requirement for async\-signal safety.

* glibc supports Unicode version 14.0.0, which provides a broader range of supported code points.

* glibc provides new tunable environment variables to enable flexible use of features and performance. Details are as follows:

   * You can configure the size of thread stack cache by using glibc.pthread.stack_cache_size.

   * You can specify the DSO sorting algorithm by using glibc.rtld.dynamic_sort.

   * You can improve system performance by using glibc.malloc.hugetlb which can work with the kernel large\-page configuration.

* LoongArch CPU is supported.


<span id="Binutils"></span>
#### Binutils

Binutils is a set of open\-source binary tools under the GNU Project, which can be used for the creation, manipulation, and analysis of binary files. BytePlus platform uses version 2.40 as a more reliable tool for the creation and management of binary programs. The main features are as follows:


* zstd can be used for the compression of debugging sections.

* Multiple practical and convenient options are provided to improve tool availability.

* elfedit/readelf support LAM_U48 and LAM_U57.

* Support from C99 compiler and library is needed.

* Added support for the LoongArch instruction set.


<span id="util-linux"></span>
#### util\-linux

util\-linux is a project that contains various Linux utilities. BytePlus platform uses version 2.38.1 to provide up\-to\-date system programs required for Linux operation.

<span id="dpkg"></span>
#### dpkg

dpkg (Debian Package) is a tool for the management of software packages on Debian systems. BytePlus platform uses version 1.21.22 to provide a more secure Linux package manager.

<span id="APT"></span>
#### APT

APT (Advanced Package Tool) is an advanced package management tool based on dpkg. BytePlus platform uses version 2.6.1 to provide a more effective and reliable package management frontend tool.

<span id=".5ZCv5Yqo5LiO5byV5a-8"></span>
#### Startup and boot

<span id="systemd"></span>
#### systemd

systemd is a system and service manager. BytePlus platform uses version 252, cgroup v2 (Control Group Version 2) by default. This provides a more reliable system and service manager. The main features are as follows:


* sd\-boot is upgraded from the original PCR 8 to support TPM PCR 12.

* More supported cgroup v2 features.

* Supported cgroup v2 BPF\-related logic.

* Supported features related to the GPT Discoverable Partitions Specification.

* udev rules of all devices are triggered during each upgrade.

* The `CPUAffinity=` option supports NUMA.

* udev rules support auto\-suspend for PCI and USB devices.

* Added userdb\-related features.

* New tools (systemd\-network\-generator, systemd\-sysext, and systemd\-repart) are added for system extension layer control, better GPT support, and other functions.

* A new naming rule "keep" for network devices is added.

* The system resource limit RLIMIT_NOFILE is set to 1024 (soft) and 4096 (hard).

* The maximum default number of inodes for /dev is increased from 64K to 1M, and that for /tmp from 400K to 1M.

* Currently, the RDRAND instruction set is preferred on x86_64.


<span id="GRUB2"></span>
#### GRUB2

GRUB2 (GNU GRand Unified Bootloader 2) is a multi\-operating system bootloader developed by the GNU project. BytePlus platform uses version 2.06. The main features are as follows:


* Supported Virtual LAN.

* ARM supports EHCI, DMA, and DTB drivers.

* Supported UUID and PARTUUID.

* NVMe devices with Open Firmware text representation are supported.

* Added support for F2FS (flash\-friendly file system).

* Supported file systems with sparse nodes.

* Supported operations (read, start, and recover) for file systems of RAID\-5, RAID\-6, or RAID1C34.

* TPM (Trusted Platform Module) is supported across all architectures.

* Supported RISC\-V architecture.


<span id=".57yW6K-R5LiO5byA5Y-R"></span>
### Compilation and development

<span id="GCC"></span>
#### GCC

GCC (GNU Compiler Collection) is an open\-source compiler suite developed by the GNU Project. It is used to compile and build programs in various programming languages. BytePlus platform uses version 12.2.0 to better support C and C++, and continuously improves support for RISC\-V and LoongArch CPU architectures. Features are as follows:


* Changed to TGCC.

   * Optimized feedback compilation to enhance effectiveness based on business\-related features.

   * Optimized LTO link.

   * Function reordering and basic block reordering are implemented based on business operation features.

* Supported ShadowCallStack sanitizer (aarch64 only).

* The default C++ compilation version is set to 17, with partial support for C++23 features.

* Supported armv9 and loongarch.


<span id="GDB"></span>
#### GDB

GDB (GNU Debugger) is a powerful open\-source debugger for programs written in various programming languages. BytePlus platform uses version 13.1 to provide debugging capabilities of the latest version. The main features are as follows:


* Multiple supported architectures, such as loongarch, openrisc, and C\-SKY.

* Floating\-point support is now added to LoongArch GNU/Linux.

* Multi\-threaded symbol table loading is supported by default.

* Python 2 is no longer supported, and the Python API is enhanced.


<span id="Vim"></span>
#### Vim

Vim is an open\-source, highly customizable text editor, and an improved and extended version of the Vi editor. BytePlus platform uses version `9.0` to support the new scripting language Vim9script.

<span id="Shell"></span>
#### Shell

Shell is a command\-line interpreter provided by the operating system. It is used to interact with the operating system kernel and execute user commands. BytePlus platform uses `bash version 5.2.15`. The main features are as follows:


* Newly added loadable built\-in commands, such as asort, mktemp, accept, mkfifo, csv, cut/lcut, and seq.

* Shell now attempts to unlink all FIFOs upon exit, regardless of whether the consumption process is completed.

* `bind -x` now supports different bindings and keyboard mappings for different editing modes.

* Writing historical records to syslog can now handle messages longer than the syslog maximum length by splitting them into multiple messages with sequence numbers. This allows the full message to be reconstructed.

* bash\-completion

   * More supported commands, such as nmap, openssl, ssh\-keygen, and gcc.

   * Added support for gssdp\-discover, xvfb\-run, influx, dmypy, carton, scrub, ecryptfs\-migrate\-home, chmod, json_xs, and more.

* The testing module is optimized and enriched.


<span id="Python"></span>
#### Python

BytePlus platform uses Python 3 (version `3.11.2`) and no longer supports Python 2. The main features are as follows:


* Python 3.11 is 10% to 60% faster than Python 3.10.

* Added tomllib module to the standard library, which supports TOML parsing.

* Multiple types of prompts are added.

   * A new standard exception type, "ExceptionGroup", and new syntax "except\*" are added. This allows programs to raise and handle multiple unrelated exceptions at the same time.

   * Added fine\-grained details of error information from Traceback to improve debugging capability (from PEP 657).


<span id="Perl"></span>
#### Perl

Perl is a high\-level, general\-purpose, interpreted programming language. BytePlus platform uses version `5.38.2`. The main features are as follows:


* Added support for Unicode 15.0.

* Added support for floating\-point exception signals.

* Added support for variable\-length lookbehind assertions.

* Added core module builtin.

* Added try/catch/finally, an exception handling mechanism.

* Supported C11 TLS features, and performance is improved in scenarios where threaded Perl is built.

* Scalar creation speed is increased by 30% in specific scenarios.

* Supported thread safety for language environment operations.

* Improved key allocation performance of Hash table.


<span id=".V2Vi5pyN5Yqh5Zmo"></span>
### Web servers

<span id="Apache"></span>
#### Apache

Apache is open\-source, cross\-platform web server software. BytePlus platform uses `version 2.4.57`. The main features are as follows:


* Added modules: mod_socache_redis and mod_systemd are added.

* Added tools: fcgistarter, htcacheclean, rotatelogs, htpasswd, and htdbm are added to improve operational convenience.

* Enhanced features: Millisecond\-level configuration for KeepAliveTimeouT and MPM asynchronous support are enhanced.


<span id="Nginx"></span>
#### Nginx

Nginx is an open\-source, high\-performance, lightweight web server and reverse proxy server software. BytePlus platform uses version `1.22.1`. The main features are as follows:


* Added support for OpenSSL 3.0.

* Improved HTTP/2 performance.

* Enhanced security: Fix vulnerabilities of CVE\-2022\-41741, CVE\-2022\-41742, and CVE\-2021\-23017.


<span id=".5pWw5o2u5bqT"></span>
### Database

<span id="MariaDB"></span>
#### MariaDB

MariaDB is an open\-source Relational Database Management System (RDBMS). BytePlus platform uses version `10.11.6`. The main features are as follows:


* Added authorization operation: GRANT to PUBLIC.

* Added UUID data type.

* InnoDB performance improvements, gap lock fixes, and redo log enhancements.

* The initialization speed of the Docker time zone library is improved.

* Supported health checks in containers.

* Skipped InnoDB buffer pool loading and dumping to improve start and initialization speed of Docker.

* Fixed vulnerabilities of CVE\-2023\-22084 and CVE\-2022\-47015.


<span id="PostgreSQL"></span>
#### PostgreSQL

PostgreSQL is an open\-source, cross\-platform Relational Database Management System (RDBMS). BytePlus platform uses version `15.6`. The main features are as follows:


* Supported SQL MERGE command.

* You can selectively publish table content in logical replication publications by specifying column lists and row filter conditions.

* More compression options, with Zstandard (zstd) included. This feature also includes support for compression on the server during pg_basebackup.

* Supported structured server log output in JSON format.

* Improved performance, especially that of sorting in memory and on disk.

* Fixed vulnerability CVE\-2024\-0985.


<span id=".5a6J5YWo55u45YWz"></span>
### Security\-related features

<span id="GnuPG 2"></span>
#### GnuPG 2

GnuPG 2 (GNU Privacy Guard 2) is the new version of the open\-source encryption software suite GnuPG, which can provide features of data encryption and digital signature. BytePlus platform uses version `2.2.40`. The main features are as follows:


* Supported AEAD encryption modes that use OCB or EAX.

* Supported keys that are issued by DFN.

* Supported Telesec ESIGN application.

* TPM 2.0 is used to protect the private key.

* Improved speed of GPG encryption, decryption, and other related processes.

* A pipeline is used for decryption to avoid memory exhaustion.

* Supported ssh\-agent authentication via OpenPGP.

* For the ed448 and cv448 algorithms, keys created must be version 5.

* Multiple types of smart cards are supported.


<span id="OpenSSL"></span>
#### OpenSSL

OpenSSL is an open\-source encryption and secure socket library that provides various encryption algorithms, protocols, and tools for securing network communications, data transmission, and data storage. BytePlus platform uses `version 3.0.8`. The main features are as follows:


* Supported Kernel TLS (KTLS) protocol.

* The "Provider" concept is introduced. This enables you specify the algorithm implementations for a specific application either programmatically or via configuration files.

* SHA1\-based signature certificates will not be trusted by authenticated clients and servers.

* Fixed vulnerabilities of CVE\-2022\-3786, CVE\-2022\-3602, CVE\-2022\-3786, CVE\-2023\-0401, and more.


<span id="OpenSSH"></span>
#### OpenSSH

OpenSSH (Open Secure Shell) is an open\-source implementation for secure remote login. It provides encrypted communication sessions with features such as remote login, file transfer, and port forwarding. BytePlus platform uses the `9.2 p1` version to provide more extensive security tunnel features, multiple authentication methods, and a more secure SSH protocol.
