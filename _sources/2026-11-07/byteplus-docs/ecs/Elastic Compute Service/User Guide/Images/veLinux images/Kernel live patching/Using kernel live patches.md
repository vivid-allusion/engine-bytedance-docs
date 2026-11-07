---
title: "Using kernel live patches"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Use_kernel_hot_patching"
---

This topic describes how to obtain, enable, and manage kernel live patches.

<span id="6uAvrmDq"></span>
## Procedure

<span id="8pm9gJB8"></span>
### Obtain and install kernel live patches

Kernel live patches provided by BytePlus are released as livepatch packages and included in the BytePlus software repository.


1. [Log in to the target instance running the veLinux operating system](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the kernel version of the current operating system.

   ```Plain Text
   uname -r
   ```
   

   When the following output is displayed, the kernel version numbers are `5.4.250-6.ve1` and `5.4.250-9-velinux1`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_887a7eb688459ee6583720715fb5b1ec.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bc1f86bbbd47cf785c674dfbbff9a50f.png) </span>

3. Execute the following command to query the kernel live patch applicable to the current operating system.

   * **veLinux**

      ```Plain Text
      sudo apt update
      sudo apt-cache search livepatch | grep "<kernel version number>"
      ```
      

   * **veLinux CentOS Compatible**

      ```Plain Text
      sudo yum makecache
      sudo yum list | grep "livepatch" | grep "<kernel version number>"
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b288dd9794e0441fb326c2ba5f16a52f.png) </span>

      Naming format for DEB/RPM packages of kernel live patches: `livepatch-${kernel_version}-${package_name}`. Where:

      * `${kernel_version}` specifies the kernel version number matched by the live patch. You can use the live patch only when the kernel version of your operating system is the same as this version number. You can execute the `uname -r` command in the instance to view the kernel version information.

      * `${package_name}` specifies the name of the live patch package.

4. Execute the following command to install the live patch.

   * **veLinux**

      ```Plain Text
      sudo apt -y install <livepatch>
      ```
      

   * **veLinux CentOS Compatible**

      ```Plain Text
      sudo yum -y install <livepatch>
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><livepatch></code> with the name of the DEB/RPM package of the target live patch.      </div>
      

5. Execute the following command to check whether the live patch is installed.

   ```Plain Text
   sudo lsmod | grep livepatch
   ```
   

   If the following output is displayed, the live patch is installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc4da5ef731d345563a91dd0ef97d10b.png) </span>


<span id="bBKkiL1H"></span>
## Related action

<span id="z1O8uIx8"></span>
### Delete kernel live patches

If a live patch does not take effect or the instance performance is affected after you enable the live patch, you can delete the live patch to resolve the issues.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to view the enabled live patch package.

   * **veLinux**

      ```Plain Text
      dpkg-query -W | grep "livepatch"
      ```
      

   * **veLinux CentOS Compatible**

      ```Plain Text
      sudo yum list installed | grep "livepatch"
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_48bdfb1f67e7795f4c18e8412bcaa280.png) </span>

3. Execute the following command to delete the anomalous live patch package.

   * **veLinux**

      ```Plain Text
      sudo apt -y remove livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64
      ```
      

   * **veLinux CentOS Compatible**

      ```Plain Text
      sudo yum -y remove livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code>livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64</code> with the actual patch package name.      </div>
      

      When the following output is displayed, the `livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64` live patch package has been deleted.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_22e7185d037097bd90b1bf19afbb6389.png) </span>

4. Execute the following command to check whether the target live patch package has been deleted.

   ```Shell
   sudo lsmod | grep livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code>livepatch-5.4.250-6.ve1-ext4-ABBA-lock-fix.x86_64</code> with the actual patch package name.   </div>
   

   If the output is empty, the live patch package has been deleted.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5156aedbeb31775a7793debb98184a1.png) </span>


<span id="YxENTCIS"></span>
### Disable the livepatch system service

If your kernel live patch is installed and effective, but you want the operating system not to automatically load all kernel modules of the live patch when the ECS instance restarts, you can perform the following steps to disable the livepatch system service.


1. [Log in to the target instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check whether the livepatch system service has started.

   ```Shell
   sudo systemctl is-enabled livepatch.service
   ```
   

   Sample output:

   If `enabled` is displayed in the output, the livepatch system service has started, and you can proceed to the next steps to disable the service.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_44839b1126ca9d1d3cef986efefd1ca1.png) </span>

2. Execute the following command to disable the livepatch system service.

   ```Shell
   sudo systemctl disable livepatch.service
   ```
   

   If the following output is displayed, the livepatch system service has been disabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6de9b35268f0b9dfdcbe87d4b81e617d.png) </span>

3. Execute the following command to view the status of the livepatch system service.

   ```Shell
   sudo systemctl status livepatch.service
   ```
   

   If the following output is displayed, the livepatch system service has been disabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_26bfa9c74326847275b1d845cbc28ef5.png) </span>

4. Subsequently, you can execute the following command to re\-enable the livepatch system service.

   ```Plain Text
   sudo systemctl enable livepatch.service
   ```
   

   When the following output is displayed, the livepatch system service has been re\-enabled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b8a6a9daaf88e027203e0a8d950996.png) </span>
