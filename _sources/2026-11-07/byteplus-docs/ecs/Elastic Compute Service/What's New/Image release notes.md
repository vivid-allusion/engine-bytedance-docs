---
title: "Image release notes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Image-release-notes"
---

This topic describes the release notes of public images for ECS instances. The images will be gradually released in all regions. Welcome to try them out.

<span id="fLrFwEOn"></span>
## Usage notes


|**Supported instance types** |
|---|
|* The following images are applicable for creating [General-purpose](https://docs.byteplus.com/en/docs/ecs/General-purpose), [Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Computing-optimized), [Memory-optimized](https://docs.byteplus.com/en/docs/ecs/Memory-optimized), [Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based), [Big Data](https://docs.byteplus.com/en/docs/ecs/Big-data-based), [Burstable](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances), and [Shared](https://docs.byteplus.com/en/docs/ecs/Shared) ECS instances.<br><br>* Except for Windows Server and CentOS 6.9 images, the following images support the creation of [Elastic Bare Metal (EBM)](https://docs.byteplus.com/en/docs/ecs/General-purpose-EBM).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Images available for selection vary slightly by instance type. Please refer to the actual instance creation page.</div><br> |
|**Lifecycle** |
|If an operating system version reaches the end of lifecycle (End of Life, EOL), BytePlus will stop providing technical support services for instances that use the operating system version. We recommend that you select an image that has not reached EOL. [Learn more](https://docs.byteplus.com/en/docs/ecs/OS-discontinuing-plan). |
|**Image version** |
|* Image versions are public images ​released at different phases. Each image version has different features and functions.<br><br>   * Each image version is valid for **2** years from its release date<br><br>   * Once a version expires, you can no longer use the image. However, instances created based on the image before expiration will not be affected.<br><br>* If you select a public image when using the console to [purchase an ECS instance](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) or [change an instance operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS) , the latest version of the public image will be selected for you by default.<br><br>* If you need to use an older version of a public image, call [RunInstances - Creates instance](https://docs.byteplus.com/en/docs/ecs/RunInstances) and [ReplaceSystemVolume - Replaces operating system](https://docs.byteplus.com/en/docs/ecs/ReplaceSystemVolume) operations. Then, specify the required public image and the image version via the parameters of `ImageId` and `ImageReleaseVersion`. |


<span id="cblEv0A8"></span>
## veLinux images

<span id="YiUk1J0F"></span>
### veLinux 2.0


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|veLinux 2.0 for TDX 64 bit |Kernel version: 5.15.120.ve.6\-tdxg.2\-amd64 |September 2024 |Firstly released online |All |GA |
|veLinux 2.0 64 bit |5.15.152.ve.7u4\-amd64 |June 2026 |* The kernel version is upgraded<br><br>* `napi_tx` is enabled<br><br>* The configuration file /etc/modprobe.d/dirtyfrag.conf is added to mitigate CVE\-2026\-43500 and CVE\-2026\-43284 vulnerabilities by disabling the loading of related kernel modules<br><br>* Vulnerabilities CVE\-2026\-31431, CVE\-2026\-28388, CVE\-2026\-28389, CVE\-2026\-28390, and CVE\-2026\-31790 are fixed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed |Asia Pacific (Jakarta) |GA |
||Kernel version: 5.15.152.ve.7u1\-amd64 |January 2026 |* The kernel version is upgraded<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable` are added and `lsm=apparmor,bpf` is changed to `lsm=apparmor,bpf,yama`<br><br>* Vulnerability CVE\-2025\-32462 is fixed<br><br>* The /etc/ssh/sshd_config file permission is changed to 600<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed |All |GA |
||Kernel version: 5.15.120.ve.3u2\-amd64 |November 2025 |The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999` |||
|||March 2025 |* The kernel version is upgraded<br><br>* The irqbalance\-ng feature is pre\-installed<br><br>* The network interface multiqueue tool adjust\-nic\-queue is pre\-installed<br><br>* Vulnerability CVE\-2024\-12084 is fixed<br><br>* Startup parameter `spec_rstack_overflow=off` is added<br><br>* The Security Center HIDS driver is updated to version 1.7.0.22<br><br>* The cloud assistant Agent is upgraded to version v1.11.3 |||
||Kernel version: 5.15.120.ve.3u1\-amd64 |October 2024 |* Vulnerability CVE\-2024\-6387 is fixed<br><br>* `ID_LIKE=debian` is added to `/etc/os-release`<br><br>* GRUB2 (GRand Unified Bootloader 2) is compatible with related hardware features of Intel TDX (Trusted Domain Extensions)<br><br>* The default policy for transparent huge pages is set to `enable=always` and `defrag=madvise`<br><br>* Cloud assistant Agent is pre\-installed |||
|||May 2024 |Firstly released online |All |Beta |
|veLinux 2.0 CentOS Compatible for TDX 64 bit |Kernel version: 5.15.120\-2.tdxg.ve2.x86_64 |September 2024 |Firstly released online |All |GA |
|veLinux 2.0 CentOS Compatible 64 bit |Kernel version: 5.15.152\-7.1.ve2.x86_64 |January 2026 |* The kernel version is upgraded<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* The disk read\-ahead cache limit parameter `read_ahead_kb` is changed to `128`.<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed |Asia Pacific (Jakarta), China (Guangzhou), Asia Pacific (Johor), China (Shanghai), China (Beijing) |GA |
||Kernel version: 5.15.120\-5.ve2.x86_64 |November 2025 |The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999` |All |GA |
|||March 2025 |* The kernel version is upgraded<br><br>* The `/etc/sysfs-ng.d/sched.conf` file is added. File configurations are as follows:<br><br>   * `kernel/debug/sched/min_granularity_ns=10000000`<br><br>   * `kernel/debug/sched/wakeup_granularity_ns=15000000`<br><br>* The `/etc/sysfs-ng.d/eth.conf` file is removed<br><br>* The auditd service is disabled<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The cloud assistant Agent is upgraded to version v1.11.3 |||
||Kernel version: 5.15.120\-4.ve2.x86_64 |October 2024 |* The kernel version is upgraded<br><br>* `/etc/velinux-release` is changed to `velinux release 2.x (lyra) CentOS Compat`<br><br>* Related hardware features of Intel TDX (Trusted Domain Extensions) are supported<br><br>* The default policy for transparent huge pages is set to `enable=always` and `defrag=madvise`<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Default behaviors are changed as follows:<br><br>   When you execute the `grub2-mkconfig` command, the value of parameter `GRUB_CMDLINE_LINUX` in the /etc/default/grub file no longer overrides the kernel command line in all BLS (Boot Loader Specification) code snippets by default.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Due to an update in the configuration method for the crashkernel parameter in kexec\-tools, the operation of overriding the kernel command line in BLS code snippets may cause the loss of the crashkernel parameter and failure of the kdump service to start. To avoid this issue, CentOS has changed the default value of parameter <code>GRUB_ENABLE_BLSCFG</code> in the /etc/default/grub file to <code>true</code>. <a href="https://docs.byteplus.com/en/docs/ecs/GRUB_CMDLINE_LINUX">Learn more</a>.</div><br> |||
||Kernel version: 5.15.120\-3.1.ve90.x86_64 |August 2024 |Vulnerability CVE\-2024\-6387 is fixed |All |Beta |
|||May 2024 |Firstly released online |||


<span id="veLinux 1.0"></span>
### veLinux 1.0


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|veLinux 1.0 Quick Boot 64 bit |Kernel version: 5.4.143\-2\-fastboot\-velinux1\-amd64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Based on the startup speed optimizations of the standard veLinux image, for this image version, the system startup further accelerated through additional optimizations to the kernel and Cloud\-init.</div><br> |All |GA |
|veLinux 1.0 MLPS(Dengbao) 64 bit |Kernel version: 5.4.250\-9\-velinux1u2\-amd64 |November 2025 |* The net.ipv4.ip_local_port_range parameter value is changed to 32768 60999<br><br>* The /etc/ssh/sshd_config file permission is changed to 600 |All |GA |
|||August 2025 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added |||
||Kernel version: 5.4.250\-9\-velinux1u1\-amd64 |May 2025 |* The kernel version is upgraded<br><br>* The clock configuration is changed to `clocksource=tsc tsc=reliable`<br><br>* The irqbalance\-ng feature is pre\-installed<br><br>* The network interface multiqueue tool adjust\-nic\-queue is pre\-installed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |||
||Kernel version: 5.4.250\-4\-velinux1u1\-amd64 |July 2024 |* The kernel version is upgraded<br><br>* Container visualization feature is supported<br><br>* The version of Security Center HIDS client is upgraded<br><br>* The value of parameter `PasswordAuthentication` in the OpenSSH configuration file is set to `yes`<br><br>* Pip source (Pypi) is changed to BytePlus intranet image address<br><br>* Hostname changing is supported<br><br>* The blk\-throttle feature is supported<br><br>* The bpfcc\-tools component is pre\-installed<br><br>* eBPF supports the Network Namespace feature<br><br>* Vulnerabilities CVE\-2023\-32233 and CVE\-2023\-1829 are fixed<br><br>* The network jitter issue caused by excessive IPVS statistics is fixed<br><br>* The fuse\-overlayfs component issue is fixed<br><br>* Kernel parameter `CPUfreq` is set to `performance` mode<br><br>* Startup parameter `crash_kexec_post_notifiers` is added<br><br>* IPv6 kernel configuration is optimized. Details are as follows:<br><br>   `net.ipv6.conf.default.accept_ra = 2`<br><br>   `net.ipv6.neigh.default.gc_thresh3=40960`<br><br>   `net.ipv6.neigh.default.gc_thresh2=20480`<br><br>   `net.ipv6.neigh.default.gc_thresh1=10240`<br><br>* Software packages are upgraded:<br><br>   * base\-files is upgraded to version 10.3+velinux1u5<br><br>   * velinux\-release is upgraded to version 1.6.0+velinux1<br><br>   * pciutils is upgraded to version 1:3.8.0\-1+velinux1 to support PCIe Gen 5<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This image version has undergone security enhancement for cloud hosts according to <strong>GB/T22239\-2019 Information security technology — Baseline for classified protection of cybersecurity</strong>. The security enhancement covers aspects such as identity authentication, access control, security auditing, intrusion prevention, and malicious code prevention.</div><br> |||
|veLinux 1.0 CentOS Compatible with 5.10 kernel 64 bit |Kernel version: 5.10.200\-5.ve1.x86_64 |November 2025 |* The CVE\-2020\-26116, CVE\-2020\-27619, CVE\-2021\-3177, CVE\-2021\-3737, CVE\-2022\-0391, CVE\-2021\-28861, CVE\-2022\-48560, CVE\-2022\-45061, CVE\-2023\-31315, and CVE\-2024\-5564 vulnerabilities are fixed<br><br>* The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999`<br><br>* The /etc/ssh/sshd_config file permission is changed to `600` |All |GA |
|||August 2025 |* The kernel version is upgraded<br><br>* Startup parameter `nospectre_v2,nospec_store_bypass_disable,spec_rstack_overflow=off,intel_idle.max_cstate=1 processor.max_cstate=1` is added<br><br>* Vulnerability CVE\-2025\-32462 is fixed<br><br>* Cloud assistant Agent is pre\-installed |||
||Kernel Version: 5.10.200\-3.ve1.x86_64 |May 2025 |* The kernel version is upgraded<br><br>* Startup parameter `spec_rstack_overflow=off` is added<br><br>* The value of `hashsize` in the `nf_conntrack` module is set to `5000000`.<br><br>* `manage_etc_hosts: local` is added to the Cloud\-init configuration<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |||
||Kernel version: 5.10.135\-6.1.ve1.x86_64 |August 2024 |* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed |||
|||May 2024 |* The version of Security Center HIDS client is upgraded<br><br>* The nscd (Name Service Cache Daemon) service is installed |||
|||March 2024 |* The kernel version is upgraded<br><br>* Container visualization feature is supported<br><br>* Dynamic Site Accelerator (DSA) is supported<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This image version supports Sapphire Rapids features such as PMT, DSA/IAX/IAA, AVX, VNNI, ISA, AMX, and SGX.</div><br> |||
|veLinux 1.0 CentOS Compatible 64 bit |Kernel version: 5.4.250\-9.2.ve1.x86_64 |November 2025 |* The CVE\-2020\-26116, CVE\-2020\-27619, CVE\-2021\-3177, CVE\-2021\-3737, CVE\-2022\-0391, CVE\-2021\-28861, CVE\-2022\-48560, CVE\-2022\-45061, CVE\-2023\-31315, and CVE\-2024\-5564 vulnerabilities are fixed<br><br>* Startup parameter `ntel_idle.max_cstate=1 processor.max_cstate=1` is added<br><br>* The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999`<br><br>* The /etc/ssh/sshd_config file permission is changed to `600` |All |GA |
|||August 2025 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added |||
||Kernel version: 5.4.250\-9.1.ve1.x86_64 |May 2025 |* The kernel version is upgraded<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |||
||Kernel version: 5.4.250\-6.ve1.x86_64 |March 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* `manage_etc_hosts: local` is added to the Cloud\-init configuration<br><br>* The value of `hashsize` in the `nf_conntrack` module is set to `5000000`<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 5.4.250\-4.ve1.x86_64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |||
|||May 2024 |* The kernel version is upgraded<br><br>* The version of Security Center HIDS client is upgraded<br><br>* The nscd (Name Service Cache Daemon) service is installed |||
||Kernel version: 5.4.250\-2.3.ve1 |March 2024 |* The kernel version is upgraded<br><br>* Container visualization feature is supported<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This image is fully compatible with CentOS Linux 7 userspace and is equipped with a velinux kernel customized from the kernel community long\-term support (LTS) version 5.4. With years of technical accumulation in the field of operating systems by BytePlus, it surpasses the community version in stability, security, features, and performance, and offers long\-term support.</div><br> |||
|veLinux 1.0 with 5.10 kernel 64 bit |Kernel version: 5.10.200\-5\-velinux1\-amd64 |November 2025 |* Startup parameter `lsm=yama(lsm=apparmor,bpf,yama)` added<br><br>* The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999`<br><br>* The /etc/ssh/sshd_config file permission is changed to `600` |All |GA |
|||August 2025 |* The kernel version is upgraded<br><br>* Startup parameter `nospectre_v2,nospec_store_bypass_disable,spec_rstack_overflow=off` is added<br><br>* Vulnerability CVE\-2025\-32462 is fixed<br><br>* Cloud assistant Agent is pre\-installed |||
||Kernel version: 5.10.200\-4\-velinux1u1\-amd64 |May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-12084 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The irqbalance\-ng feature is pre\-installed<br><br>* The network interface multiqueue tool adjust\-nic\-queue is pre\-installed<br><br>* Startup parameter `spec_rstack_overflow=off` is added. The clock configuration is changed to `clocksource=tsc tsc=reliable` |||
||Kernel version: 5.10.135\-6\-velinux1u1\-amd64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |||
|||May 2024 |* The version of Security Center HIDS client is upgraded<br><br>* The value of parameter `PasswordAuthentication` in the OpenSSH configuration file is set to `yes` |||
|||March 2024 |* The kernel version is upgraded<br><br>* Container visualization feature is supported<br><br>* Dynamic Site Accelerator (DSA) is supported<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This image version supports Sapphire Rapids features such as PMT, DSA/IAX/IAA, AVX, VNNI, ISA, AMX, and SGX.</div><br> |||
|veLinux 1.0 64 bit |Kernel version: 5.4.250\-9\-velinux1u2\-amd64 |November 2025 |* The `net.ipv4.ip_local_port_range` parameter value is changed to `32768 60999`<br><br>* The /etc/ssh/sshd_config file permission is changed to `600` |All |GA |
|||August 2025 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added |||
||Kernel version: 5.4.250\-9\-velinux1u1\-amd64 |May 2025 |The kernel version is upgraded |||
||Kernel version: 5.4.250\-9\-velinux1\-amd64 |March 2025 |* The kernel version is upgraded<br><br>* The irqbalance\-ng feature is pre\-installed<br><br>* The network interface multiqueue tool adjust\-nic\-queue is pre\-installed<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Startup parameter `spec_rstack_overflow=off` is added. The clock configuration is changed to `clocksource=tsc tsc=reliable`<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |||
||Kernel version: 5.4.250\-4\-velinux1u1\-amd64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |||
|||May 2024 |* The version of Security Center HIDS client is upgraded<br><br>* The value of parameter `PasswordAuthentication` in the OpenSSH configuration file is set to `yes` |||
|||March 2024 |* The kernel version is upgraded<br><br>* Container visualization feature is supported |||


<span id="T7MduP1l"></span>
## Third\-party and open\-source public images

<span id="CentOS"></span>
### CentOS


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|CentOS Stream 9 64 bit |Kernel version: 5.14.0\-312.el9.x86_64 |August 2024 |Vulnerability CVE\-2024\-6387 is fixed |All |GA |
|||January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |||
|CentOS Stream 8 64 bit |Kernel version: 4.18.0\-553.5.1.el8.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is preinstalled |All |EOL |
||Kernel version: 4.18.0\-521.el8.x86_64 |January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |All |GA |
|CentOS 8.3 64 bit |Kernel version: 4.18.0\-348.7.1.el8_5.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |All |EOL |
|CentOS 7.9 BIOS 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Cloud assistant Agent is pre\-installed |All |Beta |
|||May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
||Kernel version: 3.10.0\-1160.118.1.el7.x86_64 |July 2024 |Firstly released online |||
|CentOS 7.9 with ofed 23.10 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |February 2025 |Firstly released online |China (Guangzhou), China (Beijing), and China (Shanghai) |GA |
|CentOS 7.9 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |October 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||April 2025 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed<br><br>* Switch the software source to the centos\-vault source<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |||
|CentOS 7.8 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||May 2025 |* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
|||August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.7 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||May 2025 |* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
|||August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.6 with ofed 23.10 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |February 2025 |Firstly released online |China (Guangzhou), China (Beijing), and China (Shanghai) |GA |
|CentOS 7.6 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||May 2025 |* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
|||August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.5 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||May 2025 |* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
|||July 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.4 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Cloud assistant Agent is pre\-installed |All |EOL |
|||May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* The software repository is changed to the centos\-vault repository |||
||Kernel version: 3.10.0\-1160.118.1.el7.x86_64 |July 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.3 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added |All |EOL |
|||May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Switch the software source to centos\-vault source |||
||Kernel version: 3.10.0\-1160.118.1.el7.x86_64 |July 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.2 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |September 2025 |* The Virtio driver version is upgraded<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added |All |EOL |
|||May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Switch the software source to centos\-vault source |||
||Kernel version: 3.10.0\-1160.118.1.el7.x86_64 |July 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 7.1 64 bit |Kernel version: 3.10.0\-1160.119.1.el7.x86_64 |May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Switch the software source to centos\-vault source |All |EOL |
||Kernel version: 3.10.0\-1160.118.1.el7.x86_64 |July 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Vulnerability CVE\-2024\-2961 is fixed<br><br>* The bash\-completion component is pre\-installed |||
||Kernel version: 3.10.0\-1160.102.1.el7.x86_64 |January 2024 |The blk\-none tool is pre\-installed |All |GA |
|CentOS 6.9 64 bit |Kernel version: 2.6.32\-696.30.1.el6.x86_64 |July 2024 |* The growroot component is pre\-installed<br><br>* The version of Security Center HIDS client is upgraded |All |EOL |


<span id="Red Hat Enterprise Linux"></span>
### Red Hat Enterprise Linux


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Red Hat 9.3 64 bit |Kernel version: 5.14.0\-362.24.1.el9_3.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 9.2 64 bit |Kernel version: 5.14.0\-284.88.1.el9_2.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 9.1 64 bit |Kernel version: 5.14.0\-162.23.1.el9_1.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 9.0 64 bit |Kernel version: 5.14.0\-70.101.1.el9_0.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 8.10 64 bit |Kernel version: 4.18.0\-553.22.1.el8_10.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 8.9 64 bit |Kernel version: 4.18.0\-513.24.1.el8_9.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 8.8 64 bit |Kernel version: 4.18.0\-477.75.1.el8_8.x86_64 |November 2024 |Firstly released online |All |GA |
|Red Hat 8.7 64 bit |Kernel version: 4.18.0\-425.19.2.el8_7.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 8.6 64 bit |Kernel version: 4.18.0\-372.105.1.el8_6.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 8.5 64 bit |Kernel version: 4.18.0\-348.23.1.el8_5.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 8.4 64 bit |Kernel version: 4.18.0\-305.88.1.el8_4.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 8.3 64 bit |Kernel version: 4.18.0\-240.22.1.el8_3.x86_64 |December 2024 |Firstly released online |All |GA |
|Red Hat 8.2 64 bit |Kernel version: 4.18.0\-193.91.1.el8_2.x86_64 |December 2024 |Firstly released online |All |GA |


<span id="Ubuntu"></span>
### Ubuntu


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Ubuntu 24.04 with LLM Knowledge Base 64 bit |Kernel version: 6.8.0\-51\-generic |March 2025 |Firstly released online |All |GA |
|Ubuntu 24.04 64 bit |Kernel version: 6.8.0\-55\-generic |February 2026 |* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The following vulnerabilities are fixed: CVE\-2022\-48174, CVE\-2023\-42363, CVE\-2023\-42364, CVE\-2023\-42365, CVE\-2024\-3596, CVE\-2025\-5914, CVE\-2025\-5915, CVE\-2025\-5916, CVE\-2025\-5917, CVE\-2025\-6019, CVE\-2024\-47606, CVE\-2025\-6020, CVE\-2025\-8961, CVE\-2025\-9165, CVE\-2025\-9900, CVE\-2025\-7425, CVE\-2025\-6297, CVE\-2024\-52533, CVE\-2024\-20696, CVE\-2022\-36227, CVE\-2024\-48957, CVE\-2024\-48958, CVE\-2024\-10224, CVE\-2024\-11003, CVE\-2024\-48990, CVE\-2024\-48991, CVE\-2024\-48992, CVE\-2024\-7006, CVE\-2022\-49043, CVE\-2024\-34459, CVE\-2022\-49043, CVE\-2024\-34459, CVE\-2024\-56171, CVE\-2025\-24928, CVE\-2025\-27113, CVE\-2024\-55549, CVE\-2025\-41244, CVE\-2023\-32681, CVE\-2023\-45803, CVE\-2024\-3651, CVE\-2024\-47081, CVE\-2024\-6345, CVE\-2025\-6019, CVE\-2025\-8067<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed |Asia Pacific (Jakarta), China (Guangzhou), Asia Pacific (Johor), China (Shanghai), China (Beijing) |GA |
|||May 2024 |* The kernel version is upgraded<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled<br><br>* Vulnerability CVE\-2024\-12084 is fixed<br><br>* The rule of `qr(^esm-cache\\.service$) => 0` is added to the configuration file of needrestart tool to prevent restart of esm\-cache.service service by the needrestart tool after system update<br><br>* Startup parameters `spec_rstack_overflow=off` and `nospectre_v2 nospec_store_bypass_disable` are added<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |All |GA |
||Kernel version: 6.8.0\-36\-generic |September 2024 |Firstly released online |||
|Ubuntu 22.04 64 bit |Kernel version: 5.15.0\-100\-generic |November 2025 |* The kernel version is upgraded<br><br>* Startup parameter `spec_rstack_overflow=off` is removed and startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* Vulnerability CVE\-2025\-32462 is fixed<br><br>* Cloud assistant Agent is pre\-installed |All |GA |
||<div style="text-align: center"><br></div><br><br><br>Kernel version: 5.15.0\-91\-generic |April 2025 |* apt\-daily and apt\-daily\-upgrade services are disabled<br><br>* Disable jammny\-proposed mirror site<br><br>* Vulnerabilities CVE\-\-2024\-6387 and CVE\-2024\-12084 are fixed<br><br>* Startup parameter `spec_rstack_overflow=off` is added<br><br>* The Security Center HIDS driver is updated to version 1.7.0.22 |||
|||January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* The file configuration of /etc/host is updated to point the hostname to the primary network interface address |||
|Ubuntu 22.04 BIOS 64 bit |Kernel version: 5.15.0\-100\-generic |October 2025 |* The kernel version is upgraded<br><br>* Startup parameter spec_rstack_overflow=off is removed and startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Vulnerability CVE\-2025\-32462 is fixed<br><br>* Cloud assistant Agent is pre\-installed |All |Beta |
||Kernel version: 5.15.0\-91\-generic |May 2025 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-12084 is fixed<br><br>* Startup parameter `spec_rstack_overflow=off` is added<br><br>* The Security Center HIDS driver is updated to version 1.7.0.22<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled<br><br>* The mirror site jammny\-proposed is disabled |||
||Kernel version: 5.15.0\-116\-generic |September 2024 |Firstly released online |||
|Ubuntu 20.04 64 bit |Kernel version: 5.4.0\-208\-generic |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed<br><br>* The following vulnerabilities are fixed: CVE\-2023\-23583, CVE\-2022\-36227, CVE\-2024\-48957, CVE\-2024\-48958, CVE\-2024\-20696, CVE\-2022\-41916, CVE\-2021\-44758, CVE\-2022\-3437, CVE\-2022\-42898, CVE\-2023\-1667, CVE\-2023\-2283, CVE\-2023\-48795, CVE\-2022\-47629, CVE\-2024\-55549, CVE\-2023\-23931, CVE\-2023\-49083, CVE\-2022\-43551, CVE\-2022\-43552, CVE\-2023\-23914, CVE\-2023\-23915, CVE\-2023\-23916, CVE\-2023\-27533, CVE\-2023\-27534, CVE\-2023\-27535, CVE\-2023\-28321, CVE\-2023\-28322, CVE\-2023\-32001, CVE\-2023\-38545, CVE\-2023\-38546, CVE\-2023\-46218, CVE\-2023\-46219, CVE\-2022\-23521, CVE\-2022\-41903, CVE\-2023\-22490, CVE\-2023\-23946, CVE\-2023\-25652, CVE\-2023\-25815, CVE\-2023\-29007, CVE\-2024\-32002, CVE\-2024\-32004, CVE\-2024\-32020, CVE\-2024\-47606, CVE\-2020\-11080, CVE\-2019\-9511, CVE\-2019\-9513, CVE\-2023\-44487, CVE\-2022\-3479, CVE\-2023\-0767, CVE\-2021\-3695, CVE\-2021\-3696, CVE\-2021\-3697, CVE\-2019\-17594, CVE\-2019\-17595, CVE\-2021\-39537, CVE\-2025\-32906, CVE\-2025\-32909, CVE\-2025\-32910, CVE\-2025\-32908, CVE\-2025\-4476, CVE\-2023\-2602, CVE\-2023\-2603, CVE\-2023\-20593, CVE\-2023\-20569, CVE\-2024\-3651, CVE\-2023\-32681, CVE\-2022\-40897, CVE\-2024\-6345, CVE\-2023\-26112 |All |GA |
||Kernel version: 5.4.0\-200\-generic |October 2025 |* The kernel version is upgraded<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |||
||Kernel version: 5.4.0\-186\-generic |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
|Ubuntu 20.04 BIOS 64 bit |Kernel version: 5.4.0\-208\-generic |February 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* Startup parameter `nospectre_v2 nospec_store_bypass_disable` is added<br><br>* The network interface multiqueue tool adjust\-nic\-queue is removed<br><br>* The following vulnerabilities are fixed: CVE\-2022\-41916, CVE\-2021\-44758, CVE\-2022\-3437, CVE\-2022\-42898, CVE\-2023\-20593, CVE\-2023\-20569, CVE\-2021\-43618, CVE\-2023\-2602, CVE\-2023\-2603, CVE\-2022\-1586, CVE\-2022\-1587, CVE\-2019\-17594, CVE\-2019\-17595, CVE\-2021\-39537, CVE\-2022\-3515, CVE\-2022\-47629, CVE\-2023\-32681, and CVE\-2024\-3651 |All |Beta |
||Kernel version: 5.4.0\-200\-generic |September 2025 |* The kernel version is upgraded<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |||
||Kernel version: 5.4.0\-186\-generic |September 2024 |Firstly released online |||
|Ubuntu 18.04 64 bit |Kernel version: 4.15.0\-213\-generic |October 2025 |* The Virtio driver version is upgraded<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Cloud assistant Agent is pre\-installed<br><br>* The mirror site bionic\-proposed is removed<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |All |GA |
|||August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |||
|||January 2024 |* The blk\-none tool is pre\-installed<br><br>* The file configuration of /etc/host is updated to point the hostname to the primary network interface address |||
|Ubuntu 16.04 64 bit |Kernel version: 4.4.0\-210\-generic |December 2024 |The version of cloud\-monitor\-agent plugin is upgraded |All |GA |
|||January 2024 |The blk\-none tool is pre\-installed |||


<span id="Debian"></span>
### Debian


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Debian 12 64 bit |Kernel version: 6.1.0\-18\-amd64 |May 2025 |* Vulnerabilities CVE\-2024\-12084, CVE\-2024\-2961, CVE\-2024\-6387, CVE\-2023\-44487, CVE\-2023\-51385, and CVE\-2023\-28484 are fixed<br><br>* Startup parameter `spec_rstack_overflow=off` is added<br><br>* The irqbalance\-ng feature is pre\-installed<br><br>* The network interface multiqueue tool adjust\-nic\-queue is pre\-installed<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |All |GA |
|||May 2024 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2023\-6246 is fixed<br><br>* The version of Security Center HIDS client is upgraded |||
||Kernel version: 6.1.0\-13\-amd64 |January 2024 |Firstly released online |||
|Debian 11 64 bit |Kernel version: 5.10.0\-30\-amd64 |August 2024 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2024\-6387 is fixed |All |GA |
||Kernel version: 5.10.0\-26\-amd64 |January 2024 |* Vulnerabilities CVE\-2023\-4863 and CVE\-2023\-4911 are fixed<br><br>* QEMU Guest Agent is removed<br><br>* Pip source (Pypi) is changed to BytePlus intranet image address<br><br>* Hostname changing is supported<br><br>* The file configuration of /etc/host is updated to point the hostname to the primary network interface address |||
|Debian 10 BIOS 64 bit |Kernel version: 4.19.0\-27\-amd64 |October 2025 |* The kernel version is upgraded<br><br>* The Virtio driver version is upgraded<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Cloud assistant Agent is pre\-installed<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |All |Beta |
||Kernel version: 4.19.0\-26\-amd64 |July 2024 |Firstly released online |||
|Debian 10 64 bit |Kernel version: 4.19.0\-27\-amd64 |October 2025 |* The kernel version is upgraded<br><br>* The Virtio driver version is upgraded<br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22<br><br>* Startup parameter nospectre_v2 nospec_store_bypass_disable is added<br><br>* Cloud assistant Agent is pre\-installed<br><br>* apt\-daily and apt\-daily\-upgrade services are disabled |All |GA |
||Kernel version: 4.19.0\-26\-amd64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |||
|||January 2024 |The file configuration of /etc/host is updated to point the hostname to the primary network interface address |||
|Debian 9 64 bit |Kernel version: 4.9.0\-19\-amd64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |All |GA |
|||January 2024 |The file configuration of /etc/host is updated to point the hostname to the primary network interface address |||


<span id="OpenSUSE"></span>
### SUSE Linux Enterprise Server


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|SUSE 15 SP6 64 bit |Kernel version: 6.4.0\-150600.21\-default |September 2025 |Firstly released online |All |GA |
|SUSE 15 SP5 64 bit |Kernel version: 5.14.21\-150500.53\-default |May 2025 |Firstly released online |All |GA |


<span id="flrdrvAd"></span>
### OpenSUSE


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|OpenSUSE 15.6 64 bit |Kernel version: 6.4.0\-150600.23.14\-default |September 2025 |Firstly released online |All |GA |
|OpenSUSE 15.5 64 bit |Kernel version: 5.14.21\-150500.55.68\-default |January 2026 |Firstly released online |All |GA |
|OpenSUSE 15.4 64 bit |Kernel version: 5.14.21\-150400.24.100\-default |April 2025 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* Network management tool is upgraded from NetworkManager to wicked.service<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After the upgrade, the operating system will not automatically recognize the primary private IP address of the secondary network interface and add the corresponding route. You need to configure the secondary network interface and route for the ECS instances. <a href="https://docs.byteplus.com/en/docs/ecs/Configuring-auxiliary-network-interfaces-for-ECS-instances">Learn more</a>.   </div><br>   <br><br>* The Security Center HIDS driver is upgraded to version 1.7.0.22 |All |GA |
||Kernel version: 5.14.21\-150400.24.41\-default |January 2024 |QEMU Guest Agent is removed |||


<span id="Fedora"></span>
### Fedora


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Fedora 37 64 bit |Kernel version: 6.3.8\-100.fc37.x86_64 |July 2023 |* The kernel version is upgraded<br><br>* Known issues are fixed |All |GA |
||Kernel version: 6.0.18\-300.fc37.x86_64 |March 2023 |Firstly released online |||


<span id="Rocky Linux"></span>
### Rocky Linux


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Rocky Linux 9.5 64 bit |Kernel version: 5.14.0\-503.26.1.el9_5.x86_64 |May 2025 |Firstly released online |All |GA |
|Rocky Linux 9.4 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |November 2024 |Firstly released online |All |GA |
|Rocky Linux 9.3 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |Firstly released online |All |GA |
|Rocky Linux 9.2 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |* The kernel version is upgraded<br><br>* Bugs in the community kernel are mitigated<br><br>* Redundant clock synchronization sources are deleted |All |GA |
||Kernel version: 5.14.0\-362.13.1.el9_3.x86_64 |March 2024 |Firstly released online |||
|Rocky Linux 9.1 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |All |GA |
|Rocky Linux 9.0 64 bit |Kernel version: 5.14.0\-362.18.1.el9_3.x86_64 |August 2024 |The version of cloud\-monitor\-agent plugin is upgraded |All |GA |
|||March 2024 |Firstly released online |||
|Rocky Linux 8.10 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The kernel module extension package (kernel\-modules\-extra) is pre\-installed<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added |All |GA |
||Kernel version: 4.18.0\-553.16.1.el8_10.x86_64 |October 2024 |Firstly released online |||
|Rocky Linux 8.9 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The kernel module extension package (kernel\-modules\-extra) is pre\-installed<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.16.1.el8_10.x86_64 |October 2024 |Firstly released online |||
|Rock Linux 8.8 with ofed 23.10 64 bit |Kernel version: 4.18.0\-553.el8_10.x86_64 |February 2025 |Firstly released online |China (Guangzhou), China (Beijing), and China (Shanghai) |GA |
|Rocky Linux 8.8 with ofed 24.10 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |February 2025 |Firstly released online |China (Shanghai), China (Beijing) |GA |
|Rocky Linux 8.8 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The hostname is associated with the primary private IP address of the primary network interface<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.el8_10.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 4.18.0\-513.11.1.el8_9.x86_64 |March 2024 |Firstly released online |||
|Rocky Linux 8.7 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The kernel module extension package (kernel\-modules\-extra) is pre\-installed<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.el8_10.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 4.18.0\-513.5.1.el8_9.x86_64 |January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |||
|Rocky Linux 8.6 64 bit |Kernel version: 4.18.0\-553.36.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The kernel module extension package (kernel\-modules\-extra) is pre\-installed<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.5.1.el8_10.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 4.18.0\-513.11.1.el8_9.x86_64 |March 2024 |Firstly released online |||
|Rocky Linux 8.5 64 bit |Kernel version: 4.18.0\-553.36.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The client proxima is replaced by the Cloud Security Center client elkeid\-agent, which is preinstalled<br><br>* The kernel module extension package (kernel\-modules\-extra) is pre\-installed<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added<br><br>* kexec\-tools version is updated to 2.0.26\-14.el8_10.2 |All |GA |
||Kernel version: 4.18.0\-553.8.1.el8_10.x86_64 |January 2024 |* The kernel version is upgraded<br><br>* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |||
|Rocky Linux 8.4 with ofed 24.10 64 bit |Kernel version: 4.18.0\-553.51.1.el8_10.x86_64 |February 2025 |Firstly released online |China (Shanghai), China (Beijing) |GA |


<span id="AlmaLinux"></span>
### AlmaLinux


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|AlmaLinux 9.4 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |Firstly released online |All |GA |
|AlmaLinux 9.3 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |Firstly released online |All |GA |
|AlmaLinux 9.2 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |* The kernel version is upgraded<br><br>* Bugs in the community kernel are mitigated<br><br>* Redundant clock synchronization sources are deleted |All |GA |
||Kernel version: 5.14.0\-362.24.2.el9_3.x86_64 |May 2024 |Firstly released online |||
|AlmaLinux 9.1 64 bit |Kernel version: 5.14.0\-284.30.1.el9_2.x86_64 |December 2024 |* Bugs in the community kernel are mitigated<br><br>* Redundant clock synchronization sources are deleted |All |GA |
|||January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |||
|AlmaLinux 8.10 64 bit |Kernel version: 4.18.0\-553.16.1.el8_10.x86_64 |October 2024 |Firstly released online |All |GA |
|AlmaLinux 8.9 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |February 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.16.1.el8_10.x86_64 |October 2024 |Firstly released online |||
|AlmaLinux 8.8 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |March 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The hostname associated with the primary private IP address of the primary network interface<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.el8_10.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 4.18.0\-513.24.1.el8_9.x86_64 |May 2024 |Firstly released online |||
|AlmaLinux 8.7 64 bit |Kernel version: 4.18.0\-553.44.1.el8_10.x86_64 |February 2026 |* The kernel version is upgraded<br><br>* Cloud assistant Agent is pre\-installed<br><br>* irqbalance\-ng is pre\-installed<br><br>* The Cloud Security Center client proxima is replaced by the preinstalled client elkeid\-agent<br><br>* The hostname is associated with the primary private IP address of the primary network interface<br><br>* Startup parameters `nospectre_v2 nospec_store_bypass_disable spec_rstack_overflow=off` are added<br><br>* Kdump is enabled and startup parameters `crash_kexec_post_notifiers crashkernel=0M-2G:0M,2G-8G:192M,8G-16G:256M,16G-64G:384M,64G-128G:512M,128G-486G:768M,486G-:1024M` are added |All |GA |
||Kernel version: 4.18.0\-553.el8_10.x86_64 |August 2024 |* The kernel version is upgraded<br><br>* The version of cloud\-monitor\-agent plugin is upgraded |||
||Kernel version: 4.18.0\-513.5.1.el8_9.x86_64 |January 2024 |* Vulnerability CVE\-2023\-4911 is fixed<br><br>* QEMU Guest Agent is removed |||


<span id="Windows Server"></span>
### Windows Server


|Versions |Image information |Release date |Release content |Release regions |Stage |
|---|---|---|---|---|---|
|Windows Server 2022 Standard Edition 64\-bit Chinese |\- |October 2025 |Firstly released online |China (Beijing), China (Guangzhou), China (Shanghai) |GA |
|Windows Server 2022 Standard Edition 64\-bit English |\- |October 2025 |Firstly released online |China (Beijing), China (Guangzhou), China (Shanghai) |GA |
|Windows Server 2022 Datacenter Edition 64\-bit Chinese UEFI |\- |November 2025 |Firstly released online |All |GA |
|Windows Server 2022 Datacenter Edition 64\-bit Chinese |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||October 2024 |* The vulnerability of Remote Desktop Protocol (RDP) is fixed<br><br>* The issue where some applications can not be installed is fixed |||
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The account locking threshold in account lock policy ("Account Lockout Policy \> Account lockout threshold") is set to `0`<br><br>* The task of disk optimization is disabled in Task Scheduler ("Windows \> Defrag \> ScheduledDefrag") <br><br>* The task of Edge browser automatic upgrade in Task Scheduler is disabled and deleted ("Windows \> UpdateOrchestrator \> MicrosoftEdgeUpdateTaskMachineCore")<br><br>* The task of Edge browser automatic upgrade for the current account in "Task Scheduler" is disabled and deleted ("Windows \> UpdateOrchestrator \> MicrosoftEdgeUpdateTaskMachineUA")<br><br>* The Microsoft Edge Elevation Service (MicrosoftEdgeElevationService) is disabled in "Services(Local)"<br><br>* The Microsoft Edge Update Service (edgeupdate) is disabled in "Services(Local)"<br><br>* The Microsoft Edge Update Service (edgeupdatem) is disabled in "Services(Local)" |||
|Windows Server 2022 Datacenter Edition 64\-bit English |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||October 2024 |* The vulnerability of Remote Desktop Protocol (RDP) is fixed<br><br>* The issue where some applications can not be installed is fixed |||
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in Task Scheduler ("Windows \> Defrag \> ScheduledDefrag") <br><br>* The task of Edge browser automatic upgrade in Task Scheduler is disabled and deleted ("Windows \> UpdateOrchestrator \> MicrosoftEdgeUpdateTaskMachineCore")<br><br>* The task of Edge browser automatic upgrade for the current account in "Task Scheduler" is disabled and deleted ("Windows \> UpdateOrchestrator \> MicrosoftEdgeUpdateTaskMachineUA")<br><br>* The Microsoft Edge Elevation Service (MicrosoftEdgeElevationService) is disabled in "Services(Local)"<br><br>* The Microsoft Edge Update Service (edgeupdate) is disabled in "Services(Local)"<br><br>* The Microsoft Edge Update Service (edgeupdatem) is disabled in "Services(Local)" |||
|Windows Server 2019 Datacenter Edition 64\-bit Chinese |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag") |||
|Windows Server 2019 Datacenter Edition 64\-bit English |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag") |||
|Windows Server 2016 Datacenter Edition 64\-bit Chinese |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||October 2024 |* The vulnerability of Remote Desktop Protocol (RDP) is fixed<br><br>* The issue where some applications can not be installed is fixed |||
|||August 2024 |* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Cloudbase\-init is optimized |||
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag") |||
|Windows Server 2016 Datacenter Edition 64\-bit English |\- |May 2025 |* Virtio driver is upgraded to version 0.1.266<br><br>* The Windows update server address is set to `http://wsus.update.ivolces.com` |All |GA |
|||October 2024 |* The vulnerability of Remote Desktop Protocol (RDP) is fixed<br><br>* The issue where some applications can not be installed is fixed |||
|||August 2024 |* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* Cloudbase\-init is optimized |||
|||May 2024 |* Virtio driver is upgraded to version 0.1.240<br><br>* "Windows Update Group Policy \> Configure Automatic Updates" is enabled, and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag") |||
|Windows Server 2012 R2 Datacenter Edition 64\-bit Chinese |<div style="text-align: center"><br></div><br><br><br>\- |May 2025 |Set the Windows Update server address to `http://wsus.update.ivolces.com`. |All |EOL |
|||August 2024 |* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* The version of reset\-authentication plugin is upgraded<br><br>* Cloudbase\-init is optimized<br><br>* The automatic update policy is enabled ("Windows Update Group Policy \> Configure Automatic Updates"), and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag")<br><br>* Virtio driver is upgraded to version 0.1.215 |||
|Windows Server 2012 R2 Datacenter Edition 64\-bit English |\- |May 2025 |The Windows update server address is set to `http://wsus.update.ivolces.com` |All |EOL |
|||August 2024 |* The version of cloud\-monitor\-agent plugin is upgraded<br><br>* The version of reset\-authentication plugin is upgraded<br><br>* Cloudbase\-init is optimized<br><br>* The automatic update policy is enabled ("Windows Update Group Policy \> Configure Automatic Updates"), and `2 - Notify for download and auto install` is set<br><br>* The task of disk optimization is disabled in "Task Scheduler" ("Windows \> Defrag \> ScheduledDefrag")<br><br>* Virtio driver is upgraded to version 0.1.215 |||
