---
title: "Solution for remote login failure for ECS instance with Windows system due to expired service authentication"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_Remote_Login_Failure_of_ECS_Instances_with_Windows_Operating_System"
---

This topic describes how to use the MSTSC tool built into the Windows operating system to troubleshoot and resolve the issue where remote login to a Windows instance fails with the error message "No Remote Desktop license server is available".

In the example provided in this topic, Windows Server 2016 is used. Take note that procedures may vary across different operating systems. Refer to your actual operating system for guidance.

> This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no representations or warranties of any kind, express or implied, regarding the performance, reliability, or availability of any third\-party product, or any consequences arising from its use.


<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The prompt "No Remote Desktop license server is available" may appear when the Remote Desktop Services authentication expires due to the following causes:


* The Remote Desktop Session Host role is installed in the Windows operating system. This feature offers a 120\-day free trial, after which a paid subscription is required. Failure to pay will cause the service to expire, resulting in the inability to remotely log in to the Windows instance via the terminal.

* Under normal circumstances, Windows Server provides a default free remote desktop management license for two users. If you need more concurrent connections, you need to configure the Remote Desktop Session Host server role. Additionally, you need to purchase and configure the corresponding license before using more concurrent remote desktop management sessions.

* After you configure the Remote Desktop Session Host role, the default free connection license for two users will be canceled simultaneously. If the relevant license is not properly configured, remote login to the Windows instance will fail.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > In this scenario, only remote login to Windows instances via VNC is supported.   
   

2. Delete the Remote Desktop Services.

   1. In the lower\-left corner of the Windows desktop, select the "Server Manager" application.

   2. In the top\-right corner of the Server Manager page, select "Manage \> Remove Roles and Features".

   3. On the "Select destination server" page, select the target instance and click "Next".

   4. On the "Remove server roles" page, select "Remote Desktop Services" and click "Next".

   5. On the feature removal page, select "Remote Desktop Services".

   6. In the pop\-up dialog box, select "Remove management tools (if applicable)" and click "Remove Features".

   7. Click "Next". On the "Confirm removal selections" page, click "Remove".

   8. Follow the prompts to restart the Windows instance for the changes to take effect.

3. Use VNC to connect to the Windows instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

4. Check the progress of Remote Desktop Services removal.

   1. In the lower\-left corner of the Windows desktop, select "Server Manager".

   2. In the top\-right corner of the "Server Manager" page, select "Task Details".

   3. If there is no task information on the "Task Details and Notifications" page, or if a notification indicating Remote Desktop Services removal task completed appears, the Remote Desktop Services have been deleted successfully.

5. Use MSTSC to remotely log in to the Windows instance. For more information, see [Using a Windows host to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-a-Windows-host-to-log-on-to-a-Windows-instance).
