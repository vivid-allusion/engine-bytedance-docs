---
title: "Installation failure of .NET Framework 3.5 on Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cannot_install_NET_Framework_3_5_in_a_Windows_instance"
---

<span id="AiqYSRXM"></span>
## Issue description

When I install .NET Framework 3.5 on an instance running the Windows operating system, the following error occurs: "Installation of one or more roles, role services, or features failed. Error: 0x800f0954".

<span id="FpBgkyPN"></span>
## Causes

When you install features via Server Manager, the corresponding features are downloaded and installed from the WSUS server configured in the operating system. If the WSUS server configured in the system does not synchronize the .NET Framework 3.5 feature, Server Manager reports an error because it cannot obtain the required installation packages or update files.

<span id="GkfYV67e"></span>
## Solutions


1. [Log in to the target Windows server](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Windows-instance).

2. Click the "Start" button, and select "Windows PowerShell \> Windows PowerShell".

3. Execute the following command in PowerShell to disable the WSUS server you have configured and switch to the official Microsoft WSUS server.

   ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 0
   ```
   

4. Execute the following command to restart the WSUS service for the configuration to take effect.

   ```PowerShell
   Restart-Service -Name wuauserv
   ```
   

5. Reinstall the .NET Framework 3.5 feature by using Server Manager.

   
   Installation steps
   
   
   1. Click the "Start" button, and select "Server Manager".
   
   2. In the upper right corner, select "Manage \> Add Roles and Features".
   
   3. In the "Add Roles and Features Wizard" dialog box, click the "Next" button.
   
   4. Select "Role\-based or feature\-based installation" and click the "Next Page" button.
   
   5. Select the server or virtual hard disk on which you want to install .NET Framework 3.5. In the example provided in this topic, "Select a server from the server pool" is selected. Click the "Next" button.
   
   6. Select the roles to install on the selected server. In the example provided in this topic, the default settings are used. Click the "Next" button.
   
   7. Select ".NET Framework 3.5 Features", and click the "Next" button.
   
   8. Complete the optional installation configuration based on your needs. In the example provided in this topic, the default settings are used. Click the "Install" button.
   
   9. After the installation is complete, click the "Close" button to close the installation wizard.
   

6. After the installation is complete, you can execute the following command in PowerShell to restore the original WSUS server configuration.

   ```PowerShell
   Set-ItemProperty -Path 'HKLM:\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU' -Name UseWUServer -Value 1
   ```
   

7. Execute the following command to restart the WSUS service for the configuration to take effect.

   ```PowerShell
   Restart-Service -Name wuauserv
   ```
