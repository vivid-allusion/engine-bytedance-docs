---
title: "Automatically installing Tesla driver during instance creation"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Automatically_installing_Tesla_drivers_during_instance_creation"
---

<span id="wlENGBXj"></span>
## Background

To ensure that a GPU instance runs properly, you need to install the appropriate infrastructure software in advance. For NVIDIA Tesla series GPUs, the following software packages are needed:


* Hardware driver program: used to drive GPUs.

* Libraries: required by upper\-layer applications.


For general\-purpose computation scenarios, like deep learning and AI, or graphics acceleration scenarios like OpenGL, Direct3D, and cloud gaming, GPU instances can offer high\-performance computing capabilities or display smoother graphics only with the Tesla driver installed.

<span id="ii1qfOwT"></span>
## Installation methods

For ease of use, on the instance purchase page, multiple methods are available for you to install GPU drivers and associate CUDA and cuDNN. When you purchase GPU instances, select an appropriate method of driver deployment based on your business needs. For the GPU instance types provided by the platform and their release details, refer to [GPU instance type family lists](https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types#FZuiXLTc).


|Installation methods |Description |
|---|---|
|Method 1: Configure the driver to be automatically installed after you select a public image of the standard version |On the instance purchase page, in the image selection step, select a public image of the standard version and then check the "Automatically install GPU driver in the background" option. |
|Method 2: Use a public image of the GPU version with a pre\-installed Tesla driver |On the instance purchase page, in the image selection step, select a public image of the GPU version with a pre\-installed Tesla driver. |
|Method 3: Configure the driver to be installed via custom data after you select a public image of the standard version |On the instance purchase page, in the image selection step, select a public image of the standard version, and enter the driver installation script via custom data to have the driver automatically installed when the instance starts. |


<span id=".5pa55byP5LiA77ya5ZCO5Y-w6Ieq5Yqo5a6J6KOFR1BV6amx5Yqo"></span>
### Method 1: Configure the driver to be automatically installed after you select a public image of the standard version

<span id="hKAAJFUd"></span>
#### Usage notes


|Stage |Description |
|---|---|
|Purchasing instances |* If you need to batch purchase instances with GPU drivers installed, we recommend that you first purchase an instance with the "Automatically install GPU driver in the background" feature enabled. Then,[ create a custom image](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance) based on the purchased instance, and use the custom image to batch purchase instances (no need to enable the "Automatically install GPU driver in the background" feature). This shortens the duration of installing GPU drivers.<br><br>* If you stop or restart the instance before finishing installing the GPU driver, driver installation will be interrupted. After startup, the instance will neither have the GPU driver installed nor resume the installation.<br><br>* When GPU drivers are automatically installed, driver installation packages are downloaded. We recommend that the size of your system volumes be at least 40 GB to avoid installation failure due to insufficient volume space. |
|Instance usage |* If you use the instance with the "Automatically install GPU driver in the background" option enabled when creating a custom image, the created image has the GPU driver, CUDA, and cuDNN libraries pre\-installed.<br><br>* When you change the operating system of an instance with a GPU driver automatically installed, if you have enabled the "Automatically install GPU driver in the background" option, the system then reinstalls the GPU driver.<br><br>* If default driver versions can no longer meet your business requirements, you can [uninstall the NVIDIA driver](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers), [manually install a GPU driver](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers), and then [install the CUDA toolkit](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits). |


<span id="mp0AZfnP"></span>
#### Procedure


1. Go to the[ instance purchase page](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance?). 

2. Select the GPU instance type you need to purchase.

3. When you configure the parameter **Image**, select **Public Images**, and then select a Linux public image or a veLinux public image of the standard version.

4. Select the "Automatically install GPU driver in the background" option, and then select the driver version. This allows the system to automatically install the specified version of the GPU driver, CUDA, and cuDNN libraries.

   The installation process is time\-consuming​, causing a longer instance startup time. During the process, the instance is automatically restarted. The process from creating the instance to installing the driver successfully lasts about 15 to 20 minutes in total.

5. Configure remaining parameters to complete the purchase. For parameter details, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="FeNrLyHk"></span>
#### Image list

Supported public images and their corresponding driver versions are listed below. Images available for selection differ by instance type. For the actual available images, refer to the information on the instance purchase page.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Certain public images of the standard version are selectable when you purchase GPU instances. However, these images do not have GPU drivers pre\-installed and do not support installing drivers automatically in the background. Therefore, you need to manually install the needed driver after the instance based on such an image is created. In the example shown below, the public image, Windows Server 2022 Datacenter Edition 64 bit Chinese, can be used to purchase the GPU Accelerated gni3cl. However, the gni3cl created based on this image does not have any driver installed. In this case, after creating the instance, you need to manually <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">install the GPU driver</a> and <a href="https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits">the CUDA toolkit</a>. After this, you can use the instance properly.</div>



|GPU driver |CUDA version |cuDNN version |Supported public images |Supported GPU instance type families |Whether with Fabric Manager installed |
|---|---|---|---|---|---|
|580.105.08 |13.0.2 |9.17.1.4<br><br> |Ubuntu 24.04 |* gni3c/ebmgni3c |No |
||||* veLinux 2.0<br><br>* Ubuntu 22.04<br><br>* Debian 12<br><br>* Rocky Linux 9.1<br><br>* Rocky Linux 8.8 |* gni3cl<br><br>* gni3c/ebmgni3c |No |
||||* veLinux 2.0<br><br>* Ubuntu 22.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 |* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3l |Yes |
|570.86.15 |12.8.0 |9.8.0.87 |Ubuntu 24.04 |* gni3c/ebmgni3c<br><br>* gni3/ebmgni3 |No |
||||* veLinux 2.0<br><br>* Ubuntu 22.04<br><br>* Ubuntu 20.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 |* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3l<br><br>* hpcpni3le |Yes |
||||* veLinux 2.0<br><br>* Ubuntu 22.04<br><br>* Ubuntu 20.04<br><br>* Debian 12<br><br>* Rocky Linux 9.1<br><br>* Rocky Linux 8.8<br><br><br> |* gni3cl<br><br>* gni3c<br><br>* ebmgni3c |No |
|550.144.03 |12.4.1 |9.2.1.18 |Ubuntu 24.04 |* gni3c/ebmgni3c |No |
||||* Ubuntu 22.04<br><br>* Ubuntu 20.04<br><br>* Debian 12<br><br>* Rocky Linux 8.8 |* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3l<br><br>* hpcpni3le |Yes |
||||* Ubuntu 22.04<br><br>* Ubuntu 20.04<br><br>* Debian 12<br><br>* CentOS 7.9<br><br>* Rocky Linux 9.1<br><br>* Rocky Linux 8.8 |* gni3cl<br><br>* gni3c<br><br>* ebmgni3c |No |
|550.127.05 |12.4.1 |9.2.1.18 |* veLinux 1.0<br><br>* Debian 10 |* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3l |Yes |
||||* veLinux 1.0<br><br>* veLinux 1.0 with 5.10 kernel<br><br>* veLinux 1.0 CentOS Compatible<br><br>* Debian 10 |* gni3cl<br><br>* gni3c<br><br>* ebmgni3c |No |
|535.261.03 |12.2.2 |8.9.2.26 |* veLinux 1.0<br><br>* Ubuntu 22.04<br><br>* Rocky Linux 8.8 |* pni3l/pni3ld<br><br>* hpcpni3ln<br><br>* ebmhpcpni3l<br><br>* hpcpni3le |Yes |
||||* veLinux 1.0<br><br>* veLinux 1.0 with 5.10 kernel<br><br>* veLinux 1.0 CentOS Compatible<br><br>* Ubuntu 22.04<br><br>* Ubuntu 20.04<br><br>* CentOS 7.9<br><br>* Rocky Linux 9.1<br><br>* Rocky Linux 8.8 |* gni3cl<br><br>* gni3c/ebmgni3c |No |


<span id="vQ1gg8oI"></span>
### Method 2: Use a public image of the GPU version with a pre\-installed Tesla driver

<span id="YWsMNpAn"></span>
#### Procedure

Typically, a public image of the GPU version with a built\-in driver is named with the suffix "with GPU Driver xx". This indicates that the public image has the corresponding version of the GPU driver installed by default.


1. Go to the[ instance purchase page](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance?). 

2. Select the GPU instance type you need to purchase.

3. When you configure the parameter **Image**, select **Public Images**, and then select a public image of the GPU version.

4. Configure remaining parameters to complete the purchase. For parameter details, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="szFRPbHP"></span>
#### Image list

Public images of the GPU version are listed below. Images available for selection differ slightly by instance type. For the actual available images, refer to the information on the instance purchase page.


<Tabs>
<Tab zoneid="Rkvq8mrEaw" title="Linux images">
<TabTitle>Linux images</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Linux public images of the GPU version have GPU drivers pre\-installed by default. For the CUDA toolkit, after purchasing an instance, you need to log in to the instance and then install it manually. For details, refer to<a href="https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits"> Installing CUDA toolkits</a>.</div>



|**Public image name** |**Applicable instance family** |**GPU driver version (installed by default)**  |**Compatible CUDA version (installed manually)**  |**Whether with Fabric Manager installed** |
|---|---|---|---|---|
|CentOS 8.3 with GPU Driver 535.161.08 and doca 64 bit |* HPC\-optimized ebmhpcpni3l<br><br>* HPC\-optimized hpcpni3ln |Tesla 535.161.08 |12.2 |Yes |
|CentOS 7.8 with GPU Driver 535.129.03 and mlx 5.8\-3 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 535.129.03 |12.2 |Yes |
|CentOS 7.8 with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|CentOS 7.8 with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |
|Ubuntu 22.04 with GPU Driver 535.161.08 and doca 64 bit |* HPC\-optimized ebmhpcpni3l<br><br>* HPC\-optimized hpcpni3ln |Tesla 535.161.08 |12.2 |Yes |
|Ubuntu 20.04 with GPU Driver 535.161.08 and doca 64 bit |* HPC\-optimized ebmhpcpni3l<br><br>* HPC\-optimized hpcpni3ln |Tesla 535.161.08 |12.2 |Yes |
|Ubuntu 20.04 with GPU Driver 535.129.03 and mlx 5.8\-3 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 535.129.03 |12.2 |Yes |
|Ubuntu 20.04 with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|Ubuntu 20.04 with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |
|Ubuntu 18.04 with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|Ubuntu 18.04 with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |
|Debian 10 with GPU Driver 535.129.03 and mlx 5.8\-3 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 535.129.03 |12.2 |Yes |
|Debian 10 with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|Debian 10 with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |
|Rocky Linux 8.8 with GPU Driver 535.161.08 and doca 64 bit |* HPC\-optimized ebmhpcpni3l<br><br>* HPC\-optimized hpcpni3ln |Tesla 535.161.08 |12.2 |Yes |



</Tab>
<Tab zoneid="TjT9kJ7ukH" title="veLinux image">
<TabTitle>veLinux image</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">veLinux public images of the GPU version have GPU drivers pre\-installed by default. For the CUDA toolkit, after creating an instance, you need to log in to the instance and then install it manually. For details, refer to<a href="https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits"> Installing CUDA toolkits</a>.</div>


* <div data-tips="true" data-tips-type="default">If provided driver versions can not meet your business requirements, you can <a href="https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers">uninstall the NVIDIA driver</a> and then <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">reinstall a GPU driver</a>.</div>




|**Public image name** |**Applicable instance family** |**GPU driver version (installed by default)**  |**Compatible CUDA version (installed manually)**  |**Whether with Fabric Manager installed** |
|---|---|---|---|---|
|veLinux 1.0 CentOS Compatible with GPU Driver 535.129.03 and mlx 5.8\-3 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 535.129.03 |12.2 |Yes |
|veLinux 1.0 CentOS Compatible with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|veLinux 1.0 CentOS Compatible with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |
|veLinux 1.0 with GPU Driver 535.129.03 and mlx 5.8\-3 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 535.129.03 |12.2 |Yes |
|veLinux 1.0 with GPU Driver 535.161.08 and doca 64 bit |* HPC\-optimized ebmhpcpni3l<br><br>* HPC\-optimized hpcpni3ln |Tesla 535.161.08 |12.2 |Yes |
|velinux 1.0 with GPU Driver 470.161.03 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.161.03 |11.4 |Yes |
|veLinux 1.0 with GPU Driver 470.129.06 64 bit |* GPU Accelerated<br><br>* HPC\-optimized |Tesla 470.129.06 |11.4 |Yes |





</Tab>
<Tab zoneid="GoxMzKibYU" title="Windows image">
<TabTitle>Windows image</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Windows Server public images provided to you have GPU drivers and the CUDA toolkit pre\-installed by default.</div>


* <div data-tips="true" data-tips-type="default">If provided driver versions can not meet your business requirements, you can<a href="https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers"> uninstall the NVIDIA driver</a>, <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">reinstall a GPU driver</a>, and then <a href="https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits">install the CUDA toolkit</a>.</div>




|**Public image name** |**Applicable instance family** |**GPU driver version (installed by default)**  |**CUDA version (installed by default)**  |
|---|---|---|---|
|Windows Server 2019 Datacenter Edition 64\-bit Chinese (GPU) |GPU Accelerated |Tesla 470.129.06 |11.2 |
|Windows Server 2016 Datacenter Edition 64\-bit Chinese (GPU) |GPU Accelerated |Tesla 470.129.06 |11.2 |



</Tab>
</Tabs>


<span id="1rTgcdc4"></span>
### Method 3: Configure the driver to be installed via custom data after you select a public image of the standard version


1. Go to the [instance purchase page](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance?).

2. Select the GPU instance type you need to purchase.

3. When you configure the parameter **Image**, select **Public Images**, and then select a Linux public image or a veLinux public image of the standard version.

4. Select "**Custom configuration** \> **Advanced configuration** \> **Advanced options**". In the **User data** section, enter the GPU driver installation script.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Refer to the instructions in the <a href="https://docs.byteplus.com/en/docs/gpu/Automatically_installing_Tesla_drivers_during_instance_creation#FeNrLyHk">image list</a> and select the required GPU driver, CUDA, and cuDNN library versions based on the GPU instance type and image you create.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Specify the driver version to be installed via the following parameters. If you do not need to install a specific component (such as CUDA), you can leave the corresponding parameter blank.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>CUDA_VERSION</code>: Indicates the version of CUDA to be installed.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>GPU_DRIVER_VERSION</code>: Indicates the version of the GPU driver to be installed.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><code>CUDNN_VERSION</code>: Indicates the version of the cuDNN library to be installed.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">When creating a GPU instance by using the <a href="https://docs.byteplus.com/en/docs/ecs/RunInstances">RunInstances \- Creates instances</a> operation, you can pass a Base64\-encoded GPU driver installation script through the <code>Userdata parameter</code>. This way, the GPU driver, CUDA, and cuDNN library can be automatically installed when the instance is started for the first time.   </div>
   

   ```Bash
   #!/bin/bash
   CUDA_VERSION=12.4.1
   GPU_DRIVER_VERSION=550.144.03
   CUDNN_VERSION=9.2.1.18
   INSTALL_DIR="/root/auto_install"
   auto_install_script="gpu_driver_install.sh"
   
   MAX_RETRIES=2
   RETRY_COUNT=0
   while [ $RETRY_COUNT -le $MAX_RETRIES ]; do
     REGION=$(wget -O - -a /var/log/wget.log -t 1 --timeout=10 "http://100.96.0.96/latest/region_id" 2>/dev/null)
     if [ -n "$REGION" ]; then
       echo "Successfully obtained REGION: $REGION"
       break
     else
       RETRY_COUNT=$((RETRY_COUNT + 1))
       echo "Failed to obtain REGION, retry count: $RETRY_COUNT"
       sleep 2
     fi
   done
   
   if [ -z "$REGION" ]; then
     echo "Error: Failed to obtain REGION. Please check if the network connection or URL is correct."
     exit 1
   fi
   if [[ "$REGION" == "cn-chengdu-sdv" ]]; then
     script_download_url="https://gpu-install-script.tos-cn-boe.volces.com/${auto_install_script}"
   else
     script_download_url="https://gpu-install-script-${REGION}.tos-${REGION}.ivolces.com/${auto_install_script}"
   fi
   rm -rf $INSTALL_DIR
   mkdir -p $INSTALL_DIR
   cd $INSTALL_DIR
   for i in $(seq 1 10); do
       echo "Attempt $i ..."
       wget --timeout=10 "$script_download_url" && break
   done
   bash ${INSTALL_DIR}/${auto_install_script} $GPU_DRIVER_VERSION $CUDA_VERSION $CUDNN_VERSION
   ```
   

5. Configure remaining parameters to complete the purchase. For parameter details, refer to [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


<span id="zIQ7bxL8"></span>
## Related documents


* If you have not configured the Tesla driver to be automatically installed when purchasing the instance, install the driver manually after you purchase the instance. For detailed operations, refer to:

   * [Installing GPU drivers](https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers)

   * [Installing CUDA toolkits](https://docs.byteplus.com/en/docs/gpu/Installing-CUDA-toolkits)

   * [Installing NVIDIA-Fabric Manager packages](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager)

* To upgrade the Tesla driver version, refer to [How do I upgrade NVIDIA Tesla driver?](https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-FAQs#.5aaC5L2V5Y2H57qnTlZJRElBIFRlc2xh6amx5Yqo77yf)
