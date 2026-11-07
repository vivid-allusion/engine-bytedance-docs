---
title: "Installing NVIDIA-Fabric Manager packages"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

The NVIDIA\-Fabric Manager service enables interconnection between multiple graphics cards via NVSwitch. For more information about NVSwitch, visit [NVIDIA official website](https://www.nvidia.com/en-us/data-center/nvlink/).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For instances that support NVSwitch, refer to the feature overview of <a href="https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types">each instance type</a>. If the NVIDIA\-Fabric Manager service corresponding to the GPU driver version is not installed, you may fail to use this type of GPU instance normally.</div>


* <div data-tips="true" data-tips-type="warning">In the pni3l instance type family, instances equipped with two or more GPU cards are configured with an NVLink device by default. If the <code>nvidia-fabricmanager.service</code> status is <code>failed</code>, this is normal and does not affect business operations.</div>


* <div data-tips="true" data-tips-type="warning">When you upgrade the GPU driver for an NVSwitch\-supported instance, upgrading the Fabric Manager is also required. Otherwise, you fail to use the instance. <a href="https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-FAQs#.5aaC5L2V5Y2H57qnTlZJRElBIFRlc2xh6amx5Yqo77yf">How do I upgrade NVIDIA Tesla driver?</a></div>


* <div data-tips="true" data-tips-type="warning">Public images provided by the cloud platform have the NVIDIA\-Fabric Manager package and the devel package installed by default. You only need to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager">start NVIDIA\-Fabric Manager</a> to enable NVSwitch interconnection.</div>


* <div data-tips="true" data-tips-type="warning">Since custom images have no NVIDIA\-Fabric Manager installed, after you use a custom image to create a GPU instance integrated with the NVSwitch, you are required to install the NVIDIA\-Fabric Manager package that matches the GPU driver version.</div>



<span id=".5q2l6aqk5LiA77ya5a6J6KOFTlZJRElBLUZhYnJpYyBNYW5hZ2Vy"></span>
## Step 1: Install NVIDIA\-Fabric Manager

You can install the NVIDIA\-Fabric Manager service via the installation package or source code. In the following example, the GPU driver of version 470.57.02 is used to describe how to install and start the NVIDIA\-Fabric Manager service. To download a GPU driver of a different version, replace the version number in the commands with the corresponding version number of the GPU driver. You can execute the `nvidia-smi` command to view the GPU driver version.

<span id=".5pa55byP5LiA77ya6YCa6L-H5a6J6KOF5YyF5a6J6KOF"></span>
### Method 1: Install via installation package


* CentOS 8.x

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/rhel8/x86_64/nvidia-fabric-manager-470.57.02-1.x86_64.rpm
   rpm -ivh nvidia-fabric-manager-470.57.02-1.x86_64.rpm
   ```
   

* CentOS 7.x

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/rhel7/x86_64/nvidia-fabric-manager-470.57.02-1.x86_64.rpm
   rpm -ivh nvidia-fabric-manager-470.57.02-1.x86_64.rpm
   ```
   

* Ubuntu 20.04

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2004/x86_64/nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   dpkg -i nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   ```
   

* Ubuntu 18.04

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu1804/x86_64/nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   dpkg -i nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   ```
   

* Debain 10, veLinux 1.0

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/debian10/x86_64/nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   dpkg -i nvidia-fabricmanager-470_470.57.02-1_amd64.deb
   ```
   


<span id=".5pa55byP5LqM77ya6YCa6L-H5rqQ5a6J6KOF"></span>
### Method 2: Install via source code


* CentOS 8.x

   ```Plain Text
   dnf config-manager --add-repo http://developer.download.nvidia.com/compute/cuda/repos/rhel8/x86_64/cuda-rhel8.repo
   dnf module enable -y nvidia-driver:470
   dnf install -y nvidia-fabric-manager-0:470.57.02-1
   ```
   

* CentOS 7.x

   ```Plain Text
   yum -y install yum-utils 
   yum-config-manager --add-repo https://developer.download.nvidia.cn/compute/cuda/repos/rhel7/x86_64/cuda-rhel7.repo
   yum install -y nvidia-fabric-manager-470.57.02-1
   ```
   

* Ubuntu 20.04

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2004/x86_64/cuda-ubuntu2004.pin
   mv cuda-ubuntu2004.pin /etc/apt/preferences.d/cuda-repository-pin-600
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
   apt-key add 7fa2af80.pub
   rm 7fa2af80.pub
   echo "deb http://developer.download.nvidia.cn/compute/cuda/repos/ubuntu2004/x86_64 /" | tee /etc/apt/sources.list.d/cuda.list
   apt-get update
   apt-get -y install nvidia-fabricmanager-470=470.57.02-1
   ```
   

* Ubuntu 18.04

   ```Plain Text
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
   mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
   wget https://developer.download.nvidia.cn/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
   apt-key add 7fa2af80.pub
   rm 7fa2af80.pub
   echo "deb http://developer.download.nvidia.cn/compute/cuda/repos/ubuntu1804/x86_64 /" | tee /etc/apt/sources.list.d/cuda.list
   apt-get update
   apt-get -y install nvidia-fabricmanager-470=470.57.02-1
   ```
   


<span id=".5q2l6aqk5LqM77ya5a6J6KOFTnZpZGlhLUZhYnJpYy1NYW5hZ2VyLWRldmVs"></span>
## Step 2: Install Nvidia\-Fabric\-Manager\-devel


* CentOS 7.x/8.x

   `yum install nvidia-fabric-manager-devel-470.57.02-1 -y`

* Ubuntu 20.04/18.04, Debain 10, veLinux 1.0

   `dpkg -i nvidia-fabric-manager-devel-470.57.02-1_amd64.deb`


<span id=".5q2l6aqk5LiJ77ya5ZCv5YqoTlZJRElBLUZhYnJpYyBNYW5hZ2Vy"></span>
## Step 3: Start NVIDIA\-Fabric Manager


1. Execute the following command to start the Fabric Manager service.

   `sudo systemctl start nvidia-fabricmanager`

2. Execute the following command to check whether the Fabric Manager service starts as expected. If the output is `active (running)`, the service starts as expected.

   `sudo systemctl status nvidia-fabricmanager`

3. Execute the following command to specify that the Fabric Manager service starts automatically when the instance starts.

   `sudo systemctl enable nvidia-fabricmanager`
