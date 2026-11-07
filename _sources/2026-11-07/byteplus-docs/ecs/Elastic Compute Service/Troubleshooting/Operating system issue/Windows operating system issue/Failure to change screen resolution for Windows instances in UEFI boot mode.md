---
title: "Failure to change screen resolution for Windows instances in UEFI boot mode"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Failure_to_change_screen_resolution_for_Windows_instances_in_UEFI_boot_mode"
---

<span id="p5YtH74f"></span>
## Issue description

Failed to change screen resolution in a Windows instance in UEFI boot mode.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3c3bef13046fedc1d586de7a4bbf8651.png) </span>

<span id="dO8vsySg"></span>
## Cause

The method for changing the desktop screen resolution in a Windows instance with UEFI boot mode is different from that with BIOS boot mode. You cannot change it in the display settings of the system.

<span id="NIscDrQQ"></span>
## Solution

In this example, Windows Server 2022 Datacenter Edition 64\-bit English operating system in UEFI boot mode is used. Follow the actual path in your operating system.


1. [Log in to the target Windows instance using VNC](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click the Windows icon and select "Power \> Restart".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_96be3ec28df8f40be695aac3984f02f9.png) </span>

3. During the instance restart, quickly and repeatedly press the `Esc` key to enter the BIOS settings menu.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3969c20aa5c9c102dc894a1732adb7da.png) </span>

4. Use the up and down arrow keys to select the "Device Manager" menu, and press Enter to open the configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3bbc2d7f824e579b19cdbb5bc5a6210d.png) </span>

5. Use the up and down arrow keys to select the "OVMF Platform Configuration" menu, and press Enter to open the configuration page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83c58abfa74807ce0e28e5da65db02b5.png) </span>

6. Use the up and down arrow keys to select the "Change Preferred" option, and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_edfa6348eb6d231bef3ce0671a7dd66f.png) </span>

7. In the list that appears, use the up and down arrow keys to select the target screen resolution (example: 1280x760), and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_50a141c5c34e30ec8f38973dd34e11dd.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_329070baf2440126f03bb5830f995be5.png) </span>

8. Use the up and down arrow keys to select the "Commit Changes and Exit" option, and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9a3d68916f833e31d7a5e2a6643a16d.png) </span>

9. Press the `Esc` key to exit the Device Manager menu.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fe2d5746f270c0d6273d5fdf10a91709.png) </span>

10. Use the up and down arrow keys to select the "Reset" option and press Enter to confirm.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you select the "Continue" option, after entering the instance, you need to restart the instance for the change to take effect.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_61684dbcbdc79a558bda2bc246c6aba1.png) </span>

11. Log in to the instance and check whether the desktop screen resolution settings have been updated.

   1. Right\-click on a blank area of the desktop and select "Display Settings".

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dbd29192efe8f690ef84b60f47a8adaf.png) </span>

   2. Check whether the current screen resolution has been changed to the value you reconfigured in BIOS.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1d14b6618951caa86bdbd2f24b4b48c1.png) </span>
