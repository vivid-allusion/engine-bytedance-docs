---
title: "Methods to start the RDP service in Windows operating system instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Method_for_enable_Remote_Desktop_Connection_RDP_service_for_Windows_system_instances"
---

The Remote Desktop Protocol (RDP) service facilitates the management and operation of Windows instances. If it is not enabled, remote desktop connections cannot be established. This topic describes how to enable the RDP service for remote desktop connections.

In the example provided in this topic, Windows Server 2016 is used. The operating system may differ slightly depending on the version. Please refer to the actual version for accuracy.

> This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".6YCa6L-H57O757uf5bGe5oCn5byA5ZCvUkRQ5pyN5Yqh"></span>
### Enable the RDP service through system properties


1. In the search box, enter "This PC" and select the "This PC" app from the results.

2. Select "This PC \> Properties", and click "Advanced system settings".

3. Select the "Remote" tab, confirm that "Allow remote connections to this computer" is selected, and select "Allow connections only from computers running Remote Desktop with Network Level Authentication (recommended)" based on your needs.

4. Click "OK" to complete the operation.


<span id=".6YCa6L-H5ZG95Luk5byA5ZCvUkRQ5pyN5Yqh"></span>
### Enable the RDP service by using commands


1. Log in to the target instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > We recommend that you use the VNC method in this scenario.   
   

2. Open the command line tool.

   1. In the "Run" window, enter "cmd".

   2. Press the "Enter" key to open the command line tool.

3. Execute the following command to check if port 3389 is in the listening state.

   ```Plain Text
   netstat -aon | findstr "3389"
   ```
   

4. If port 3389 is not in the listening state, follow these steps to enable the RDP service for remote desktop connections and activate port 3389.

   1. Execute the following command to enter PowerShell mode.

   ```Plain Text
   powershell
   ```
   

   2. Execute the following command to enable the RDP service for remote desktop connections.

   ```Plain Text
   Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server" -Name fDenyTSConnections -Value 0 -Force
   Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" -Name UserAuthentication -Value 1 -Force
   netsh.exe advfirewall firewall add rule name="Open RDP Port 3389" dir=in action=allow protocol=TCP localport=3389
   ```
