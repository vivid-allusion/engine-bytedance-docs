---
title: "Quickly installing Tesla drivers in created instances"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Quickly_installing_Tesla_drivers_in_created_instances"
---

<span id="IFU0jeG3"></span>
## Background

To ensure that a GPU instance runs properly, you need to install the appropriate infrastructure software in advance. For NVIDIA Tesla series GPUs, the following software packages are needed:


* Hardware driver program: used to drive GPUs.

* Libraries: required by upper\-layer applications.


For general\-purpose computation scenarios, like deep learning and AI, or graphics acceleration scenarios like OpenGL, Direct3D, and cloud gaming, GPU instances can offer high\-performance computing capabilities or display smoother graphics only with the Tesla driver installed.

<span id="y6EVOqZA"></span>
## Installation method

For the GPU instance types provided by the platform and their release details, refer to [GPU instance type family lists](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types#FZuiXLTc).


|Installation method |Description |
|---|---|
|Method 1: Use the cloud assistant to batch install drivers |If you only need to install the GPU drivers installed in images for GPU instances, not the CUDA/cuDNN libraries, you can install them in a batch in created GPU instances by executing a public command via the cloud assistant. |
|Method 2: Select a public image with a pre\-installed driver when you change the instance operating system |On the Replace operating system page, in the image selection step, select Public Image and then check the "Automatically install GPU driver in the background" option. |


<span id="cNqrNWRv"></span>
### Method 1: Use the cloud assistant to batch install drivers

**List of recommended driver versions**

You can use the cloud assistant to install NVIDIA GPU drivers and Fabric Manager. Supported GPU driver versions provided by the system are listed below. If you need a custom driver version, provide the download address of the corresponding driver installation package.


|**GPU driver**<br><br> |**Supported public images** |**Supported GPU instance type families** |**Whether with Fabric Manager installed** |
|---|---|---|---|
|570.86.15 |* Ubuntu 22.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 |* gni3cg/gni3cgd<br><br>* gni3cl<br><br>* gna3c<br><br>* gni3c<br><br>* ebmgni3c<br><br>* gni3/ebmgni3<br><br>* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3ln<br><br>* ebmhpcpni3l<br><br>* hpcpni3le |Yes |
|550.144.03 |* Ubuntu 22.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 ||Yes |
|550.127.05 |veLinux 1.0 ||Yes |
|535.230.02 |* Ubuntu 22.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 ||Yes |
|535.216.03 |veLinux 1.0 ||Yes |


**Usage notes**


* After the GPU driver is installed, the system restarts the associated instance by default. Restarting the instance is recommended, since this ensures that the GPU driver takes effect. If you wish not to restart, specify the IS_REBOOT value as false.

* If you stop or restart the instance before the GPU driver is finished installing, driver installation will be interrupted. After startup, the instance will neither have the GPU driver installed nor resume the installation.

* If the GPU instance can not access the address of the driver installation package you provided via the intranet, this may incur public network fees. Download time will be affected by the public network bandwidth.


**Procedure**

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The instance must be in the <strong>Running</strong> (<code>Running</code>) status.</div>


* <div data-tips="true" data-tips-type="default">Cloud assistant Agent is installed. For operation details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client">Installing cloud assistant Agent</a>.</div>


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the top menu bar, select the region where your business is located.

3. In the left\-side navigation pane, select "Maintenance & Monitoring \> Cloud Assistant" and then select the "Public commands" tab.

4. Find the target command for installing the Tesla GPU driver, and then click the "Create a job" button. Command\-related parameters and related descriptions are listed below. For more parameters, refer to [Creating jobs](https://docs.byteplus.com/en/docs/ecs/Creating-a-job#.5pON5L2c5q2l6aqk).

&nbsp;

   
   |**Parameter name** |**Type** |**The description.**  |
   |---|---|---|
   |DRIVER_VERSION<br><br> |String |Specifies GPU driver version. Default value: 535.230.02.<br><br>If you wish to install a recommended GPU driver version, enter its version number based on the list of recommended driver versions. |
   |DRIVER_PATH<br><br> |String |Specifies the custom path of GPU driver installation package. Default value: empty_path.<br><br>If you want to install a GPU driver version not in the list of recommended driver versions, specify the path of the GPU driver installation package. For example, you can enter a TOS address path, which supports access by ECS instances.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you specify DRIVER_VERSION and DRIVER_PATH at the same time, the driver is installed as specified by DRIVER_PATH.</div><br> |
   |IS_REBOOT |String |Determines whether to restart the instance. Default value: true.<br><br>If you do not want to restart the instance after installing the driver, enter "false". Restarting the instance is recommended, since this ensures that the GPU driver takes effect. |
   |IS_FABRIC |String |Determines whether to install Fabric Manager. Default value: true.<br><br>The system defaults to installing Fabric Manager. If you need Fabric Manager not to be installed, enter "false". |
   |FABRIC_PATH<br><br> |String |Specifies a custom path of the Fabric Manager installation package. Default value: empty_path.<br><br><br>* If you have specified the DRIVER_VERSION and need to install Fabric Manager, leave FABRIC_PATH empty. Then, the corresponding configuration is matched by default.<br><br>* If you have specified the DRIVER_PATH and also need to install Fabric Manager, specify FABRIC_PATH and FABRIC_DEV_PATH accordingly (such as a TOS address path that can be accessed by ECS instances). Otherwise, Fabric Manager is not installed. |
   |FABRIC_DEV_PATH<br><br> |String |Specifies a custom path of the Fabric Manager DEV package. Default value: empty_path.<br><br><br>* If you have specified the DRIVER_VERSION and need to install Fabric Manager, leave FABRIC_DEV_PATH empty. Then, the corresponding configuration is matched by default.<br><br>* If you need a custom GPU driver version and Fabric Manager, specify FABRIC_PATH and FABRIC_DEV_PATH accordingly (such as a TOS address path that can be accessed by ECS instances). Otherwise, Fabric Manager is not installed. |
   

6. After the job is created, the GPU driver and NVIDIA Fabric Manager are installed automatically.


<span id="q16oLGbp"></span>
### Method 2: Select a public image with a pre\-installed driver when you change the instance operating system


1. [When you change the instance operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS), select a public image with a pre\-installed driver in the image selection step.

2. After change, [log in to the instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

3. Execute the `nvidia-smi` command to verify whether the driver is installed.
