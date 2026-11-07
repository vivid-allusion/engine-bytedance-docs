---
title: "Overview of operating system (OS) images"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images"
---

When you create a Vital Kubernetes Engine (VKE) cluster or node pool, you need to select an OS image for nodes. This topic describes the image types supported by VKE, especially public images and their compatible instance families.

<span id=".5YWN6LSj5aOw5piO"></span>
## Disclaimers

VKE has different service level objectives (SLO) for different image types. For custom images and shared images, only limited support and guarantees are available.


* For custom images built from compatible public images with OS\-independent configurations (such as pre\-installed model files or pre\-pulled container images), data plane component availability is guaranteed.

* For custom images built from compatible public images with modified OS configurations (such as sysctl settings, boot parameters, or driver versions), VKE component availability cannot be guaranteed. However, troubleshooting assistance is still provided for such cases.

* For custom images built from incompatible public images (for example, those using unsupported machine models or custom kernels), VKE component availability cannot be guaranteed. Unfortunately, we cannot offer troubleshooting for these unsupported scenarios.


<span id=".5a655Zmo5pyN5Yqh5pSv5oyB55qE6ZWc5YOP57G75Z6L"></span>
## Image types

VKE supports three image types: public, custom, and shared. For details about images, see [Image overview](https://docs.byteplus.com/en/docs/ecs/Image-overview).


* **Public images**: official, copyrighted images provided by . These images combine basic OS with initialization components, delivering security, high availability, and open access for all users.

* **Custom images**: user\-uploaded images that contain customized OS and pre\-deployed applications (public or private). These images offer a high level of configuration customization. They are ideal for replicating complex initialization systems or deploying systems with identical configurations at scale. VKE allows you to specify custom images as node operating systems.

* **Shared images**: images shared by other  users. You can use a shared image to quickly deploy a software environment the same as that created by other users. Conversely, you can share your custom image with other  users.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">You need to create custom images and shared images by using VKE base images. Check whether a GPU version is required based on your business requirements.</div>


* <div data-tips="true" data-tips-type="warning">Custom images are available at the node pool project level.</div>


* <div data-tips="true" data-tips-type="warning">As of April 14, 2025, VKE has discontinued maintenance for public GPU Driver 470 series images. New nodes can no longer be provisioned by using this image series.</div>



<span id=".5a655Zmo5pyN5Yqh5pSv5oyB55qE5YWs5YWx6ZWc5YOP"></span>
## Public images

An image is a pre\-configured file that contains an OS and applications for node deployment. When you create a VKE cluster or node pool, you need to select a supported OS image for nodes. This section lists public OS images supported by VKE and the instance families associated with each image.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>



* <div data-tips="true" data-tips-type="warning">VKE maintains its own list of supported OS images, which may differ from the latest images available on Elastic Compute Service (ECS). Ensure that you use OS images supported by VKE when you provision nodes.</div>


* <div data-tips="true" data-tips-type="warning">The system provides the latest version of each public image by default, but existing nodes that were created using older versions of public images will still function normally.</div>


* <div data-tips="true" data-tips-type="warning">All public images use system architecture (<strong>x86_64</strong>) and boot mode<strong>UEFI</strong>.</div>


* <div data-tips="true" data-tips-type="warning">The <strong>image IDs</strong> provided in this topic are valid only in specified regions. For other regions, locate the corresponding image IDs by searching for image names in the VKE console.</div>



<span id="velinux"></span>
### veLinux

The veLinux image series is a Linux distribution developed and optimized by  specifically for its public cloud environment. It delivers a stable, high\-performance, and secure operating system with full lifecycle management capabilities. For details, see [veLinux overview](https://docs.byteplus.com/en/docs/ecs/veLinux-image-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The veLinux 2.0 series images are currently in the public beta stage.</div>


* <div data-tips="true" data-tips-type="tip">You can choose whether to disable GSP firmware if you use public images with driver 535. For details, see <a href="https://docs.byteplus.com/en/docs/vke/How_to_turn_off_the_GSP_configuration_in_the_public_image">How do I disable GSP firmware for public images?</a></div>




|**Image name** |**Image ID** (Johor) |System size |Kernel version |**Instance family of associated nodes** |
|---|---|---|---|---|
|veLinux 1.0 64 bit |image\-yce62qvi49bhcbf53gw5 |8 GB |5.4 |All specification families in General\-purpose,Compute\-optimized, Big Data, Memory\-optimized, High Frequency, Local\-SSD, EBM, and Shared |
|veLinux 1.0 CentOS Compatible 64 bit |image\-yce62xs5babhccamtyhq |8 GB |5.4 ||
|veLinux 1.0 with 5.10 kernel 64 bit |image\-yce62tu9kibhcbfzcypb |8 GB |5.10 |The third generation specification family in General\-purpose,Compute\-optimized, Big Data, Memory\-optimized, High Frequency, Local\-SSD, and Shared |
|veLinux 1.0 CentOS Compatible with 5.10 kernel 64 bit |image\-yce62warl3bhcd9soei8 |8 GB |5.10 ||
|veLinux 1.0 with GPU Driver 535.161.08 and doca 64 bit |image\-yddqiaxmwwbhcbr5utb6 |12 GB |5.4 |ebmhpcpni3l |
|veLinux 1.0 with GPU Driver 535.154.05 and mlx 5.8\-3 64 bit |image\-yddimqp0a6bhcbozzq4i |8 GB |5.4 |gni3cl |
|veLinux 1.0 with GPU Driver 535.129.03 and mlx 23.10 64 bit |image\-ycwh8im22ae94875tqja |8 GB |5.4 |hpcpni3h |
|veLinux 2.0 64 bit<br><br> |image\-yd7m36o070bhccsa6p6o<br><br> |8 GB |5.15 |All CPU\-related instance families, such as those in categories General\-purpose, Compute\-optimized, and Memory\-optimized<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only clusters running Kubernetes version 1.30 or later support veLinux 2.0 series images.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">veLinux 2.0 series images use cgroupv2 by default.</div><br> |
|veLinux 2.0 CentOS Compatible 64 bit<br><br> |image\-yd7m5cxrf0bhcddu2vsm |8 GB |5.15 ||


<span id="ubuntu"></span>
### Ubuntu

The Ubuntu image series is a tested, open\-source public image optimized by  based on the Ubuntu community version. For details, see [Overview of public images](https://docs.byteplus.com/en/docs/ecs/Public-image-overview).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The Ubuntu 20.x image is currently in the public beta stage.</div>


* <div data-tips="true" data-tips-type="tip">The Ubuntu 22.x image is currently in the public beta stage.</div>


* <div data-tips="true" data-tips-type="tip">You can choose whether to disable GSP firmware if you use public images with driver 535. For details, see <a href="https://docs.byteplus.com/en/docs/vke/How_to_turn_off_the_GSP_configuration_in_the_public_image">How do I disable GSP firmware for public images?</a></div>




|**Image name** |**Image ID** (Johor) |System size |Kernel version |**Instance family of associated nodes** |
|---|---|---|---|---|
|Ubuntu 20.04 64 bit |image\-yce62a21q2bhcd6i0awl |8 GB |5.4 |* ecs.g3i<br><br>* ecs.r3i<br><br>* ecs.c3i<br><br>* ecs.i3s<br><br>* ecs.ebmg3id<br><br>* ecs.ebmc3id<br><br>* ecs.ebmr3id |
|Ubuntu 20.04 with GPU Driver 535.161.08 and doca 64 bit |image\-yddqirim9ybhcc4dm5q1 |12 GB |5.4 |ebmhpcpni3l |
|Ubuntu 20.04 with GPU Driver 535.154.05 and mlx 5.8\-3 64 bit |image\-yddin2mu2bbhcbhmeuvo |8 GB |5.4 |gni3cl |
|Ubuntu 22.04 64 bit |image\-ycdr3l1zguhj8321g8aq |8 GB |5.15 |All CPU\-related instance families, such as those in categories General\-purpose, Compute\-optimized, and Memory\-optimized<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Only clusters running Kubernetes version 1.30 or later support Ubuntu 22.x images.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Ubuntu 22.x images use cgroupv2 by default.</div><br> |


<span id="yvu3XMsY"></span>
## Custom images

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Custom images are non\-standard environments for which BytePlus does not provide official support or ongoing maintenance.</div>


VKE allows you to install operating systems on nodes by using custom images. Two methods of packaging custom images are available. You can select an appropriate method based on your business requirements.


* Use the `docker run` method to package and preheat custom images. For detailed operations, see [Packaging custom images by using Docker](https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-Docker).

* Quickly create custom images by using ECS. For detailed operations, see [Creating custom images by using ECS](https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-ECS).
