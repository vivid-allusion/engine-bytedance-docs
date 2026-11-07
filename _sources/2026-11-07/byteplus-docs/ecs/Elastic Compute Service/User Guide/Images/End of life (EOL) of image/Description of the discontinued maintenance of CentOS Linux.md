---
title: "Description of the discontinued maintenance of CentOS Linux"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/discontinuing-of-CentOS-Linux"
---

CentOS has officially announced the plan​ to discontinue maintenance of the CentOS Linux project. This will also affect the CentOS Linux public images provided by the platform. By then, the maintenance and support for the CentOS Linux operating system will no longer be available. This topic introduces impacts of discontinued maintenance of CentOS Linux, and responsive measures.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

On December 8, 2020, CentOS officially announced it would discontinue maintenance of the CentOS Linux project and shift its focus to the CentOS Stream project. For more information, see the [official announcement on the CentOS website](https://blog.centos.org/2020/12/future-is-centos-stream/?spm=a2c4g.11186623.0.0.3b001a2eVa6q7u).

After the discontinuation, impacts on current CentOS versions and future versions are as follows:


1. Maintenance of CentOS Linux 7 will be discontinued on June 30, 2024 (EOL).

2. Maintenance of CentOS Linux 8 was discontinued on December 31, 2021 (EOL).

3. CentOS Linux 9 and future versions will not be provided; instead, CentOS Stream will be available.


<span id=".5b2x5ZON"></span>
## Impact

Based on the official change plan of CentOS on the CentOS Linux project, impacts on users of the CentOS Linux operating system are as follows: 


* After December 31, 2021, CentOS Linux 8 users will no longer receive any software maintenance or support, with bug fixes and feature updates included.

* After June 30, 2024, CentOS Linux 7 users will no longer receive any software maintenance or support, with bug fixes and feature updates included.


Public images and services provided by the platform will also be affected to some extent as follows:


* Currently, BytePlus will not discontinue CentOS 8 images. Existing ECS instances created by using CentOS 8 images will not be affected. However, the images will not be updated.

* Support services for CentOS will align with CentOS official end\-of\-support dates. Service support for CentOS Linux 8 will discontinue after December 31, 2021; for CentOS Linux 7, the support will extend to June 30, 2024.


For more information about the CentOS change plan, check the [official FAQ](https://centos.org/distro-faq/).

<span id=".5bqU5a-5562W55Wl"></span>
## Responsive measures

For the normal operation of services that use the CentOS system, you can replace the operating system or switch the mirror site for CentOS 8.

<span id=".5pu_5o2i5pON5L2c57O757uf"></span>
### Replace the operating system

The platform provides public images for multiple operating systems. Based on your business needs, you can select appropriate public images or import a custom image to replace CentOS Linux.


|Operating system |Overview |
|---|---|
|veLinux |A self\-developed Linux operating system launched by ByteDance. It extensively integrates the system\-level technical experience that ByteDance has accumulated over years when supporting massive services and 100M\-level concurrency. For more information, refer to [veLinux overview](https://docs.byteplus.com/en/docs/ecs/veLinux-image-overview). |
|Red Hat Enterprise Linux |The enterprise edition operating system provided by Red Hat, which requires payment for use. In return, you can enjoy subscription services from Red Hat. For more information, check [Red Hat Enterprise Linux](https://www.redhat.com/zh/technologies/linux-platforms/enterprise-linux?spm=a2c4g.11186623.0.0.40a54026KJ8tih). |
|Rocky Linux |A derivative product of CentOS, which is located downstream of Red Hat Enterprise Linux (RHEL). Like CentOS, this operating system offers a stable version for servers. |
|AlmaLinux |Created by the CloudLinux team, this operating system maintains 1:1 binary compatibility with Red Hat Enterprise Linux (RHEL). |
|Debian, Ubuntu, and other operating systems |Other Linux distributions. These distributions differ in their usage practices and application compatibility. |
|CentOS Stream |A rolling version officially provided by CentOS. |


The operating system images mentioned above will continue to be developed and supported by the platform. For the latest updates, refer to the [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes).

<span id=".5YiH5o2iQ2VudE9TIDjplZzlg4_mupA="></span>
### Switch the mirror site for CentOS 8

As CentOS 8 operating system reached end\-of\-life (EOL) on December 31, 2021, the Linux community has no longer maintained it. Currently, if you execute the source configuration, the following issues may occur:

<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f9245383aaab03cbcf64c8a3e183292) </span>

If you still need to use some installation packages in CentOS 8, you can follow the instructions below to switch the CentOS 8 mirror site to the platform site.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that you use the veLinux operating system provided by the platform. For details, refer to the <a href="https://docs.byteplus.com/en/docs/ecs/veLinux-image-overview">veLinux overview</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Execute the following command to replace the CentOS mirror site.

   ```Plain Text
   sed -i 's/\$releasever/8.5.2111/g' /etc/yum.repos.d/CentOS-Base.repo
   ```
   

3. Execute the following commands to regenerate the local cache.

   ```Plain Text
   yum clean all 
   yum makecache
   ```
   

   After the replacement is complete, the configuration of the CentOS\-Base.repo file is as follows:

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_37c40b7d7ed9b0a066eacc2609623cec) </span>


<span id=".6L-B56e75pON5L2c57O757uf"></span>
### Migrate the operating system

The Operating System Migration feature of SMC (Server Migration Center) enables you to seamlessly switch the operating system of an instance from CentOS 7.x or CentOS Stream 8 to veLinux (CentOS\-compatible version). Therefore, you do not need to replace the operating system (that means no impacts on the system volume data). [Learn more](https://docs.byteplus.com/en/docs/smc/Operating-System-Migration-Task).

<span id=".55u45YWz5paH5qGj"></span>
## Related document


* [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS)

* [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1)
