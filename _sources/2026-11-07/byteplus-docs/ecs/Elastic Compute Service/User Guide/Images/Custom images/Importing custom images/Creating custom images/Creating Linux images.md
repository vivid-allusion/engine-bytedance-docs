---
title: "Creating Linux images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If you have the base image for the required distribution, you can use virt\-manager to create a QCOW2 image and import your private image to the platform by following the instructions in this topic.

This method allows you to create custom system images based on your business requirements and is applicable to scenarios in which complex initialization operations are required to create system images. After you import an image to the platform, you can use the image to deploy a system without performing complex initialization operations or deploy multiple ECS instances with the same configurations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The following 32\-bit and 64\-bit base image operating systems and relevant versions are supported for the method described in this topic.


* CentOS 6.x and later versions

* Ubuntu series

* Debian series


<span id=".56ys5LiA5q2l77ya5a6_5Li75py6546v5aKD5YeG5aSH77yI5Y-v6YCJ77yJ"></span>
## Step 1: Prepare the host machine environment (optional)

This step is applicable to users that do not have a virtual machine. If you already have a virtual machine, skip this step.


1. Configure the host machine.

   1. Prepare a physical server as the host machine.

      > No strict requirements are imposed on the operating system distribution of the host machine. In the example in this topic, the host machine running the x86 CentOS 7.9 operating system with [Graphical User Interface (GUI)](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux) installed is used.      
      

   2. Log in to the host machine.

   3. Execute the following command to check whether the virtualization capability is enabled for the host machine.

      ```Bash
      egrep '(vmx|svm)' /proc/cpuinfo
      ```
      

      If the output contains `vmx` or `svm` as shown in the following figure, the virtualization capability is enabled for the host machine.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_273745ac070097a758da4ad9fdc6c50d.png) </span>

   4. Execute the following command to check whether the kernel version of the host machine is higher than 3.10.

      ```Bash
      uname -r
      ```
      

      Sample output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e356d96f68be57777f8b3e21999ae781.png) </span>

2. Install virtualization software.

   1. Execute the following command to install KVM and related packages.

      ```Bash
      yum install -y qemu-kvm libvirt libvirt-python libvirt-client
      ```
      

   2. Execute the following commands to start the libvirtd service.

      ```Bash
      systemctl start libvirtd
      systemctl enable libvirtd
      ```
      

   3. Execute the following command to check whether the libvirtd service is started.

      ```Bash
      systemctl status libvirtd
      ```
      

      If the following information is returned, the service is started as expected.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74495d1348d14e391cea05ec4e133f71.png) </span>

3. Execute the following command to install virt\-manager.

   ```Bash
   yum install -y virt-manager
   ```
   

4. When you create a virtual machine with the `UEFI` boot mode, you must complete the following configurations.

   1. Execute the following command to install OVMF.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If OVMF is not available in the operating system sources of your host machine, before you install OVMF, execute the <code>sudo yum install -y epel-release</code> command to enable the EPEL repository and system supplementary repositories.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The architecture of the host machine and the virtual machine created in this topic is <code>X86_64</code>. If you create virtual machines of other architectures, install OVMF of the corresponding architecture.      </div>
      

      ```Bash
      yum install -y OVMF
      ```
      

   2. Execute the following command to query the OVMF file path.

      ```Bash
      rpm -ql OVMF
      ```
      

      When the output appears as shown below, the firmware file address in the currently installed OVMF package is `/usr/share/OVMF/OVMF_CODE.secboot.fd`, and the variable file address is `/usr/share/OVMF/OVMF_VARS.fd`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_07a5475c064fba170096db8a05f42d78.png) </span>

   3. Configure libvirtd to enable UEFI.

      1. Execute the following command and press `i` to enter edit mode.

         ```Bash
         vim /etc/libvirt/qemu.conf
         ```
         

      2. Insert the following content in the configuration file to add OVMF and runtime variable templates to the libvirt configuration.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Please replace <code>/usr/share/OVMF/OVMF_CODE.secboot.fd</code> with the actual path of the OVMF firmware file you installed.         </div>
         

         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">Please replace <code>/usr/share/OVMF/OVMF_VARS.fd</code> with the actual path of the OVMF variable file you installed.         </div>
         

         ```Plain Text
         nvram = [
           "/usr/share/OVMF/OVMF_CODE.secboot.fd:/usr/share/OVMF/OVMF_VARS.fd"
         ]
         ```
         

      3. Press `Esc`, enter `:wq`, and then press Enter to save and exit the configuration file.

      4. Execute the following command to restart the libvirtd service.

         ```Bash
         systemctl restart libvirtd
         ```
         

5. Enable the ip_forward feature for the host machine.

   1. Execute the following command to configure the ip_forward feature.

      ```Bash
      echo "net.ipv4.ip_forward = 1" >> /etc/sysctl.conf
      ```
      

   2. Execute the following command to make the configuration take effect.

      ```Bash
      sysctl -p
      ```
      


<span id=".56ys5LqM5q2l77ya5Zyo5a6_5Li75py65LiK5Yib5bu66Jma5ouf5py6"></span>
## Step 2: Create a virtual machine on the host machine


1. Prepare the base image on the host machine. Use a single\-partition image with the EXT3 or EXT4 file system, and do not create any partitions. Otherwise, issues such as automatic scaling\-up or boot exceptions may occur.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you use an official image.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your optional image files are in QCOW2 and ISO formats, we recommend that you use the ISO image.   </div>
   

2. Execute the following command to open virt\-manager.

   ```Bash
   virt-manager
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4acd96f3373d38120298823af21eec26.png) </span>

3. Click the new virtual machine icon to enable the new virtual machine wizard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aa48c2c1e0c8c5152b9df12160e55ca4.png) </span>

4. Select the "Local install media (ISO image or CDROM)" option and click the "Forward" button to install the virtual machine operating system by using the prepared base image.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4af838db63ec90a3f91351dd2dd2146b.png) </span>

5. Click the "Browse..." button to open the selection window.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50b7a24314022108b5d18b25674b5522.png) </span>

6. Click the "Browse Local" button to open the host machine storage directory, select the prepared base image on the host machine, click the "Open" button, and return to the new virtual machine wizard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d02ebc0d81bb4a4a30dd2014de6a211.png) </span>

7. Clear the "Automatically detect operating system based on install media" option, and manually select the OS type (image type) and version (platform version) based on the image information used.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3213b114c822fa29ca9e93d7191f18e5.png) </span>

8. Click the "Forward" button to configure virtual machine memory and CPU information.

   > You cannot allocate more virtual CPUs than the physical processors (or hyper\-threads) available in the host machine system. The number of available virtual CPUs is displayed as `Up to X available` following the configuration box.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3826d936d7eb392c3c16880cb0e662f0.png) </span>

9. Click the "Forward" button to configure the size of the created disk image.

   > Allocate sufficient space for virtual machine startup and the applications installed on the virtual machine.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_624bd4b5d72eef4d38c085516ee2ab02.png) </span>

10. Click the "Forward" button to configure the virtual machine name and network and select "Customize configuration before install".

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The virtual machine name can contain letters, digits, and the following characters: underscores (_), periods (.), and hyphens (\-).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default network configuration is <code>Virtual network 'default' : NAT</code>. You can change the network configuration by selecting another configuration from the "Network selection" drop\-down list.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0b98db68c438f8b0f18e7a45426e88b6.png) </span>

11. After you confirm the virtual machine configuration, click the "Finish" button to create the virtual machine.

12. On the configuration customization page, you can set the virtual machine boot mode to `UEFI` or adjust the hardware configuration of the virtual machine. You can perform the following steps to adjust the boot mode:

   1. In the left directory tree, select "Overview".

   2. In the "Firmware" drop\-down list of the "Hypervisor Details" area, select `UEFI` and click the "Apply" button to set the virtual machine boot mode to `UEFI`.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d58cc9ae39774c759e052302d8d15c0b.png) </span>


      c. Click the "Begin Installation" button in the upper left corner of the window to start installing the virtual machine.


13. When you follow the installation wizard to access the virtual machine configuration page, you must go to the network configuration page to enable the network connection.

   1. Click the "NETWORK & HOST NAME" button to go to the network configuration page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2ddac4a64ceef4cce8dc1b3384efd2b6.png) </span>

   2. Switch on the network connection, confirm that network connection is enabled, and click the "Done" button in the upper left corner to save the configuration and return to the configuration customization page.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4860d06e094c113f0abc1b0d60b391ce.png) </span>

14. After you specify other custom configurations, click the "Continue" button and follow the wizard to complete the virtual machine installation.


<span id=".56ys5LiJ5q2l77ya5L-u5pS56Jma5ouf5py65paH5Lu2"></span>
## Step 3: Modify the virtual machine files

<span id=".5L-u5pS5L2V0Yy9mc3RhYuaWh-S7tg=="></span>
### Edit the /etc/fstab file.

You need to log in to the created virtual machine, and comment out or delete the data volume directory information in the /etc/fstab file.


1. Execute the following command to open the /etc/fstab file.

   ```Bash
   vi /etc/fstab
   ```
   

2. Press `i` to enter edit mode and comment out or delete the data volume directory information.

3. Press `Esc` , enter `:wq`, and press Enter to save the configurations and exit the edit mode.


<span id=".5L-u5pS55ZCv5Yqo5byV5a-85paH5Lu277yI5Y-v6YCJ77yJ"></span>
### Modify the boot loader file (optional)

If you want to create an image in the `UEFI` boot mode, you can follow the instructions in this section to log in to the virtual machine and modify the boot loader file of the virtual machine.


<Tabs>
<Tab zoneid="hTw0IJonGr" title="CentOS 6.x、7.x、8.x">
<TabTitle>CentOS 6.x、7.x、8.x</TabTitle>

1. Execute the following command on the virtual machine to install grub2\-efi.

   ```Bash
   yum install grub2-efi-x64 && yum install grub2-efi-x64-modules
   ```
   

2. Execute the following command to reinstall grub with UEFI specified as the bootloader.

   ```Bash
   grub2-install --target=x86_64-efi --efi-directory=/boot/efi /dev/vda
   grub2-install --target=x86_64-efi --removable --efi-directory=/boot/efi --bootloader-id=GRUB
   ```
   

3. Execute the following command to regenerate the grub2\-config file.

   > The grub2\-config file that is regenerated overwrites the original configurations. We recommend that you back up data in advance.   
   

   ```Bash
   grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
   ```
   

4. Execute the following command to modify the configuration of the grub2\-mkconfig file.

   ```Bash
   sed -i 's/linux16/linuxefi/g' /boot/grub2/grub.cfg
   sed -i 's/initrd16/initrdefi/g' /boot/grub2/grub.cfg
   ```
   


</Tab>
<Tab zoneid="WgRXyLMQuw" title="Debian/Ubuntu">
<TabTitle>Debian/Ubuntu</TabTitle>

1. Execute the following command on the virtual machine to install grub2\-efi.

   ```Bash
   apt install --reinstall grub-common grub-efi-amd64
   ```
   

2. Execute the following command to reinstall grub with UEFI specified as the bootloader.

   ```Bash
   grub-install --target=x86_64-efi --efi-directory=/boot/efi /dev/vda
   grub-install --target=x86_64-efi --removable --efi-directory=/boot/efi --bootloader-id=GRUB
   ```
   

3. Execute the following command to regenerate the grub2\-config file.

   > The grub2\-config file that is regenerated overwrites the original configurations. We recommend that you back up data in advance.   
   

   ```Bash
   grub-mkconfig -o /boot/grub/grub.cfg
   ```
   


</Tab>
</Tabs>


<span id=".56ys5Zub5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWQtaW5pdA=="></span>
## Step 4: Install Cloud\-init on the virtual machine


1. Execute the following commands in sequence to install a Python 3 version and cloud\-init dependencies.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Install Python 3.6 or later. Otherwise, the incompatibilities between Python 3 and certain pip packages affect the running of Cloud\-init.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">We recommend that you manually download and install Python 3 from <a href="http://www.python.org/downloads/source/">the official Python website</a>.   </div>
   

   
   <Tabs>
   <Tab zoneid="M6mmDLpjbN" title="CentOS 6.x、7.x、8.x">
   <TabTitle>CentOS 6.x、7.x、8.x</TabTitle>
   
   ```Bash
   yum install python3 python3-pip cloud-utils-growpart -y
   ```
   
   
   
   </Tab>
   <Tab zoneid="wwOcnwsmVZ" title="Ubuntu/Debian">
   <TabTitle>Ubuntu/Debian</TabTitle>
   
   ```Bash
   apt-get install python3 python3-pip  cloud-guest-utils -y
   ```
   
   
   
   </Tab>
   </Tabs>
   

2. Install and configure Cloud\-init.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can download the official Cloud\-init or the community edition of Cloud\-init based on your business requirements. We recommend that you use the official Cloud\-init.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you want to access metadata in security hardening mode, install Cloud\-init in security hardening mode. For information about how to view metadata and the available metadata items, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata">Viewing instance metadata</a>.   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">   </div>
   

   
   <Tabs>
   <Tab zoneid="MKAmuZfXNV" title="Officially provided Cloud-init">
   <TabTitle>Officially provided Cloud-init</TabTitle>
   
   1. Download Cloud\-init.
   
      * **Download over the Internet**
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">We recommend that you select the download link for the region where the target instance is located to reduce access latency and improve download speed.      </div>
         
   
         * China (Hong Kong)
   
            ```Bash
            wget https://cloud-init-cn-hongkong.tos-cn-hongkong.bytepluses.com/ecs.linux.cloudinit_1.0.0.3.tar.gz
            ```
            
   
         * Asia Pacific (Johor)
   
            ```Bash
            wget https://cloud-init-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/ecs.linux.cloudinit_1.0.0.3.tar.gz
            ```
            
   
      * **Download over the intranet**
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Use the download link for the region where the target instance is located to download Cloud\-init over the platform intranet.      </div>
         
   
         * China (Hong Kong)
   
            ```Bash
            wget https://cloud-init-cn-hongkong.tos-cn-hongkong.ibytepluses.com/ecs.linux.cloudinit_1.0.0.3.tar.gz
            ```
            
   
         * Asia Pacific (Johor)
   
            ```Bash
            wget https://cloud-init-ap-southeast-1.tos-ap-southeast-1.ibytepluses.com/ecs.linux.cloudinit_1.0.0.3.tar.gz
            ```
            
   
   2. Execute the following command to install Cloud\-init.
   
      ```Bash
      tar zxvf ecs.linux.cloudinit_1.0.0.3.tar.gz
      ls
      cd cloud-init-20.3
      pip3 install -r requirements.txt -i https://mirrors.ivolces.com/pypi/simple/
      python3 setup.py build
      python3 setup.py install --init-system systemd
      
      ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init
      
      systemctl enable cloud-init-local.service
      systemctl enable cloud-init.service
      systemctl enable cloud-config.service
      systemctl enable cloud-final.service
      ```
      
   
   3. Modify the cloud.cfg file.
   
      1. Execute the following command to open the cloud.cfg file.
   
         ```Bash
         vim /etc/cloud/cloud.cfg
         ```
         
   
      2. Press `i` to enter edit mode and replace the content in the Cloud\-init configuration file with the following content.
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you want to create a CentOS image, add the <code>distro: rhel</code> configuration to the <code>system_info</code> module.      </div>
         
   
         ```YAML
         users:
          - default
         
         disable_root: 0
         ssh_pwauth: 1
         growpart:
             mode: auto
             devices: ['/']
             ignore_growroot_disabled: false
         
         mount_default_fields: [~, ~, 'auto', 'defaults,nofail,x-systemd.requires=cloud-init.service', '0', '2']
         resize_rootfs_tmp: /dev
         ssh_deletekeys: 1
         syslog_fix_perms: ~
         disable_vmware_customization: false
         
         manage_etc_hosts: localhost
         
         cloud_init_modules:
          - disk_setup
          - migrator
          - bootcmd
          - write-files
          - growpart
          - resizefs
          - set_hostname
          - update_hostname
          - update_etc_hosts
          - rsyslog
          - users-groups
          - ssh
         
         cloud_config_modules:
          - mounts
          - locale
          - set-passwords
          - rh_subscription
          - yum-add-repo
          - package-update-upgrade-install
          - timezone
          - puppet
          - chef
          - salt-minion
          - mcollective
          - disable-ec2-metadata
          - runcmd
         
         cloud_final_modules:
          - rightscale_userdata
          - scripts-per-once
          - scripts-per-boot
          - scripts-per-instance
          - scripts-user
          - ssh-authkey-fingerprints
          - keys-to-console
          - phone-home
          - final-message
          - power-state-change
         
         system_info:
           # distro: rhel
           paths:
             cloud_dir: /var/lib/cloud
             templates_dir: /etc/cloud/templates
           ssh_svcname: sshd
         ```
         
   
      3. Press `Esc` to exit the edit mode, enter `:wq`, and press Enter to save the changes.
   
   3. Replace the cloud\-init data source.
   
      1. Execute the following command to open the configuration file.
   
         ```Bash
         vim /etc/cloud/cloud.cfg.d/90_dpkg.cfg
         ```
         
   
      2. Press `i` to enter edit mode and write the following content into the file.
   
         ```YAML
         datasource_list: [ConfigDrive, VolcStack]
         
         datasource:
           VolcStack:
             metadata_urls: ["http://100.96.0.96"]
             max_wait: -1
             timeout: 5
             retries: 24
             apply_network_config: True
         ```
         
   
      3. Press `Esc` to exit the edit mode, enter `:wq`, and press Enter to save the changes.
   
   
   </Tab>
   <Tab zoneid="BDwQy0KXVl" title="Community version of Cloud-init">
   <TabTitle>Community version of Cloud-init</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">In the example in this topic, the 20.03 version of Cloud\-init is downloaded. For more versions, visit the <a href="https://launchpad.net/cloud-init/+download">Cloud\-init official website</a> to obtain the download link.</div>
   
   
   
   1. Download Cloud\-init.
   
      ```Bash
      wget https://launchpad.net/cloud-init/trunk/20.3/+download/cloud-init-20.3.tar.gz
      ```
      
   
   2. Execute the following command to install Cloud\-init.
   
      ```Bash
      tar zxvf cloud-init-20.3.tar.gz
      ls
      cd cloud-init-20.3
      pip3 install -r requirements.txt -i https://mirrors.ivolces.com/pypi/simple/
      python3 setup.py build
      python3 setup.py install --init-system systemd
      
      ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init
      
      systemctl enable cloud-init-local.service
      systemctl enable cloud-init.service
      systemctl enable cloud-config.service
      systemctl enable cloud-final.service
      ```
      
   
   3. Modify the cloud.cfg file.
   
      1. Execute the following command to open the cloud.cfg file.
   
         ```Bash
         vim /etc/cloud/cloud.cfg
         ```
         
   
      2. Press `i` to enter edit mode and replace the content in the Cloud\-init configuration file with the following content.
   
         <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
         
   
         <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If you want to create a CentOS image, add the <code>distro: rhel</code> configuration to the <code>system_info</code> module.      </div>
         
   
         ```YAML
         users:
          - default 
         
         disable_root: 0
         ssh_pwauth: 1
         growpart:
             mode: auto
             devices: ['/']
             ignore_growroot_disabled: false
         
         mount_default_fields: [~, ~, 'auto', 'defaults,nofail,x-systemd.requires=cloud-init.service', '0', '2']
         resize_rootfs_tmp: /dev
         ssh_deletekeys: 1
         syslog_fix_perms: ~
         disable_vmware_customization: false
         
         manage_etc_hosts: localhost
         
         cloud_init_modules:
          - disk_setup
          - migrator
          - bootcmd
          - write-files
          - growpart
          - resizefs
          - set_hostname
          - update_hostname
          - update_etc_hosts
          - rsyslog
          - users-groups
          - ssh
         
         cloud_config_modules:
          - mounts
          - locale
          - set-passwords
          - rh_subscription
          - yum-add-repo
          - package-update-upgrade-install
          - timezone
          - puppet
          - chef
          - salt-minion
          - mcollective
          - disable-ec2-metadata
          - runcmd
         
         cloud_final_modules:
          - rightscale_userdata
          - scripts-per-once
          - scripts-per-boot
          - scripts-per-instance
          - scripts-user
          - ssh-authkey-fingerprints
          - keys-to-console
          - phone-home
          - final-message
          - power-state-change
         
         system_info:
           # distro: rhel
           paths:
             cloud_dir: /var/lib/cloud
             templates_dir: /etc/cloud/templates
           ssh_svcname: sshd
         ```
         
   
      3. Press `Esc` to exit the edit mode, enter `:wq`, and press Enter to save the changes.
   
   4. Replace the cloud\-init data source.
   
      1. Execute the following command to open the configuration file.
   
         ```Bash
         vim /etc/cloud/cloud.cfg.d/90_dpkg.cfg
         ```
         
   
      2. Press `i` to enter edit mode and write the following content into the file.
   
         ```YAML
         datasource_list: [ConfigDrive, OpenStack]
         
         datasource:
           OpenStack:
             metadata_urls: ["http://100.96.0.96"]
             max_wait: -1
             timeout: 5
             retries: 5
             apply_network_config: True
         ```
         
   
      3. Press `Esc` to exit the edit mode, enter `:wq`, and press Enter to save the changes.
   
   
   </Tab>
   <Tab zoneid="bnAbZyQ5uy" title="Cloud-Init supporting security hardening mode">
   <TabTitle>Cloud-Init supporting security hardening mode</TabTitle>
   
   1. Execute the following command to create the installation script.
   
      ```Bash
      vim install_cloudinit.sh
      ```
      
   
   2. Press `i` to enter edit mode and fill the following content into the script file.
   
      ```Bash
      #!/bin/bash
      which cloud-init >/dev/null 2>&1
      if [ "$?" -eq 0 ]; then
          echo "cloud-init installed.Please uninstall cloud-init before install volc hardening cloud-init."
          exit 1
      fi
      if [ -f /root/ecs.linux.cloudinit_1.0.0.7.tar.gz ]; then
          rm -rf /root/ecs.linux.cloudinit_1.0.0.7.tar.gz
      fi
      wget  -P /root/ https://cloud-init-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/hardening_mode/ecs.linux.cloudinit_1.0.0.7.tar.gz
      if [ ! -f /root/ecs.linux.cloudinit_1.0.0.7.tar.gz ]; then
          echo "Download volc hardening cloud-init failed."
          exit 1
      fi
      if [ -f /root/volc_cloudinit_1_0_0_7 ]; then
          rm -rf /root/volc_cloudinit_1_0_0_7
      fi
      mkdir /root/volc_cloudinit_1_0_0_7
      tar -zxvf /root/ecs.linux.cloudinit_1.0.0.7.tar.gz -C /root/volc_cloudinit_1_0_0_7/
      if [ $? -ne 0 ]; then
          echo "Uncompress volc hardening cloud-init pacakage failed."
          rm -rf /root/volc_cloudinit_1_0_0_7
          rm -rf /root/ecs.linux.cloudinit_1.0.0.7.tar.gz
          exit 1
      fi
      cd /root/volc_cloudinit_1_0_0_7/cloud-init-20.3/
      pip3 install -r requirements.txt -i https://mirrors.ivolces.com/pypi/simple/
      python3 setup.py build
      python3 setup.py install --init-system systemd
      if [ ! -f /usr/local/bin/cloud-init ]; then
          ln -s /usr/local/bin/cloud-init /usr/bin/cloud-init
      fi
      systemctl enable cloud-init-local.service
      systemctl enable cloud-init.service
      systemctl enable cloud-config.service
      systemctl enable cloud-final.service
      
      cat > /etc/cloud/cloud.cfg.d/90_dpkg.cfg << EOF
      datasource_list: [ConfigDrive, VolcStack]
      
      datasource:
        VolcStack:
          metadata_urls: ["http://100.96.0.96"]
          max_wait: -1
          timeout: 5
          retries: 24
          apply_network_config: True
      EOF
      distro=`lsb_release -a 2> /dev/null | grep "Distributor ID:" | cut -d ":" -f2`
      if [[ $distro =~ "CentOS" ]]; then
          cat << EOF > /etc/cloud/cloud.cfg
      users:
       - default
      disable_root: 0
      ssh_pwauth: 1
      growpart:
          mode: auto
          devices: ['/']
          ignore_growroot_disabled: false
      mount_default_fields: [~, ~, 'auto', 'defaults,nofail,x-systemd.requires=cloud-init.service', '0', '2']
      resize_rootfs_tmp: /dev
      ssh_deletekeys: 1
      syslog_fix_perms: ~
      disable_vmware_customization: false
      manage_etc_hosts: localhost
      cloud_init_modules:
       - disk_setup
       - migrator
       - bootcmd
       - write-files
       - growpart
       - resizefs
       - set_hostname
       - update_hostname
       - update_etc_hosts
       - rsyslog
       - users-groups
       - ssh
      cloud_config_modules:
       - mounts
       - locale
       - set-passwords
       - rh_subscription
       - yum-add-repo
       - package-update-upgrade-install
       - timezone
       - puppet
       - chef
       - salt-minion
       - mcollective
       - disable-ec2-metadata
       - runcmd
      cloud_final_modules:
       - rightscale_userdata
       - scripts-per-once
       - scripts-per-boot
       - scripts-per-instance
       - scripts-user
       - ssh-authkey-fingerprints
       - keys-to-console
       - phone-home
       - final-message
       - power-state-change
      system_info:
        distro: rhel
        paths:
          cloud_dir: /var/lib/cloud
          templates_dir: /etc/cloud/templates
        ssh_svcname: sshd
      EOF
      else
          cat << EOF > /etc/cloud/cloud.cfg
      users:
       - default
      disable_root: 0
      ssh_pwauth: 1
      growpart:
          mode: auto
          devices: ['/']
          ignore_growroot_disabled: false
      mount_default_fields: [~, ~, 'auto', 'defaults,nofail,x-systemd.requires=cloud-init.service', '0', '2']
      resize_rootfs_tmp: /dev
      ssh_deletekeys: 1
      syslog_fix_perms: ~
      disable_vmware_customization: false
      manage_etc_hosts: localhost
      cloud_init_modules:
       - disk_setup
       - migrator
       - bootcmd
       - write-files
       - growpart
       - resizefs
       - set_hostname
       - update_hostname
       - update_etc_hosts
       - rsyslog
       - users-groups
       - ssh
      cloud_config_modules:
       - mounts
       - locale
       - set-passwords
       - rh_subscription
       - yum-add-repo
       - package-update-upgrade-install
       - timezone
       - puppet
       - chef
       - salt-minion
       - mcollective
       - disable-ec2-metadata
       - runcmd
      cloud_final_modules:
       - rightscale_userdata
       - scripts-per-once
       - scripts-per-boot
       - scripts-per-instance
       - scripts-user
       - ssh-authkey-fingerprints
       - keys-to-console
       - phone-home
       - final-message
       - power-state-change
      system_info:
        paths:
          cloud_dir: /var/lib/cloud
          templates_dir: /etc/cloud/templates
        ssh_svcname: sshd
      EOF
      fi
      
      cat << EOF > /etc/cloud/cloud.cfg.d/90_dpkg.cfg
      datasource_list: [ConfigDrive, VolcStack]
      
      datasource:
        VolcStack:
          metadata_urls: ["http://100.96.0.96"]
          max_wait: -1
          timeout: 5
          retries: 24
          apply_network_config: True
      EOF
      
      rm -rf /root/volc_cloudinit_1_0_0_7
      rm -rf /root/ecs.linux.cloudinit_1.0.0.7.tar.gz
      if cloud-init -v; then
          echo "Install volc hardening cloud-init success."
          exit 0
      else
          echo "Install volc hardening cloud-init failed."
          exit 1
      fi
      ```
      
   
   3. Press the Esc key to exit the edit mode, enter :wq, and then press Enter to save and exit the file.
   
   4. Execute the following command to grant the execute permission on the script.
   
      ```Bash
      chmod +x install_cloudinit.sh
      ```
      
   
   5. Execute the following command to execute the script, and install and configure Cloud\-init that supports security hardening mode.
   
      ```Bash
      ./install_cloudinit.sh
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="5VeObo5n"></span>
## Step 5: Install the driver on the virtual machine

<span id=".5a6J6KOFVmlydGlv6amx5Yqo"></span>
### Install the Virtio driver

<span id=".5q2l6aqk5LiA77ya56Gu6K6k5YaF5qC45piv5ZCm5pSv5oyBVmlydGlv6amx5Yqo"></span>
#### Step I: Confirm whether the kernel supports the Virtio driver

Execute the following command to check whether the current virtual machine operating system supports the Virtio driver.

```Bash
grep -i virtio /boot/config-$(uname -r)
```


Sample output:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b18553d69a7ef9cbea8697014edffd52.png) </span>

Output description:

Perform subsequent operations based on the value of the `CONFIG_VIRTIO_BLK` parameter in the command output.


|Results |Description |
|---|---|
|Parameter value: `m` |The operating system kernel supports the Virtio driver.<br><br>Perform [Step 2](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5q2l6aqkMg==) to check whether the Virtio driver is included in the temporary file system initramfs or initrd. |
|Parameter value: `y` |This indicates that the operating system kernel already includes the Virtio driver. You can continue to[ install the Virtio1.1 driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo). |
|These two parameters are not available. |The operating system kernel does not support the Virtio driver. You need to compile and install the Virtio driver yourself. |


<span id=".5q2l6aqk5LqM77ya56Gu6K6k5Li05pe25paH5Lu257O757uf5piv5ZCm5YyF5ZCrVmlydGlv6amx5Yqo"></span>
####  Step 2: Check whether the temporary file system includes the Virtio driver


<Tabs>
<Tab zoneid="tRlK81v87y" title="CentOS 6 and later versions / Redhat 6 and later versions">
<TabTitle>CentOS 6 and later versions / Redhat 6 and later versions</TabTitle>

```Bash
lsinitrd /boot/initramfs-$(uname -r).img | grep virtio
```



</Tab>
<Tab zoneid="vubE4x1Vb3" title="Debian/Ubuntu">
<TabTitle>Debian/Ubuntu</TabTitle>

```Bash
lsinitramfs /boot/initrd.img-$(uname -r) | grep virtio
```



</Tab>
</Tabs>


Sample output:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_87ae41d41e48d060f1048a38143f7784.png) </span>

Output description:


* As shown in the preceding figure, information related to the Virtio driver is displayed. This indicates that the initramfs temporary file system already contains the virtio_blk driver and the virtio.ko, virtio_pci.ko, and virtio_ring.ko dependencies. Continue to [install the Virtio1.1 driver](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo).

* If the output is empty, the temporary file system does not contain the Virtio driver. Proceed to [III](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5q2l6aqkMw==) to repair the temporary file system.


<span id=".5q2l6aqk5LiJ77ya5L-u5aSN5Li05pe25paH5Lu257O757uf"></span>
####  Step 3: Repair the temporary file system


<Tabs>
<Tab zoneid="wjDONYGQjw" title="CentOS 6 and later versions / Redhat 6 and later versions">
<TabTitle>CentOS 6 and later versions / Redhat 6 and later versions</TabTitle>

1. Execute the following command to open the dracut.conf file.

   ```Bash
   vim /etc/dracut.conf
   ```
   

2. Press `i` to enter edit mode and add the following content.

   ```Plain Text
   add_drivers+="virtio_blk virtio_scsi virtio_net virtio_pci virtio_ring virtio"
   ```
   

3. After you modify the file, press `Esc`, enter `:wq`, and then press Enter to save the modification and exit the file.

4. Execute the following command to regenerate initrd.

   ```Bash
   dracut -f
   ```
   


</Tab>
<Tab zoneid="vHgIcXQ2Ne" title="Debian/Ubuntu">
<TabTitle>Debian/Ubuntu</TabTitle>

1. Execute the following command to open the modules file.

   ```Bash
   vim /etc/initramfs-tools/modules
   ```
   

2. Press `i` to enter edit mode and add the following content.

   ```YAML
   virtio_blk
   virtio_scsi
   virtio_net
   virtio_pci
   virtio_ring
   virtio
   ```
   

3.  After you modify the file, press `Esc`, enter `:wq`, and then press Enter to save the modification and exit the file.

4. Execute the following command to regenerate initramfs.

   ```Plain Text
   update-initramfs -u
   ```
   





</Tab>
</Tabs>


<span id=".5q2l6aqk5Zub77ya6aqM6K-B5L-u5aSN57uT5p6c"></span>
#### Step 4: Verify the repair results

After you repair the temporary file system, you can execute the command in [Step 2](https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5q2l6aqkMg==) again to verify that the Virtio driver is contained in the temporary file system initramfs or initrd.

<span id=".5a6J6KOFVmlydGlvMS4x6amx5Yqo"></span>
### Install the Virtio 1.1 driver

If you want to apply the image you create on ECS instances based on the platform proprietary DPU architecture, and the image kernel does not support the Virtio 1.1 protocol, install the Virtio 1.1 driver by following the instructions in this topic.


<Tabs>
<Tab zoneid="6unZmVym" title="Instance type of the DPU architecture">
<TabTitle>Instance type of the DPU architecture</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The following table describes the instance types based on the platform DPU architecture. If you do not want to use your image to create instances of the following types, skip this section.</div>



|System architecture |Type |Instance specification |
|---|---|---|
|x86 |[General-purpose](https://docs.byteplus.com/en/docs/ecs/General-purpose) |* General\-purpose g3i<br><br>* General\-purpose g3a |
||[Compute-optimized](https://docs.byteplus.com/en/docs/ecs/Computing-optimized) |* Compute\-optimized c3i<br><br>* Compute\-optimized c3a |
||[Memory-optimized](https://docs.byteplus.com/en/docs/ecs/Memory-optimized) |* Memory\-optimized r3i<br><br>* Memory\-optimized r3a |
||[Local SSD](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based) |Local SSD i3s |
|EBM |All [Elastic Bare Metal (EBM) ](https://docs.byteplus.com/en/docs/ecs/EBM-overview)instance types |\- |





</Tab>
<Tab zoneid="Jr9kOhY9" title="A kernel image that supports the Virtio 1.1 protocol">
<TabTitle>A kernel image that supports the Virtio 1.1 protocol</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The table below lists mainstream Linux operating systems that support the Virtio 1.1 protocol. If the platform version of the image you uploaded to the VM is listed below, please skip this step.</div>



|Image name |Versions |
|---|---|
|CentOS |CentOS 8.3 and later versions |
|Ubuntu |Ubuntu 20.xx and later versions |
|Debian |Debian 11 and later versions |





</Tab>
</Tabs>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before you install the driver:</div>


   * <div data-tips="true" data-tips-type="tip">Install kernel\-headers and kernel\-devel for the virtual machine and make sure that they match the kernel version. Otherwise, the driver installation may fail. If you upgrade the kernel, restart the virtual machine before you install the driver. You can also compile <a href="https://github.com/volcengine/dkms-virtio1.1">the driver source code</a>   .</div>


   * <div data-tips="true" data-tips-type="tip">Make sure that the virtual machine can access the Internet.</div>


* <div data-tips="true" data-tips-type="tip">If you want to use the image to create an Elastic Bare Metal (EBM)\-type instance with the LTS\-kernel, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFTFRTLeWGheaguOS4jlZpcnRpbzEuMempseWKqO-8iOWPr-mAie-8iQ==">Installing LTS\-kernel and Virtio 1.1 driver on virtual machines</a> for instructions.</div>


1. Execute the following command to download the Virtio 1.1 driver management script.

   ```Bash
   wget -O virtio_tool https://virtio11-drivers.tos-cn-beijing.volces.com/virtio_tool_1.1.2
   ```
   

2. Run the following command to grant the execute permission on the script file.

   ```Bash
   chmod +x ./virtio_tool
   ```
   

3. In the directory where the virtio_tool file resides, execute the following command to check whether the Virtio 1.1 driver version meets the requirements.

   ```Bash
   ./virtio_tool -check
   ```
   

   * If the following output is displayed, the required Virtio 1.1 driver is already installed on your virtual machine. Skip this section.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e78ef3e3bd7bf2dbe8f4595598e8b1f7.png) </span>

   * If the following output is displayed, the required Virtio 1.1 driver is not installed on your virtual machine. Proceed to the next operation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cdb39409b30118e152b051199f391b11.png) </span>

4. Install the Virtio 1.1 driver by using virtio_tool.

   
   <Tabs>
   <Tab zoneid="xMHjTRmdMy" title="CentOS">
   <TabTitle>CentOS</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Currently, only the following operating systems and kernel versions are supported for installing the Virtio1.1 driver.</div>
   
   
   <div data-tips="true" data-tips-type="default">
   |<strong>Image version</strong> |<strong>Kernel version</strong> |
   |---|---|
   |CentOS 7.9 64 bit |3.10.0\-1160.x |
   |CentOS 7.8 64 bit |3.10.0\-1127.x |
   |CentOS 7.7 64 bit |3.10.0\-1062.x |
   |CentOS 7.6 64 bit |3.10.0\-957.x |
   |64\-bit CentOS 7.5 |3.10.0\-862.x |
   |64\-bit CentOS 7.4 |3.10.0\-693.x |
   |64\-bit CentOS 7.3 |3.10.0\-514.x |
   |64\-bit CentOS 7.2 |3.10.0\-327.x |
   </div>
   
   
   In the directory where the virtio_tool script is located, execute the following command to install the Virtio1.1 driver.
   
   ```Bash
   yum -y install rpm-build redhat-lsb-core
   yum -y install epel-release
   
   sed -e 's!^metalink=!#metalink=!g' \
       -e 's!^#baseurl=!baseurl=!g' \
       -e 's!//download\.fedoraproject\.org/pub!//mirrors.volces.com!g' \
       -i /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel-testing.repo
     
   yum -y install --enablerepo=epel dkms
   
   ./virtio_tool -install
   ```
   
   
   
   </Tab>
   <Tab zoneid="fEWDZ81tas" title="Ubuntu">
   <TabTitle>Ubuntu</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Currently, only the following operating systems and kernel versions are supported for installing the Virtio1.1 driver.</div>
   
   
   <div data-tips="true" data-tips-type="default">
   |<strong>Image version</strong> |<strong>Kernel version</strong> |
   |---|---|
   |Ubuntu Server 18.04 LTS 64 bit |4.15.x |
   |Ubuntu Server 16.04 LTS 64 bit |4.4.x |
   </div>
   
   
   In the directory where the virtio_tool script is located, execute the following command to install the Virtio1.1 driver.
   
   
   1. Execute the following command to install the required tools.
   
      ```Bash
      apt install -y dkms fakeroot
      ```
      
   
   2. Execute the following command to install the Virtio1.1 driver.
   
      ```Bash
      ./virtio_tool -install
      ```
      
   
   3. Execute the following command to modify the driver configuration.
   
      ```Bash
      cat <<EOF > /etc/udev/rules.d/72-virtio.rules
      ACTION=="add" \
      , ATTRS{device}=="0x1042" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1041" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1001" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      ACTION=="add" \
      , ATTRS{device}=="0x1000" \
      , ATTRS{vendor}=="0x1af4" \
      , SUBSYSTEM=="virtio" \
      , RUN+="/etc/initramfs-tools/scripts/init-premount/rebind.sh"
      EOF
      ```
      
   
   
   </Tab>
   <Tab zoneid="G5rWjaORlm" title="Debian">
   <TabTitle>Debian</TabTitle>
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">Currently, only the following operating systems and kernel versions are supported for installing the Virtio1.1 driver.</div>
   
   
   <div data-tips="true" data-tips-type="default">
   |<strong>Image version</strong> |<strong>Kernel version</strong> |
   |---|---|
   |64\-bit Debian 10 |4.19.x |
   |64\-bit Debian 9 |4.9.x |
   </div>
   
   
   In the directory where the virtio_tool script is located, execute the following command to install the Virtio1.1 driver.
   
   ```Bash
   apt install -y dkms fakeroot
   apt install -y linux-image-$(uname -r)
   apt install -y linux-headers-$(uname -r)
   apt install -y linux-tools
   
   ./virtio_tool -install
   ```
   
   
   
   </Tab>
   </Tabs>
   

5. If you change the kernel version within the instance after you install the driver, you must reinstall the Virtio 1.1 driver that is compatible with the new kernel version. Otherwise, the instance cannot be used as expected.


<span id=".5a6J6KOFTFRTLeWGheaguOS4jlZpcnRpbzEuMempseWKqO-8iOWPr-mAie-8iQ=="></span>
### Install the LTS\-kernel and Virtio 1.1 driver (optional)

This section is applicable only if you want to create EBM\-type instances by using Linux images with the LTS\-kernel. If you do not want to use your image to create EBM\-type instances, skip this section.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you want to use your image to create EBM\-type instances but your image does not have the LTS\-kernel, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Creating-Linux-images#.5a6J6KOFVmlydGlvMS4x6amx5Yqo">Installing the Virtio 1.1 driver on virtual machines</a> for instructions.</div>


* <div data-tips="true" data-tips-type="tip">You cannot perform this operation directly on EBM instances. Instead, you need to perform this operation on an ECS instance, create a custom image from the instance, and then apply the image to EBM instances.</div>


* <div data-tips="true" data-tips-type="tip">This section only provides an approach and method for using a custom kernel on an EBM\-type instance.</div>


* Overall installation process:

   * If an old version of the Virtio 1.1 driver exists, delete the old version first.

   * Install the LTS\-kernel on the ECS instance and restart the instance to switch to the LTS\-kernel.

   * Install the Virtio 1.1 driver package specified by the LTS\-kernel.

   * Update initramfs/initrd and restart the instance to check whether the instance works as expected.

1. Execute the following command to download the Virtio 1.1 driver management script over the Internet.

   ```Bash
   wget -O virtio_tool https://virtio11-drivers.tos-cn-beijing.volces.com/virtio_tool_1.1.2
   ```
   

2. Execute the following command to grant the execute permission on the script file.

   ```Bash
   chmod +x ./virtio_tool
   ```
   

3. In the directory where the virtio_tool file is located, execute the following command to check whether the Virtio1.1 driver is installed on the virtual machine.

   ```Bash
   ./virtio_tool -check
   ```
   

   * If the following output is displayed, the Virtio1.1 driver is installed on the virtual machine.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08aaa016d3e020f6d038735f52cecd6e.png) </span>

      Execute the following command to uninstall the old Virtio1.1 driver version before you proceed to the next operation.

      ```Bash
      ./virtio_tool -uninstall
      ```
      

      If the following output is displayed, the driver is uninstalled.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0d514cfb4f39e4295eec3d824ec33c9b.png) </span>

   * If the following output is displayed, the Virtio1.1 driver is not installed on your virtual machine. Proceed to the next operation.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9dfda9aa7c58ee4b4801b6eab25fe5ed.png) </span>

4. Install the kernel and driver.

   
   <Tabs>
   <Tab zoneid="sFvCbg11W1" title="CentOS 7.x">
   <TabTitle>CentOS 7.x</TabTitle>
   
   1. Install the LTS\-kernel.
   
      1. Execute the following commands in sequence to install the LTS\-kernel.
   
         * LTS\-4.9 kernel: Execute the following commands in sequence to install the LTS\-kernel.
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-4.9.324-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-devel-4.9.324-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-headers-4.9.324-1.x86_64.rpm
            yum install -y kernel-headers-4.9.324-1.x86_64.rpm kernel-devel-4.9.324-1.x86_64.rpm
            yum install -y kernel-4.9.324-1.x86_64.rpm
            ```
            
   
         * LTS\-4.14 kernel: Execute the following commands in sequence to install the LTS\-kernel.
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-4.14.289-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-devel-4.14.289-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-headers-4.14.289-1.x86_64.rpm
            yum install -y kernel-headers-4.14.289-1.x86_64.rpm kernel-devel-4.14.289-1.x86_64.rpm
            yum install -y kernel-4.14.289-1.x86_64.rpm
            ```
            
   
         * LTS\-4.19 kernel: Execute the following commands in sequence to install the LTS\-kernel.
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-4.19.253-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-devel-4.19.253-1.x86_64.rpm
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-rpm/kernel-headers-4.19.253-1.x86_64.rpm
            yum install -y kernel-headers-4.19.253-1.x86_64.rpm kernel-devel-4.19.253-1.x86_64.rpm
            yum install -y kernel-4.19.253-1.x86_64.rpm
            ```
            
   
      2. Execute the following commands in sequence to switch kernels and restart the instance. This way, the instance runs with the specified LTS\-kernel version. In this example, LTS\-4.9 is used.
   
         1. View the number of kernels currently on the system.
   
            ```Bash
            cat /boot/efi/EFI/centos/grub.cfg |grep menuentry
            ```
            
   
            Sample output
   
            ```Plain Text
            if [ x"${feature_menuentry_id}" = xy ]; then
               menuentry_id_option="--id"
               menuentry_id_option=""
            export menuentry_id_option
            menuentry 'CentOS Linux (4.9.324) 7 (Core)' --class centos --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-3.10.0-1127.19.1.el7.x86_64-advanced-bf734ac7-0328-4e7f-8ada-ca0917a32945' {
            menuentry 'CentOS Linux (3.10.0-1127.19.1.el7.x86_64) 7 (Core)' --class centos --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-3.10.0-1127.19.1.el7.x86_64-advanced-bf734ac7-0328-4e7f-8ada-ca0917a32945' {
            menuentry 'CentOS Linux (0-rescue-ccc58c7f32cb4030969ada15e4ae0d0f) 7 (Core)' --class centos --class gnu-linux --class gnu --class os --unrestricted $menuentry_id_option 'gnulinux-0-rescue-ccc58c7f32cb4030969ada15e4ae0d0f-advanced-bf734ac7-0328-4e7f-8ada-ca0917a32945' {
            ```
            
   
         2. Set the default startup kernel.
   
            Specify the "CentOS Linux (4.9.324) 7 (Core)" kernel in the preceding output as the default startup kernel.
   
            ```Bash
            grub2-set-default "CentOS Linux (4.9.324) 7 (Core)"
            ```
            
   
         3. View the default startup kernel.
   
            ```Bash
            grub2-editenv list 
            ```
            
   
            Sample output:
   
            ```Plain Text
            saved_entry=CentOS Linux (4.9.324) 7 (Core)
            ```
            
   
         4. Restart the instance.
   
            ```Bash
            reboot
            ```
            
   
         5. After the instance is restarted, view the current operating system kernel.
   
            ```Bash
            uname -r 
            ```
            
   
            Sample output:
   
            ```Plain Text
            4.9.324
            ```
            
   
   2. After the instance is switched to the LTS\-kernel, install the LTS\-Virtio1.1 driver.
   
      1. Install the required dkms package tool.
   
         * Installation on a platform instance.
   
            ```Bash
            yum -y install rpm-build redhat-lsb-core
            yum -y install epel-release
            sed -e 's!^metalink=!#metalink=!g' \
                -e 's!^#baseurl=!baseurl=!g' \
                -e 's!//download\.fedoraproject\.org/pub!//mirrors.ivolces.com!g' \
                -i /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel-testing.repo
            yum -y install --enablerepo=epel dkms
            ```
            
   
         * Installation on a non\-platform instance.
   
            ```Bash
            yum -y install rpm-build redhat-lsb-core
            yum -y install epel-release
            sed -e 's!^metalink=!#metalink=!g' \
                -e 's!^#baseurl=!baseurl=!g' \
                -e 's!//download\.fedoraproject\.org/pub!//mirrors.volces.com!g' \
                -i /etc/yum.repos.d/epel.repo /etc/yum.repos.d/epel-testing.repo
            yum -y install --enablerepo=epel dkms
            ```
            
   
      2. Execute the following commands in sequence to install the LTS\-Virtio1.1 driver.
   
         ```Bash
         wget https://virtio11-drivers.tos-cn-beijing.volces.com/virtio-1.1.0.dkms.tar.gz
         dkms ldtarball virtio-1.1.0.dkms.tar.gz
         dkms build virtio/1.1.0
         dkms install virtio/1.1.0
         ```
         
   
   3. For CentOS 7/8 operating system, add kernel startup parameters.
   
      ```Bash
      sed -i 's/\(^GRUB_CMDLINE_LINUX=.*\)"/\1 pci=realloc intel_idle.max_cstate=1 processor.max_cstate=1 iommu=pt"/g' /etc/default/grub
      grub2-mkconfig -o /boot/efi/EFI/centos/grub.cfg
      dracut --force /boot/initramfs-$(uname -r).img $(uname -r)
      ```
      
   
   
   </Tab>
   <Tab zoneid="m1LpTbxLGj" title="Debian 9/10">
   <TabTitle>Debian 9/10</TabTitle>
   
   1. Install the LTS\-kernel.
   
      1. Execute the following commands in sequence to install the LTS\-kernel.
   
         * LTS\-4.9 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.9.324_4.9.324-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.9.324_4.9.324-1_amd64.deb
            apt install -y ./linux*4.9*.deb
            ```
            
   
         * LTS\-4.14 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.14.289_4.14.289-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.14.289_4.14.289-1_amd64.deb
            apt install -y ./linux*4.14*.deb
            ```
            
   
         * LTS\-4.19 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.19.253_4.19.253-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.19.253_4.19.253-1_amd64.deb
            apt install -y ./linux*4.19*.deb
            ```
            
   
   2. Execute the following commands in sequence to switch kernels and restart the instance. This way, the instance runs with the specified LTS\-kernel version. In this example, LTS\-4.9 is used.
   
      1. View the number of kernels currently on the system.
   
         ```Bash
         cat /boot/grub/grub.cfg | grep menuentry
         ```
         
   
         Sample output:
   
         ```Plain Text
         if [ x"${feature_menuentry_id}" = xy ]; then
            menuentry_id_option="--id"
            menuentry_id_option=""
         export menuentry_id_option
         menuentry 'Debian GNU/Linux' --class debian --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-8b9ce818-459e-4024-83f6-a5165ae179f2' {
         submenu 'Advanced options for Debian GNU/Linux' $menuentry_id_option 'gnulinux-advanced-8b9ce818-459e-4024-83f6-a5165ae179f2' {
         menuentry 'Debian GNU/Linux, with Linux 4.19.0-18-amd64' --class debian --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-4.19.0-18-amd64-advanced-8b9ce818-459e-4024-83f6-a5165ae179f2' {
         menuentry 'Debian GNU/Linux, with Linux 4.9.324' --class debian --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-4.9.324-advanced-8b9ce818-459e-4024-83f6-a5165ae179f2' {
         menuentry 'System setup' $menuentry_id_option 'uefi-firmware' {
         ```
         
   
      2. Set the default startup kernel.
   
         Specify the "Debian GNU/Linux, with Linux 4.9.324" kernel in the preceding output as the default startup kernel.
   
         ```Bash
         vim /etc/default/grub
         ```
         
   
         Modify `GRUB_DEFAULT=0` in the file:
   
         > `Advanced options for Debian GNU/Linux `is the primary menu, and `Debian GNU/Linux, with Linux 4.9.324` is the secondary menu. The primary menu and secondary menu are separated by `>`.      
         
   
         ```YAML
         GRUB_DEFAULT="Advanced options for Debian GNU/Linux>Debian GNU/Linux, with Linux 4.9.324"
         ```
         
   
      3. Update the GRUB file.
   
         ```Bash
         update-grub
         ```
         
   
      4. Restart the instance.
   
         ```Bash
         reboot
         ```
         
   
      5. After the instance is restarted, view the current operating system kernel.
   
         ```Bash
         uname -r 
         ```
         
   
         Sample output
   
         ```Plain Text
         4.9.324
         ```
         
   
   3. After the instance is switched to the LTS\-kernel, install the LTS\-Virtio1.1 driver.
   
      1. Install the required dkms package tool.
   
         ```Plain Text
         apt install -y dkms fakeroot dh-make
         ```
         
   
      2. Execute the following commands in sequence to install the LTS\-Virtio1.1 driver.
   
         ```Bash
         wget https://virtio11-drivers.tos-cn-beijing.volces.com/virtio-1.1.0.dkms.tar.gz
         dkms ldtarball virtio-1.1.0.dkms.tar.gz
         dkms build virtio/1.1.0
         dkms install virtio/1.1.0
         ```
         
   
   4. Add kernel startup parameters.
   
      ```Bash
      sed -i 's/\(^GRUB_CMDLINE_LINUX=.*\)"/\1 pci=realloc intel_idle.max_cstate=1 processor.max_cstate=1 iommu=pt"/g' /etc/default/grub
      update-grub
      ```
      
   
   
   </Tab>
   <Tab zoneid="XLA1wGOXTC" title="Ubutun Server 16.04/18.04">
   <TabTitle>Ubutun Server 16.04/18.04</TabTitle>
   
   1. Install the LTS\-kernel.
   
      1. Execute the following commands in sequence to install the LTS\-kernel.
   
         * LTS\-4.9 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.9.324_4.9.324-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.9.324_4.9.324-1_amd64.deb
            apt install -y ./linux*4.9*.deb
            ```
            
   
         * LTS\-4.14 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.14.289_4.14.289-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.14.289_4.14.289-1_amd64.deb
            apt install -y ./linux*4.14*.deb
            ```
            
   
         * LTS\-4.19 kernel
   
            ```Bash
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-image-4.19.253_4.19.253-1_amd64.deb
            wget https://virtio11-drivers.tos-cn-beijing.volces.com/lts-deb/linux-headers-4.19.253_4.19.253-1_amd64.deb
            apt install -y ./linux*4.19*.deb
            ```
            
   
      2. Execute the following commands in sequence to switch kernels and restart the instance. This way, the instance runs with the specified LTS\-kernel version. In this example, LTS\-4.9 is used.
   
         1. View the number of kernels currently on the system.
   
            ```Bash
            cat /boot/grub/grub.cfg | grep menuentry
            ```
            
   
            Sample output:
   
            ```Plain Text
            if [ x"${feature_menuentry_id}" = xy ]; then
               menuentry_id_option="--id"
               menuentry_id_option=""
            export menuentry_id_option
            menuentry 'Ubuntu' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-simple-832b0bb8-00f9-41b6-9d0d-8387e07a4f8c' {
            submenu 'Advanced options for Ubuntu' $menuentry_id_option 'gnulinux-advanced-832b0bb8-00f9-41b6-9d0d-8387e07a4f8c' {
            menuentry 'Ubuntu, with Linux 4.15.0-174-generic' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-4.15.0-174-generic-advanced-832b0bb8-00f9-41b6-9d0d-8387e07a4f8c' {
            menuentry 'Ubuntu, with Linux 4.9.324' --class ubuntu --class gnu-linux --class gnu --class os $menuentry_id_option 'gnulinux-4.9.324-advanced-832b0bb8-00f9-41b6-9d0d-8387e07a4f8c' {
            menuentry 'System setup' $menuentry_id_option 'uefi-firmware' {
            ```
            
   
         2. Set the default startup kernel.
   
   
   Specify the `Ubuntu, with Linux 4.9.324` kernel in the preceding output as the default startup kernel.
   
   
   ```Bash
   vim /etc/default/grub
   ```
   
   
            Modify `GRUB_DEFAULT=0` in the file:
   
            `Advanced options for Ubuntu` is the primary menu, and `Ubuntu, with Linux 4.9.324` is the secondary menu. The primary menu and the secondary menu are separated by \>.
   
            ```YAML
            GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.9.324"
            ```
            
   
         3. Update the GRUB file.
   
            ```Bash
            update-grub
            ```
            
   
         4. Restart the instance.
   
            ```Bash
            reboot
            ```
            
   
         5. After the instance is restarted, view the current operating system kernel.
   
            ```Bash
            uname -r 
            ```
            
   
            Sample output:
   
            ```Plain Text
            4.9.324
            ```
            
   
   2. After the instance is switched to the LTS\-kernel, install the LTS\-Virtio1.1 driver.
   
      1. Install the required dkms package tool.
   
         ```Bash
         apt install -y dkms fakeroot dh-make
         ```
         
   
      2. Execute the following commands in sequence to install the LTS\-Virtio1.1 driver.
   
         ```Plain Text
         wget https://virtio11-drivers.tos-cn-beijing.volces.com/virtio-1.1.0.dkms.tar.gz
         dkms ldtarball virtio-1.1.0.dkms.tar.gz
         dkms build virtio/1.1.0
         dkms install virtio/1.1.0
         ```
         
   
   3. Add kernel startup parameters.
   
      ```Plain Text
      sed -i 's/\(^GRUB_CMDLINE_LINUX=.*\)"/\1 pci=realloc intel_idle.max_cstate=1 processor.max_cstate=1 iommu=pt"/g' /etc/default/grub
      update-grub
      ```
      
   
   
   </Tab>
   </Tabs>
   


<span id=".5a6J6KOFTUxOWOmpseWKqO-8iOWPr-mAie-8iQ=="></span>
### Install the MLNX driver (optional).

If you want to use the network interface Offload feature, install the MLNX driver on the virtual machine. For more information, see [Linux Drivers](https://network.nvidia.com/products/infiniband-drivers/linux/mlnx_ofed/).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you want to use a type that supports the network interface Offload feature, install the MLNX driver.</div>


<span id=".56ys5YWt5q2l77ya5Zyo6Jma5ouf5py65Lit5a6J6KOF5o-S5Lu2"></span>
## Step 6: Install plugins on the virtual machine


* **Password plugin**

   To reset, associate, and disassociate passwords, you must install the password plugin for the custom image you create. Otherwise, the image may not work as expected. For more information, see [Installing the password plugin](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in).

   
   If you want to access metadata in security hardening mode, install the password plugin in security hardening mode. For information about how to view metadata and the available metadata items, refer to [Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata).
   
   
   <Tabs>
   <Tab zoneid="V6iXz6XpPl" title="veLinux, Ubuntu, and Debian series">
   <TabTitle>veLinux, Ubuntu, and Debian series</TabTitle>
   
   1. Execute the following command to download the installation package for the password plugin that supports security hardening mode.
   
      ```Plain Text
      wget https://reset-authentication.tos-ap-southeast-1.bytepluses.com/hardening_mode/reset-authentication_1.0.13-0_amd64.deb
      ```
      
   
   2. Execute the following command to install the plugin.
   
      ```Plain Text
      dpkg -i reset-authentication_1.0.13-0_amd64.deb
      ```
      
   
   3. Execute the following command. If "active" is displayed in the output, the plugin is successfully installed.
   
      ```Plain Text
      systemctl is-active reset-authentication.service
      ```
      
   
   
   
   
   
   </Tab>
   <Tab zoneid="ocBmEqk98t" title="OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series">
   <TabTitle>OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series</TabTitle>
   
   1. Execute the following command to download the installation package for the password plugin that supports security hardening mode.
   
      ```Plain Text
      wget https://reset-authentication.tos-ap-southeast-1.bytepluses.com/hardening_mode/reset-authentication-1.0.13-0.x86_64.rpm
      ```
      
   
   2. Execute the following command to install the plugin.
   
      ```Plain Text
      rpm -i reset-authentication-1.0.13-0.x86_64.rpm
      ```
      
   
   3. Execute the following command to start the service.
   
      ```Plain Text
      systemctl start reset-authentication.service
      systemctl enable reset-authentication.service
      ```
      
   
   4. Execute the following command. If "active" is displayed in the output, the plug\-in is successfully installed.
   
      ```Plain Text
      systemctl is-active reset-authentication.service
      ```
      
   
   
   
   
   
   </Tab>
   </Tabs>
   
   

* **Cloud Monitor plugin**

   If monitoring from within the instance is required to gain deeper and more accurate insights into the status of the instance, you can also install the Cloud Monitor plugin for the custom image. For information about how to install the plugin, see [Installing an agent](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent).

* **blk\-none**

   To prevent I/O issues that occur when you decompress large packages within an instance, the platform provides the blk\-none tool. This tool sets the disk scheduling algorithm to none or noop based on the instance disk type to prevent such issues. For more information, see [Solution](https://docs.byteplus.com/en/docs/ecs/blk-none#.6Kej5Yaz5pa55qGI).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you want to create a CentOS 7.x, Ubuntu 16.04, Ubuntu 18.04, or Debian 9 image and use the image to create General\-purpose (g3a/g3i), Compute\-optimized (c3a/c3i), or Memory\-optimized (r3a/r3i) instances, you must install this tool.   </div>
   

<span id=".56ys5LiD5q2l77ya5Zyo6Jma5ouf5py65Lit5a6J6KOF5Liq5oCn5YyW6L2v5Lu277yI5Y-v6YCJ77yJ"></span>
## Step 7: Install software on the virtual machine (optional)

You can install software on the system volume based on your business requirements. For example, you can install JDK and the Linux graphical desktop.

<span id=".56ys5YWr5q2l77ya5qOA5rWL6ZWc5YOP6KeE6IyD"></span>
## Step 8: Detect image specifications

You can execute the custom image specification detection tool in the virtual machine to check whether the current operating system configurations meet the requirements for creating ECS instances. This ensures that instances created by using a custom image work as expected. For more information, see [Using tool to check custom image specifications](https://docs.byteplus.com/en/docs/ecs/verify-custom-images).

<span id=".56ys5Lmd5q2l77ya5a-85Ye66ZWc5YOP"></span>
## Step 9: Import an image


1. In the top menu bar of the virtual machine page, click "Virtual Machine \> Shut Down \> Shut Down" to shut down the virtual machine.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f32ba9f1793fb007b37a3d32951e6f2d.png) </span>

2. Execute the following command on the host machine to open the folder that stores images. You can view the image files created for your virtual machine based on the name of your virtual machine.

   ```Bash
   xdg-open /var/lib/libvirt/images/
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_58e3b9e10d04e196eff77d55e6d1db2c.png) </span>


<span id=".56ys5Y2B5q2l77ya6L2s5o2i6ZWc5YOP5qC85byP"></span>
## Step 10: Convert image format

Currently, only QCOW2, RAW, VHD, VMDK image formats are supported. Otherwise, you need to convert the image format first. [Learn more](https://docs.byteplus.com/en/docs/ecs/Converting-image-file-formats).

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

You can upload the created image file to the platform as a custom image. After the image file is uploaded, you can use this image to create an instance. For more information, see [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).
