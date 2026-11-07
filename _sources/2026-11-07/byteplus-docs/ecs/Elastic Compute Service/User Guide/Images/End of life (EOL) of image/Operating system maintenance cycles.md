---
title: "Operating system maintenance cycles"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/OS-discontinuing-plan"
---

When using an ECS instance, we recommend you learn​ two key points: the lifecycle of the operating system on the image and the technical support plan during your usage of an ECS instance. This can help you comprehensively select an image version suitable for businesses to support long\-term stable operations and reduce maintenance costs caused by downtime of the operating system.

This topic introduces operating systems of public images provided by the platform, and the end\-of\-support plans for third\-party operating systems.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If an operating system version reaches the end of lifecycle (End of Life, EOL), the platform will stop providing technical support services for instances that use this operating system version.</div>



* <div data-tips="true" data-tips-type="warning">veLinux is the official operating system provided by the platform. After veLinux reaches EOL, the platform will still provide technical support to you as much as possible.</div>


* <div data-tips="true" data-tips-type="warning">For commercial or open\-source operating system images provided by other third parties, if the third party stops support or maintenance (EOL), the platform will no longer provide technical support.</div>



<span id=".dmVMaW51eCBFT0zorqHliJI="></span>
## EOL plan for veLinux

<span id="veLinux 2.0"></span>
### veLinux 2.0


|Version |Full support phase |Maintenance and support phase |Extended support phase |End of service date |
|---|---|---|---|---|
|veLinux 2.0 64 bit |2024\-05 to 2027\-04 |2027\-04\-30 to 2030\-04\-30 |2030\-04\-30 to 2031\-04\-30 |2031\-04\-30 |
|veLinux 2.0 CentOS Compatible 64 bit |2024\-05 to 2027\-04 |2027\-04\-30 to 2029\-04\-30 |2029\-04\-30 to 2031\-04\-30 |2031\-04\-30 |


<span id="veLinux 1.0"></span>
### veLinux 1.0


|Version |Full support phase |Maintenance and support phase |Extended support phase |End of service date |
|---|---|---|---|---|
|veLinux 1.0 |2021\-12 to 2024\-06 |2024\-06\-30 to 2027\-06\-30 |2027\-06\-30 to 2028\-06\-30 |2028\-06\-30 |
|veLinux 1.0 Quick Boot |2022\-09 to 2024\-06 |2024\-06\-30 to 2027\-06\-30 |2027\-06\-30 to 2028\-06\-30 |2028\-06\-30 |
|veLinux 1.0 MLPS (Dengbao) |2022\-09 to 2024\-06 |2024\-06\-30 to 2027\-06\-30 |June 30, 2027 to June 30, 2028 |2028\-06\-30 |
|veLinux 1.0 with 5.10 kernel |2022\-09 to 2024\-06 |2024\-06\-30 to 2027\-06\-30 |2027\-06\-30 to 2028\-06\-30 |2028\-06\-30 |
|veLinux 1.0 CentOS Compatible with 5.10 kernel |2022\-09 to 2024\-06 |2024\-06\-30 to 2026\-06\-30 |2026\-06\-30 to 2028\-06\-30 |2028\-06\-30 |
|veLinux 1.0 CentOS Compatible |2022\-09 to 2024\-06 |2024\-06\-30 to 2026\-06\-30 |2026\-06\-30 to 2028\-06\-30 |2028\-06\-30 |


<span id=".56ys5LiJ5pa55pON5L2c57O757ufRU9M6K6h5YiS"></span>
## EOL plan for third\-party operating systems

You can view EOL plans for certain operating system versions in the table below. For more EOL information, refer to the official website of the corresponding operating system.

<span id="Red Hat Enterprise Linux（RHEL）"></span>
### Red Hat Enterprise Linux (RHEL)

For the official maintenance time of more versions, check the [Red Hat Enterprise Linux official website](https://access.redhat.com/support/policy/updates/errata).


|Version |End of full support date |End of maintenance support date |End of extended lifecycle support (ELS) add\-on service |
|---|---|---|---|
|Red Hat Enterprise Linux 9 |2027\-05\-31 |2032\-05\-31 |2035\-05\-31 |
|Red Hat Enterprise Linux 8 |2024\-05\-31 |2029\-05\-31 |2032\-05\-31 |


<span id="CentOS"></span>
### CentOS

For the official maintenance time of more versions, check the [CentOS official website](https://www.centos.org/cl-vs-cs/).


|Version |End of full update date |End of maintenance and update date |
|---|---|---|
|CentOS Stream 9 |2027\-05\-31 |2027\-05\-31 |
|CentOS Stream 8 |2024\-05\-31 |2024\-05\-31 |
|CentOS 8 |2021\-12\-31 |2021\-12\-31 |
|CentOS 7 |2020\-08\-06 |2024\-06\-30 |
|CentOS 6 |2017\-05\-10 |2020\-11\-30 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For response policies after the maintenance for CentOS Linux stops, refer to the <a href="https://docs.byteplus.com/en/docs/ecs/discontinuing-of-CentOS-Linux">Description of the discontinued maintenance of CentOS Linux</a>.</div>


<span id="Ubuntu"></span>
### Ubuntu

For the official maintenance time of more versions, check the [Ubuntu official website](https://wiki.ubuntu.com/Releases?spm=a2c63.p38356.0.0.4aed1c70rz0PQz).


|Version |Standard support end date |EOL date |
|---|---|---|
|Ubuntu 24.04 64 bit |2029\-06 |2036\-04 |
|Ubuntu 22.04 64 bit |2027\-06 |2034\-04 |
|Ubuntu 20.04 64 bit |2025\-04 |2032\-04 |
|Ubuntu 18.04 64 bit |2023\-06 |2030\-04 |
|Ubuntu 16.04 64 bit |2021\-04 |2028\-04 |


<span id="Debian"></span>
### Debian

For the official maintenance time of more versions, check the [Debian official website](https://wiki.debian.org/DebianReleases?spm=a2c63.p38356.0.0.4aed1c70rz0PQz).


|Version |EOL date |LTS date |ELTS date |
|---|---|---|---|
|Debian 12 |\- |\- |\- |
|Debian 11 |2024\-07 |\- |\- |
|Debian 10 |2022\-09\-10 |2024\-06\-30 |\- |
|Debian 9 |2020\-07\-18 |2022\-07\-01 |2027\-06\-30 |


<span id="OpenSUSE"></span>
### SUSE Linux Enterprise Server (SUSE Linux)

For the official maintenance time of more versions, check the [SUSE Linux official website](https://www.suse.com/lifecycle/).


|**Version** |**General support end date (** General Ends **)**  |**End of LTSS date (** LTSS Ends **)**  |
|---|---|---|
|SUSE Linux Enterprise Server 15 SP6 |6 months after the release of SUSE Linux Enterprise Server 15 SP7 |42 months after the release of SUSE Linux Enterprise Server 15 SP7 |
|SUSE Linux Enterprise Server 15 SP5 |2024\-12\-31 |2027\-12\-31 |


<span id="OpenSUSE"></span>
### OpenSUSE

For the official maintenance time of more versions, check the [OpenSUSE official website](https://en.opensuse.org/Lifetime?spm=a2c63.p38356.0.0.4aed1c70rz0PQz).


|Version |EOL date |
|---|---|
|OpenSUSE 15.4 |2023\-12 |


<span id="Fedora"></span>
### Fedora

For the official maintenance time of more versions, check the [Fedora official website](https://docs.fedoraproject.org/en-US/releases/eol/?spm=a2c63.p38356.0.0.4aed1c70rz0PQz).


|Version |EOL date |
|---|---|
|Fedora 37 |2023\-12\-05 |


<span id="Rocky Linux"></span>
### Rocky Linux

For the official maintenance time of more versions, check the [Rocky Linux official website](https://docs.rockylinux.org/release_notes/).


|Version |EOL date |
|---|---|
|Rocky Linux 9.4 |2032\-05\-31 |
|Rocky Linux 9.3 ||
|Rocky Linux 9.2 ||
|Rocky Linux 9.1 ||
|Rocky Linux 9.0 ||
|Rocky Linux 8.10 |2029\-05\-31 |
|Rocky Linux 8.9 ||
|Rocky Linux 8.8 ||
|Rocky Linux 8.7 ||
|Rocky Linux 8.6 ||
|Rocky Linux 8.5 ||


<span id="AlmaLinux"></span>
### AlmaLinux

For the official maintenance time of more versions, check the [AlmaLinux official website](https://wiki.almalinux.org/release-notes/).


|Version |Active support end date |Security support end date |
|---|---|---|
|AlmaLinux 9.4 |2027\-05\-31 |2032\-05\-31 |
|AlmaLinux 9.3 |||
|AlmaLinux 9.2 |||
|AlmaLinux 9.1 |||
|AlmaLinux 8.8 |2024\-05\-31 |2029\-05\-31 |
|AlmaLinux 8.7 |||


<span id="Windows Server"></span>
### Windows Server

For the official maintenance time of more versions, check the [Microsoft Windows Server official website](https://docs.microsoft.com/zh-cn/lifecycle/products/?products=windows).


|Version |Mainstream support end date |End of extended service support date |
|---|---|---|
|Windows Server 2022 Datacenter Edition |2026\-10\-13 |2031\-10\-14 |
|Windows Server 2019 Datacenter Edition |2024\-01\-09 |2029\-01\-09 |
|Windows Server 2016 Datacenter Edition |2022\-01\-11 |2027\-01\-12 |
|Windows Server 2012 R2 Datacenter Edition |2018\-10\-09 |2023\-10\-10 |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Microsoft stopped providing support for Windows Server 2012 R2 operating systems on October 10, 2023. Therefore, the platform will no longer provide technical support for ECS instances that use this operating system. If you have ECS instances that use the above operating systems, please upgrade to Windows Server 2019 or a later version as soon as possible.</div>
