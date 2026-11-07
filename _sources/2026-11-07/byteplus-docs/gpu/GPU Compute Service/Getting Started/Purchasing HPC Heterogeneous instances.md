---
title: "Purchasing HPC Heterogeneous instances"
product: "GPU Compute Service"
product_code: "gpu"
source: "https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances"
---

You can purchase HPC\-optimized instances based on your needs.

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits


* The following limits are applicable to HPC\-optimized instances:

   * After you create an HPC\-optimized instance, an RDMA network interface is added to the HPC cluster's RDMA network, built on top of the VPC network. Currently, the default IP address of the RDMA device is in the fixed 198.x.x.x/33.x.x.x CIDR block. You can use this CIDR block for RDMA network communication between multiple HPC\-optimized instances equipped with RDMA network interfaces.

   * After an RDMA network interface is associated with a GPU instance, you cannot mount other RDMA network interfaces to the instance or unmount the RDMA network interface.

   * Communication between the RDMA network interface and the VPC network interface is not allowed. Communication between GPU instances can only be performed in the mode of VPC network interface to VPC network interface or RDMA network interface to RDMA network interface.

   * You cannot mount EIPs to RDMA network interfaces or configure load balancing for RDMA network interfaces.


<span id=".5q2l6aqk5LiA77ya5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k"></span>
## Step 1: Create an HPC cluster

Before you create HPC\-optimized instances, you need to first create an HPC cluster. Subsequently, you can deploy new HPC\-optimized instances in this cluster. However, you are not allowed to add existing ECS instances to the cluster.

For information about how to create an HPC cluster, see [Creating HPC clusters](https://docs.byteplus.com/en/docs/gpu/Creating-HPC-clusters).

<span id=".5q2l6aqk5LqM77ya6LSt5Lmw6auY5oCn6IO96K6h566XR1BV5Z6L5a6e5L6L"></span>
## Step 2: Purchase an HPC\-optimized instance

The purchase process for HPC\-optimized instances is similar to that for ECS instances, except that you need to select the HPC cluster created in [Step 1](https://docs.byteplus.com/en/docs/gpu/Buying-High-Performance-Computing-Optimized-instances#.5q2l6aqk5LiA77ya5Yib5bu66auY5oCn6IO96K6h566X6ZuG576k) on the basic configuration page. For more information, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For an introduction to the types of  HPC\-optimized instances, see <a href="https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types">Instance types</a>.</div>


* <div data-tips="true" data-tips-type="tip">For information related to the GPU driver, see <a href="https://docs.byteplus.com/en/docs/gpu/NVIDIA-driver-installation-guide">Installation guide of NVIDIA drivers</a>.</div>



**Enable RDMA network observability enhancement (hpcpni2)** 

When you create an **HPC\-optimized** **hpcpni2** instance using a public image, you also need to decide whether to enable RDMA network observability enhancement (enabled by default) during the image selection phase. Once enabled, the system will automatically install an RDMA network monitoring plugin to monitor the health status of the RDMA network.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can also manually install the plugin by referring to <a href="https://docs.byteplus.com/en/docs/6419/141332">RDMA network monitoring</a> after the instance is created.</div>


* <div data-tips="true" data-tips-type="tip">Do not stop or restart the instance while the plugin is being installed, as this will cause the installation to fail. Once the instance restarts, the installation will not resume.</div>


* <div data-tips="true" data-tips-type="tip">If you use an hpcpni2 instance enabled with RDMA network observability enhancement to create a custom image, the image contains the RDMA network monitoring plugin.</div>


* <div data-tips="true" data-tips-type="tip">When you change the operating system for an hpcpni2 instance, if RDMA network observability enhancement is enabled, the new image also contains the RDMA network monitoring plugin.</div>



<span id=".5q2l6aqk5LiJ77ya5ZCv5YqoRmFicmljIE1hbmFnZXLmnI3liqE="></span>
## Step 3: Start the Fabric Manager service

The NVIDIA\-Fabric Manager service enables interconnection between multiple graphics cards via NVSwitch. After you use a public image to purchase an instance equipped with multiple graphics cards and NVSwitch support, the service will be installed by default. You need to start the service manually. Otherwise, the instance does not work as expected.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">For instances that support NVSwitch, refer to the feature overview of each <a href="https://docs.byteplus.com/en/docs/gpu/Introduction-to-instance-types">instance type</a>.</div>


* <div data-tips="true" data-tips-type="warning">If you select an image in which the service is not installed, manually install the service by referring to <a href="https://docs.byteplus.com/en/docs/gpu/Installing-NVIDIA-Fabric-Manager">Installing NVIDIA\-Fabric Manager packages</a>.</div>


1. Execute the following command to start the Fabric Manager service.

   `sudo systemctl start nvidia-fabricmanager`

2. Execute the following command to check whether the Fabric Manager service starts as expected. If the output is `active (running)`, the service starts as expected.

   `sudo systemctl status nvidia-fabricmanager`

3. (Optional) Execute the following command to specify that the Fabric Manager service starts automatically when the instance starts.

   `sudo systemctl enable nvidia-fabricmanager`


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

For information about how to create HPC\-optimized instances by calling an API operation, see [RunInstances - Creates instances](https://docs.byteplus.com/en/docs/ecs/RunInstances).
