---
title: "How to troubleshoot startup failure after migrating a server in UEFI boot mode to a 3rd-generation ECS instance via file-level replication?"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Use-File-Duplication-to-migrate-the-UEFI-server-to-the-third-generation-Serve"
---

<span id=".5pWF6Zqc546w6LGh"></span>
## Issue description

When a source server with `UEFI` boot mode is migrated to a 3rd\-generation DPU instance on the BytePlus platform (for example, [General-purpose g3i](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNp), [General-purpose g3a](https://docs.byteplus.com/en/docs/ecs/General-purpose#.6YCa55So5Z6LZzNh), or [Local-SSD i3s](https://docs.byteplus.com/en/docs/ecs/Local-SSD-based#8IH6RHiz)), the destination instance cannot start properly. The system boot process stalls and displays a `grub>` or `Shell>` prompt.


* **Sample 1**

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c8f40673000439fb4be60b79c7c66aab.png) </span>

* **Sample 2**

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9f1652f592ca23770591ed56674af058.png) </span>


<span id=".6Kej5Yaz5pa55qGI"></span>
## Solution


1. Log in to the faculty BytePlus instance via VNC. For detailed operations, refer to [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Restart the instance via the toolbar on the right side of the screen.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_82fcdf304c284ed39ef1ea762ff7fe73.png) </span>

3. During the initial boot screen, immediately press and hold the `esc` key to access the BIOS setup utility.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_27f038242e0d10bc084b1f6ba5157d00.png) </span>

4. Use the arrow keys to select `Boot Maintenance Manager` and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_04765e9f030717749e36ae60430f5a18.png) </span>

5. In the BIOS, use the arrow keys to select `Boot From File` and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_babd69dbde08c4ab178e7b1357503f1c.png) </span>

6. On the "File Explorer" page, press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a294f79d2e396b40f3c8544a2c2c66a.png) </span>

7. Use the arrow keys to select `EFI` and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2b0088885577f43e6efd6c54aaaaa360.png) </span>

8. Use the arrow keys to select the operating system used by the current instance (here, Ubuntu is used as an example), and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1ca193f787732fcb05916406df052f54.png) </span>

9. Use the arrow keys to select `grubx64.efi` and press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9fff8b3a76a2d6cc144d46d7fa0d60a.png) </span>

10. On the "GNU GRUB" page, press Enter to confirm.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ed27c0507c84ff017880d88042b12c39.png) </span>

11. Use your login credentials to log in to the instance.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6a144ca030a5f055e90f727a891fbe2f.png) </span>

12. Execute the following command to fix the issue.

   ```Plain Text
   /opt/efi_repair.sh
   ```
   

13. After the script execution is complete, execute the following command to restart the instance to verify whether the instance can start as expected.

   ```Plain Text
   reboot
   ```
