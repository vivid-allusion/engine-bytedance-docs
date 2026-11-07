---
title: "Uninstalling NVIDIA GRID drivers"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-GRID-drivers"
---

You can refer to this topic to uninstall the GRID driver.

<span id=".5Y246L29R1JJROmpseWKqO-8iFdpbmRvd3PvvIk="></span>
## Uninstall GRID driver (Windows)


1. [Log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

2. Click "Start \> Control Panel".

3. In Control Panel, find "Programs" and click "Uninstall a program".

4. Right\-click the GRID driver that needs to be detached, and then click "Uninstall/Change (U)".

5. In the pop\-up "NVIDIA Uninstaller" dialog box, click "Uninstall (U)".

6. After the uninstall is complete, click "Restart Now (R)" to complete the uninstallation.


<span id=".5Y246L29R1JJROmpseWKqO-8iExpbnV477yJ"></span>
## Uninstall GRID driver (Linux)


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to uninstall the GRID driver.

   `nvidia-uninstall`

3. When the system prompts you to back up the X screen configuration file, we recommend keeping the default option "NO" and pressing Enter.

   > Prompts in different operating systems may vary. Select based on your business scenarios.   
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5d79e429517bd84b911b8a3da6762a52.png) </span>

4. When the following output is displayed, the driver uninstallation is successful. Select "OK" and press the Enter key to exit the page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_092db66a2431ca88eff55c17b64a8c5f.jpeg) </span>

5. Execute the `reboot` command to restart the instance to make the operation take effect.
