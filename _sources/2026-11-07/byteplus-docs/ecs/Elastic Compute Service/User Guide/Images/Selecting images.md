---
title: "Selecting images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Select_image"
---

An image consists of the operating system, pre\-installed software, driver, and other components.​​ You can select an image based on your needs when creating an ECS instance. The following factors are for your reference.

<span id=".6LS555So"></span>
## Fee

Fees may be incurred when you use images. [Learn more](https://docs.byteplus.com/en/docs/ecs/Imagebilling).

<span id=".5Zyw5Z-f"></span>
## Region

Images are regional resources. When creating an instance, you can select an image in the region where your business is located.    

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d94bb7fa06bb24a9fb3a93ede54f630f.png) </span>

<span id=".6ZWc5YOP57G75Z6L"></span>
## Image type

ECS images include public images, custom images, shared images based on different sources. [Learn more](https://docs.byteplus.com/en/docs/ecs/Image-overview#.6ZWc5YOP57G75Z6L).

<span id=".5pON5L2c57O757uf"></span>
## Operating systems

<span id=".57O757uf57G75Z6L"></span>
### System type


|Operating system type |Login method |Feature |Applicable scenario |
|---|---|---|---|
|Windows |* The platform console<br><br>* The official Microsoft Remote Desktop |* The Windows user interface is user\-friendly and easy to use.<br><br>* By default, the `NTFS` file system is used. This supports advanced features such as file permissions and encryption.<br><br>* Windows offers various software ecosystems. Many commercial applications, games, and enterprise software are developed for Windows. |* This operating system is suitable for beginners or ordinary users to run programs developed for Windows.<br><br>* SQL Server and other databases (manual installation required) are supported. |
|Linux/Unix\-like |* The platform console<br><br>* SSH |* Linux is an open\-source operating system that allows anyone to view, modify, and distribute its source code, which makes Linux more transparent and customizable.<br><br>* Linux supports multiple file systems, such as XFS, EXT3, and EXT4. Each file system has its own advantages and features.<br><br>* Besides, it offers many different distributions (such as Ubuntu, Debian, and CentOS). Each distribution has its own usages and features.<br><br>* Users have more control over the system and can customize various aspects of the system. |* This operating system is applicable for developers and application scenarios that require high stability and performance, such as high\-performance web servers and embedded systems.<br><br>* MySQL and other databases (manual installation required) are supported. |


<span id=".5ZCv5Yqo5qih5byP"></span>
### Boot mode


|Boot mode |Feature |Applicable scenario |
|---|---|---|
|UEFI |* The GPT (GUID Partition Table) partition table is used, which supports larger disks and more partitions (up to 128 primary partitions).<br><br>* Secure Boot is supported. This prevents unauthorized operating systems or malware from running during startup.<br><br>* Typically faster boot times and better system performance.<br><br>* Modern operating systems and hardware are supported. This can provide advanced features such as network boot and graphical user interface. |This boot mode is applicable to scenarios where newly released operating systems require large\-capacity disks, secure boot, and a shorter boot duration. |
|Legacy |* The MBR partition table is used for booting.<br><br>* Good compatibility. This supports many old hardware and operating systems and also meets basic computing needs. |This boot mode is applicable to scenarios that require high compatibility, such as with old operating systems and hardware. |


<span id=".6K645Y-v6K-B5LiO6aKE572u6L2v5Lu2"></span>
## License and pre\-installed software


|Image type |Feature |
|---|---|
|Public images |* Kernel parameters, pre\-installed drivers, and system tools are optimized based on aspects such as instance operation requirements, performance enhancement, and security. [Learn more](https://docs.byteplus.com/en/docs/ecs/Public-image-overview).<br><br>* The  Official License is used. |
|Custom image |* Management by yourself. You can pre\-install public or private applications based on your needs.<br><br>* Either the  Official License or your Bring Your Own License (BYOL) can be used. |


<span id=".55u45YWz5paH5qGj"></span>
## Related document

After creating an instance, if you need to change the instance operating system to a public image, custom image, or shared image, you can refer to [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS).
