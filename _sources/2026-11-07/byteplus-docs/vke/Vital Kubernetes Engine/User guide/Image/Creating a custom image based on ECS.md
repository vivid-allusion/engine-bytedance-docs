---
title: "Creating a custom image based on ECS"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-custom-image-based-on-ECS"
---

In the cloud\-native era, the growing diversity of business scenarios demands advanced capabilities from container platforms, including the ability to provision cluster nodes by using custom images and swiftly deploy nodes with identical configurations. This topic describes how to quickly create a custom image from an Elastic Compute Service (ECS) instance.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The snapshot feature has been enabled. For details, see [Snapshots](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots).

* The resources required to create an ECS instance, such as a Virtual Private Cloud (VPC) and instance specification, have been made available.

* The link to a target GPU driver has already been obtained for use in this example. You can get a target driver link from [NVIDIA](http://www.nvidia.com/Download/Find.aspx).

* Other items to be included in the custom image (such as a container image and custom application) have been made ready.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* **Disclaimer: Custom images are non\-standard environments for which  does not provide official support or ongoing maintenance**. For detailed disclaimer statements regarding custom images, see [Disclaimers](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

* Currently, this solution is applicable only to General\-purpose and GPU Accelerated instances. To create a custom image based on a **High Performance Computing Optimized** ECS instance, please [submit a ticket](https://console.byteplus.com/workorder/create).

* When you create a custom image for a GPU Accelerated instance, ensure the selected public base image strictly matches the instance specification to prevent compatibility issues, such as networking anomalies.

* Do not modify `/etc/fstab`.

* You can create a custom image only by using base images (**kernel 5.4 is recommended**) provided by Vital Kubernetes Engine (VKE). For a list of available base images, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images).

* We recommend that you use a new node as the base for custom image creation. This prevents node initialization issues  caused by residual data from prior node usage.

* If you are adding existing nodes, verify that the available capacity of the system volume exceeds the image volume capacity. To avoid failures in adding an existing server as a cluster node, we recommend that you use a system volume that has at least 10 GiB of free space beyond the image capacity.

* To prevent node creation failures, ensure that your custom image fits within the system volume capacity of the node pool.

* To ensure that multiple NVSwitch\-compatible GPUs (for example, A100 and A800) can be interconnected via NVSwitch, you can install and start the NVIDIA\-Fabric Manager that matches the GPU driver version on GPU nodes. For more details, see [installing the NVIDIA-Fabric Manager](https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager).

* To prevent production disruptions from modifying operating system parameters, test and verify your changes thoroughly in a test environment before applying your changes to production.

* For custom and shared images based on ‌veLinux 2.0 or later, or Ubuntu 22.x or later, cgroupv2 is enabled by default in Kubernetes v1.30 and later. To use cgroupv1, [submit a ticket](https://console.byteplus.com/workorder/create).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu6LWVjcy3lrp7kvos="></span>
### Step 1: Create an ECS instance


1. Log in to the [ECS console.](https://console.byteplus.com/ecs/instance)

2. In the left navigation bar, click **Instances & Images \> Instances** to open the Instances page.

3. Click **Create instance**. Follow the wizard to configure instance settings.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This step describes only the key configuration items for creating an ECS instance, including the instance specification, image, Elastic IP (EIP) address, and the login method. For detailed parameter settings for creating an ECS instance, see <a href="https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances">Purchasing an instance by following the wizard</a>.   </div>
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Instance type |Select an instance type that suits your business scenario. Different instance types offer varied network and storage performance levels. For details, see [Instance types](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types). In this example scenario, the GPU Accelerated `ecs.g1te.xlarge` specification is selected. |
   |Image |Select an image. An image provides an operating system and essential application data for the ECS instance. Available images vary by region and instance specification. For public images available to individual regions of VKE, see [Overview of operating system images](https://docs.byteplus.com/en/docs/vke/Overview-of-operating-system-images). |
   

   
   |**Parameter** |**Description** |
   |---|---|
   |EIP |By default, an EIP address is automatically allocated to the instance upon creation to allow access to the instance over the Internet. In this scenario, the default configuration is retained. |
   

   
   |**Parameter** |**Description** |
   |---|---|
   |Login methods |Set the type of credentials for logging in to the ECS instance. In this example, select **Password**, set a password for the root user, and confirm the password.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please remember the password. If you forget your password, you can reset it in the ECS console.</div><br> |
   


<span id=".5q2l6aqk5LqM77ya6Ieq5a6a5LmJ6YWN572u6ZWc5YOP"></span>
### Step 2: Configure custom image settings

After you have created the ECS instance, configure custom image settings based on your business scenario. Typical configurations include installing an NVIDIA driver, a container image, or custom applications. This scenario installs a GPU driver. You can also add your own custom settings.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Installations in this step vary based on your actual business requirements. After you complete all installations, proceed with the subsequent steps.</div>


* <div data-tips="true" data-tips-type="tip">The GPU driver to be installed must match the GPU model. Never directly use the GPU driver link provided in the following example. For a complete, detailed GPU driver installation example, see <a href="https://docs.byteplus.com/en/docs/gpu/Installing-GPU-drivers">Installing GPU drivers</a>.</div>


1. Log in to the [NVIDIA driver download page](http://www.nvidia.com/Download/Find.aspx). Select the preferred operating system and the CUDA version to get the GPU driver link.

2. Log in to the ECS instance through the console or SSH tool. For details, see [Logging in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Logging-on-to-a-Linux-instance).

3. Download the GPU driver package by using the GPU driver link that you got previously. The following line is an example command:

   ```Bash
   wget https://us.download.nvidia.com/tesla/470.161.03/NVIDIA-Linux-x86_64-470.161.03.run
   ```
   

3. Run the following command to run the driver installer. Follow the on\-screen prompts to complete the installation.

   ```Bash
   sh NVIDIA-Linux-x86_64-470.161.03.run
   ```
   

4. After installation is complete, execute the following command to verify the installation. If the returned information is similar to the GPU information shown below, the driver has been installed successfully.

   ```Bash
   nvidia-smi
   ```
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_868cebe9fd4118c9f5b33111bdd7b2a6.png) </span>


<span id=".5q2l6aqk5LiJ77ya5riF6ZmkLWNsb3VkLWluaXQt6YWN572u"></span>
### Step 3: Clear the Cloud\-Init configuration

Execute the following command to delete the `/var/lib/cloud` file and clear the Cloud\-Init configuration. If you do not delete the file, ECS instances created by using the custom image cannot have instance information (such as hostnames and passwords) injected.

```Bash
rm -rf /var/lib/cloud
echo -n > /etc/machine-id
```


<span id=".5q2l6aqk5Zub77ya5YWz6ZSu5L6d6LWW6aG55qOA5p-l"></span>
### Step 4: Check critical dependencies

VKE provides a dependency check to ensure the availability of custom images in VKE. You can run the following command to perform an environment check for key dependencies of VKE:

```Bash
wget -qc https://tailor-vke.tos-cn-beijing.volces.com/tailor-vke-detection.tar.gz && tar -zxvf tailor-vke-detection.tar.gz && cd test/os && bash build1.sh
```


The expected output is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5414f7426ed6c28aae38d487e680f0a3.png) </span>

If all checks **pass**, proceed to export the image. If there are dependencies that fail the check, you must resolve all the issues before you can export the image.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">These checks may not capture all evolving business requirements. We recommend that you perform thorough validation in your test environment before production deployment.</div>


<span id=".5q2l6aqk5LqU77ya77yI5p2h5Lu25Y-v6YCJ77yJ5YGc5q2i5a6e5L6L"></span>
### Step 5: (Optional) Stop the instance

Stop the ECS instance by following the steps described in [Stopping an instance](https://docs.byteplus.com/en/docs/ecs/Stopping-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you create a custom image using an ESSD, you can skip this step.</div>


<span id=".5q2l6aqk5YWt77ya5a-85Ye66Ieq5a6a5LmJ6ZWc5YOP"></span>
### Step 6: export the custom image


1. Return to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left navigation bar, click **Instances & Images \> Instances** to open the Instances page.

3. In the Actions column on the right side of the target instance, click `...`  \> **Volumes & Image \> Create custom image**.

4. Set an image name and then click **Confirm** to begin exporting the custom image.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Exporting a custom image takes some time. You can go back to the custom image list to view the progress.</div>


<span id=".5q2l6aqk5LiD77ya5re75Yqg5o-P6L-w5L-h5oGv"></span>
### Step 7: Add a description

To make a custom image available for reference by VKE, you need to declare the description `SYS_SUPPORT_VKE`.


1. Log in to the [ECS console.](https://console.byteplus.com/ecs/instance)

2. In the left navigation bar, click **Instances & Images \> Images** to go to the Images page.

3. Click the **Custom Image** tab and click the name of the target image to go to the custom image details page.

4. In the **Basic information** section, click the Edit icon next to the Description field, enter `SYS_SUPPORT_VKE` in the field, and then click the check mark to save the change.


<span id=".5ZCO57ut5pON5L2c"></span>
## Subsequent operations

Now that you have created a custom image from an ECS instance, you can create a node pool by using the custom image. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

&nbsp;
