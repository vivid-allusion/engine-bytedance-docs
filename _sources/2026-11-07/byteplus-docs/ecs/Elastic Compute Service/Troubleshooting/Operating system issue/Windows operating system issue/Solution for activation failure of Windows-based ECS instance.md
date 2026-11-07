---
title: "Solution for activation failure of Windows-based ECS instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance"
---

This topic describes how to resolve the activation failure of Windows\-based ECS instances.

A Windows instance is preconfigured with an activation script by default. Under normal circumstances, the instance can communicate with the KMS server to activate the operating system. If activation fails, it may be due to the following reasons:


* [Software protection exception](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.c29mdHdhcmUtcHJvdGVjdGlvbuW8guW4uOWvvOiHtOa_gOa0u-Wksei0pQ==)

* [Activation failure caused by network errors](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.572R57uc5byC5bi45a-86Ie05r-A5rS75aSx6LSl)

* [Activation failure caused by server clock desynchronization](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.5pyN5Yqh5Zmo5pe26ZKf5LiN5ZCM5q2l5a-86Ie05r-A5rS75aSx6LSl)

* [Activation failure caused by insufficient disk space](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.56OB55uY56m66Ze05LiN6Laz5a-86Ie05r-A5rS75aSx6LSl)

* [ctivation code](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.5r-A5rS756CB5LiN5q2j56Gu5a-86Ie05r-A5rS75aSx6LSl)[ctivation code](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.5r-A5rS756CB5LiN5q2j56Gu5a-86Ie05r-A5rS75aSx6LSl)[ctivation code](https://docs.byteplus.com/en/docs/ecs/Solution_for_Activation_Failure_of_Windows_System_ECS_Instance#.5r-A5rS756CB5LiN5q2j56Gu5a-86Ie05r-A5rS75aSx6LSl)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The copyright of the official Microsoft links cited in this topic belongs to Microsoft. The BytePlus platform assumes no responsibility for the scope of operating systems applicable to this topic, or issues that may arise from Microsoft Windows product iterations or delayed document updates.</div>


* <div data-tips="true" data-tips-type="tip">This topic may contain information about third\-party products. Related information is provided for reference only. The BytePlus platform makes no representations or warranties of any kind, express or implied, regarding the performance, reliability, or availability of any third\-party product, or any consequences arising from its use.</div>



<span id=".U29mdHdhcmUgUHJvdGVjdGlvbuW8guW4uOWvvOiHtOa_gOa0u-Wksei0pQ=="></span>
## Activation failure caused by software protection exception

<span id=".6Zeu6aKY546w6LGh5Y-K5YiG5p6Q"></span>
### Issue symptoms and analysis

When you activate the Windows operating system by using the `slmgr -ato` command, the following error occurs.

This issue may occur because the Software Protection service is not running, which prevents the operating system from being activated. You can refer to this section to start the service.

<span id=".5pON5L2c6K-05piO"></span>
### Usage note


* Improper modification of the Windows Registry may lead to severe system issues. We recommend that only personnel with a basic understanding of the Windows operating system perform such modifications.

* To avoid system issues or data loss caused by accidental Registry modifications, always back up data on the system disk and data disk before making changes to the Registry. A common backup method is to [create a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

2. In the lower\-left corner of the desktop, click the "Start" icon and select "Windows Administrative Tools \> Services".

3. Find and double\-click the "Software Protection" service.

4. Click the "Start" button. Once the service starts, click the "OK" button.

   If the Software Protection service fails to start as expected or is not detected during startup, follow these steps to rebuild the service:

   1. Open cmd. Then run the `regedit` command to open the Registry Editor.

   2. Navigate to `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\sppsvc`, right\-click it, select "Export", and back up the current file to `C:\sppsvc_bak.reg`.

   3. On a normal ECS instance of the same version, use the preceding method to export `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\sppsvc` as the file named "sppsvc_good.reg".

   4. Copy the exported "sppsvc_good.reg" file to the problematic ECS instance and double\-click the file. When the system prompts you to confirm the registry import, click "Yes".

   5. Start the service and activate the operating system again.

   6. (Optional) If activation still fails, re\-import the backup file `C:\sppsvc_bak.reg` (created in Step 2) into the system.


<span id=".572R57uc5byC5bi45a-86Ie05r-A5rS75aSx6LSl"></span>
## Activation failure caused by network errors

<span id=".6Zeu6aKY546w6LGh5Y-K5YiG5p6Q"></span>
### Issue symptoms and analysis


* A "Windows is not genuine" notification appears in the bottom\-right corner of the desktop.

* The system displays the error: "Error: 0xC004F074 The Software Licensing Service reported that the computer could not be activated. The Key Management Service (KMS) is unavailable."


This issue typically occurs due to network issues between the server and the KMS server, which prevent the two from communicating as expected.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Network issues may occur because the communication between the ECS instance and the ECS activation server is blocked by the system firewall, IP security policies, or other network security management software on the Windows\-based ECS instance.</div>


<span id=".5pON5L2c6K-05piO"></span>
### Usage note


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

2. Check if the system firewall blocks the TCP port of the KMS server. If your firewall has inbound/outbound rules that block this TCP port, delete the rules.

3. Check if an IP security policy is configured to block access to the IP addresses resolved from the KMS server. If such a policy exists, delete it.

4. Check if other security software blocks the TCP port of the KMS server.

5. Run the `route print` command to verify if the internal routing of the instance is normal. If the internal network route is missing, add it manually.


<span id=".5pyN5Yqh5Zmo5pe26ZKf5LiN5ZCM5q2l5a-86Ie05r-A5rS75aSx6LSl"></span>
## Activation failure caused by server clock desynchronization

<span id=".6Zeu6aKY546w6LGh5Y-K5YiG5p6Q"></span>
### Issue symptoms and analysis

The server clock must be consistent with the clock of the KMS server. Any deviation between the two clocks will also result in activation failure.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure

Check the current system time in the bottom\-right corner of the system desktop to confirm its accuracy. If there is an obvious deviation in the system time, perform the following operations:


* Manually adjust the system time settings, and then attempt to activate the operating system again.

* Execute the following commands to synchronize the clock, and then attempt to activate the operating system again.

   ```Plain Text
   net start W32Time
   w32tm /resync
   ```
   

   The system returns information similar to the following:


<span id=".56OB55uY56m66Ze05LiN6Laz5a-86Ie05r-A5rS75aSx6LSl"></span>
## Activation failure caused by insufficient disk space

<span id=".6Zeu6aKY546w6LGh5Y-K5YiG5p6Q"></span>
### Issue symptoms and analysis

During activation, the error message "product not found" is displayed.

This error may occur because the system disk of the instance has insufficient space, which means there is not enough storage available to complete the activation process.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the target instance. For more information, see [Login overview](https://docs.byteplus.com/en/docs/ecs/Overview-1#.55m75b2V5pa55byP).

2. Clean up the C drive to free up disk space.

3. Execute the `slmgr -ato` command to attempt to activate the operating system again.


<span id=".5r-A5rS756CB5LiN5q2j56Gu5a-86Ie05r-A5rS75aSx6LSl"></span>
## Activation failure caused by activation code

<span id=".6Zeu6aKY546w6LGh5Y-K5YiG5p6Q"></span>
### Issue symptoms and analysis

During activation, an error message appears with the error code "C004F015".

This issue may occur because the product key used by the system does not match the system version. It is generally caused by manual modifications to the activation settings.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Query the product key based on the actual version of the operating system. For more information, see the [Microsoft official documentation](https://technet.microsoft.com/en-us/library/jj612867(v=ws.11).aspx).

2. Execute the `slmgr /ipk [$Setup_Key]` command to replace the product key with a matching one.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Replace [$Setup_Key] with the actual product key for your system.   </div>
   

3. Execute the `slmgr -ato` command to attempt to activate the operating system again.
