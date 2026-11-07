---
title: "Changing boot mode from BIOS to UEFI for custom Linux images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Changing-the-boot-mode-of-Linux"
---

This topic describes how to change the boot mode of the operating system from `BIOS` to `UEFI` in a cloud environment.

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario

Some ECS instance types provided by the BytePlus platform only support the UEFI boot mode. You cannot select such instance types if the custom image you want to use is in `BIOS` mode. You can follow the instructions provided in this topic to change the boot mode of the target custom image to `UEFI`.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have imported a Linux image that uses `BIOS` boot mode into the BytePlus platform. For more information, see [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).

* This operation may compromise data security. We recommend that you back up your data in advance to ensure data security by performing operations such as [copying images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Image console](https://console.byteplus.com/image/images). 

2. In the top navigation bar, select the region and project where the target custom image is located.

3. Click the "Create Instances" button in the "Actions" column to the right of the target image to create a temporary instance by using the image.

   > You can use the image to create an instance with the lowest\-specification instance type, such as ecs.g2i.large.   
   

4. [Log in to the temporary instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

5. Execute the following command in the temporary instance to check whether the system volume of the instance has free space for creating an `efi` partition.

   ```Plain Text
   parted /dev/vda print free
   ```
   

   * If the following output is displayed, the system volume has no free space or less than 1 GB of free space. In this case, you need to scale up the system volume by approximately 1 GB. For more information, see [Scaling up volumes (Linux)](https://docs.byteplus.com/en/docs/ecs/Extend-volume-linux).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a9d05053a6e404ef6fa4a3456caf6e63.png) </span>

   * If the following output is displayed, the system volume has at least 1 GB of free space. In this case, skip this step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f8c4c44bec872e69b4d19102a4625c3a.png) </span>

6. Use the GPT fdisk tool to partition the free space.

   1. Execute the `gdisk /dev/vda` command to add two partitions: `BIOS boot partition` and `EFI System`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5f6e592869b8344cf48426e10895ccb.png) </span>

   2. Enter `n`  and follow the prompts to add the `BIOS boot partition`, and then press Enter.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The value of <code>first sector</code> must be <code>34</code>.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_93b895c33b8e5ae0ef76cb1236b1c98d.png) </span>

   3. Enter `n` , and add an `EFI System` partition and press Enter.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A partition size of 200 MB is required.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4b121d0444ce33f5ca5147ecd3394838.png) </span>

   4. Enter `w` , and enter `y` to confirm and complete the partitioning.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fd16a5dc510a3476ed71bfc8ceea871e.png) </span>

   5. Execute the following command to read the partition table and update partition information.

      ```Plain Text
      partprobe /dev/vda
      ```
      

7. Execute the following command to view information about the `BIOS boot partition` and `EFI System` partitions.

   ```Plain Text
   parted -l
   lsblk -l
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7b77fbbaeafb1f91b368f634ddd43464.png) </span>

8. Mount the UEFI partition.

   1. Execute the following command to format the ESP.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the command cannot be found during execution, execute the <code>yum install dosfstools</code> command to install the tool.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Replace the digit <code>3</code> in <code>vda3</code> with the <code>Partition number</code> of the <code>EFI</code> partition in Step 6.2.      </div>
      

      ```Plain Text
      mkfs.vfat /dev/vda3
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_087e2ebf9179b72235aaae827f509c04.png) </span>

   2. Execute the following command to mount the UEFI partition to the /boot/efi directory.

      > If the /boot/efi directory does not exist, execute the `mkdir /boot/efi` command to create it.      
      

      ```Plain Text
      mount /dev/vda3 /boot/efi
      ```
      

   3. Execute the following command to check whether the mount is successful.

      ```Plain Text
      lsblk
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7415d56d8bb819056f79caa24d1eba5f.png) </span>

9. Write the mount information of the UEFI partition to the `fstab` file.

   1. Execute the following command to view the UUID of the UEFI partition.

      > In this practice, the UUID of the `/dev/vda3` partition is `F6BA-62E7`.      
      

      ```Plain Text
      blkid
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f84814fe77fa032d9fae54458903b61b.png) </span>

   2. Execute the following command to edit the fstab file.

      ```Plain Text
      vim /etc/fstab
      ```
      

   3. Press the `i` key to enter insert mode, and add the UUID of the UEFI partition to the file.

      ```Plain Text
      UUID=F6BA-62E7  /boot/efi        vfat  umask=0077   0   1
      ```
      

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

10. Reinstall BootLoader

   1. Execute the following command to update the software package list.

      * CentOS image

         ```Plain Text
         yum makecache
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         apt-get update
         ```
         

   2. Execute the following command to install efibootmgr.

      * CentOS image

         ```Plain Text
         yum install efibootmgr
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         apt install efibootmgr
         ```
         

   3. Execute the following command to install shim.

      * CentOS image

         ```Plain Text
         yum install shim
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         apt install shim
         ```
         

   4. Execute the following command to install grub2\-efi.

      * CentOS image

         ```Plain Text
         yum install grub2-efi-x64 && yum install grub2-efi-x64-modules
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         apt install --reinstall grub-common grub-efi-amd64
         ```
         

   5. Execute the following command to reinstall grub with UEFI specified as the bootloader.

      * CentOS image

         ```Plain Text
         grub2-install --target=x86_64-efi --removable --efi-directory=/boot/efi --bootloader-id=GRUB
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         grub-install --target=x86_64-efi --removable --efi-directory=/boot/efi --bootloader-id=GRUB
         ```
         

   6. Execute the following command to regenerate the grub2\-config file.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">The grub2\-config file that is regenerated overwrites the original configurations. We recommend that you back up data in advance.      </div>
      

      * CentOS image

         ```Plain Text
         grub2-mkconfig -o /boot/grub2/grub.cfg
         ```
         

      * Debian/Ubuntu image

         ```Plain Text
         grub-mkconfig -o /boot/grub/grub.cfg
         ```
         

   7. Execute the following command to modify the configuration of the grub2\-mkconfig file.

      > If you are using a Debian or Ubuntu image, skip this step.      
      

      ```Plain Text
      sed -i 's/linux16/linuxefi/g' /boot/grub2/grub.cfg
      sed -i 's/initrd16/initrdefi/g' /boot/grub2/grub.cfg
      ```
      

11. To ensure you can properly use the instance types provided by the BytePlus platform, follow the instructions provided in the [Install the Virtio1.1 driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo) section to install the Virtio1.1 driver.

12. Create a custom image from the operating system of the temporary instance. For more information, see [Creating custom image based on instance (Linux)](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5q2l6aqk5Zub77ya6YCa6L-H5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP).

13. At this point, you obtain a custom image in `UEFI` boot mode. Subsequently, you can release cloud resources such as the temporary instance, volumes, and EIPs based on your needs. You can also use the new custom image to purchase instances or change the operating systems for existing instances. For more information, see [Purchasing instances based on custom images](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) and [Changing operating systems](https://docs.byteplus.com/en/docs/ecs/Changing-OS).

   You can also execute the following commands in an instance created by using this image to verify whether the modification is successful.

   ```Plain Text
   df -h
   efibootmgr
   ```
   

   Sample output:

   > If the following output is displayed, the new image uses `UEFI` boot mode.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15ed92e075272996a43ca2dc36018b45.png) </span>


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQ

**Why does the "Boot mode" value of a newly created image still show as ** **`BIOS`** ** when I check its information in the Image console?** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_daf17fae1a6545c40759bc87120dee02.png) </span>


* Cause:

   The boot mode of the image in the console inherits the boot mode (`BIOS`) of the temporary instance used to create the image. Therefore, the displayed boot mode of the new image in the console is `BIOS`. You need to change the boot mode displayed in the console to `UEFI` to ensure proper image usage.

* Solution:

   You can [use the console](https://docs.byteplus.com/en/docs/ecs/Modifying-custom-image-information) or call the [ModifyImageAttribute](https://docs.byteplus.com/en/docs/ecs/ModifyImageAttribute) operation to change the boot mode of the target custom image to `UEFI`.


<span id="gVxqgav2"></span>
#### Why does the screen display garbled characters when I log in via VNC to an instance created from the new image?

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a46d77daeb5e10a3c8d6a5fd033ac84f.png) </span>


* Cause:

   This issue may occur because the image lacks the Cirrus graphics card driver for the corresponding kernel version, leading to display anomalies when you log in via VNC.

* Solution:

   1. Log in to the target instance by using SSH.

   2. Execute the following command to check whether the Cirrus graphics card driver is installed in the operating system.

      ```Plain Text
      modinfo cirrus
      ```
      

      * If the driver is already installed, submit a ticket to obtain technical support.

      * If not installed, execute the following command to install the Cirrus graphics driver for the corresponding kernel version.

         * CentOS image

            ```Plain Text
            yum makecache
            install linux-modules-extra-$(uname -r) -y
            ```
            

         * Debian/Ubuntu image

            ```Plain Text
            apt-get update
            apt-get install linux-modules-extra-$(uname -r) -y
            ```
