---
title: "Windows Server operating systems"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Windows_Server_Operating_System"
---

This topic describes how to fix issues in the Windows Server operating system detected by the image detection feature.

<span id=".56aB55SoWGVu6amx5Yqo"></span>
## Disable the Xen driver

ECS instances no longer use Xen drivers. Xen drivers remaining in the image may cause startup exceptions for ECS instances. You can configure the registry according to the instructions in this section to disable the Xen driver.


1. Log in to the server for creating images.

2. Click the "Start" button, and click "System Tools \> Run".

3. Enter `regedit`, and click the "OK" button.

4. In the left directory tree, click "HKEY_LOCAL_MACHINE \> SYSTEM \> ControlSet001 \> Services \> XenPCI \> Parameters".

5. Double\-click the `hide_devices` parameter, delete the value, and then click the "OK" button to complete the modification.

6. After you fix the issues, you can re\-import the image and perform image detection. [Learn more](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images#.5a-85YWl6ZWc5YOP5pe25qOA5rWL).


<span id=".5YWB6K645a6J6KOF6amx5Yqo"></span>
## Allow driver installation

If the service that prohibits driver installation is enabled in the image registry tree, drivers cannot be updated for instances created by using the image. You can modify the registry configuration according to the guidance in this section to allow driver installation.


1. Log in to the server for creating images.

2. Click the "Start" button, and click "System Tools \> Run".

3. Enter `regedit`, and click the "OK" button.

4. Open the registry entry in the path corresponding to the operating system version:

   * Windows Server 2008 R2 and later: HKEY_LOCAL_MACHINE \> SYSTEM \> ControlSet001 \> Services \> DeviceInstall \> Parameters.

   * Windows Server 2008 R2 and earlier: HKEY_LOCAL_MACHINE \> SYSTEM \> ControlSet001 \> Services \> PlugPlay \> Parameters.

5. If the value of the `DeviceInstallDisabled` parameter is not `0`, you can change the parameter value to `0`, or delete the parameter.

   * Modify the parameter value (recommended)

      1. Right\-click the parameter name, click the "Modify..." button.

      2. Set "Value data" to `0`.

      3. Click the "OK" button to complete the modification.

   * Delete the parameter

      1. Right\-click the parameter name, and click the "Delete" button.

      2. Click the "Yes" button to complete the deletion.

6. After you fix the issues, you can re\-import the image and perform image detection. [Learn more](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images#.5a-85YWl6ZWc5YOP5pe25qOA5rWL).
