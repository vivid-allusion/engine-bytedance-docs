---
title: "Solution for port conflict during remote login to a Windows system instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_resolving_port_conflicts_during_remote_login_to_Windows_system_instances"
---

This topic describes how to resolve the issue where remote login to a Windows instance fails due to a port conflict. The conflict occurs when the remote connection port (default port 3389) is occupied by another process or service.

In the example provided in this topic, the built\-in remote desktop connection tool (MSTSC) of the Windows operating system is used to remotely log in to a Windows instance.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Using a Windows host to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Windows-instance).

2. Open the Task Manager of the Windows operating system.

   1. In the lower\-left corner of the desktop, click the "Start" icon.

   2. Click the "Task Manager" card.

3. Check the process occupying the remote port.

   1. In the upper\-left corner of Task Manager, select "File \> Run new task".

   2. In the "Create new task" dialog box, enter "cmd" and click "OK".

   3. In the command prompt window, run the following command to find the process occupying the remote port.

      ```Plain Text
      netstat -ano|findstr "3389"
      ```
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7db5945e1dc7fca8c7ae577b6794b3a1.png) </span>

4. Open the Registry Editor.

   1. In the upper\-left corner of Task Manager, select "File \> Run new task".

   2. In the "Create new task" dialog box, enter "regedit" and click "OK".

5. Modify the remote service port number.

   1. Navigate to the following registry path: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\Wds\rdpwd\Tds\tcp. Right\-click "PortNumber", and then change the value of the "Value data" parameter from "3389" to another unused port.

   2. Navigate to the following registry path: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP\-Tcp. Right\-click "PortNumber", and then change the value of the "Value data" parameter to the same port specified in the preceding TCP path.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You must specify the same value for the "Value data" parameter of "PortNumber" in both the TCP and RDP\-TCP paths.      </div>
      

   3. After the configuration is complete, the Windows operating system will automatically recognize the new remote service port number.

6. (Optional) Configure firewall inbound rules. If the firewall is not enabled, skip this step.

   1. In the lower\-left corner of the desktop, enter "Firewall" and select "Firewall & network protection".

   2. Click "Advanced settings".

   3. Select "Inbound Rules \> New Rule \> Port (0)".

   4. Click "Next", select "Specific local ports", and enter the same new port used in the registry.

   5. Retain the default settings, and click "Next" repeatedly until the "Name" page is displayed.

   6. Enter a custom name for the inbound rule, and click the "Finish" button.

7. Restart Remote Desktop Services.

   1. Open Task Manager by following Step 2.

   2. Click the "Services" tab.

   3. Right\-click "Remote Desktop Services", and then click "Restart".

8. Add the remote service port number to the security group configuration. For more information, see [Configuring security group rules](https://docs.byteplus.com/en/docs/ecs/How-to-configure-security-group-rules).

9. Log in to the instance again and check whether the issue is resolved. For more information, see [Using a Windows host to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Windows-instance).
