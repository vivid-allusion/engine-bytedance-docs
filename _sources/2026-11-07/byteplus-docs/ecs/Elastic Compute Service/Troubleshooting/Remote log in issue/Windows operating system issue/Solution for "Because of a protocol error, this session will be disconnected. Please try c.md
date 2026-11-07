---
title: "Solution for \"Because of a protocol error, this session will be disconnected. Please try connecting to the remote computer again.\" error occurred when local PC connects to Windows ECS instance via Remote Desktop"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_the_error_Because_of_a_protocol_error_the_session_will_be_disconnected"
---

<span id="ql9EcQIJ"></span>
## Problem description

When a local PC connects to an ECS instance running the Windows operating system via Remote Desktop, the "Because of a protocol error, this session will be disconnected. Please try connecting to the remote computer again." error occurs.

<span id="iUSpZq5m"></span>
## Causes

Some causes of this error are as follows:


* Incorrect security configuration of the Remote Desktop Session Host leads to a protocol error prompt when a remote connection is established. You can fix this error by [modifying the security configuration of the Remote Desktop Session Host](https://docs.byteplus.com/en/docs/49/69782#aJnFG9fS).

* Under normal circumstances, the remote connection port is occupied by the svchost.exe process. When the port is occupied by a process other than svchost.exe, a remote connection cannot be established as expected. You can resolve this error by [closing the application that is occupying the remote connection port](https://docs.byteplus.com/en/docs/49/69782#TCx99yX1) or [changing the remote connection port](https://docs.byteplus.com/en/docs/49/69782#PFHbYuVh).


<span id="PpnWhwD7"></span>
## Solutions

In the example provided in this topic, Windows Server 2016 Datacenter Edition 64 bit is used as an example to introduce solutions. The solutions include modifying the security configuration policy of the Remote Desktop Session Host, closing the application that is occupying the remote connection port, or changing the remote connection port.

<span id="aJnFG9fS"></span>
### Modify the security configuration of the Remote Desktop Session Host


1. Log in to the instance HammerDB\-01 via VNC. For detailed steps, refer to [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > If you are unable to use VNC to log in to the instance, [reset the login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) and then try again.   
   

2. Click the "Start" icon, and select "Windows System \> Run".

3. Enter the following command in the "Run" dialog box, and click the "OK" button.

   ```Plain Text
   gpedit.msc
   ```
   

4. In the "Local Group Policy Editor" window, select "Computer Configuration \> Administrative Templates \> Windows Components \> Remote Desktop Services \> Remote Desktop Session Host \> Security".

5. Double\-click "Require use of specific security layer for remote (RDP) connections" to open the security layer configuration window.

6. Click "Enabled", select "RDP" in the "Security Layer" drop\-down list, and then click the "Apply" and "OK" buttons in sequence to complete the operation.

7. Click the "Start" button, and select "Windows System \> Command Prompt".

8. Execute the following command to make the updated policy take effect.

   ```Plain Text
   gpupdate
   ```
   

9. Use Remote Desktop to connect to the instance again and check whether you can log in to the instance as expected.


<span id="TCx99yX1"></span>
### Close the application that is occupying the remote connection port


1. Log in to the instance HammerDB\-01 via VNC. For detailed steps, refer to [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > If you are unable to use VNC to log in to the instance, [reset the login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) and then try again.   
   

2. Click the "Start" button, and select "Windows PowerShell \> Windows PowerShell".

3. Execute the following command to obtain the PID (process ID) of the process occupying the remote connection port.

   ```PowerShell
   Get-NetTCPConnection -LocalPort 3389 | Select-Object OwningProcess, State | Get-Unique
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the example provided in this topic, port <code>3389</code> is used as the default port for Remote Desktop connections. Replace it with the actual port used by your Remote Desktop service.   </div>
   

4. Execute the following command to view the application associated with the process ID (PID).

   ```PowerShell
   Get-Process -Id <PID>
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><PID></code> with the process ID obtained in Step 3.   </div>
   

5. Execute the following command to close the process with the specified PID.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">There are risks associated with closing a process directly. Make sure that this operation will not affect the normal operation of your business.    </div>
   

   ```PowerShell
   Stop-Process -Id <PID> -Force
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Replace <code><PID></code> with the ID of the process that you want to close.   </div>
   

6. Execute the following command to restart the RDP service.

   ```PowerShell
   Restart-Service -Name TermService -Force
   ```
   

7. Use Remote Desktop to connect to the instance again and check whether you can log in to the instance as expected.


<span id="PFHbYuVh"></span>
### Change the remote connection port


1. Log in to the instance HammerDB\-01 via VNC. For detailed steps, refer to [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > If you are unable to use VNC to log in to the instance, [reset the login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) and then try again.   
   

2. Click the "Start" icon, and select "Windows System \> Run".

3. Enter the following command in the "Run" dialog box, and click the "OK" button.

   ```Plain Text
   regedit
   ```
   

4. In the "Registry Editor" window, select "HKEY_LOCAL_MACHINE \> SYSTEM \> CurrentControlSet \> Control \> Terminal Server \> WinStations \> RDP\-Tcp".

5. Double\-click "PortNumber" in the parameter list on the right.

6. On the parameter editing page, set the "Base" option to "Decimal", modify the value in the "Value data" field to the new port number used for remote connection, and click the "OK" button to complete the operation.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e04cf7c7841727b0b9f18fee4eb4795c.png) </span>

7. Click the "Start" button, and select "Windows PowerShell \> Windows PowerShell".

8. Execute the following command to restart the RDP service.

   ```PowerShell
   Restart-Service -Name TermService -Force
   ```
   

9. Use Remote Desktop to connect to the instance again and check whether you can log in to the instance as expected.
