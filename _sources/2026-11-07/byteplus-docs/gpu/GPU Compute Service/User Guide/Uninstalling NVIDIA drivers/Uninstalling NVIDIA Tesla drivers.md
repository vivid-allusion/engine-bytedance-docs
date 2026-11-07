---
title: "Uninstalling NVIDIA Tesla drivers"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers"
---

<span id=".5Y246L29TlZJRElBIFRlc2xh6amx5Yqo77yITGludXjvvIk="></span>
## Uninstall NVIDIA Tesla driver in Linux instance

<span id=".5rOo5oSP5LqL6aG5"></span>
### Usage notes


* To uninstall a GPU driver, you need permission granted by the `root` account. If you are an ordinary user, execute the `sudo` command to obtain permission for the `root` account first. In this topic, logging in as the `root` account is used as an example.

* The commands for uninstalling different CUDA versions may vary. If the "cuda\-uninstaller" file does not exist, go to the "/usr/local/cuda/bin/" directory and check for the file name​ starting with "uninstall_cuda". If the file exists, replace "cuda\-uninstaller" in the command with the filename starting with "uninstall_cuda".


<span id=".5Y246L29cnVu5YyF5pa55byP5a6J6KOF55qETlZJRElB6amx5Yqo"></span>
### Uninstall Tesla driver installed via run package


1. [Log in to the Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following command to uninstall the GPU driver.

   `/usr/bin/nvidia-uninstall`

3. Execute the following commands to uninstall the CUDA and cuDNN toolkits. In this example, cuda\-12.2 is used.

   `/usr/local/cuda/bin/cuda-uninstaller`

   `rm -rf /usr/local/cuda-12.2`

4. Execute the `reboot` command to restart the GPU instance.


<span id="rbBKXSiB"></span>
### Use the cloud assistant to uninstall Tesla driver

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The instance must be in the <strong>Running</strong> (<code>Running</code>) status.</div>


* <div data-tips="true" data-tips-type="default">Cloud assistant Agent is installed. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Installing cloud assistant Agent</a>.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Public commands" tab.

4. Find the target command for uninstalling the Tesla GPU driver, and then click the "Create a job" button. Command\-related parameters are listed below. For more parameters, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job#.5pON5L2c5q2l6aqk).

   
   |Parameter​ |Type |The description. |
   |---|---|---|
   |IS_REBOOT |String |Determines whether to restart the instance. Default value: true.<br><br>If you do not want to restart the instance after uninstalling the driver, enter "false". We recommend restarting. |
   |IS_FABRIC |String |Determines whether to uninstall Fabric Manager. Default value: true.<br><br>The system defaults to uninstalling Fabric Manager. If you need Fabric Manager not to be uninstalled, enter "false". |
   

6. After the job is created, the GPU driver and NVIDIA Fabric Manager are uninstalled automatically.


<span id=".5Y246L29TlZJRElBIFRlc2xh6amx5Yqo77yIV2luZG93c--8iQ=="></span>
## Uninstall NVIDIA Tesla driver in Windows instance


1. [Log in to the Windows instance.](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance)

2. Enter Device Manager and then expand "Display adapters".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d9e636ab754589e1c0e18b5ef1ab24ea.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6c71d1733762fef72bdd64ea3d11454.png) </span>

4. Right\-click the NVIDIA\-related driver, and then select "Uninstall Device".

5. Check the "Delete the driver software for this device." option, and then click the "Uninstall" button.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5ca1d495fb2440c64fb2b0c75e73617b.png) </span>
