---
title: "Installing or uninstalling system patches in Windows operating system"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Install_uninstall_system_patches"
---

Windows system patches are update programs released by Microsoft for the Windows operating system. They are used to fix system vulnerabilities, enhance security, optimize performance, and add new features. This topic describes how to manually install/uninstall specific system patches in the Windows operating system.

<span id="kj2Tw6TW"></span>
## Applicable scenarios

<span id="QhCIcscB"></span>
### Install system patches


* **Improve security**

   When Microsoft releases security patches for system vulnerabilities, you can install them promptly to effectively defend against various network attacks and reduce the risk of malicious intrusion.

* **Enhance system stability**

   Some patches can fix various errors and exceptions that occur during system operation, improving system stability and reliability.

* **Provide optimized features**

   Some patches bring new features or optimize existing ones, improving the overall performance of the system and the user experience.


<span id="2M7ira1t"></span>
### Uninstall system patches


* **Resolve issues caused by patches**

   If issues such as failure to start the system as expected, inability to run applications, or severe degradation of system performance occur after you install a patch, you can uninstall the patch to restore the system to normal operation.

* **Meet specific environment requirements**

   In specific testing environments or business scenarios, you can uninstall system patches based on your needs to improve system compatibility and stability.


<span id="Lohsxbrx"></span>
## Procedure

This section uses the Windows Server 2022 64 bit operating system as an example to describe the operation process. Use the actual path of your operating system.


<Tabs>
<Tab zoneid="g3Vdt4MxdQ" title="Install system patches">
<TabTitle>Install system patches</TabTitle>

1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon, and then select "Windows System \> Run".

3. In the "Run" dialog box, enter `winver` and click the "OK" button.

4. In the "About Windows" dialog box, confirm the version information of the current operating system.

5. Download the target patch file.

   1. Open the browser and visit [the official Microsoft website](https://www.catalog.update.microsoft.com/home.aspx).

   2. Enter the target patch number and click the "Search" button to query the patch file.

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the example provided in this topic, <code>KB5041160</code> is installed. You can visit the <a href="https://msrc.microsoft.com/update-guide/en-us">official Microsoft website</a> to find more patch information.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d65920fdf38e3cad201c74f043097681.png) </span>

   4. Click the "Download" button to the right of the patch corresponding to the system version information confirmed in Step 4.

      > In the example provided in this topic, you are required to download the "2024\-08 Cumulative Update for Microsoft Server Operating System Version 21H2 (KB5041160) for x64\-based Systems" patch.      
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_520f91a2349ca168b0b07f9c4c103688.png) </span>

   5. Click the patch link to download the patch file.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc1148427777ca903e9bee2e1c2c333c.png) </span>

6. Install the patch.

   1. Double\-click the patch file you downloaded.

   2. Click the "Yes" button.

   3. After the update is complete, click the "Restart now" button to restart the instance and apply the configuration.

7. Click the Windows icon, and select "Windows PowerShell \> Windows PowerShell".

8. Execute the following command in PowerShell to view information about installed system patches and check whether the target patch is installed.

   ```PowerShell
   Get-HotFix | Sort-Object InstalledOn -Descending | Format-Table HotFixID,InstalledOn
   ```
   

   If the following output is displayed, the `KB5041160` patch is installed.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8f7ff0c6da51157b824391a240e093ff.png) </span>


</Tab>
<Tab zoneid="XWTp1JuWmh" title="Uninstall system patches">
<TabTitle>Uninstall system patches</TabTitle>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you uninstall a system patch, compatibility, stability, and security issues may occur. We strongly recommend that you <a href="https://docs.byteplus.com/en/docs/ecs/Disaster_recovery_and_restoration">back up data</a> in advance.</div>



1. [Log in to the target Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon, right\-click "Windows PowerShell" in the Windows PowerShell directory, and then select "More \> Run as administrator".

3. Execute the following command in PowerShell to query information about installed system patches.

   ```PowerShell
   Get-HotFix | Sort-Object InstalledOn -Descending | Format-Table HotFixID,InstalledOn
   ```
   

   Sample output:

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ab237deb637a363c8020e2cb057dda22.png) </span>

4. Uninstall the target patch.

   1. Execute the following command to uninstall a patch.

      ```PowerShell
      wusa /uninstall /<patch number>
      ```
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Replace <code><patch number></code> with the patch that you want to uninstall in the format of <code>kb:patch number</code>. In the example provided in this topic, to uninstall <code>KB5041160</code>, enter <code>kb:5041160</code>.      </div>
      

   2. Click the "Yes" button to uninstall the patch.

   3. Click the "Restart now" button to restart the instance.

5. Log in to the instance after it restarts, and execute the following command in PowerShell to check whether the target patch is uninstalled.

   ```PowerShell
   Get-HotFix | Sort-Object InstalledOn -Descending | Format-Table HotFixID,InstalledOn
   ```
   

   If the following output is displayed, the `KB5041160` patch is uninstalled.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7cbf7a44bb7c920a2794f64d49f430b2.png) </span>


</Tab>
</Tabs>
