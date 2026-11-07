---
title: "Public image overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Public-image-overview"
---

Public images are images officially provided by the platform with legitimate copyrights. Therefore, this type of image offers high security and stability. Currently, public images include the mainstream Windows Server and Linux images and self\-developed veLinux images of the platform. They are available for all users to view or use.

<span id=".5YWs5YWx6ZWc5YOP57G75Z6L"></span>
## Public image type

The platform provides self\-developed, third\-party, and open\-source public images.


|Public image type |Description |Technical support |
|---|---|---|
|[veLinux image](https://docs.byteplus.com/en/docs/ecs/Public-image-overview#.dmVMaW51eOmVnOWDjw==) |A self\-developed Linux operating system launched by the platform. veLinux is deeply customized and optimized for public cloud environments. This aims to provide you with a stable, high\-performance, secure, and user\-friendly Linux operating system option, as well as a comprehensive full\-lifecycle management solution. |veLinux images provide long\-term support that includes security updates and issue fixes, and technical support for any issues you encounter during usage. |
|[Third-party and open-source public images](https://docs.byteplus.com/en/docs/ecs/Public-image-overview#.56ys5LiJ5pa55Y-K5byA5rqQ5YWs5YWx6ZWc5YOP) |Images that the platform develops based on the community version. The platform carries out strict testing before releasing them. This ensures that images can run safely and stably on ECS instances. The images include:<br><br><br>* Commercial images: Windows Server, Red Hat Enterprise Linux, SUSE Linux Enterprise Server<br><br>* Open source images: CentOS, CentOS Stream, Ubuntu, Debian, OpenSUSE, Fedora, Rocky Linux, AlmaLinux |* For commercial edition images, the platform provides you with a license for activation and with technical support by working with original operating system manufacturers.<br><br>* For open\-source images, please contact open source communities for technical support. Meanwhile, BytePlus platform will also provide corresponding technical assistance for issue investigation. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Fees may be incurred when you use commercial images. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Imagebilling">Billing of image</a>.</div>


* <div data-tips="true" data-tips-type="tip">The above technical support service is only available to images in their lifecycles. If an image version has reached the end of lifecycle (End of Life, EOL), the services will be provided based on the EOL image support policy. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/OS-discontinuing-plan">Operating system maintenance cycle</a>.</div>


* <div data-tips="true" data-tips-type="tip">The platform regularly releases or updates public images. To view the public image list, refer to the <a href="https://docs.byteplus.com/en/docs/ecs/Image-release-notes">Image release notes</a>, or go to the <a href="https://console.byteplus.com/image/images">Image console</a>.</div>



<span id=".dmVMaW51eOmVnOWDjw=="></span>
## veLinux image


|Operating system type |Operating system version |
|---|---|
|veLinux |* veLinux 2.0 64 bit<br><br>* veLinux 2.0 for TDX 64 bit |
||* veLinux 1.0 64 bit<br><br>* veLinux 1.0 Quick Boot 64 bit<br><br>* veLinux 1.0 MLPS(Dengbao) 64 bit<br><br>* veLinux 1.0 CentOS Compatible with 5.10 kernel 64 bit<br><br>* veLinux 1.0 CentOS Compatible 64 bit<br><br>* veLinux 1.0 with 5.10 kernel 64 bit |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">veLinux images use <code>UEFI</code> as the default boot mode.</div>


<span id=".56ys5LiJ5pa55Y-K5byA5rqQ5YWs5YWx6ZWc5YOP"></span>
## Third\-party and open\-source public images

<span id=".TGludXjplZzlg48="></span>
### Linux image


|Operating system type |Operating system version |
|---|---|
|Red Hat Enterprise Linux |* Red Hat 9.3 64 bit<br><br>* Red Hat 9.2 64 bit<br><br>* Red Hat 9.1 64 bit<br><br>* Red Hat 9.0 64 bit<br><br>* Red Hat 8.10 64 bit<br><br>* Red Hat 8.9 64 bit<br><br>* Red Hat 8.8 64 bit<br><br>* Red Hat 8.7 64 bit<br><br>* Red Hat 8.6 64 bit<br><br>* Red Hat 8.5 64 bit<br><br>* Red Hat 8.4 64 bit<br><br>* Red Hat 8.3 64 bit<br><br>* Red Hat 8.2 64 bit |
|CentOS |* CentOS Stream 9 64 bit<br><br>* CentOS Stream 8 64 bit<br><br>* CentOS 8.3 64 bit<br><br>* CentOS 7.9 BIOS 64 bit<br><br>* CentOS 7.9 64 bit<br><br>* CentOS 7.8 64 bit<br><br>* CentOS 7.7 64 bit<br><br>* CentOS 7.6 64 bit<br><br>* CentOS 7.5 64 bit<br><br>* CentOS 7.4 64 bit<br><br>* CentOS 7.3 64 bit<br><br>* CentOS 7.2 64 bit<br><br>* CentOS 7.1 64 bit<br><br>* CentOS 6.9 64 bit |
|Ubuntu |* Ubuntu 24.04 64 bit<br><br>* Ubuntu 22.04 64 bit<br><br>* Ubuntu 22.04 BIOS 64 bit<br><br>* Ubuntu 20.04 64 bit<br><br>* Ubuntu 20.04 BIOS 64 bit<br><br>* Ubuntu 18.04 64 bit<br><br>* Ubuntu 16.04 64 bit |
|Debian |* Debian 12 64 bit<br><br>* Debian 11 64 bit<br><br>* Debian 10 64 bit<br><br>* Debian 10 BIOS 64 bit<br><br>* Debian 9 64 bit |
|SUSE Linux Enterprise Server |* SUSE 15 SP6 64 bit<br><br>* SUSE 15 SP5 64 bit |
|OpenSUSE |* OpenSUSE 15.6 64 bit<br><br>* OpenSUSE 15.4 64 bit |
|Fedora |Fedora 37 64 bit |
|Rocky Linux |* Rocky Linux 9.5 64 bit<br><br>* Rocky Linux 9.4 64 bit<br><br>* Rocky Linux 9.2 64 bit<br><br>* Rocky Linux 9.1 64 bit<br><br>* Rocky Linux 9.0 64 bit<br><br>* Rocky Linux 8.10 64 bit<br><br>* Rocky Linux 8.9 64 bit<br><br>* Rocky Linux 8.8 64 bit<br><br>* Rocky Linux 8.7 64 bit<br><br>* Rocky Linux 8.6 64 bit<br><br>* Rocky Linux 8.5 64 bit |
|AlmaLinux |* AlmaLinux 9.4 64 bit<br><br>* AlmaLinux 9.3 64 bit<br><br>* AlmaLinux 9.2 64 bit<br><br>* AlmaLinux 9.1 64 bit<br><br>* AlmaLinux 8.10 64 bit<br><br>* AlmaLinux 8.9 64 bit<br><br>* AlmaLinux 8.8 64 bit<br><br>* AlmaLinux 8.7 64 bit |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">BIOS images are in Beta. If you need a trial, please contact your account manager.</div>


* <div data-tips="true" data-tips-type="tip">For the certification information of Red Hat Enterprise Linux and supported instance types, please visit the <a href="https://catalog.redhat.com/cloud/detail/250467">Red Hat official website</a>.</div>


* <div data-tips="true" data-tips-type="tip">Linux public images use <code>UEFI</code> as the default boot mode. For Linux public images of distributions that support <code>BIOS</code>, the boot mode is <code>Legacy</code>.</div>



<span id=".V2luZG93cyBTZXJ2ZXLplZzlg48="></span>
### Windows Server image


|Operating system type |Operating system version |
|---|---|
|Windows Server 2022 |* Windows Server 2022 Datacenter Edition 64\-bit Chinese<br><br>* Windows Server 2022 Datacenter Edition 64\-bit English |
|Windows Server 2019 |* Windows Server 2019 Datacenter Edition 64\-bit Chinese<br><br>* Windows Server 2019 Datacenter Edition 64\-bit English |
|Windows Server 2016 |* Windows Server 2016 Datacenter Edition 64\-bit Chinese<br><br>* Windows Server 2016 Datacenter Edition 64\-bit English |
|Windows Server 2012 R2 |* Windows Server 2012 R2 Datacenter Edition 64\-bit Chinese<br><br>* Windows Server 2012 R2 Datacenter Edition 64\-bit English |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Windows Server public images use <code>Legacy</code> as the default boot mode.</div>


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

Except for the Windows Server public images, the public images provided by the platform do not have graphical desktop components installed by default. You can [install the graphical user interface of the Linux operating system](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux) by yourself.
