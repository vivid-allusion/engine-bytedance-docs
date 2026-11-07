---
title: "Solution for cursor exceptions on instances that use the self-developed software-hardware integrated virtualization architecture and run Windows"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/windows-cursor-abnormal-issue-fix-on-in-house-virtualization-instances"
---

## Issue description

When you log in to a Windows\-based instance (such as [General-purpose g4i](https://docs.byteplus.com/en/docs/ecs/General-purpose?lang=en#ZHRHYffU)) with the **self\-developed software\-hardware integrated virtualization architecture** through VNC, cursor issues may occur. The situations include: dual cursors, delayed cursor response, or the cursor being unable to reach the screen edges.

## Causes

In the Windows OS, **Enhance pointer precision** is enabled by default, which adjusts pointer displacement based on mouse movement speed. In a general virtualization architecture, the Hypervisor first performs coordinate conversion and synchronization for mouse input events, and then passes them to the Guest OS. Therefore, the mouse pointer can usually move normally. However, the self\-developed software\-hardware integrated virtualization architecture uses hardware passthrough mode. Mouse input events bypass the Hypervisor and are passed directly to the Guest OS. In this case, if **Enhance pointer precision** is still enabled in Windows, its pointer acceleration mechanism may be incompatible with the coordinate mapping or synchronization mechanism of the current architecture. This may cause issues such as delayed cursor response, dual cursors, or the inability to move the cursor to the screen edges.

## Solution

In this example, the Windows Server 2022 Datacenter Edition 64 bit English operating system is used. Operation paths may vary depending on the operating system. Please follow what is shown on your actual interface.

1. [Log in to the target Windows-based instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon and select "Control Panel".

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0ffc5ea9205c1e850420ddbab03ba6be.png)

3. In the upper\-right corner of the page, switch "View by" to "Small icons", and click "Mouse" to open the configuration page.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_19016efabf7d3b73ff8ddac6938f03ea.png)

4. Select the "Pointer Options" tab, and **uncheck** the "Enhance pointer precision" option. Click the "OK" button to disable pointer precision enhancement.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4d102d7278dcefa6d2f5d2f571f23ab7.png)

5.  **(Optional) ** If dual cursors still appear after you disable pointer precision enhancement in "Control Panel", please modify the registry to completely disable mouse acceleration.

   > **warning**

   > Modifying the registry is a **high\-risk operation** and may impact system stability. Before modification, we recommend backing up the current registry by selecting "File \> Export" in the Registry Editor. If an exception occurs, you can roll back by selecting "File \> Import" in the registry.

   1. Click the Windows icon and click "Windows System \> Run".

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6ac8ecac001563b5bd8bbb6698b803e.png)

   2. Enter `regedit` and click the "OK" button to open the Registry Editor.

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cad1963b694e00bfcb5caf0c261f879d.png)

   3. In the left\-side directory tree, select "Computer \> HKEY_USERS \> .DEFAULT \> Control Panel \> Mouse".

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c6198d390254aff0d210f7ab6df68b1.png)

   4. Double\-click the registry entry "MouseSpeed", and change "Value data" to `0`. Then, click "OK".

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4802632a96117318a1a25a2c50d63c48.png)

6. [Use VNC to log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance) again, and verify whether the cursor issue has been resolved.
