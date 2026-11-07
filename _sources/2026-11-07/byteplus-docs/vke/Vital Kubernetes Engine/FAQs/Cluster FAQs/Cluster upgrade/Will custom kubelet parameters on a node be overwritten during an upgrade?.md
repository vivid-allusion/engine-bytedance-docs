---
title: "Will custom kubelet parameters on a node be overwritten during an upgrade?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Are-custom-kubelet-parameters-on-a-node-overwritten-during-a-node-upgrade"
---

<span id="6JEfR4Fm"></span>
## Configuration method

VKE supports configuring kubelet parameters on nodes through different methods. Different configuration methods support different parameters, and the logic for retaining parameters during an upgrade also differs. The following table describes the details.


|**Configuration method** |Configuration method |**Post\-upgrade processing logic** |
|---|---|---|
|Use the console |Specify the kubelet parameters of the node pool in the console and allow them to be synchronized to existing nodes. For details, see [Configuring Kubelet parameters for node pools](https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend first using this method to configure the kubelet parameters of nodes.</div><br> |* The parameters are retained after the node upgrade.<br><br>* When synchronizing the node pool configuration to existing nodes, parameters on the existing nodes that are the same as the node pool parameters will be updated to the configuration of the node pool. |
|Custom configuration |For parameters that are not supported by the console, you can specify custom configurations by modifying the ConfigMap or node configuration files. For details, see [Custom cluster kubelet parameters](https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter). |* Parameters will not necessarily be retained after the node upgrade. During the upgrade, files such as `/var/lib/kubelet/config.yaml` and `/var/lib/kubelet/kubeadm-flags.env` may be regenerated or updated.<br><br>* Record the existing configuration before the upgrade and recheck whether the parameters take effect after the upgrade. |


<span id="8bUTFXX6"></span>
## Parameter cleanup

During a node upgrade, VKE checks the compatibility of Feature Gates based on the target Kubernetes version and removes incompatible configurations. For example:


* When you upgrade from v1.26 to v1.28, `QoSResourceManager` is removed.

* `IPv6DualStack` is removed during the upgrade.

* When you upgrade from v1.34 to v1.36, this configuration is removed from the node, including `InPlacePodVerticalScaling`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The actual cleanup scope is subject to the compatibility check results of the target Kubernetes version. Do not re\-add Feature Gates that are not supported by the target version after the upgrade. Otherwise, it may cause kubelet startup exceptions or node unavailability.</div>
