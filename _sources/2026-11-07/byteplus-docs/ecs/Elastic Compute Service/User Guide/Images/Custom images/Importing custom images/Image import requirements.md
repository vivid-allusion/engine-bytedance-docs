---
title: "Image import requirements"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Requirements"
---

To ensure the availability of a custom image and improve image import efficiency, read the requirements and limits in this topic before you import the custom image.

<span id=".TGludXjmk43kvZzns7vnu5_plZzlg48="></span>
## Linux operating system images


|**Operating systems** ||
|---|---|
|x86 architecture |* veLinux (BytePlus proprietary Linux operating system)<br><br>* Red Hat Enterprise Linux 5.x to 9.x<br><br>* CentOS<br><br>* Debian<br><br>* SUSE Linux Enterprise Server 12.x and 15.x<br><br>* OpenSUSE<br><br>* Ubuntu<br><br>* Fedora<br><br>* Rocky Linux<br><br>* AlmaLinux |
|ARM64 architecture |* CentOS 8.5 and later versions<br><br>* Debian 11 and later versions<br><br>* Fedora 35 and later versions<br><br>* Rocky Linux 8.4 and later versions<br><br>* Ubuntu LTS HWE version 20.04.03 and later versions |
|**File system and partition** ||
|File system |* Ensure the integrity of the image file system.<br><br>* XFS, EXT3, and EXT4 file systems are supported. |
|Partition type |MBR partitions are supported. |
|**System environment requirements** ||
|Volume |The size of the system volume of the ECS instance that you create by using the custom image is determined based on the total capacity (not the used capacity) of the system volume in the image. The total capacity of the system volume in the image ranges from 40 GiB to 500 GiB.<br><br>When the actual data in the system volume exceeds 128 GiB, you cannot create instances with PTSSD volumes. |
|Boot mode |We recommend that you use the `UEFI` boot mode.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/ecs/EBM-overview">Elastic Bare Metal (EBM)\-type</a> ECS instances support images only in the <code>UEFI</code> boot mode.</div><br> |
|Network |Make sure that the DHCP service is enabled. [Learn more](https://docs.byteplus.com/en/docs/ecs/Start-SHCP-Service-in-Linux-image). |
|Driver |Make sure that the Virtio driver is installed. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#5VeObo5n). |
|Software |Make sure that Cloud\-init is installed and modify the Cloud\-init configuration file to ensure that the instances created by using the image can be initialized as expected. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.56ys5Zub5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWQtaW5pdA==). |
|**Image file format** ||
|Only images in the QCOW2, RAW, VHD, or VMDK format are supported. Images in other formats (for example, ISO) must be converted to a supported image format before you import the images. [Learn more](https://docs.byteplus.com/en/docs/ecs/Converting-image-file-formats). ||


<span id=".V2luZG93cyBTZXJ2ZXLmk43kvZzns7vnu5_plZzlg48="></span>
## Windows Server operating system images


|**Operating systems** ||
|---|---|
|x86 or ARM architecture |* Windows Server 2022 Standard Edition<br><br>* Windows Server 2022 Datacenter Edition<br><br>* Windows Server 2019 Datacenter Edition<br><br>* Windows Server 2016 Datacenter Edition<br><br>* Windows Server 2012 R2 Datacenter Edition |
|**System environment requirements** ||
|Volume |The size of the system volume of the ECS instance that you create by using the custom image is determined based on the total capacity (not the used capacity) of the system volume in the image. The total capacity of the system volume in the image ranges from 40 GiB to 500 GiB.<br><br>When the actual data in the system volume exceeds 128 GiB, you cannot create instances with PTSSD volumes. |
|Driver |Make sure that the virtio\-win driver is installed. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo). |
|Software |If you want to log in to the ECS instance by using the preset password, modify the Cloudbase\-init configuration file in the image file. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images#.56ys5LiJ5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWRiYXNlLWluaXQ=). |
|**Image file format** ||
|Only images in the QCOW2, RAW, VHD, or VMDK format are supported. Images in other formats (for example, ISO) must be converted to a supported image format before you import the images. [Learn more](https://docs.byteplus.com/en/docs/ecs/Converting-image-file-formats). ||
