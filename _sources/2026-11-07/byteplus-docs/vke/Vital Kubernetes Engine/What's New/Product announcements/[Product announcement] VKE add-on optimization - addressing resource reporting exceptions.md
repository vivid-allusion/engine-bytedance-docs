---
title: "[Product announcement] VKE add-on optimization - addressing resource reporting exceptions in the Kubernetes Device Plugin framework"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product-announcement_VKE_add-on_optimization"
---

<span id="gKqGWugb"></span>
## Background

In the native Kubernetes Device Plugin framework, kubelet calls the ListAndWatch API of Device Plugin via a long\-lived gRPC connection to continuously obtain device resource information on the node (such as GPUs and RDMA NICs). When this gRPC connection is unexpectedly broken due to network issues, process crashes, or other reasons, the kubelet reports the corresponding device resources as 0, making GPUs or RDMA resources on the node unavailable for scheduling.

This issue is a known design flaw in the Kubernetes community's Device Plugin framework. If the ListAndWatch stream is broken, the kubelet does not automatically re\-establish the connection or retry. Recovery depends completely on the Device Plugin side proactively re\-registering. The community currently does not provide any built\-in automatic recovery mechanism for the Device Plugin framework. The long\-term direction is to replace Device Plugin with the DRA (Dynamic Resource Allocation) architecture, but a full migration will take considerable time.

<span id="Sl6ozbdS"></span>
## Scope of impact

<span id="yAqJApBE"></span>
### Affected add\-ons

The following add\-ons are involved in this resource reporting issue:


* nvidia\-device\-plugin

* rdma\-device\-plugin

* vpc\-cni

* mgpu


<span id="oRvj4TGC"></span>
### Issue description

When the ListAndWatch connection between the above add\-ons and kubelet is unexpectedly disconnected, the following symptoms occur:


* GPU or RDMA resources on the node are reported as 0.

* Pods that depend on these resources cannot be scheduled to the node.

* Existing workloads are unaffected, but new scheduling requests will fail.


<span id="QqGe5rKx"></span>
## Solution

To address the above community framework flaw, VKE has released new versions for all affected add\-ons, adding automatic detection and recovery capabilities for resource reporting exceptions. When a resource reporting anomaly is detected, the add\-on will automatically initiate the re\-registration process to restore device resource reporting, requiring no manual intervention.

<span id="P28Wh3zu"></span>
### Considerations


* During add\-on upgrades, already allocated device resources and running workloads are unaffected.

* We recommend performing add\-on upgrades during off\-peak hours.

* If you still encounter resource reporting anomalies after the upgrade, [submit a ticket](https://console.byteplus.com/workorder/create?step=1) to contact us.


<span id="dQ2b8hP3"></span>
### Operational recommendations

If you have installed and used any of the above add\-ons in your cluster, we recommend upgrading them to the latest versions promptly to benefit from automatic detection and recovery capabilities and other related optimizations.


|Add\-on name |Minimum version requirements |Upgrade notes |
|---|---|---|
|nvidia\-device\-plugin |v2.2.1 or later |* After upgrading to this version, automatic detection and recovery are enabled.<br><br>* cgroupv2 is supported starting with this version. To use cgroupv2 on your nodes, upgrade to v2.2.1 or later. |
|rdma\-device\-plugin |v3.6.2\-vke.1 or later |After upgrading to this version, automatic detection and recovery are enabled. |
|vpc\-cni |v1.8.11 or later |After upgrading to this version, automatic detection and recovery are enabled. |
|mgpu |v0.6.5 or later |After upgrading to this version, enable **Health check** in the mgpu add\-on configuration (for configuration details, see [mgpu](https://docs.byteplus.com/en/docs/vke/mgpu-add-on)). If enabled, the add\-on will automatically trigger re\-registration and restore resource reporting upon detection of a resource reporting anomaly. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For detailed steps and instructions on upgrading add\-ons, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>.</div>


<span id="9KeCybgr"></span>
## Related documentation


* [nvidia-device-plugin add-on release notes](https://docs.byteplus.com/en/docs/vke/nvidia-device-plugin)

* [rdma-device-plugin add-on release notes](https://docs.byteplus.com/en/docs/vke/rdma-device-plugin?lang=en)

* [vpc-cni add-on release notes](https://docs.byteplus.com/en/docs/vke/vpc-cni?lang=en)

* [mgpu add-on release notes](https://docs.byteplus.com/en/docs/vke/mgpu?lang=en)
