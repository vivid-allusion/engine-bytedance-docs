---
title: "Upgrading reset-authentication plug-in"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Updating-the-password-plug-in"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

Before you [change the hostname of an instance](https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance), you need to follow the instructions in this topic to upgrade the reset\-authentication plug\-in to the specified version.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".TGludXjplZzlg48="></span>
### Linux images

Refer to the following instructions to upgrade the reset\-authentication plug\-in based on your Linux distribution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Instances created using CentOS 6.9/6.10 or Ubuntu 14.04 do not support hostname changes.</div>


* <div data-tips="true" data-tips-type="tip">For an instance in the China (Beijing) region, if an EIP is not associated with the instance, you can use the private domain name to download the reset\-authentication plug\-in. For an instance in other regions, <a href="https://docs.byteplus.com/en/docs/ecs/associating-an-EIP">associate an EIP with the instance</a>, and then use the public domain name to download the reset\-authentication plug\-in.</div>




<Tabs>
<Tab zoneid="WxAo7l0u5I" title="Ubuntu, Debian, and veLinux series">
<TabTitle>Ubuntu, Debian, and veLinux series</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check whether the reset\-authentication plug\-in is installed.

   ```Bash
   dpkg -s reset-authentication
   ```
   

   * If the following output is displayed, the 1.0.4 version of the reset\-authentication plug\-in has been installed. Proceed to Step 3.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30a1c7df8e44464df019fc066bfd7594.png) </span>

   * If the following output is displayed, the plug\-in is not installed. Proceed to Step 4.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_15ea0b2eac28a3d7ab13e00738bbcf21.png) </span>

3. Execute the following command to uninstall the old version of the reset\-authentication plug\-in.

   ```Bash
   dpkg -r reset-authentication
   ```
   

4. Execute the following command to download the latest version of the plug\-in.

   * Download over the Internet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication_1.0.11-0_amd64.deb
      ```
      

   * Download over the intranet

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only the China (Beijing) region supports this feature.      </div>
      

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.ivolces.com/reset-authentication_1.0.11-0_amd64.deb
      ```
      

5. Execute the following command to install the latest version of the plug\-in.

   ```Bash
   dpkg -i reset-authentication_1.0.11-0_amd64.deb
   ```
   

6. Verify the result.

   * Execute the following command. If "active" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-active reset-authentication.service
      ```
      

   * Execute the following command. If "enabled" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-enabled reset-authentication.service
      ```
      




</Tab>
<Tab zoneid="gjT5zbpefb" title="OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series">
<TabTitle>OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to check whether the reset\-authentication plug\-in is installed.

   ```Bash
   rpm -q reset-authentication
   ```
   

   * If the following output is displayed, the 1.0.4 version of the reset\-authentication plug\-in has been installed. Proceed to Step 3.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_11aceb293bd39f378c71cc7208a94543.png) </span>

   * If the following output is displayed, the plug\-in is not installed. Proceed to Step 4.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_79096c0168f7c4b3c34b8a4799f22b6a.png) </span>

3. Execute the following command to uninstall the old version of the reset\-authentication plug\-in.

   ```Bash
   rpm -e reset-authentication
   ```
   

4. Execute the following command to download the latest version of the plug\-in.

   * Download over the Internet

      ```Bash
      wget http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication-1.0.11-0.x86_64.rpm
      ```
      

   * Download over the intranet

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only the China (Beijing) region supports this feature.      </div>
      

      ```Bash
      wget http://volc-ecs.tos-s3-cn-beijing.ivolces.com/reset-authentication-1.0.11-0.x86_64.rpm
      ```
      

5. Execute the following command to install the latest version of the plug\-in.

   ```Bash
   rpm -i reset-authentication-1.0.11-0.x86_64.rpm
   ```
   

6. Verify the result.

   * Execute the following command. If "active" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-active reset-authentication.service
      ```
      

   * Execute the following command. If "enabled" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-enabled reset-authentication.service
      ```
      




</Tab>
</Tabs>


<span id=".V2luZG93c-mVnOWDjw=="></span>
### Windows images


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Check whether the reset\-authentication plug\-in is installed.

   Check whether the `C:\Program Files\Reset Authentication` directory exists and whether there are any files and a log folder in the directory, open the log file, and view the version.

   * If the preceding files exist, an older version of the plug\-in has been installed (as shown in the following figure). You can re\-download the new plug\-in and execute the following command to start the reset\-authentication plug\-in.

      `"C:\Program Files\Reset Authentication\reset-authentication.exe"`

   * If the preceding files do not exist, the reset\-authentication plug\-in is not installed. Proceed to Step 3.

3. Download and install the latest version of the plug\-in.

   1. Create the `C:\Program Files\Reset Authentication` directory.

   2. On the desktop of the ECS instance, click "Start \> Windows PowerShell" to open PowerShell.

   3. Execute the following commands in PowerShell to download the ps1 auto\-start script and the reset\-authentication plug\-in, and save them to the specific directories.

      * ps1 auto\-start script

         ```PowerShell
         wget -Uri "http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication.ps1" -OutFile "C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\reset-authentication.ps1"
         ```
         

      * Reset\-authentication plug\-in

         ```PowerShell
         wget -Uri "http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication.exe" -OutFile "C:\Program Files\Reset Authentication\reset-authentication.exe"
         ```
         

4. In PowerShell, execute the following commands in sequence to perform initialization operations.

   1. Execute the following command to obtain the instance UUID.

      ```Bash
      $instance_id = ((Invoke-WebRequest -URI "http://100.96.0.96/openstack/latest/meta_data.json" -UseBasicParsing).Content | ConvertFrom-Json).uuid
      ```
      

   2. Execute the following command to delete part of the Cloudbase\-init registry configuration so that the reset\-authentication plug\-in can work as expected.

      If you have not run Cloudbase\-init, you do not need to execute this command.

      ```PowerShell
      Remove-ItemProperty "HKLM:\SOFTWARE\Cloudbase Solutions\Cloudbase-Init\$instance_id\Plugins" LocalScriptsPlugin
      ```
      

   3. Execute the following command to start the reset\-authentication plug\-in.

      ```PowerShell
      "C:\Program Files\Reset Authentication\reset-authentication.exe"
      ```
