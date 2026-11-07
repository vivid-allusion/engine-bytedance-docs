---
title: "Configuring NTP service for Windows instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Configuring-the-NTP-service-for-Windows"
---

This topic describes how to use the NTP service to synchronize the local time of Windows instances. In the example provided in this topic, Windows Server 2019 Datacenter Edition 64 bit is used.

<span id=".5LuA5LmI5pivTlRQ77yf"></span>
## What is NTP?

Network Time Protocol (NTP) is an application\-layer protocol in the TCP/IP protocol suite, designed for clock synchronization between clients and servers and providing highly accurate time calibration.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can enable and configure the NTP service by using either the Graphical User Interface (GUI) or the command line.


<Tabs>
<Tab zoneid="qqTICp3Wej" title="GUI-based configuration">
<TabTitle>GUI-based configuration</TabTitle>

<span id="RTHJj7zC"></span>
### Step 1: Enable the NTP service

By default, the Windows Time service is enabled in the Windows Server operating system. To ensure that time synchronization works as expected after the NTP service is configured, you need to enable the NTP service in the instance. Perform the following steps to check and enable the NTP service:


1. Log in to the Windows instance. For more information, refer to [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows `Start` icon, click "Windows System", and then click "Run". In the Run window, execute the `services.msc` command.

3. In the "Services" window, locate and double\-click "Windows Time".

4. In the "Windows Time Properties (Local Computer)" window, select the "General" tab and modify the following settings:

   1. Set "Start type" to "Automatic".

   2. Make sure that the value of "Service status" is "Running". Otherwise, click the “Start” button to start the Windows Time service.

   3. After you click the "Apply" button, click the "OK" button to enable the NTP service.


<span id=".5L-u5pS56buY6K6kTlRQ5pyN5Yqh5Zmo5Zyw5Z2A"></span>
### Step 2: Modify the default NTP server address

By default, the Microsoft NTP server (time.windows.com) is configured for the Windows Server operating system. You can change the default NTP server to the NTP server you want to use.


1. Log in to the Windows instance. For more information, refer to [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. In the notification area of the taskbar, click the date and time, and then click the "Change date and time settings" button.

3. In the "Related settings" section of the "Date & time" window, click the "Add clocks for different time zones" button.

4. In the newly opened "Date and Time" window, click the "Internet Time" tab, and then click the "Change settings" button.

5. In the "Internet Time Settings" window, select the "Synchronize with an Internet time server" option, and enter the NTP server address you want to use in the "Server" text box.

6. Click the "Update now" button. Windows immediately synchronizes time with the NTP server.

7. Click the "OK" button to complete the modification of the NTP server address.


<span id=".5L-u5pS5TlRQ5pyN5Yqh5pe26Ze05ZCM5q2l6Ze06ZqU"></span>
### Step 3: Modify the time synchronization interval for the NTP service (optional)

The default time synchronization interval is 400 (in hexadecimal, equivalent to 1024 seconds, or approximately 17 minutes). You can specify a custom time synchronization interval for the NTP service based on your needs. Perform the following steps to modify the time synchronization interval:


1. Connect to the Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows `Start` icon, click "Windows System", and then click "Run". In the Run window, execute the `regedit` command.

3. In the left directory tree of the "Registry Editor" window, select "HKEY_LOCAL_MACHINE \> SYSTEM \> CurrentControlSet \> Services \> W32Time \> TimeProviders \> NtpClient".

4. In the "Name" column of the details window on the right, double\-click "SpecialPollInterval".

5. In the "Edit DWORD (32\-bit) Value" window, set "Base" to "Decimal" and enter a value in the "Value data" field based on your needs. The value you enter is the synchronization interval you need, in seconds.

6. Click the "OK" button to complete the modification operation.

7. After you complete the modification, you need to restart the instance or the service for the configuration to take effect. If you do not want to restart the instance due to your business requirements, you can perform the following steps to restart the service for the modification to take effect.

   1. Click the Windows `Start` icon, click "Windows System", and then click "Run". In the Run window, execute the `services.msc` command.

   2. In the "Services" window, locate and right\-click "Windows Time".

   3. Click the "Restart" button to restart the service.


</Tab>
<Tab zoneid="FvRTMtBlpR" title="Command line-based configuration">
<TabTitle>Command line-based configuration</TabTitle>

1. Connect to the Windows instance. For more information, see [Logging in to Windows instances](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the "Windows" icon, right\-click "Command Prompt" in "Windows System", and then click "Run as administrator" under "More".

3. Start the NTP service.

   Execute the following command in the Command Prompt window to enable the NTP service and set "Startup type" to "Automatic".

   ```Plain Text
   sc config W32Time start=auto
   net start w32time
   ```
   

4. Modify the default NTP server address.

   Execute the following command in the Command Prompt window to modify the address of the NTP service.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more details about the W32tm tool, see <a href="https://learn.microsoft.com/zh-cn/windows-server/networking/windows-time-service/windows-time-service-tools-and-settings">Windows Time service tools and settings</a>.   </div>
   

   ```Plain Text
   w32tm /config /manualpeerlist:"ntp0.ivolces.com,0x9 ntp1.ivolces.com,0x9 ntp2.ivolces.com,0x9 ntp3.ivolces.com,0x9" /syncfromflags:manual /reliable:yes  /update
   ```
   

5.  **(Optional)**  Modify the time synchronization interval for the NTP service

   Execute the following command in the Command Prompt window to modify the time synchronization interval settings in the NTP configuration of the registry.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, the time synchronization interval is set to <code>600</code> seconds. You can convert your desired time interval to hexadecimal and replace <code>258</code> in the command with this converted value.   </div>
   

   ```Plain Text
   reg add HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient /v SpecialPollInterval /d 0x258 /t REG_DWORD /f
   ```
   

6. Execute the following commands in the Command Prompt window to restart the time service and resynchronize the time.

   ```Plain Text
   net stop w32time
   net start w32time
   w32tm /resync
   ```
   

7. Execute the following command in the Command Prompt window to query the time synchronization status.

   ```Plain Text
   w32tm /query /status
   ```
   




</Tab>
</Tabs>
