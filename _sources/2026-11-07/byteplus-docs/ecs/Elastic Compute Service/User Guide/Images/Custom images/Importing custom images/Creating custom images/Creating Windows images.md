---
title: "Creating Windows images"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating-Windows-images"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If you have an image with the required applications pre\-installed, you can use virt\-install to create a QCOW2 image and import the QCOW2 image to the platform as a private image by referring to this topic.

This method allows you to create custom system images based on your business requirements and is applicable to scenarios in which complex initialization operations are required to create system images. After you import an image to the platform, you can use the image to deploy a system without performing complex initialization operations or deploy multiple ECS instances with the same configurations.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The following 32\-bit and 64\-bit base image operating systems and relevant versions are supported for the method described in this topic.


* Windows Server 2012

* Windows Server 2016

* Windows Server 2019


<span id=".56ys5LiA5q2l77ya5a6_5Li75py6546v5aKD5YeG5aSH"></span>
## Step 1: Prepare the host machine environment


1. Configure the host machine.

   1. Prepare a physical server running Linux to serve as the host machine for image creation.

      > There is no strict requirement for the distribution of the operating system running on the host machine. In this topic, CentOS 8.3 is used as an example.      
      

   2. Log in to the host machine.

   3. Execute the following command to check whether the virtualization capability is enabled for the host machine.

      ```Plain Text
      lscpu | grep vmx
      ```
      

   4. Execute the following command to check whether the kernel version of the host machine is higher than 3.10.

      ```Plain Text
      uname -r
      ```
      

2. Execute the following commands in sequence to install the virtualization software.

   ```Plain Text
   sudo yum install qemu-kvm 
   sudo yum install libvirt
   sudo yum install virt-install
   sudo yum install virt-manager
   ```
   

3. Load virtualization\-related services.

   1. Execute the following command to enable the libvirtd service.

      ```Plain Text
      systemctl restart libvirtd.service
      ```
      

   2. Execute the following command to check whether the virbr0 network interface is created.

      ```Plain Text
      ip link show virbr0
      ```
      

   3. Execute the following command to load kvm.

      ```Plain Text
      modprobe kvm
      modprobe kvm-intel
      ```
      


<span id=".56ys5LqM5q2l77ya5Zyo5a6_5Li75py65LiK5Yib5bu66Jma5ouf5py6"></span>
## Step 2: Create a virtual machine on the host machine


1. Upload the base image.

   * Upload the base image file you need to the `/home` folder of the host machine. We recommend that you use the official image.

   * If both QCOW2 and ISO image formats are available, we recommend that you select the image in QCOW2.

2. Create a virtual machine.

   Assume that the names of the uploaded base image files are windows\-2019\-x64.qcow2 and windows\-2019\-x64.iso.

   * When the base image is in QCOW2 format, execute the following command to create a virtual machine.

      * Replace the parameter next to `--os-variant` with the operating system type of the virtual machine. You can execute the `osinfo-query` command to view the available types.

      * Replace the parameter next to `--disk=` with the storage location of the virtual machine operating system, that is, the path to the base image.

      * Replace the port number next to `--graphics vnc,port=` with the VNC port you use.

         > Some operators consider port `5900 risky` and block the port by default. We recommend that you do not use the port.         
         

         ```Plain Text
         virt-install --name bp-tob-windows-2019-x64 --connect qemu:///system --os-variant windows2019 --virt-type kvm --memory 2048 --vcpus 2 --disk=/home/windows-2019-x64.qcow2 --boot=hd --network default --graphics vnc,port=6000,listen=0.0.0.0 --noautoconsole
         ```
         

   * When the base image is in ISO format, execute the following command.

      1. Execute the following command to create a QCOW2 image with a size of 20 GB.

         ```Plain Text
         qemu-img create -f qcow2 /home/windows-2019-x64.qcow2 20G
         ```
         

      2. Execute the following command to create a virtual machine based on the base image.

         * Replace the parameter next to `--os-variant` with the operating system type of the virtual machine. You can execute the `osinfo-query` command to view available types.

         * Replace the parameter next to `--disk=` with the storage location of the virtual machine operating system, that is, the path to the new image.

         * Replace the parameter next to `--cdrom=` with the path to the base image.

         * Replace the port number next to `--graphics vnc,port=` with the VNC port you use.

            > Some operators consider port `5900 risky` and block the port by default. We recommend that you do not use the port.            
            

            ```Plain Text
            virt-install --name bp-tob-windows-2019-x64 --connect qemu:///system --os-variant windows2019 --virt-type kvm --memory 2048 --vcpus 2 --disk=/home/windows-2019-x64.qcow2,format=qcow2,bus=virtio --cdrom=/home/windows-2019-x64.iso --boot=hd --network default --graphics vnc,port=6000,listen=0.0.0.0 --noautoconsole
            ```
            

3. Execute the following command to check whether the virtual machine is created and view the VNC address.

   > Replace port `6000` in the command with the actual port number.   
   

   ```Plain Text
   virsh list bp-tob-windows-2019-x64
   netstat -lntp | grep 6000
   ```
   

4. Enter "vnc address:vnc port number" on VNC Viewer to remotely log in to the virtual machine.

5. Check the OS virtio driver. Make sure that the image supports full virtualization and that the virtio\-net driver (network) and the virtio\-blk driver (disk) are installed.

   Open the CMD command prompt and execute the `driverquery` command to locate the network interface driver (netkvm) and disk driver (viostor) in the list. The driver time may vary depending on the driver version.

   * Network interface driver

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/e8fa0ca29f5841058bc71550ec1dd06f.png) </span>

   * Disk driver

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/a5f6a0f2bf764cf8a2eeae639fd91d89.png) </span>


<span id=".56ys5LiJ5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFQ2xvdWRiYXNlLWluaXQ="></span>
## Step 3: Install Cloudbase\-init on the virtual machine


1. Download the Cloudbase\-init installer.

   * [64-bit operating system](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x64.msi)

   * [32-bit operating system](https://www.cloudbase.it/downloads/CloudbaseInitSetup_Stable_x86.msi)

2. Open the installation package to start the installation and click the "Next" button.

3. Select "I accept the terms in the License Agreement", and click the "Next" button.

4. You can select the Cloudbase\-init installation path based on your business requirements (optional), and click the "Next" button.

5. Set Username to `Administrator`, set Serial port for logging to `COM1`, and select `Run Cloudbase-init service as LocalSystem`. Click the "Next" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_192e23edcc0347b54d5bc68a48c611cc.png) </span>

6. Click the "Install" button to install Cloudbase\-init.

7. After Cloudbase\-init is installed, click the "Finish" button to close the installation page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When you close the Cloudbase\-init installation page, do not select any check boxes and do not run Sysprep.   </div>
   

8. Modify the Cloudbase\-init configuration file. Make the following changes. The default path for Cloudbase\-init is C:\Program Files\Cloudbase Solutions\Cloudbase\-Init\conf\cloudbase\-init.conf.

   * If Cloudbase\-init is not in the default path, find Cloudbase\-init in the installation path you specified in step 4.

      ```Plain Text
      [DEFAULT]
      username=Administrator
      groups=Administrators
      inject_user_password=true
      config_drive_raw_hhd=true
      config_drive_cdrom=true
      config_drive_vfat=true
      metadata_services=cloudbaseinit.metadata.services.httpservice.HttpService
      metadata_base_url=http://100.96.0.96/
      verbose=true
      debug=true
      log_dir=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\log\
      log_file=cloudbase-init.log
      default_log_levels=comtypes=INFO,suds=INFO,iso8601=WARN,requests=WARN
      logging_serial_port_settings=
      mtu_use_dhcp_config=true
      ntp_use_dhcp_config=true
      check_latest_version=true
      first_logon_behaviour=no
      local_scripts_path=C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\
      ```
      

   * To log in to an ECS instance by using the password preset by using Cloudbase\-init, add the following content to the configuration file. After you complete the configurations, enable instance login based on the preset password in the image. For information about how to enable the feature, see "Custom configurations \> Login methods \> Login credentials" in [Purchasing instances by following wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

      ```Plain Text
      plugins=cloudbaseinit.plugins.common.mtu.MTUPlugin,cloudbaseinit.plugins.windows.ntpclient.NTPClientPlugin,cloudbaseinit.plugins.common.sethostname.SetHostNamePlugin,cloudbaseinit.plugins.common.networkconfig.NetworkConfigPlugin,cloudbaseinit.plugins.windows.licensing.WindowsLicensingPlugin,cloudbaseinit.plugins.common.sshpublickeys.SetUserSSHPublicKeysPlugin,cloudbaseinit.plugins.windows.extendvolumes.ExtendVolumesPlugin,cloudbaseinit.plugins.common.userdata.UserDataPlugin,cloudbaseinit.plugins.common.setuserpassword.SetUserPasswordPlugin,cloudbaseinit.plugins.windows.winrmlistener.ConfigWinRMListenerPlugin,cloudbaseinit.plugins.windows.winrmcertificateauth.ConfigWinRMCertificateAuthPlugin,cloudbaseinit.plugins.common.localscripts.LocalScriptsPlugin
      ```
      

9. Modify the DHCP settings of the network interface

   1. Click "Start \> Control Panel \> Network and Internet".

   2. Click the network connection as shown in the following figure.

   3. Click the "Properties" button, and then double\-click the "Internet Protocol Version 4 (TCP/IPv4)" button to open the property configuration window.

   4. Select "Obtain an IP address automatically" and "Obtain DNS server address automatically". Then click the "OK" button.

10.  **(Optional)**  If you want to use the network interface Offload feature, install the MLNX driver on the virtual machine. For more information, see [MLNX_OFED for Windows - WinOF / WinOF-2](https://www.mellanox.com/products/adapter-software/ethernet/windows/winof-2).

11.  **(Optional)**  If you want to access metadata in security hardening mode, you also need to modify the Cloudbase\-init configuration by using the following script. For information about how to view metadata and the available metadata items, refer to [Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata).

   1. Execute the following command in PowerShell to create and open a configuration script. In this topic, a script file named config.ps1 is created on the desktop.

      ```PowerShell
      notepad.exe .\Desktop\config.ps1
      ```
      

   2. Click the "Yes" button to confirm the creation of a new file.

   3. Copy the following content to the script file.

      ```PowerShell
      $Script:volc_log_path = "c:\volc.log"
      $Script:service_name = "cloudbase-init"
      $Script:cloudbase_init_folder_path = "c:\cloudbase_init_1_0_0_3"
      $Script:cloudbase_init_path = "C:\ecs.windows.cloudbase_init_1.0.0.3.tar.gz"
      if (Test-Path -Path $Script:volc_log_path) {
          Remove-Item -Path $Script:volc_log_path -Recurse -Force
      }
      if (Test-Path -Path $Script:cloudbase_init_folder_path) {
          Remove-Item -Path $Script:cloudbase_init_folder_path -Recurse -Force
      }
      if (Test-Path -Path $Script:cloudbase_init_path) {
          Remove-Item -Path $Script:volc_log_path -Recurse -Force
      }
      echo "Modify cloudbase-init service begin."  >> $Script:volc_log_path
      Get-Service -DisplayName $Script:service_name
      if ($?) {
          echo "Current system installed service:$Script:service_name, continue." >> $Script:volc_log_path
      } else {
          echo "Current system didn't install service:$Script:service_name, exit." >> $Script:volc_log_path
          exit 1001
      }
      New-Item -Path "C:\" -Name "cloudbase_init_1_0_0_3" -type directory
      Invoke-WebRequest -Uri https://cloudbase-init-ap-southeast-1.tos-ap-southeast-1.bytepluses.com/hardening_mode/ecs.windows.cloudbase_init_1.0.0.3.tar.gz -OutFile $Script:cloudbase_init_path
      tar -xzf C:\ecs.windows.cloudbase_init_1.0.0.3.tar.gz -C $Script:cloudbase_init_folder_path
      cmd.exe /c "C:\cloudbase_init_1_0_0_3\config-cloudbase-init.bat" -NoNewWindow >> $Script:volc_log_path
      Set-Service -Name $Script:service_name -StartupType Automatic
      echo "Query service's running state after modify."
      Get-Service $Script:service_name | Select-Object -Property Name, StartType, Status >> $Script:volc_log_path
      Remove-Item -Path $Script:cloudbase_init_folder_path -Recurse -Force >> $Script:volc_log_path
      Remove-Item -Path $Script:cloudbase_init_path -Recurse -Force >> $Script:volc_log_path
      echo "Modify cloudbase-init service end."  >> $Script:volc_log_path
      exit 0
      ```
      

   4. Press `Control + S` to save the changes, and then close the file.

   5. Right\-click the script file, and select "Run with PowerShell".

   6. If an execution policy change prompt appears, enter `A` and press Enter to confirm.


<span id=".56ys5LqU5q2l77ya5Zyo6Jma5ouf5py65LiK5a6J6KOFVmlydGlv6amx5Yqo"></span>
## Step 4: Install the Virtio driver on the virtual machine


1. Click "Start \> Control Panel".

2. On the Control Panel page, click the "Programs" button.

3. Click the "Programs and Features" button to go to the Programs and Features page.

4. In the search box in the upper right corner, search for `Virtio` to check whether the Virtio driver is installed on the virtual machine.

   * If the Virtio driver is installed on the virtual machine, skip this step.

   * If the Virtio driver is not installed on the virtual machine, install the Virtio driver by following the instructions in this step.

      
      <Tabs>
      <Tab zoneid="aMQXGSOsp6" title="Windows Server 2016 and later versions">
      <TabTitle>Windows Server 2016 and later versions</TabTitle>
      
      1. In PowerShell, execute the following command to download the Virtio driver installer.
      
         ```PowerShell
         Invoke-WebRequest -Uri 'https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.266-1/virtio-win-gt-x64.msi' -OutFile 'virtio-win-gt-x64.msi'
         ```
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also <a href="https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.266-1/virtio-win-gt-x64.msi">click here</a> to download the driver installer in the browser.   </div>
         
      
      2. Execute the following command in PowerShell to start the driver installation process.
      
         ```PowerShell
         msiexec /i <Installer folder>\virtio-win-gt-x64.msi
         ```
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you download the driver installer by using your browser, you can also double\-click the downloaded .msi file to start the driver installation process.   </div>
         
      
      3. Click the "Next" button to continue the installation process.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_faf3dbc0a1bea973714aad1d2ab62c39.png) </span>
      
      4. Select "I accept the terms in the License Agreement" and click the "Next" button.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53af10bb2bb850753ed06706f455e491.png) </span>
      
      5. After you confirm the features to be installed, click the "Next" button.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb867b1e4320d7b9646073f7ae83d276.png) </span>
      
      6. Click the "Install" button and confirm the installation options to start installing the Virtio driver.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9ad6d68f1a5aecb50b61d3fdef7ca9c.png) </span>
      
      7. Click the "Finish" button to complete the Virtio driver installation.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbeacdbce6723332d16695c04c1559b4.png) </span>
      
      
      </Tab>
      <Tab zoneid="SwcgtPsHsN" title="Windows Server 2012R2">
      <TabTitle>Windows Server 2012R2</TabTitle>
      
      1. In PowerShell, execute the following command to download the Virtio driver installer.
      
         ```PowerShell
         Invoke-WebRequest -Uri 'https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.215-2/virtio-win-gt-x64.msi' -OutFile 'virtio-win-gt-x64.msi'
         ```
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If PowerShell reports the "The request was aborted: Could not create SSL/TLS secure channel" error, execute the following commands before you download the Virtio driver installer again.   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Ssl3 -bor [Net.SecurityProtocolType]::Tls -bor [Net.SecurityProtocolType]::Tls11 -bor [Net.SecurityProtocolType]::Tls12</code>   </div>
         
      
         * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can also <a href="https://fedorapeople.org/groups/virt/virtio-win/direct-downloads/archive-virtio/virtio-win-0.1.215-2/virtio-win-gt-x64.msi">click here</a> to download the driver installer in the browser.   </div>
         
      
      2. Execute the following command in PowerShell to start the driver installation process.
      
         ```PowerShell
         msiexec /i <Installer folder>\virtio-win-gt-x64.msi
         ```
         
      
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
         
      
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you download the driver installer by using your browser, you can also double\-click the downloaded .msi file to start the driver installation process.   </div>
         
      
      3. Click the "Next" button to continue the installation process.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_faf3dbc0a1bea973714aad1d2ab62c39.png) </span>
      
      4. Select "I accept the terms in the License Agreement" and click the "Next" button.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_53af10bb2bb850753ed06706f455e491.png) </span>
      
      5. After you confirm the features to be installed, click the "Next" button.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fb867b1e4320d7b9646073f7ae83d276.png) </span>
      
      6. Click the "Install" button and confirm the installation options to start installing the Virtio driver.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9ad6d68f1a5aecb50b61d3fdef7ca9c.png) </span>
      
      7. Click the "Finish" button to complete the Virtio driver installation.
      
         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fbeacdbce6723332d16695c04c1559b4.png) </span>
      
      
      </Tab>
      </Tabs>
      


<span id=".56ys5YWt5q2l77ya5a6J6KOF5o-S5Lu2"></span>
## Step 5: Install a plugin


* You can also install the CloudMonitor plugin for custom images. This allows you to monitor an instance from within the instance and obtain deeper, more accurate information about the running status of the instance. For information about how to install the CloudMonitor plugin, see [Installing an agent](https://docs.byteplus.com/en/docs/cloudmonitor/Installing-an-agent).

* If you want to use the [offline password reset](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords#.5pa55byP5LqM77ya56a757q_6YeN572u5a6e5L6L5a-G56CB) feature, [install the password plugin](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in).

   
   If you want to access metadata in security hardening mode, refer to the following steps to install the password plugin. For information about how to view metadata and the available metadata items, refer to [Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata).
   
   
   1. Create the `C:\Program Files\Reset Authentication` directory.
   
   2. Click "Start \> Windows PowerShell" to open PowerShell.
   
   3. Execute the following commands in PowerShell to download the ps1 auto\-start script and the password plugin, and save them to the specific directories.
   
      * ps1 auto\-start script
   
         ```PowerShell
         wget -Uri "http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication.ps1" -OutFile "C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\reset-authentication.ps1"
         ```
         
   
      * Reset\-authentication plug\-in
   
         ```PowerShell
         wget -Uri "https://reset-authentication.tos-ap-southeast-1.bytepluses.com/hardening_mode/reset-authentication-1.0.13-x86_64.exe" -OutFile "C:\Program Files\Reset Authentication\reset-authentication.exe"
         ```
         
   
   4. In PowerShell, execute the following commands in sequence to perform initialization operations.
   
      1. Execute the following command to obtain the instance UUID.
   
         ```Bash
         $instance_id = ((Invoke-WebRequest -URI "http://100.96.0.96/openstack/latest/meta_data.json" -UseBasicParsing).Content | ConvertFrom-Json).uuid
         ```
         
   
      2. Execute the following command to delete part of the Cloudbase\-init registry configuration so that the reset\-authentication plug\-in can work as expected.
   
         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">If you have not run Cloudbase\-init, you do not need to execute this command.      </div>
         
   
         ```PowerShell
         Remove-ItemProperty "HKLM:\SOFTWARE\Cloudbase Solutions\Cloudbase-Init\$instance_id\Plugins" LocalScriptsPlugin
         ```
         
   
      3. Execute the following command to start the reset\-authentication plug\-in.
   
         ```PowerShell
         "C:\Program Files\Reset Authentication\reset-authentication-1.0.13-x86_64.exe"
         ```
         
   
   
   
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For instances not on the BytePlus platform, after you import the custom image and create an instance by using the custom image, install the password plugin on the instance.   </div>
   

<span id=".56ys5LiD5q2l77ya6I635Y-W5r-A5rS76ISa5pys"></span>
## Step 6: Obtain the activation script


1. In PowerShell, execute the following command to download the Windows activation script and save the script to the local directory for Cloudbase\-init scripts.

   ```PowerShell
   Invoke-WebRequest -Uri "https://byteplus-windows-activate.tos-ap-southeast-1.bytepluses.com/windws-activate.ps1" -OutFile "C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\windws-activate.ps1"
   ```
   

2. Make sure that the script files are executable.

   1. Right\-click the script file, and select "Properties".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b06b48ff0ea399c7f03b416f6312e01.png) </span>

   2. On the "General" tab, check whether the "Security" area exists.

      * If the "Security" area does not exist, skip this step.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6922c78c2956232d63af140ee7e430f6.png) </span>

      * If the "Security" area exists, select "Unblock" in the "Security" area, click "Apply", and then click "OK".

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4bb43629f8f9b6afd749d23439e6c833.png) </span>


<span id=".56ys5YWr5q2l77ya5a6J6KOF5Liq5oCn5YyW6L2v5Lu277yI5Y-v6YCJ77yJ"></span>
## Step 7: Install software (optional)

You can install software on the system volume based on your business requirements. For example, you can install JDK and the Linux graphical desktop.

<span id=".56ys5Zub5q2l77ya5omn6KGMU3lzcHJlcA=="></span>
## Step 8: Execute the Sysprep command

You need to use Sysprep to delete specific information from the image so that the image can be used on different devices. For more information, see [Sysprep (system preparation) overview](https://learn.microsoft.com/zh-cn/windows-hardware/manufacture/desktop/sysprep--system-preparation--overview?view=windows-11).


* If you use the public image provided by the platform to create a custom image, execute the following command in the CMD command prompt. For information about the public image versions, see [Image release notes](https://docs.byteplus.com/en/docs/ecs/Image-release-notes).

   ```Plain Text
   reg delete "HKLM\SOFTWARE\Cloudbase Solutions"
   sc config cloudbase-init start= disabled 
   net stop wuauserv
   C:\Windows\System32\Sysprep\sysprep.exe /generalize /shutdown /oobe /quiet "/unattend:C:\Program Files\Cloudbase Solutions\Cloudbase-Init\conf\Unattend.xml"
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you execute the command, the virtual machine enters the generalization process:   </div>
   

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Delete information specific to the virtual machine, including but not limited to the Security Identifier (SID), hostname, and password. Applications and related data are retained.   </div>
   

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Uninstall (but do not delete) drivers specific to the virtual machine.   </div>
   

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the content in the unattended answer file can be added to the existing installation.   </div>
   

   2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After generalization is complete, the virtual machine automatically shuts down.   </div>
   

* If you use the public image not provided by the platform to create a custom image, execute the following command in the CMD command prompt.

   ```Plain Text
   %WINDIR%\system32\sysprep\sysprep.exe /generalize /shutdown /oobe
   ```
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After you execute the command, the virtual machine enters the generalization process:   </div>
   

      1. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Delete information specific to the virtual machine, including but not limited to the Security Identifier (SID), hostname, and password. Applications and related data are retained.   </div>
   

      2. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Uninstall (but do not delete) drivers specific to the virtual machine.   </div>
   

      3. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the virtual machine starts in Out\-of\-Box Experience (OOBE) mode.   </div>
   

      4. <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Specify that the content in the unattended answer file can be added to the existing installation.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After generalization is complete, the virtual machine automatically shuts down.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Cloudbase\-init runs after the OOBE process is complete, the password you create during the OOBE process is overwritten by the login password specified in the configuration file. After you create an ECS instance by using the image, use the login password you create during instance creation, rather than the password created during the OOBE process.   </div>
   


<span id=".56ys5Lmd5q2l77ya5a-85Ye66ZWc5YOP"></span>
## Step 9: Export the image


1. Execute the following command to shut down the virtual machine and obtain the image file.

   ```Plain Text
   virsh shutdown bp-tob-windows-2019-x64
   ```
   

2. Execute the following command to view the image file.

   ```Plain Text
   virt-install --disk
   ```
   


<span id=".56ys5Y2B5q2l77ya6ZWc5YOP5qC85byP6L2s5o2i"></span>
## Step 10: Convert image format

Currently, only QCOW2, RAW, VHD, VMDK image formats are supported. Otherwise, you need to convert the image format first. [Learn more](https://docs.byteplus.com/en/docs/ecs/Converting-image-file-formats).

<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

You can upload the created image file to the platform as a custom image. After the image file is uploaded, you can use this image to create an instance. For more information, see [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1).
