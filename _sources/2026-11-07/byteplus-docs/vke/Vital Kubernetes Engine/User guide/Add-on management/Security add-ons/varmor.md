---
title: "varmor"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/varmor-add-on"
---

varmor is a container security enhancement add\-on that leverages Linux technologies AppArmor LSM, BPF LSM, and Seccomp to harden containers. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="0f74G1Y8"></span>
## Add\-on overview

vArmor is a container security sandbox add\-on designed specifically for cloud\-native environments. It performs fine\-grained permission management on container runtime behavior. This restricts container access permissions at the kernel level, thereby improving the overall security defense level of clusters.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more information, see <a href="https://docs.volcengine.com/docs/6507/2582778?lang=zh">What is container hardening?</a></div>


After the varmor add\-on is installed in your cluster, the system creates the following Kubernetes resources in the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|varmor\-manager |Deployment |Acts as the control plane of the vArmor component. It responds to and manages security policies and hosts Webhook and management logic. |
|varmor\-agent |DaemonSet |Runs on cluster nodes to manage enforcers and profiles on nodes. |
|varmorpolicy |CRD |A namespace\-level CRD resource that defines and delivers runtime security policies for workloads within a specific namespace. It binds to business containers in the same namespace using label selectors, automatically converts protection rules into underlying security configurations, and injects the configurations for enforcement. |
|varmorclusterpolicy |CRD |A cluster\-level CRD that is used to establish and uniformly distribute the runtime security protection baseline across the global scope. Its scope is not namespace\-restricted. This resource performs ‌mandatory security takeovers‌ for all workloads that match the label selector in the cluster. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="F2hXRcSl"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.volcengine.com/docs/6460/2586545).

<span id="F6FBrwiW"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Security** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |**Feature switch** ||
   |AppArmor Enforcer |Restrict workload behaviors using the AppArmor mechanism. When enabled, it enforces ‌default security policies‌ to limit the operations that containers or processes can perform, such as accessing specific files, invoking certain capabilities, or executing high\-risk actions.<br><br>The core function of this parameter is to confine runtime behaviors within controlled boundaries‌, reducing exposure to unauthorized access, privilege escalation, and potential attack surfaces. |
   |BPF Enforcer |Detect and control runtime behaviors based on eBPF capabilities. Compared to traditional static constraints, it excels at ‌kernel\-space, fine\-grained interception and governance‌ of process activities, system calls, and runtime events.<br><br>The core function of this parameter is to enhance the flexibility and observability of runtime protection, enabling the system to identify and process abnormal behavior more accurately. |
   |BehaviorModeling Mode |The BehaviorModeling mode (an experimental feature). You can collect and process the behaviors of target workloads within a specified time period to build behavioral models. Once modeling is complete, vArmor will generate an [ArmorProfileModel](https://github.com/bytedance/vArmor/blob/main/apis/varmor/v1beta1/armorprofilemodel_types.go) object to store the behavior model of the target workload.<br><br>This behavior model can be used to analyze which built\-in rules can harden the target application or guide users in implementing a least\-privilege security context for workloads. For details, see [BehaviorModeling mode](https://www.varmor.org/zh-cn/docs/main/guides/policies_and_rules/policy_modes/behavior_modeling). |
   |Service Egress Control |Limit workloads' access to services based on security policies. This feature allows containers to access only legitimate and necessary external or internal services by configuring network policies (such as allowing or denying IP addresses, network segments, ports, or domain names).<br><br>The core function of this parameter is to ‌block unauthorized outbound traffic‌, preventing malicious communication or internal network scanning by anomalous processes. |
   |The Match Label of Webhook |Define which workloads will be identified, intercepted, or injected with configurations. Essentially, it functions as a selection mechanism that informs the system which objects require the capabilities of varmor. The add\-on's capabilities can be precisely applied to the specified workload based on label matching.<br><br><br>* You can configure workload match labels using the `key=value` format, for example, `sandbox.varmor.org/enable=true`.<br><br>* You can specify empty match labels‌ to enforce hardening on ‌any workloads that meet policy match conditions‌. |
   |**Agent Configuration** ||
   |Run in the Host Network |Set whether the Agent runs in the host network namespace. When this option is enabled, the Agent ‌will not be allocated a dedicated virtual Pod IP‌. Instead, it directly uses the host's physical network interface, IP address, and routing tables. |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Resource configuration |Specify the CPU and memory requests/limits for resources in the Agent. |
   |**Manager Configuration** ||
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Resource configuration |Specify the CPU and memory requests/limits for resources in the Manager. |
   

5. Click **Confirm** to finish configuration.


<span id="Oy2bj39j"></span>
## Upgrade the add\-on

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="rfFJAfjf"></span>
## Related documentation


* [Implementing cloud-native container security with vArmor.](https://docs.byteplus.com/en/docs/vke/Implementing_cloud-native_container_security_with_vArmor?lang=en)
