---
title: "Properly using runtimes and operating systems"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Using-runtimes-and-operating-systems-correctly"
---

This topic describes precautions, operational configuration recommendations, and usage best practices regarding runtimes (including containerd and secure containers) and operating systems for using VKE.

<span id=".5ZCI55CG6YWN572uLWt1YmVsZXQt55qE5bm25Y-R5a655Zmo6ZWc5YOP5ouJ5Y-W6ZmQ5Yi2"></span>
## Configuring a proper limit on concurrent container image pulling for kubelet

When you create pods, configure a proper limit on concurrent container image pulling for kubelet. If this limit is too low, an error message similar to `Failed to pull image "xxxxx:xxxxx": pull QPS exceeded` may occur in scenarios such as creating multiple pods on a node.

You can adjust this concurrency limit by changing the value of the `--registry-pull-qps` parameter (the kubelet `registryPullQPS` parameter) in the `/etc/kubernetes/kubelet.conf` configuration file.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying the <code>--registry-pull-qps</code> parameter in the <code>/etc/kubernetes/kubelet.conf</code> file will have the following impacts:</div>



* <div data-tips="true" data-tips-type="warning">Kubelet must be restarted for the configuration change to take effect. Restarting kubelet may cause the node to be unavailable for a short period of time. We recommend performing this operation during off\-peak business hours.</div>


* <div data-tips="true" data-tips-type="warning">You need to evaluate both the node bandwidth limit and the image registry rate limit to avoid additional issues caused by an excessively high rate.</div>



<span id=".6YG_5YWN5L2_55SoLWNlbnRvcy02LXgt5Y-K5Lul5LiL54mI5pys5L2c5Li65Z-656GA6ZWc5YOP"></span>
## Avoid using CentOS 6.x or an earlier version as the base image

We recommend against using CentOS 6.x or an earlier version as the base image for your VKE workloads. CentOS 6.x images rely on the vsyscall mechanism of the system, while worker nodes in VKE clusters use the vDSO mechanism, with vsyscall disabled by default. Therefore, running CentOS 6.x images or container images based on CentOS 6.x may cause errors.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For information about vsyscall and vDSO, see <a href="https://lwn.net/Articles/446528/">On vsyscalls and the vDSO</a>.</div>


If you run CentOS 6.x images or images built from CentOS 6.x base images on veLinux or other later Linux versions, the containers may fail to start with the following errors:


* The State.Reason of containers is CrashLoopBackOff.

* The Last State.Exit code of containers is 139.


We recommend the following methods for using CentOS images:


* **Method 1 (recommended)** 

   Rebuild the image based on CentOS 7.X or a later CentOS version and use this image in your containerized application.

* **Method 2**

   If CentOS 7.X or a later CentOS version cannot be used as a base image, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to obtain technical support.


<span id="w22W4p0v"></span>
## Avoid using runtimes not supported by VKE

VKE currently supports only the containerd runtime. Do not use or install Docker or other runtimes on nodes. ‌Using runtimes unsupported by VKE may cause node failures and impact business operations.

If you have already used another runtime, restore the container runtime as follows:


1. Remove the node from the VKE cluster and retain its corresponding ECS instance. For detailed operations, see [Removing nodes](https://docs.byteplus.com/en/docs/vke/Managing-nodes#.56e76Zmk6IqC54K5).

2. ‌Re\-add the ECS instance to the VKE cluster via the "Add existing node" method to restore the node's container runtime to VKE\-supported containerd. For details, see [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).
