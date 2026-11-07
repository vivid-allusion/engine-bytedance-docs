---
title: "node-problem-detector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/node-problem-detector"
---

The node\-problem\-detector add\-on is a node health surveillance add\-on, which is used to detect node anomalies, and report the anomalies to kube\-apiserver. This topic includes the change logs of the node\-problem\-detector add\-on.

For more information about add\-ons, see [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-management).

<span id="k7LS8eW7"></span>
## January 2026


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.6 |All versions |Maintained |* Exposed pod information in pod OOM events.<br><br>* Adjusted the default resource parameters.<br><br>* Updated the add\-on port to 9122.<br><br>* Fixed CVE security vulnerabilities of the add\-on image. |None |


<span id="dCyBBB9d"></span>
## September 2025


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.5 |All versions |Maintained |* The Rodan service is no longer installed by default. You can install it as needed.<br><br>* Optimized the GPU detection logic: Memory error thresholds can be configured, and GPU driver version compatibility can be checked.<br><br>* Supported disabling the health check feature of the cloud assistant Agent. |None |


<span id="u0Dtj9lS"></span>
## July 2025


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.4 |All versions |Maintained |Fixed configurations related to container operation. |None |


<span id="mWYaFsU1"></span>
## April 2025


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.3 |All versions |Maintained |* Added the GPU detection capability.<br><br>* Supported installation through Rodan scripts.<br><br>* Fixed the issue where the batch job client fails to be installed in some scenarios.  |None |


<span id="_2024-08"></span>
## August 2024


|Versions |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.2 |All versions |Maintained |* Turn off the self\-healing actions of services such as kubelet and containerd.<br><br>* Adjusted the detection interval for the batch job client to once every 10 minutes. |None |


<span id="_2024-06"></span>
## June 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.8.19\-vke.1 |All versions |Maintained |* Restores the detection and self\-healing mechanisms of services such as kubelet and containerd.<br><br>* Adds the detection and installation of batch job client ends.<br><br>* Limits the resources used by the add\-on to no more than 0.5 core CPU and 256 MiB of memory. |None |
