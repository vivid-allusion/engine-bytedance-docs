---
title: "csi-ebs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-ebs"
---

The csi\-ebs add\-on is an Elastic Block Storage (cloud disk) service add\-on that provides the standard CSI interface, enabling container clusters to use block storage services. This topic describes the change history of the csi\-ebs add\-on.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions

For csi\-ebs add\-on upgrade risks and upgrade verification, refer to [Upgrading csi-ebs add-on](https://docs.byteplus.com/en/docs/vke/csi-ebs-add-on). For more related introductions and usage methods of add\-ons, refer to [Add-on management](https://docs.byteplus.com/en/docs/vke/Add-on-overview).

<span id=".54mI5pys5Y-Y5pu0"></span>
## Version changes

<span id="S1RudRch"></span>
### June 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.3 |All versions |Maintained |Supported enabling performance bursting on dynamically provisioned FlexPL cloud disks. |None |


<span id="ycfNj2Ek"></span>
### April 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.2 |All versions |Maintained |PV and PVC labels are added by default when you create dynamic EBS volumes. |None |


<span id="j1Zttssr"></span>
### March 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.1 |All versions |Maintained |The WatchList feature is enabled by default to optimize APIServer memory usage. For details, see [Streaming List responses](https://kubernetes.io/blog/2025/05/09/kubernetes-v1-33-streaming-list-responses/). |The client\-side processing latency slightly increases. |


<span id="WmKkWFGx"></span>
### January 2026


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.3.0 |All versions |Maintained |* Supported `mountOptions`.<br><br>* Supported `mkfsOptions`.<br><br>* Upgraded the csi sidecar version, synchronized to the latest community version, and resolved known CVE issues.<br><br>* Adjusted the default `resources.limits` to support large\-scale online PV scenarios. |Optimization for large\-scale PV scenarios leads to increased resource usage of cluster controllers.<br><br><br>* Adjusted the container limit for csi\-provisioner from the default value 300m/900Mi to 600m/2Gi.<br><br>* Adjusted the container limit for csi\-attacher from the default value 300m/900Mi to 600m/1.5Gi.<br><br>* Adjusted the container limit for csi\-snapshotter from the default value 300m/300Mi to 600m/500Mi.<br><br>* Adjusted the container limit for csi\-snapshotter from the default value 100m to 200m.<br><br>* Adjusted the container limit for ebsplugin from the default value 700m/1Gi to 1400m/1.9Gi.<br><br><br>Optimization for large\-scale PV scenarios leads to increased node resource usage.<br><br><br>* Adjusted the container limit for ebsplugin from the default value 200m/200Mi to 1C/1Gi. |


<span id="EfZ8o2lE"></span>
### October 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.15 |All versions |Maintained |* Changed the default port for data collection on nodes to 11815, and console users are allowed to change the settings.<br><br>* Changed the default node health\-check port to 9808, which can be customized in the console.<br><br>* Optimized the csi\-ebs startup logic so that the add\-on does not start until the node has successfully connected to the management center. This feature is disabled by default and can be enabled in the console. |None |


<span id="I1GxkRJ9"></span>
### September 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.14 |All versions |Maintained |Supported IPv6only clusters. |None |
|v1.2.13 |All versions |Maintained |Supported the instant snapshot feature. |None |


<span id="R5gKwbAX"></span>
### July 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.11 |All versions |Maintained |1. ARM clusters are supported.<br><br>2. Added anti\-affinity feature to EBS clusters. |None |


<span id="IErxDfJF"></span>
### May 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.10 |All versions |Maintained |Fixed the issue of taint configuration anomaly. |None |


<span id="vShTfgFa"></span>
### April 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.9 |All versions |Maintained |Fixed the issue where calling the [DescribeInstanceTypes](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceTypes) API with the parameter **InstanceTypes** could not query the `ecs.ddhr2s.define.c32m64` specification. |None |


<span id="_2025-02"></span>
### February 2025


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.8 |All versions |Maintained |* Supports specifying the number of reserved volumes at the node dimension.<br><br>   * A new parameter **Node reserve volumes Synchronization period** is added for the add\-on, and the node label key for the number of reserved volumes is ebs.csi.volcengine.com/reserve\-volumes.<br><br>   * A new parameter **Node reserve volumes count** is added for the add\-on, which is used to configure the number of EBS volumes reserved for each node. This value should include the system volume and data volume used by the node.<br><br>* Supports exposing the metrics of the number of assignable disks per node and the number of assigned disks per node. A new parameter **Enable node allocated volumes metric** has been added for the add\-on. It is disabled by default.<br><br>* By default, add the system Tag created\-by\-cluster\-id for the EBS disk created through CSI. |None |


<span id="_2024-10"></span>
### October 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.6 |All versions |Maintained |* Supports configuring the NodeSelector, Tolerations, and Resources of csi\-ebs\-controller while installing add\-ons.<br><br>* Fixed an issue where csi\-ebs\-node failed to access the metadata server or OpenAPI during startup, causing an inaccurate count of available disks on nodes.<br><br>* Supports specifying the number of node reserved volumes through setting parameters.<br><br>* After csi\-ebs\-node is ready, the taint with the key ebs.csi.volcengine.com/agent\-not\-ready on the node will be automatically deleted. |None |


<span id="_2024-07"></span>
### July 2024


|**Version** |**Compatibility with Kubernetes version** |**Version status** |**Description** |**Impact** |
|---|---|---|---|---|
|v1.2.5 |All versions |Maintained |Authentication via dynamic Secret is now enabled by default. |None |
|v1.2.4 |All versions |Maintained |* Deprecates the built\-in PTSSD cloud disk type StorageClass.<br><br>* Supports configuring parameters of additional performance package for the Enhanced FlexPL cloud disk type.<br><br>* Supports implementing authentication (turned off by default) through dynamic secret.<br><br>* Upgrade CSI spec version to v1.9.0.<br><br>* Upgraded the sidecar image version.<br><br>* Enable pprof through Unix Domain Socket.<br><br>* Adjust the log level to 2 to avoid printing a large amount of invalid information.<br><br>* Add trace module to increase trace information for critical paths. |Note the following impact related to the deprecation of the built\-in PTSSD cloud\-disk StorageClass.<br><br><br>* If PTSSD was allowlisted during the last installation of the csi\-ebs add\-on:<br><br>   * If the add\-on is still allowlisted during the upgrade, after the upgrade, the cloud disk type of the stock ebs\-ssd StorageClass will be modified to the Enhanced PL0.<br><br>   * If allowlisting is canceled during the add\-on upgrade, the existing ebs\-essd StorageClass will be deleted, and the cloud\-disk type of the ebs\-ssd StorageClass will be changed to Enhanced PL0.<br><br>* If PTSSD was not allowlisted in the previous csi\-ebs installation, it remains not allowlisted during the upgrade and nothing changes; the cloud\-disk type of the built\-in ebs\-ssd StorageClass will be changed to the Enhanced PL0. |


<span id="_2024-05"></span>
### May 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.3 |All versions |Maintained |Supports specifying custom tag for StorageClass. Custom tags can be specified through StorageClass parameters.tags in the format: `"key\|value,key\|value"`.<br><br><br>* Naming rules for Key:<br><br>   * `volc:` or `sys:` prefixes are system\-reserved tag keys. You cannot create tag keys that start with any case variation of the `volc:` or `sys:` prefix.<br><br>   * It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>   * The length is limited to 1 to 128 characters.<br><br>* Value naming rules:<br><br>   * It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>   * The length should be between 0 and 256 characters and can be empty. |None |


<span id="_2024-04"></span>
### April 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.2 |All versions |Maintained |* Supports XFS file system type.<br><br>* Adapt to Serverless final state (only Serverless supports managed deployment). |None |


<span id="_2024-03"></span>
### March 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.2.1 |All versions |Maintained |Added a specific tag to disks created or used by csi\-ebs. |None |
|v1.2.0 |All versions |Maintained |Supports deployment on Vital Container Instance (VCI). |None |


<span id="_2024-01"></span>
### January 2024


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.9 |All versions |Maintained |Avoids scheduling the add\-on pods to the DCP registered nodes. |None |


<span id="_2023-12"></span>
### December 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.8 |All versions |Maintained |* Fixed the issue where during the upgrade, the csi\-ebs plugin did not register to kubelet. <br><br>* Add csi\-ebs\-controller\-metric\-server service. |None |


<span id="_2023-11"></span>
### November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.7 |All versions |Maintained |Fixed the issue where access to the metadata server timed out causing the zone to be empty, preventing the csi node/controller from starting. |None |
|v1.1.6 |All versions |Maintained |* Fixed the issue where storageClass did not specify projectName but ebs volume already existed causing projectName check failure.<br><br>* Optimized the problem of rate limiting caused by accessing the metadata server. |None |


<span id="_2023-11"></span>
### November 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.5 |All versions |Maintained |Added support for projectName. |StorageClass adds projectName parameter to specify the project. The default is default if not added. |


<span id="_2023-09"></span>
### September 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.4 |All versions |Maintained |Optimized the verification logic for successful cloud disk scale\-out. |None |


<span id="_2023-08"></span>
### August 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.3 |All versions |Maintained |Cancel the dependency on OpenAPI allowlist parameters. |None |


<span id="_2023-06"></span>
### June 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.2 |All versions |Maintained |Supports Elastic Compute Service (ECS) general\-purpose g3i, compute\-optimized c3i, and memory\-optimized r3i specifications.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The above specifications are <strong>beta</strong> specifications on the ECS side.</div><br> |None |


<span id="_2023-05"></span>
### May 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.1.1 |All versions |Maintained |Supports self\-adaptation of the maximum number of mounting Persistent Volumes (PV) per single node according to node specifications. |None |
|v1.1.0 |All versions |Maintained |* Optimize verification logic before mounting cloud disk.<br><br>* Optimize mounting method for Block type volumes. |None |


<span id="_2023-03"></span>
### March 2023


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.4 |All versions |No longer maintained |Supports cloud disk snapshot. |None |
|v1.0.3 |All versions |No longer maintained |Supports Vital Container Instance (VCI) deployment mode. |None |


<span id="_2022-12"></span>
### December 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.2 |All versions |No longer maintained |Adapted to the Addon (add\-on) refactoring. |None |
|v1.0.1 |All versions |No longer maintained |Supports topology spread configuration. |None |


<span id="_2022-11"></span>
### November 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v1.0.0 |All versions |No longer maintained |Kubernetes v1.24 is supported. |None |


<span id="_2022-09"></span>
### September 2022


|Version |Compatibility with Kubernetes version |Version status |Description |Impact |
|---|---|---|---|---|
|v0.1.13 |All versions |No longer maintained |Supports deleting persistent volumes through concurrent Detach. |None |
