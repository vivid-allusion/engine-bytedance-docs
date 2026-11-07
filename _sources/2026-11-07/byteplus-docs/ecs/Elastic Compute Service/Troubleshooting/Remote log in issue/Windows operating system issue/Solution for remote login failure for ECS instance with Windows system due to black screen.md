---
title: "Solution for remote login failure for ECS instance with Windows system due to black screen"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_ECS_instance_with_Windows_system_unable_to_log_in_remotely"
---

This topic describes how to troubleshoot and resolve the issue where a black screen appears when you log in to a Windows instance, the explorer.exe file is missing from the "C:\Windows" directory, and the desktop cannot be accessed.

> This topic may contain information about third\-party products. Related information is for reference only. The BytePlus platform makes no implication or other form of commitment regarding the performance and reliability of third\-party products, or potential impacts that may result from their operation.


<span id=".6Zeu6aKY5Y6f5Zug"></span>
## Causes

Possible causes for the missing explorer.exe in the "C:\Windows" directory of the instance operating system:


* The file is deleted manually.

* The file is deleted by third\-party software.


You can resolve this issue by adding the `explorer.exe` file to the `C:\Windows` directory of the Windows operating system.

> To re\-add the bfsvc.exe, regedit.exe, or write.exe files that are missing from your Windows operating system, you can also perform the following steps.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the target instance. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

   > In this scenario, VNC is required to connect to the Windows instance.   
   

2. Open the Task Manager of the Windows operating system.

3. Open the command window of the Windows operating system.

   1. In the upper\-left corner of Task Manager, select "File \> Run new task".

   2. In the "Create new task" dialog box, enter "cmd".

   3. Click the "OK" button.

4. In the command line window, use the `copy` command to copy the explorer.exe file from another directory to the "C:\Windows" directory of the instance.

   1. Execute the `dir c:\explorer.exe /s /b` command to obtain the directory of the explorer.exe file.

      Sample command output:

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_38a5669ec8dfdda3dae046ebdcdade2a.png) </span>

   2. Execute the `copy explorer.exe` command in the directory where explorer.exe is located to add the explorer.exe file.

5. Open the explorer.exe file.

   1. In the upper\-left corner of Task Manager, select "File \> Run new task".

   2. In the "Create new task" dialog box, enter "explorer.exe".

   3. Click the "OK" button.

      The operating system automatically opens the "This PC" page, indicating that the explorer.exe file is added.

   4. Refer to Step 1 to log in remotely to the instance again and check whether the issue is resolved.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the issue persists, the explorer.exe file in the Windows system is completely corrupted and is no longer usable. We recommend that you <a href="https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot">create snapshots</a> in the ECS console to back up instance data, reinitialize the system volume to restore the operating system.      </div>
