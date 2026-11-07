---
title: "Installing reset-authentication plug-in"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Applicable scenarios

Before you reset the password, associate a key pair with an instance, or disassociate a key pair from an instance, you need to follow the instructions in this topic to install the reset\-authentication plug\-in for the instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Instances created by using a custom image must have the reset\-authentication plug\-in installed. Otherwise, the image may not work as expected.</div>


* <div data-tips="true" data-tips-type="warning">Some images provided by the platform have the reset\-authentication plug\-in pre\-installed. You can <a href="https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance">log in to a Linux instance</a> and execute the following command to check whether the plug\-in is installed:</div>


   <div data-tips="true" data-tips-type="warning"><code>systemctl status reset-authentication</code>   </div>
   

   <div data-tips="true" data-tips-type="warning">If the following output is returned, the plug\-in is not installed. You can refer to this topic for installation instructions.   </div>
   

   <div data-tips="true" data-tips-type="warning"><code>reset-authentication.service could not be found.</code>   </div>
   


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".TGludXjplZzlg48="></span>
### Linux image

Download and install the reset\-authentication plug\-in based on your Linux distribution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For an instance in the China (Beijing) region, if an EIP is not associated with the instance, you can use the private domain name to download the reset\-authentication plug\-in. For an instance in other regions, <a href="https://docs.byteplus.com/en/docs/ecs/associating-an-EIP">associate an EIP with the instance</a>, and then use the public domain name to download the reset\-authentication plug\-in.</div>



<Tabs>
<Tab zoneid="tXkpovxGiI" title="Ubuntu, Debian, and veLinux series">
<TabTitle>Ubuntu, Debian, and veLinux series</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to download the reset\-authentication plug\-in.

   * Download over the Internet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication_1.0.11-0_amd64.deb
      ```
      

   * Download over the intranet

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Only the China (Beijing) region is supported.      </div>
      

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.ivolces.com/reset-authentication_1.0.11-0_amd64.deb
      ```
      

3. Execute the following command to install the reset\-authentication plug\-in.

   ```Plain Text
   dpkg -i reset-authentication_1.0.11-0_amd64.deb
   ```
   

4. Verify the installation result.

   * Execute the following command. If "active" is displayed in the output, the plug\-in is successfully installed.

      ```Plain Text
      systemctl is-active reset-authentication.service
      ```
      

   * Execute the following command. If "enabled" is displayed in the output, the plug\-in is successfully installed.

      ```Plain Text
      systemctl is-enabled reset-authentication.service
      ```
      


</Tab>
<Tab zoneid="VpWlRk1Sqx" title="OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series">
<TabTitle>OpenSUSE, Fedora, CentOS 7/8/Stream, Rocky Linux, and AlmaLinux series</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to download the reset\-authentication plug\-in.

   * Download over the Internet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication-1.0.11-0.x86_64.rpm
      ```
      

   * Download over the intranet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.ivolces.com/reset-authentication-1.0.11-0.x86_64.rpm
      ```
      

3. Execute the following command to install the reset\-authentication plug\-in.

   ```Bash
   rpm -i reset-authentication-1.0.11-0.x86_64.rpm
   ```
   

4. Execute the following command to start the service.

   ```Plain Text
   systemctl start reset-authentication.service
   ```
   

5. Execute the following command to specify that the reset\-authentication plug\-in starts automatically upon startup.

   ```Plain Text
   systemctl enable reset-authentication.service
   ```
   

6. Verify the installation result.

   * Execute the following command. If "active" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-active reset-authentication.service
      ```
      

   * Execute the following command. If "enabled" is displayed in the output, the plug\-in is successfully installed.

      ```Bash
      systemctl is-enabled reset-authentication.service
      ```
      


</Tab>
<Tab zoneid="xQ9GrCFLVT" title="CentOS 6 series">
<TabTitle>CentOS 6 series</TabTitle>

1. [Log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to download the reset\-authentication plug\-in.

   * Download over the Internet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication-1.0.4-el6.x86_64.rpm
      ```
      

   * Download over the intranet

      ```Plain Text
      wget http://volc-ecs.tos-s3-cn-beijing.ivolces.com/reset-authentication-1.0.4-el6.x86_64.rpm
      ```
      

3. Execute the following command to install the reset\-authentication plug\-in.

   ```Bash
   rpm -i reset-authentication-1.0.4-el6.x86_64.rpm
   ```
   

4. Execute the following command to verify the installation result.

   If no error is displayed in the output, the plug\-in is installed successfully.

   ```Plain Text
   service reset-authentication start
   ```
   


</Tab>
</Tabs>


<span id=".V2luZG93c-mVnOWDjw=="></span>
### Windows image

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can install the reset\-authentication plug\-in only on a BytePlus instance.</div>



1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. On the desktop of the ECS instance, click "Start \> Windows PowerShell" to open PowerShell.

3. Execute the following command in PowerShell to download the script and the reset\-authentication plug\-in.

   1. Execute the following command to create the `C:\Program Files\Reset Authentication` folder.

      ```PowerShell
      New-Item -ItemType Directory -Path "C:\Program Files\Reset Authentication"
      ```
      

   2. Execute the following command to enter the `Reset Authentication` folder.

      ```PowerShell
      cd "C:\Program Files\Reset Authentication"
      ```
      

   3. Execute the following command to download the ps1 auto\-start script to the `C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts` folder.

      ```PowerShell
      Invoke-WebRequest -Uri "http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication.ps1" -OutFile "C:\Program Files\Cloudbase Solutions\Cloudbase-Init\LocalScripts\reset-authentication.ps1"
      ```
      

   4. Execute the following command to download the reset\-authentication plug\-in to the `C:\Program Files\Reset Authentication` folder.

      ```PowerShell
      Invoke-WebRequest -Uri "http://volc-ecs.tos-s3-cn-beijing.volces.com/reset-authentication.exe" -OutFile "C:\Program Files\Reset Authentication\reset-authentication.exe"
      ```
      

4. In PowerShell, execute the following commands in sequence to perform initialization operation.

   1. Execute the following command to obtain the instance UUID.

      ```PowerShell
      $instance_id = ((Invoke-WebRequest -URI "http://100.96.0.96/openstack/latest/meta_data.json" -UseBasicParsing).Content | ConvertFrom-Json).uuid
      ```
      

   2. Execute the following command to delete part of the Cloudbase\-init registry configuration so that the reset\-authentication plug\-in can work as expected.

      If you have not run Cloudbase\-init, you do not need to execute this command.

      ```PowerShell
      Remove-ItemProperty "HKLM:\SOFTWARE\Cloudbase Solutions\Cloudbase-Init\$instance_id\Plugins" LocalScriptsPlugin
      ```
      

   3. Execute the following command to start the reset\-authentication plug\-in.

      ```PowerShell
      Start-Process -Wait -FilePath "C:\Program Files\Reset Authentication\reset-authentication.exe"
      ```
