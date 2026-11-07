---
title: "Usage notes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Usage-notes"
---

<span id="eTSavLoI"></span>
## Usage notes for Elastic Compute Service (ECS) instances


* After you create an ECS instance, you have the highest administrator permission for the instance. The cloud platform does not have the permission to log in to or modify your instance.

* Do not use ECS instances to engage in activities such as fake order brushing, gambling, or fraudulent online transactions.

* Do not use ECS instances to provide traffic penetration services.

* Do not use ECS instances to initiate attacks, scan, or penetrate external systems.

* Do not modify the MAC address of the network interface.

* Do not uninstall the drivers of the related hardware.

* We recommend that you do not enable SELinux.

* You can not use sound card applications.

* The usage of external hardware settings is not supported, such as settings of USB drives, bank Ukeys, external hard drives, and hardware encryption keys.

* Please exercise caution when you perform kernel compilation, kernel upgrades, or operating system upgrades within the ECS instance to ensure its proper functioning. If you need to perform such operations, refer to [Upgrading the Linux kernel version](https://docs.byteplus.com/en/docs/ecs/Replace_the_Linux_operating_system_kernel_version).

* Except for Elastic Bare Metal servers, secondary virtualization is not supported. You can not install virtualization software.

* Some software or applications use licenses that need to be associated with the hardware information of the ECS instance. Therefore, when an instance is migrated, it may cause hardware information to be changed, resulting in the license being invalidated.

* Without filing, you are not allowed to provide non\-operating internet information services within the People's Republic of China. This conduct is considered illegal, and your website will be disabled.  the [BytePlus filing management system](https://docs.byteplus.com/en/docs/6428)


<span id="iB3Q5zix"></span>
## Usage notes for Linux\-based instances


* Do not perform the `poweroff` action to disable the instance and cut the power on a bare metal instance. After doing so, it will be unable to power on independently and the instance is unavailable.

* Do not run the `shutdown -H` command to shut down the system on the ECS instance. This will result in an improper shutdown and the instance is unavailable.

* Do not modify the default content of the `/etc/issue` file on the instance. Otherwise, the platform version of the operating system in the custom image created based on the instance will not be recognized. Therefore, the instance you create using that image fails to start.

* Do not change the permissions of directories under the partition where the root directory is located, such as `/etc`, `/sbin`, `/bin`, `/boot`, `/dev`, `/usr`, `/lib`. If the permissions are improperly changed, the system will encounter exceptions.

* Do not rename, delete, or disable the root account to ensure normal use of the instance.

* Exercise caution when you use the administrator account to perform actions such as fio, mkfs, fsck, and scaling up. If such actions are necessary, back up data in advance to avoid data loss due to misoperations.

* For more information about the type, boot mode, license, and other precautions of images, refer to [Selecting images](https://docs.byteplus.com/en/docs/ecs/Select_image).


<span id="IjIkBl9Q"></span>
## Usage notes for Windows\-based instances


* Do not change the hostname of the domain controller.

* Do not rename, delete, or disable the administrator account to ensure normal use of the instance.

* We recommend that you do not create a custom image from the virtual machine of the domain controller.

* Exercise caution when you use the administrator account to perform actions such scaling up, cross\-region volumes, registry, and system updates. If such actions are necessary, back up data in advance to avoid data loss due to misoperations.

* For more information about the type, boot mode, license, and other precautions of images, refer to [Selecting images](https://docs.byteplus.com/en/docs/ecs/Select_image).
