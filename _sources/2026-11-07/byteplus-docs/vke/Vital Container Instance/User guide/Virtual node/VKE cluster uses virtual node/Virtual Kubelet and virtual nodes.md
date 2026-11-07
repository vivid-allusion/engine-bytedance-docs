---
title: "Virtual Kubelet and virtual nodes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Virtual-Kubelet-and-virtual-nodes"
---

VKE manages the vci\-virtual\-kubelet add\-on by default, so you do not need to perform O&M for the add\-on.

<span id=".dmNpLXZpcnR1YWwta3ViZWxldC3nu4Tku7bor7TmmI4="></span>
## vci\-virtual\-kubelet notes


* VKE provides a managed, maintenance\-free vci\-virtual\-kubelet add\-on and automated creation of virtual nodes. This enables seamless integration with VCI.

* The managed vci\-virtual\-kubelet add\-on is managed, upgraded, and scaled out by the VCI system.

* For questions about the managed add\-on, [submit a ticket](https://console.byteplus.com/workorder/create).


<span id=".6Jma5ouf6IqC54K56K-05piO"></span>
## Virtual node notes


* After you install the vci\-virtual\-kubelet add\-on in the VKE cluster, virtual nodes will be automatically created.

* A single virtual node supports up to 6,000 pods. Pay attention to the number of pods in the cluster in your business scenario.

* The console only supports editing or deleting non\-system labels and annotations of virtual nodes.

* To avoid causing service unavailability, you are advised not to bring virtual nodes offline, remove them, or cordon them.
