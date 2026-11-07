---
title: "Uninstalling NVIDIA-Fabric Manager software packages"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Fabric-Manager"
---

In the example provided in this topic, the GPU driver of version 470.57.02 is used to describe how to uninstall NVIDIA Fabric Manager\-related packages.

<span id=".5Y246L29TlZJRElBLUZhYnJpYyBNYW5hZ2Vy"></span>
## Uninstall NVIDIA\-Fabric Manager


* CentOS 7.x/8.x

   `yum remove nvidia-fabric-manager-470.57.02`

* Ubuntu 20.04/18.04, Debain 10, veLinux 1.0

   `dpkg -r nvidia-fabricmanager-470`


<span id=".5Y246L29TnZpZGlhLUZhYnJpYy1NYW5hZ2VyLWRldmVs"></span>
## Uninstall Nvidia\-Fabric\-Manager\-devel


* CentOS 7.x/8.x

   `yum -y remove nvidia-fabric-manager-devel`

* Ubuntu 20.04/18.04, Debain 10, veLinux 1.0

   `dpkg -r nvidia-fabricmanager-dev-470`


<span id="tjdPT0D6"></span>
## Use the cloud assistant to uninstall NVIDIA\-Fabric Manager

For details, refer to [Uninstalling Tesla drivers installed via cloud assistant](https://docs.byteplus.com/en/docs/gpu/Uninstalling-NVIDIA-Tesla-drivers#rbBKXSiB).
