---
title: "Instructions on compatibility between AMD instance types and operating systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/AMD-instance-types-and-OS-compatibility"
---

Due to defects in support for some new features of AMD processors on older operating systems, you need to select an operating system for AMD instances as appropriate. This topic describes ECS instances equipped with AMD processors and their compatibility with different operating systems.

<span id=".5pSv5oyBQU1EIEVQWUPihKIgR2Vub2HlpITnkIblmajnmoTmk43kvZzns7vnu58="></span>
## Operating systems compatible with AMD EPYC™ Genoa processor

**Instance types**

ECS instances equipped with the 4th\-generation AMD EPYC™ Genoa processors are as follows:


* [General-purpose g3al](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNhbA==), [Compute-optimized c3al](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNhbA==), and [Memory-optimized r3al](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#zOMddgDz)

* [General-purpose g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNh), [Compute-optimized c3a](https://docs.byteplus.com/en/docs/ecs/Computing-optimized#.6K6h566X5Z6LYzNh), and [Memory-optimized r3a](https://docs.byteplus.com/en/docs/ecs/Memory-optimized#qEWtPNM0)


**List of supported images**

The following table lists the BytePlus public image versions supported for instance types equipped with the 4th\-generation AMD EPYC™ Genoa processors.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you run AMD instances on an operating system not officially supported, please evaluate and bear the potential risks.</div>



|Operating systems |Operating system version |
|---|---|
|CentOS |CentOS Stream 9 64 bit |
|Debian |Debian 11 64 bit |
|Ubuntu |Ubuntu Server 22.04 LTS 64 bit |
|veLinux |* veLinux 1.0 64 bit<br><br>* veLinux 1.0 64 bit CentOS\-compatible version<br><br>* veLinux 1.0 with 5.10 kernel 64 bit<br><br>* veLinux 1.0 CentOS compatible version with 5.10 kernel 64 bit |
|OpenSUSE |OpenSUSE 15.4 64 bit |
|Fedora |Fedora 37 64 bit |
|AlmaLinux |* AlmaLinux 9.x 64 bit<br><br>* AlmaLinux 8.x 64 bit |
|Rocky Linux |* Rocky Linux 9.x 64 bit<br><br>* Rocky Linux 8.x 64 bit |
|Windows Server |* Windows Server 2022 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2022 Datacenter Edition 64 bit English<br><br>* Windows Server 2019 Datacenter Edition 64 bit Chinese<br><br>* Windows Server 2019 Datacenter Edition 64 bit English<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, only g3al, c3al, and r3al support using the above Windows image. g3a, c3a, r3a, and i4ag do not support these images.</div><br> |


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* For details about other public image versions provided by BytePlus, see the [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes).

* For more information about images compatible with AMD processors, refer to the official AMD documentation: [Minimum operating system requirements for AMD EPYC™ 9004 and AMD EPYC™ 9005 series processors](https://www.amd.com/content/dam/amd/en/documents/products/epyc/epyc-operating-systems.pdf).
