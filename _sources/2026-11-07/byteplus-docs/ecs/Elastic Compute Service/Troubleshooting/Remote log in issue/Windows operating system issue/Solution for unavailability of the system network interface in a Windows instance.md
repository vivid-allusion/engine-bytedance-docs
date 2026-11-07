---
title: "Solution for unavailability of the system network interface in a Windows instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Repair_method_for_unavailable_status_of_system_network_interface_in_Windows_instances"
---

This topic describes how to resolve the issue where remote connection fails due to an unavailable system network interface in a Windows instance.

In the example provided in this topic, Windows Server 2016 is used. The operating system may differ slightly depending on the version.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This topic may contain information about third\-party products, which is provided for reference only. BytePlus makes no representations or warranties of any kind, express or implied, regarding the performance, reliability, or availability of any third\-party product, or any consequences arising from its use.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1).

   > Use VNC to log in to the Windows instance.   
   

2. On the right side of the bottom taskbar, click the network icon and select "Network & Internet settings".

3. Select "Network and Sharing Center \> Change adapter settings", and then check whether the network interface is disabled.

   * If it is disabled, right\-click the network interface name and select "Enable" to resolve the issue.

   * If it is not disabled, close the "Change adapter settings" window.

4. If the network interface is still unavailable, perform the following operations:

   1. Click the search icon in the lower\-left corner of the desktop, enter `regedit` in the search box, and click "OK" to open the Registry Editor.

   2. In the left navigation pane, expand the path in sequence: HKEY_LOCAL_MACHINE \> SYSTEM \> CurrentControlSet \> Control \> Class \>{4d36e972\-e325\-11ce\-bfc1\-08002be10318}.

   3. Check if there is an entry named "Installer32" (Type: "REG_SZ", Data: "NetCfgx.dll,NetClassInstaller").

   4. If the entry does not exist, add it manually:

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Editing the registry may cause system instability or errors. Before you edit the registry, we recommend that you back up the registry or create a system restore point to restore the system if issues occur.      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Make sure that the entered information is completely accurate. Otherwise, unpredictable consequences may arise.      </div>
      

      1. Right\-click the blank area on the current page and select "New \> String Value".

      2. Rename the new string value to "Installer32".

      3. Double\-click "Installer32", enter "NetCfgx.dll,NetClassInstaller" in the "Value data" field, and click "OK" to save the settings.

   5. After you add the registry entry, restart the system for the settings to take effect.

   6. Update the network interface driver.

      1. Once the system restarts, enter `devmgmt.msc` in the search box in the lower\-left corner of the desktop and click "OK" to open Device Manager.

      2. Double\-click "Network adapters", right\-click the target network interface name, and select "Update Driver Software".

      3. Select "Search automatically for updated driver software" to update the adapter driver.

5. Check whether the issue is resolved.
