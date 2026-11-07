---
title: "NVIDIA driver FAQ"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-FAQs"
---

<span id=".TlZJRElBIFRlc2xh6amx5Yqo6Zeu6aKY"></span>
## FAQ about NVIDIA Tesla driver

<span id=".5ZOq5Lqb5a6e5L6L6ZyA6KaB5a6J6KOFTlZJRElBIFRlc2xh6amx5Yqo77yf"></span>
### For which instances do I need to install NVIDIA Tesla driver?

For general\-purpose computation, we recommend installing the NVIDIA Tesla driver (GPU driver, CUDA toolkit, and other related components) on Compute\-optimized and HPC\-optimized instances. For installation instructions, refer to [Nvidia driver installation guide](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide).

<span id=".5a6e5L6L5aaC5L2V5a6J6KOFR1BV6amx5Yqo77yf"></span>
### How to install the Tesla driver in an instance?

For the Tesla driver installation method, refer to [Nvidia driver installation guide](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide).

<span id=".TnZpZGlh6amx5Yqo5a6J6KOF5oiQ5Yqf77yM5L2G5omn6KGMbnZpZGlhLXNtaeWRveS7pOaXoOaViO-8jOaYvuekuumpseWKqOacquWuieijhe-8jOivpeWmguS9leaOkuafpe-8nw=="></span>
### After installing the Nvidia driver, I failed to execute the `nvidia-smi` command, and the driver was reported not installed. How should I troubleshoot this issue?

**Analysis**: If the kernel\-devel and kernel versions are different, a compilation error may occur when the RPM package is being installed.

**Solution**: Execute the `rpm -qa | grep $(uname -r)` command in the instance to view the version numbers of kernel and kernel\-devel. Then, check whether their versions are the same. If not, download the corresponding kernel\-devel package from an official channel, and then reinstall the driver.

<span id=".5omn6KGMbnZpZGlhLXNtaeWRveS7pOafpeeci-eahENVREHniYjmnKzlkozlrp7pmYXnmoTlronoo4XniYjmnKzkuLrkvZXkuI3kuIDoh7TvvJ8="></span>
### Why is the CUDA version returned after executing the `nvidia-smi` command different from the one I actually installed?

The CUDA version returned after the `nvidia-smi` command is executed indicates the maximum CUDA version supported by your GPU instance, not the CUDA version you have actually installed.

<span id=".5aaC5L2V5p-l6K-iR1BV5pi-5Y2h55qE6K-m57uG5L-h5oGv77yf"></span>
### How to view detailed information about a GPU graphics card?

To view GPU graphics card information on GPU instances of different operating systems, follow these steps:


* For Linux instances, execute the `nvidia-smi` command.

* For Windows instances, view related information in the Device Manager.


To learn how GPU cards operate and are utilized, refer to [Cloud Monitor overview](https://docs.byteplus.com/en/docs/gpu/Cloud-Monitor-overview).

<span id=".5Li65LuA5LmIQTEwMC9BODAw5pi-5Y2h6Ze0572R57uc5peg5rOV5LqS6YCa77yf"></span>
### Why is there no network connectivity between A100/A800 graphics cards?

If an instance is equipped with multiple A100/A800 graphics cards, you need to install the NVIDIA\-Fabric Manager package first to enable interconnection between graphics cards via NVSwitch.


* Public images have the NVIDIA\-Fabric Manager package installed by default. To enable interconnection between graphics cards for public image\-based instances, you only need to [start NVIDIA-Fabric Manager](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager#.5q2l6aqk5LiJ77ya5ZCv5YqoTlZJRElBLUZhYnJpYyBNYW5hZ2Vy).

* If you create a GPU instance that is equipped with multiple A100/A800 graphics cards based on a custom image (which does not have a NVIDIA\-Fabric Manager package preinstalled), install the NVIDIA\-Fabric Manager package that matches the GPU driver version first. Otherwise, you may fail to use the instance normally. For instructions, refer to [Installing NVIDIA-Fabric Manager packages](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager).


<span id=".5aaC5L2V5p-l55yLTlZTd2l0Y2ggR1BV5pi-5Y2h6Ze05bim5a6977yf"></span>
### How to check the bandwidth between NVSwitch\-connected GPU graphics cards?

Instances equipped with A100/A800 graphics cards support interconnection via NVSwitch. To learn more about NVSwitch GPU\-to\-GPU bandwidth, access the [official NVIDIA website](https://www.nvidia.com/en-us/data-center/nvlink/).

<span id=".5aaC5L2V5Y2H57qnTlZJRElBIFRlc2xh6amx5Yqo77yf"></span>
### How do I upgrade NVIDIA Tesla driver?

If the version of the installed Tesla driver in your GPU instance does not match the current scenario, or if you can not access your GPU instance due to an inappropriate type or version of the installed driver, you can upgrade the Tesla driver. To upgrade the Tesla driver, you need to uninstall the current Tesla driver first and then install the new version.


1. Uninstall the Tesla driver.

   1. [Uninstall the GPU driver and CUDA toolkit](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers).

   2. (Conditionally required​) [Uninstall the NVIDIA-Fabric Manager software package](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Fabric-Manager). If your GPU instance supports NVSwitch (for example, A100/A800 graphics cards), you need to uninstall the NVIDIA\-Fabric Manager package.

2. Install the new Tesla driver.

   1. [Install the GPU driver](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers).

   2. [Install the CUDA toolkit](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits).

   3. (Conditionally required​) [Install the NVIDIA-Fabric Manager package](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager). Iff your GPU instance supports NVSwitch (for example, A100/A800 graphics cards), you need to install the NVIDIA\-Fabric Manager package that matches the GPU driver version. Otherwise, you may fail to use the GPU instance normally.


<span id=".TlZJRElBIEdSSUTpqbHliqjpl67popg="></span>
## FAQ about NVIDIA GRID driver

<span id=".5ZOq5Lqb5a6e5L6L5o6o6I2Q5a6J6KOFTlZJRElBIEdSSUTpqbHliqjvvJ8="></span>
### For which instances is it recommended to install NVIDIA GRID driver?

Rendering instances. This helps meet the needs of graphics processing (such as 3D rendering and video encoding/decoding). For information about rendering instance families, refer to [Instance types](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types).

<span id=".R1BV6K6h566X5Z6L5a6e5L6L5pSv5oyB5a6J6KOFR1JJROmpseWKqOWQl--8nw=="></span>
### Can I install the GRID driver on a GPU Accelerated instance?

Yes, you can. GRID driver is used to obtain graphics acceleration capabilities of GPU cards, applicable for graphics computing scenarios like OpenGL. You need to purchase an NVIDIA GRID License through official NVIDIA channels before installation. For detailed instructions, refer to [Installing NVIDIA GRID drivers](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers).

<span id=".5Li65LuA5LmIV2luZG93c-ezu-e7n-eahEdQVeWunuS-i-WuieijhUdSSUTpqbHliqjlkI7vvIzkvb_nlKhWTkPnmbvlvZXlh7rnjrDpu5HlsY_vvJ8="></span>
### When I use VNC to log in to a Windows\-based GPU instance with GRID driver installed, the screen turns black. Why?

After you install the GRID driver on a Windows\-based GPU instance, the display output of the VM is managed by the GRID driver. As a result, VNC can no longer capture the display feed from the integrated graphics card, causing a black screen on VNC, which is normal. We recommend logging in to the GPU instance via ECS Terminal. For more information, see [Using the console to log in to a Windows instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Windows-instance).

<span id=".5aaC5L2V5Y2H57qnTlZJRElBIEdSSUTpqbHliqjvvJ8="></span>
### How to upgrade the NVIDIA GRID driver?

If the installed GRID driver version can not meet your business requirements, you can:


1. First, [uninstall the GRID driver](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-GRID-drivers).

2. Obtain the new GRID driver installation package through the official NVIDIA channel, and then [install the GRID driver](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-GRID-drivers#.5q2l6aqk5LiJ77ya5a6J6KOFR1JJROmpseWKqA==).


<span id=".TnZpZGlhIEVDQyBNb2Rl6Zeu6aKY"></span>
## FAQ about Nvidia ECC Mode

<span id=".5LuA5LmI5pivRUNDIE1vZGU_"></span>
### What is ECC Mode?

ECC (Error Correcting Code) is a technology for detecting and correcting memory errors. After ECC Mode is enabled via the GPU driver, a portion of the video memory is used as check bits to detect data corruption. Typically, data corruption can be automatically corrected. If automatic corrections fail, which also indicates that UE (Uncorrectable Error) occurs in video memory, the bad block will be avoided via [Dynamic Page Retirement](https://docs.nvidia.com/deploy/dynamic-page-retirement/index.html#overview) or [Row Remapping](https://docs.nvidia.com/deploy/a100-gpu-mem-error-mgmt/index.html#row-remapping).

<span id=".5aaC5L2V5p-l55yL5a6e5L6L55qERUND54q25oCB77yf"></span>
### How to view the ECC status of an instance?

[Log in to the GPU instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance), and then execute the following command. After this, you can view the current ECC status.

```Plain Text
nvidia-smi -q -d ecc
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6632c4354495b5b7fa982fd3d43be8d8.png) </span>

<span id=".5LuA5LmI5oOF5Ya15LiL5bqU6K-l5YWz6Zet5oiW6ICF5omT5byARUND77yf"></span>
### When should ECC be enabled or disabled?

In general, it is recommended to disable ECC for rendering workloads and enable ECC for computing workloads. Since ECC itself consumes video memory and causes performance overhead, ECC can be disabled in certain computing scenarios. This can be risky and is generally not recommended.

<span id=".5Li65LuA5LmI5ZyoR1BV5LqR5pyN5Yqh5Zmo5LiK5byA5ZCvL-WFs-mXrUVDQ-S4jeeUn-aViO-8nw=="></span>
### Why does enabling/disabling ECC on a GPU instance fail?

**Issue description**: Some users use a driver to set ECC Mode on a GPU instance, but after they restart the instance, the setting is reported invalid.

**Cause**: Insufficient support for Legacy Persistence Mode in NVIDIA Tesla driver versions 535 and later.

**Solution**: You need to enable the Persistence Daemon to activate the new persistence feature before configuring ECC. The steps are as follows:


1. [Log in to the GPU instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).

2. Execute the following commands to enable Persistence Mode. In this topic, Persistence Mode is enabled as guided in [Persistence Daemon](https://docs.nvidia.com/deploy/driver-persistence/index.html#persistence-daemon).

   ```Bash
   sudo nvidia-persistenced --user <username>    # Run Persistence Daemon ("username" is your username)
   nvidia-smi -pm 1                                    # Enable Persistence Mode
   ```
   

3. Execute the following commands to configure ECC.

   ```Bash
   nvidia-smi -pm 0                                   # Disable Persistence Mode
   nvidia-persistenced --persistence-mode            # Start Persistence Daemon
   nvidia-smi -e 1                                    # Enable ECC Mode (1=Enable, 0=Disable)
   reboot now                                        # Restart OS
   ```
   

4. Log in to the instance again, and then execute the following command to view the ECC status.​

   ```Plain Text
   nvidia-smi -q -d ecc
   ```
