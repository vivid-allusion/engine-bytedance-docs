---
title: "Upgrading kernel version of Linux operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Replace_the_Linux_operating_system_kernel_version"
---

If the kernel of the server operating system cannot meet your business needs, you can upgrade the kernel version, which can meet business requirements with less impact (compared with changing the operating system).

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenario


* **Improve system performance**

   New kernel versions may provide performance optimizations, for example, faster file system operations, lower latency, or higher throughput.

* **Support new hardware devices**

   When the server is equipped with a new hardware device that is not supported by the current kernel, it may be necessary to upgrade the kernel to support the new hardware.

* **Fix security vulnerabilities**

   New kernel versions may fix some security vulnerabilities found in older kernel versions.

* **Obtain support for more features**

   New kernel versions may introduce new features, such as new file systems, virtualization technologies, and containerization capabilities.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Upgrading the system kernel may lead to compatibility, stability, and security issues. We recommend that you[ back up data](https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration) before you upgrade the kernel.

* Kernel upgrade actions require `root` permission.


<span id="8lb59i0M"></span>
## CentOS OS


<Tabs>
<Tab zoneid="h7eBhI4If5" title="Upgrade the minor version of the kernel">
<TabTitle>Upgrade the minor version of the kernel</TabTitle>

If you only need to upgrade the minor version of the kernel, you can use the official Yum repository.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the example provided in this section, the CentOS 7.9 kernel version is upgraded from <code>3.10.0-1160.102.1.el7</code> to <code>3.10.0-1160.119.1</code>.</div>



1. [Log in to the target Linux server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current kernel version.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0745aa974d3e1cdae9c28c9f3d3f7a8f.png) </span>

3. Execute the following command to upgrade the system package list.

   ```Plain Text
   sudo yum makecache
   ```
   

4. Execute the following command to view the installable kernel versions.

   ```Plain Text
   sudo yum list kernel --showduplicates
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_69ceeaecddc9edd21d8369ab06c37651.png) </span>

5. Execute the following command to install the specified version of the kernel.

   ```Plain Text
   sudo yum install kernel-3.10.0-1160.119.1.el7 -y
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>3.10.0-1160.119.1.el7</code> with the actual kernel version.   </div>
   

6. Update boot configuration.

   * BIOS boot mode:

      ```Plain Text
      grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      

   * UEFI boot mode:

      ```Plain Text
      grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
      ```
      

7. Execute the following command to view the installed kernels.

   * BIOS boot mode:

      ```Plain Text
      awk -F\' '$1=="menuentry " {print i++ " : " $2}' /boot/grub2/grub.cfg
      ```
      

   * UEFI boot mode:

      ```Plain Text
      awk -F\' '$1=="menuentry " {print i++ " : " $2}' /boot/efi/EFI/centos/grub.cfg
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e54d8cf1ac519d7c177d78a903be0149.png) </span>

8. Execute the following command to specify the default kernel.

   ```Plain Text
   sudo grub2-set-default 0
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace <code>0</code> with the serial number of the installed kernel that you obtained in Step 7.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cffeb107b17dafaf29e59dc11229e94b.png" width="693px" />   </div>
   

9. Execute the following command to restart the instance.

   ```Plain Text
   sudo reboot
   ```
   

10. Execute the following command to view the current kernel version and check whether the kernel is upgraded.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc13b3324b6fcdf46dea47000f16aa91.png) </span>

11. Execute the following command to install the kernel software packages related to the new kernel.

   ```Plain Text
   yum install kernel-devel kernel-headers kernel-modules-extra kernel-tools kernel-tools-libs kernel-tools-libs-devel -y
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0e032c24ddf52a3371ad90ba2c8d0091.png) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the required version of kernel\-headers, kernel\-devel, etc., is not available in the Yum repository. You can download and install them yourself:   </div>
   

   1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Download the target software packages. One option is to download them from the <a href="https://mirrors.tuna.tsinghua.edu.cn/elrepo/archive/kernel/el7/x86_64/RPMS/">Tsinghua University Mirror Site</a>.   </div>
   

   2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Upload the software packages to the target instance. <a href="https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview">Learn more</a>.   </div>
   

   3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Execute the <code>rpm -ivh <RPM package to be installed></code> command to install the target software package.   </div>
   


</Tab>
<Tab zoneid="zrUGyeX9so" title="Upgrade the major version of the kernel">
<TabTitle>Upgrade the major version of the kernel</TabTitle>

If you need to upgrade the major version of the kernel, you can use the ELRepo repository or compile the kernel yourself.


<Tabs>
<Tab zoneid="MExpwAIE6P" title="Upgrade through ELRepo source">
<TabTitle>Upgrade through ELRepo source</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the example provided in this section, the CentOS 8.3 kernel version is upgraded from <code>4.18.0-348.7.1</code> to <code>6.10.11</code>.</div>


<span id="agTsQGmz"></span>
#### Step 1: Install the ELRepo repository


1. [Log in to the target Linux server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current kernel version.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ec4447d89eff317428d3f9b51f66eaff.png) </span>

3. Execute the following command to update the software packages.

   ```Plain Text
   sudo yum makecache
   ```
   

4. Execute the following command to import the ELRepo public key.

   ```Plain Text
   rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
   ```
   

5. Execute the following command to install the ELRepo repository.

   ```Plain Text
   yum install https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm -y
   ```
   

6. Execute the following command to replace the ELRepo repository address with the Tsinghua University open\-source software mirror site, and comment out `mirrorlist`.

   ```Plain Text
   sed -i "s@mirrorlist@#mirrorlist@g" /etc/yum.repos.d/elrepo.repo ;sed -i "s@elrepo.org/linux@mirrors.tuna.tsinghua.edu.cn/elrepo@g" /etc/yum.repos.d/elrepo.repo
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the address of the Tsinghua University open\-source software mirror site <code>https://mirrors.tuna.tsinghua.edu.cn/</code> is used as address of the repository. You can use other mirror sites based on your needs. <a href="https://elrepo.org/wiki/doku.php?id=download">Learn more</a>.   </div>
   

7. Execute the following command to update the software package cache.

   ```Plain Text
   sudo yum makecache
   ```
   


<span id="ZEAj9cQ9"></span>
#### Step 2: Install a new kernel


1. Execute the following command on the target instance to load data from the ELRepo repository.

   ```Plain Text
   yum --disablerepo="*" --enablerepo="elrepo-kernel" repolist
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_048fef69e12d9ca6b70ca01b4e321ade.png) </span>

2. View the kernel packages in the ELRepo repository that are supported by the current operating system.

   ```Plain Text
   yum --disablerepo="*" --enablerepo="elrepo-kernel" list available
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7a991ea450b11db75bb76e0fffb1c124.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">kernel\-ml: represents the mainline kernel. It includes the latest features, improvements, and experimental functionalities, with frequent updates. You can use this type of kernel if you pursue the latest technologies and features, have a certain tolerance for system instability, and are willing to handle potential issues.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">kernel\-lt: represents the Long\-Term Support (LTS) kernel. It focuses on stability and compatibility. These kernel versions undergo extensive testing and receive support for an extended period. You can use this type of kernel if you need a stable operating environment, do not want to update the kernel frequently, or have no high demand for new features.   </div>
   

3. Execute the following command to install the latest mainline kernel.

   ```Plain Text
   yum --enablerepo=elrepo-kernel install kernel-ml -y
   ```
   

   If you want to install the specified kernel, you can execute the following command. Replace kernel\-ml\-6.10.11\-1.el8.elrepo with the target kernel version obtained from the previous step.

   ```Plain Text
   yum --enablerepo="elrepo-kernel" install kernel-ml-6.10.11-1.el8.elrepo
   ```
   


<span id="rQoOVa2F"></span>
#### Step 3: Modify Grub configuration


1. Execute the following command to view information about installed kernels.

   ```Plain Text
   grubby --info=ALL | grep ^kernel
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_127cae5e7661e646828319c8c2dd8db6.png) </span>

2. Execute the following command to specify the default kernel used when the instance starts.

   ```Plain Text
   grubby --set-default=/boot/vmlinuz-6.10.11-1.el8.elrepo.x86_64
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_896b64fee364a63b3981fa4cf915f541.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the installed 6.10.11\-1.el8.elrepo.x86_64 kernel is used. Replace /boot/vmlinuz\-6.10.11\-1.el8.elrepo.x86_64 with the actual target kernel information obtained from the previous step.   </div>
   

3. Execute the following command to restart the instance.

   ```Plain Text
   reboot
   ```
   

4. Execute the following command to check whether the instance kernel is updated.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b8a2a6d67eba10618651b4ef359e5b34.png) </span>

5. Install software packages related to the new kernel.

   1. Execute the following command to view the installed kernel software packages.

      ```Plain Text
      rpm -qa | grep kernel
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8a9803823a98ffefc578d16a62ea2bf5.png) </span>

   2. Execute the following command to delete old kernel software packages.

      ```Plain Text
      yum remove kernel-core-4.18.0 kernel-devel-4.18.0 kernel-tools-libs-4.18.0 kernel-headers-4.18.0 -y
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, software packages related to v4.18.0 kernel are deleted. Replace the software packages with the actual ones to delete them.      </div>
      

   3. Execute the following command to install the software packages related to the new kernel currently in use.

      ```Plain Text
      yum --enablerepo="elrepo-kernel" install kernel-ml-devel kernel-ml-headers kernel-ml-modules-extra kernel-ml-tools kernel-ml-tools-libs kernel-ml-tools-libs-devel -y
      ```
      

   4. Execute the following command to check whether the required new kernel and its kernel software packages are installed.

      ```Plain Text
      rpm -qa | grep kernel
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_407ca4b764c32f57a40210c5248a12f7.png) </span>


</Tab>
<Tab zoneid="WplJPDhfgj" title="Upgrade by compiling your own kernel">
<TabTitle>Upgrade by compiling your own kernel</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In the example provided in this section, the CentOS 7.9 kernel version is upgraded from <code>3.10.0-1160.102.1.el7</code> to <code>5.4.278</code>.</div>


<span id="BwEcqpJW"></span>
#### Step 1: Download the kernel source code


1. Go to the [official kernel](https://mirrors.edge.kernel.org/pub/linux/kernel/) site and go to the directory for the kernel version you want to download.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_675b8230e97dbabcedd7f821764f6d5b.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the v5.x kernel source package is downloaded.   </div>
   

2. Obtain the download link for the kernel source package of the target version.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1c12159a815e5a278deaa7923bd7ba15.png) </span>

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the 5.4.278 kernel is installed. After you go to the v5.x directory, obtain the download link for linux\-5.4.278.tar.gz, which is https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/linux\-5.4.278.tar.gz.   </div>
   

3. [Log in to the target Linux server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

4. In the instance for which you want to replace the kernel, execute the following command to download the kernel source package.

   ```Bash
   wget https://mirrors.edge.kernel.org/pub/linux/kernel/v5.x/linux-5.4.278.tar.gz
   ```
   

5. Execute the following command to download the software packages related to system installation.

   ```Bash
   yum install bc gcc make python3 ncurses-devel flex bison openssl-devel elfutils-libelf-devel -y
   ```
   

6. Execute the following command to view the GCC version.

   ```Bash
   gcc --version
   ```
   

   * If the version is not lower than `7`, proceed to the next step.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_786067f0667208835a91094dcae13cd3.png) </span>

   * If the version is lower than `7`, execute the following command to upgrade GCC.

      1. Execute the following command to install the default SCL repository.

         ```Plain Text
         yum install centos-release-scl scl-utils-build -y
         ```
         

      2. Execute the following command to replace the software repository address with a mirror site address in the Chinese mainland.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">In the example provided in this topic, the software repository address is replaced by the BytePlus mirror site address <code>https://mirrors.volces.com/</code>. You can use another mirror site address based on your needs.         </div>
         

         ```Plain Text
         sed -i "s@#baseurl=http://mirror.centos.org@baseurl=https://mirrors.volces.com/@g" /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo
         sed -i "s@mirrorlist=@#mirrorlist=@g" /etc/yum.repos.d/CentOS-SCLo-scl-rh.repo
         sed -i "s@# baseurl=http://mirror.centos.org@baseurl=https://mirrors.volces.com/@g" /etc/yum.repos.d/CentOS-SCLo-scl.repo
         sed -i "s@mirrorlist=@#mirrorlist=@g" /etc/yum.repos.d/CentOS-SCLo-scl.repo
         ```
         

      3. Execute the following command to refresh the yum cache.

         ```Plain Text
         yum repolist && yum clean all && yum makecache
         ```
         

      4. Execute the following command to install a later version of GCC.

         ```Plain Text
         yum install -y devtoolset-10-gcc devtoolset-10-gcc-c++ devtoolset-10-binutils
         ```
         

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">In the example provided in this topic, GCC v10 is installed. Install the GCC version based on your needs.         </div>
         

      5. Execute the following command to make the new GCC version to take effect.

         * Temporarily valid (becomes invalid after instance restart or bash exit)

            ```Plain Text
            scl enable devtoolset-10 bash
            ```
            

         * Permanently valid

            ```Plain Text
            echo "source /opt/rh/devtoolset-10/enable" >>/etc/profile
            source /etc/profile
            ```
            

      6. Execute the following command to check whether the newly installed GCC takes effect.

         ```Plain Text
         gcc --version
         ```
         

         Sample output:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8b8f438e2d59a2a4335c6c10cc361e72.png) </span>


<span id="LqoPG21J"></span>
#### Step 2: Compile the kernel


1. In the directory where the downloaded kernel source package is located, execute the following command to decompress it.

   ```Plain Text
   tar xvf linux-5.4.278.tar.gz
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace linux\-5.4.278.tar.gz with the actual source package.   </div>
   

2. Execute the following command to enter the source code directory obtained after decompression.

   ```Plain Text
   cd linux-5.4.278
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace linux\-5.4.278 with the actual source code package.   </div>
   

3. Execute the following command to copy the configuration file currently used by the kernel.

   ```Plain Text
   cp -p /boot/config-$(uname -r) .config
   ```
   

4. Execute the following command to modify the configuration file of the new kernel.

   ```Plain Text
   sed -i "s@CONFIG_SYSTEM_TRUSTED_KEYS@#CONFIG_SYSTEM_TRUSTED_KEYS@g" /root/linux-5.4.278/.config ;sed -i "s@CONFIG_DEBUG_INFO_BTF@#CONFIG_DEBUG_INFO_BTF@g" /root/linux-5.4.278/.config
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace /root/linux\-5.4.278/.config with the path where the configuration file you copied in Step 8 is located.   </div>
   

5. Modify kernel parameters.

   1. Execute the following command to enter the text interface.

      ```Plain Text
      make menuconfig
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_261975333f2ccf4f35dd05089f16f394.png) </span>

   2. Modify the kernel parameter configuration based on your needs. In the example provided in this topic, only the kernel name is modified.

      1. Use the arrow keys to select `General setup`, and then press Enter to go to the general settings page.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8cfa66c2fe6742591bc29c98b727866e.png) </span>

      2. Use the arrow keys to select `Local version - append to kernel release`, and then press Enter to go to the page for specifying the kernel version.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6ccc4ada4d8c303e1eb81940007f2119.png) </span>

      3. Enter the local information that follows the kernel version. Taking `-1.el7.x86` as an example in this topic, the final kernel information will be displayed as `5.4.278-1.el7.x86`.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_767b0d553c0c6f5e4d9697689afdcee5.png) </span>

      4. Press the `Tab` key to select `< Ok >`, and then press Enter to save the changes.

   3. Press the `Tab` key to select `< Exit >`, and then press the Enter key to return to the homepage.

   4. Press the `Tab` key to select `< Save >`, and then press the Enter key to save the changes.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, the default settings are used. Modify the settings based on your needs.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5467ca32c899a2ca254f7f984a6a288e.png) </span>

   5. Modify the name of the kernel configuration file based on your needs, press the `Tab` key to select `< Ok >`, and then press the Enter key to save the changes.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, the default settings are used. Modify the settings based on your needs.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_422060ef65109b3cc47555e3c6392e3f.png) </span>

   6. Press the Enter key to exit edit mode.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_310a21db9b79b8ca695c812d8bd42d56.png) </span>

   7. Press the `Tab` key to select `< Exit >`, and then press the Enter key to exit edit mode.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_deca151eb4d6dfbee131161310adf0f1.png) </span>

6. Execute the following command to compile the kernel.

   ```Plain Text
   make -j $(nproc)
   ```
   

   Sample output of a compilation success:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f6b7dfa6b0ace8f3afed2d80b126719.png) </span>

7. Execute the following command to copy the compiled kernel module to the system directory.

   ```Plain Text
   make modules_install
   ```
   

8. Execute the following command to install the kernel image and the image of the boot initialization file system.

   ```Plain Text
   make install
   ```
   


<span id="a3jwZw6N"></span>
#### Step 3: Modify Grub configuration


1. Update boot configuration.

   * BIOS boot mode:

      ```Plain Text
      grub2-mkconfig -o /boot/grub2/grub.cfg
      ```
      

   * UEFI boot mode:

      ```Plain Text
      grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
      ```
      

2. Execute the following command to view the installed kernels.

   * BIOS boot mode:

      ```Plain Text
      awk -F\' '$1=="menuentry " {print i++ " : " $2}' /boot/grub2/grub.cfg
      ```
      

   * UEFI boot mode:

      ```Plain Text
      awk -F\' '$1=="menuentry " {print i++ " : " $2}' /boot/efi/EFI/centos/grub.cfg
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7beb350e4761dc2fde850ab650405bfe.png) </span>

3. Execute the following command to specify the default kernel.

   ```Plain Text
   sudo grub2-set-default 0
   ```
   

   Replace `0` with the serial number of the installed kernel that you obtained in Step 2.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_601bae7353ddd199fab529207445e4f4.png) </span>

4. Execute the following command to restart the instance.

   ```Plain Text
   sudo reboot
   ```
   

5. Execute the following command to view the current kernel version and check whether the kernel is upgraded.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cd580a016a2ec913e8817aeed3d3a451.png) </span>

6. Install software packages related to the new kernel.

   1. Execute the following command to view the installed kernel software packages.

      ```Plain Text
      rpm -qa | grep kernel
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b50de8f9a071a62b9f50e8a88288c73a.png) </span>

   2. Execute the following command to delete old kernel software packages.

      ```Plain Text
      yum remove kernel-tools-3.10.0 kernel-3.10.0 kernel-tools-libs-3.10.0 kernel-headers-3.10.0 kernel-devel-3.10.0 -y
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, v3.10.0 kernel and software packages related to it are deleted. Replace the kernel version and software packages with the actual ones to delete them.      </div>
      

   3. Execute the following command to install the kernel software packages related to the new kernel.

      ```Plain Text
      yum  install kernel-devel kernel-headers kernel-modules-extra kernel-tools kernel-tools-libs kernel-tools-libs-devel -y
      ```
      

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the Yum repository does not contain the required versions of kernel\-headers, kernel\-devel, and other packages, you can download and install them yourself:      </div>
      

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Download the target software packages. One option is to download them from the <a href="https://mirrors.tuna.tsinghua.edu.cn/elrepo/archive/kernel/el7/x86_64/RPMS/">Tsinghua University Mirror Site</a>.      </div>
      

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e013359c6139b9df088d510cfc0d6d0.png" width="622px" />   </div>
   

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Upload the software packages to the target instance. <a href="https://docs.byteplus.com/en/docs/ecs/Local-data-uploading-overview">Learn more</a>.      </div>
      

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Execute <code>rpm -ivh <RPM package to be installed></code> command to install the target package      </div>
      

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4caa09f802f900233b911168855de991.png" width="897px" />   </div>
   

   4. Execute the following command to check whether the required new kernel and its kernel software packages are installed.

      ```Bash
      rpm -qa | grep kernel
      ```
      





</Tab>
</Tabs>



</Tab>
</Tabs>


<span id="f8MJbbSk"></span>
## Ubuntu OS

In this section, the operation of upgrading the Ubuntu 22.04 kernel version from `5.15.0-91-generic` to `6.8.0-56-generic` is used as an example.


1. [Log in to the target Linux server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current kernel version.

   ```Prolog
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a124b27351d31e900f79ef956a591e39.png) </span>

3. Execute the following command to update the system software package list.

   ```Prolog
   sudo apt update
   ```
   

4. Execute the following command to view the installable kernel versions.

   ```Prolog
   apt-cache search linux-image
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9cff69476bbe580a98a920c62119cc89.png) </span>

5. Install the specified kernel version.

   1. Execute the following command to install the specified version of the kernel.

      ```Plain Text
      sudo apt install linux-image-6.8.0-56-generic -y
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>6.8.0-56-generic</code> with the actual kernel version.      </div>
      

   2. Press Enter to confirm new kernel information.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01d8dae8e25838fc67266b84360d2484.png) </span>

6. Install kernel packages required by the new kernel.

   1. Execute the following command to install kernel packages required by the new kernel.

      ```Plain Text
      apt install linux-headers-6.8.0-56-generic linux-modules-extra-6.8.0-56-generic linux-generic -y
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Please replace <code>6.8.0-56-generic</code> with the actual kernel version.      </div>
      

   2. Press the Enter key to confirm the new kernel information.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_01d8dae8e25838fc67266b84360d2484.png) </span>

7. Execute the following command to forcibly update Initramfs.

   ```Plain Text
   sudo update-initramfs -u -k 6.8.0-56-generic
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace <code>6.8.0-56-generic</code> with the actual kernel version.   </div>
   

8. Execute the following command to update the GRUB configuration file.

   * BIOS boot mode:

      ```Plain Text
      sudo grub-mkconfig -o /boot/grub/grub.cfg
      ```
      

   * UEFI boot mode

      ```Plain Text
      sudo [ -d /boot/efi/EFI/ubuntu ] && sudo grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg
      ```
      

9. Edit the default kernel.

   1. Execute the following command to view the serial numbers of installed kernels.

      ```Plain Text
      grep menuentry /boot/grub/grub.cfg
      ```
      

      When the following appears, it means that `6.8.0-56-generic`, `5.15.0-135-generic`, and `5.15.0-91-generic` kernels have been installed. Their order is arranged from top to bottom, with the serial numbers starting from`0`, i.e., `6.8.0-56-generic` serial number is `0`, `5.15.0-135-generic` serial number is `1`, and `5.15.0-91-generic` serial number is `2`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_126e11713834ad1b875677a1bf561e74.png) </span>

   2. Execute the following command to open the GRUB file.

      ```Plain Text
      vim /etc/default/grub
      ```
      

   3. Please replace the `GRUB_DEFAULT` argument value with the target kernel number.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d294ed1801b47db8a3ed9a3416179c21.png) </span>

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

   5. Execute the following command to update the GRUB configuration file.

      ```Plain Text
      sudo update-grub
      ```
      

10. Execute the following command to restart the instance.

   ```Plain Text
   sudo reboot
   ```
   

11. Execute the following command to check whether the kernel is upgraded.

   ```Plain Text
   uname -r
   ```
   

   The callback shown below indicates that the kernel version has been successfully upgraded to `6.8.0-56-generic`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe22fb2193320f39736093a935915e65.png) </span>


<span id="PnOjeZdr"></span>
## Debian OS

This section uses the example of upgrading the kernel version of Debian 12 from `6.1.0-18-amd64` to `6.1.0-31-amd64`.


1. [Log in to the target Linux server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

2. Execute the following command to view the current kernel version.

   ```Plain Text
   uname -r
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a440f4e964320160fa0138308233a860.png) </span>

3. Execute the following command to update the system software package list.

   ```Plain Text
   sudo apt update
   ```
   

4. Execute the following command to view the installable kernel versions.

   ```Plain Text
   apt-cache search linux-image
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1f4b4db39b2c7cc50ed33453ef98ae83.png) </span>

5. Execute the following command to install the specified version of the kernel.

   ```Plain Text
   sudo apt install linux-image-6.1.0-31-amd64 -y
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace <code>6.1.0-31-amd64</code> with the actual kernel version.   </div>
   

6. Execute the following command to force update initramfs.

   ```Plain Text
   sudo update-initramfs -u -k 6.1.0-31-amd64
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Please replace <code>6.1.0-31-amd64</code> with the actual kernel version.   </div>
   

7. Execute the following command to update the GRUB configuration file.

   * BIOS boot mode:

      ```Plain Text
      sudo grub-mkconfig -o /boot/grub/grub.cfg
      ```
      

   * UEFI boot mode:

      ```Plain Text
      sudo [ -d /boot/efi/EFI/ubuntu ] && sudo grub-mkconfig -o /boot/efi/EFI/ubuntu/grub.cfg
      ```
      

8. Edit the default kernel.

   1. Execute the following command to view the serial numbers of installed kernels.

      ```Plain Text
      grep menuentry /boot/grub/grub.cfg
      ```
      

      When the following is echoed, it indicates two installed kernels: `Kernel version: 6.1.0-31-amd64` and `6.1.0-18-amd64`. Their order is arranged from top to bottom, with the serial numbers starting from `0`, i.e.,  `6.1.0-31-amd64` number is `0`, and `6.1.0-18-amd64` number is `1`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64c94ca401e1d407e3ba8361444ec113.png) </span>

   2. Execute the following command to open the GRUB file.

      ```Plain Text
      vim /etc/default/grub
      ```
      

   3. Please replace the `GRUB_DEFAULT` argument value with the target kernel number.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_47efd20f3b15c93ecb97a7423026479f.png) </span>

   4. Press the `Esc` key to exit edit mode, enter `:wq`, and then press Enter to save the changes and exit the file.

   5. Execute the following command to update the GRUB configuration file.

      ```Plain Text
      sudo update-grub
      ```
      

9. Execute the following command to restart the instance.

   ```Plain Text
   sudo reboot
   ```
   

10. Execute the following command to check whether the kernel is upgraded.

   ```Plain Text
   uname -r
   ```
   

   When the echo is as follows, it indicates that the kernel version has been successfully upgraded to `6.1.0-31-amd64`.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_899855ab75fa3c057e28970b1811448c.png) </span>
