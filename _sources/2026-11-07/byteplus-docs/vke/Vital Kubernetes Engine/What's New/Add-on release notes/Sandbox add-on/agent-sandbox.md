---
title: "agent-sandbox"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/agent-sandbox"
---

The agent\-sandbox add\-on manages security sandboxes for AI agents. This topic describes the features, core resources, installation and configuration, and post\-installation verification of the agent\-sandbox add\-on.

<span id="am3NiAwT"></span>
## Add\-on overview

The agent\-sandbox add\-on is the core add\-on for the VCI Agent Sandbox scenario. Built on the Kubernetes community SIG Agent Sandbox, it adds capabilities such as sandbox snapshot, pause, and resume, and is compatible with the E2B API design. After you install the add\-on, you can manage the lifecycle of the sandboxes required to run AI agents in the cluster. When E2B Server is enabled, the add\-on also provides control plane and data plane capabilities for the E2B\-compatible API.

After you install the agent\-sandbox add\-on, the system creates the controller, the E2B Server workloads, and the access credentials based on your configuration. The following table lists only the core resources confirmed by the available information. If you change resource names, the E2B Server setting, or other configurations during installation, the actual installation result prevails.


|**Resource name** |**Resource type** |**Description** |
|---|---|---|
|agent\-sandbox\-controller |Deployment |This resource provides the add\-on controller capabilities. It reconciles resources such as Sandbox, SandboxClaim, SandboxWarmPool, and SandboxTemplate, and manages the sandbox lifecycle. |
|agent\-sandbox\-control\-plane |Deployment / Service |This resource is created after E2B Server is enabled. It provides the control plane service for the E2B\-compatible API and uses port 8081 by default. |
|agent\-sandbox\-data\-plane |Deployment / Service |This service is created after E2B Server is enabled. It provides the data plane service for the E2B\-compatible API and uses port 8080 by default. |
|e2b\-key\-store |Secret |This resource stores the automatically generated administrator key when control plane authentication is enabled and no administrator key is manually configured. |


<span id="MAXFQW4T"></span>
## Add\-on versions

For the agent\-sandbox add\-on, the release notes, new features added in each version, and optimization descriptions are provided. For details, see [Add-on release notes](https://docs.byteplus.com/en/docs/vke/agent-sandbox).

<span id="JVSO5iPZ"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the name of the target cluster to go to the management page of this cluster.

3. In the left navigation pane of the cluster management page, select **Addons**. Then, click the **Sandbox** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |**Deployment configuration** ||
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |**Access Credentials** ||
   |Access Key |Enter the API access key (AK and SK) of your BytePlus root user to authorize resource deployment related to the agent\-sandbox add\-on. For information about how to obtain an access key, see [API credentials (Access Key and API Key)](https://docs.byteplus.com/en/docs/IAM/about-access-keys).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Make sure that your BytePlus root user (including IAM users) has been configured with the <strong>VKEFullAccess</strong> system preset policy, or that the custom policy includes the following minimum set of authorization items (Actions). This ensures that the current account can access and manage resources by using VCI Agent Sandbox:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">ExecContainerImageCommitment</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DescribeContainerImageCommitments</div><br><br><br>* <div data-tips="true" data-tips-type="warning">CreateSnapshot</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DeleteSnapshot</div><br><br><br>* <div data-tips="true" data-tips-type="warning">DescribeSnapshots</div><br><br><br>* <div data-tips="true" data-tips-type="warning">CreateImageCache</div><br><br><br>* <div data-tips="true" data-tips-type="warning">ListImageCaches</div><br><br><br><br><div data-tips="true" data-tips-type="warning">For information about granting permissions to IAM users, see <a href="https://docs.byteplus.com/en/docs/vke/IAM_user_permissions">IAM permissions</a>.</div><br> |
   |Secret Key ||
   |**Controller Configuration** ||
   |Enable Extensions |Whether to enable the extended capabilities of the agent\-sandbox add\-on.<br><br><br>* Enabled: Extended capabilities such as Snapshot, Commit, SandboxWarmPool, SandboxTemplate, and SandboxClaim are enabled. We strongly recommend keeping the default setting (enabled).<br><br>* Disabled: Extended capabilities are disabled. |
   |Default Sandbox Service |When you do not specify whether to create a Service for the Sandbox CR, this controller parameter determines whether to create a Service.<br><br><br>* Enabled: A Service is created, allowing resources within the cluster to access the Sandbox.<br><br>* Disabled: No Service is created. You need to configure access to the Sandbox manually. |
   |Replicas |Number of replicas for the add\-on's Pod. If you specify more than one replica, you also need to enable the **Leader Election** option. |
   |Sandbox Concurrent Workers |The maximum number of concurrent reconciliations for the Sandbox controller.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 32. We recommend keeping the default value. |
   |SandboxClaim Concurrent Workers |The maximum number of concurrent reconciliations for the SandboxClaim controller.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 32. We recommend keeping the default value. |
   |SandboxWarmPool Concurrent Workers |The maximum number of concurrent reconciliations for the SandboxWarmPool controller.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 32. We recommend keeping the default value. |
   |SandboxTemplate Concurrent Workers |The maximum number of concurrent reconciliations for the SandboxTemplate controller.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 32. We recommend keeping the default value. |
   |Kube API QPS |The QPS rate\-limiting parameter for Kubernetes API calls. This parameter is used to prevent component management operations from placing excessive load on the API server.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 100. We recommend keeping the default value. |
   |Kube API Burst |The maximum burst request limit for Kubernetes API calls. This parameter is used to prevent component management operations from placing excessive load on the API server.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 200. We recommend keeping the default value. |
   |Leader Election |If you enable this option, the leader election mechanism is used to resolve resource contention issues.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">In a multi\-replica deployment, this option must be <strong>enabled</strong> to prevent multiple replicas from executing business logic simultaneously and causing resource contention.</div><br> |
   |Extra Args |Pass additional startup flags, such as Zap logging parameters and other flags that are not individually abstracted. |
   |Node Label Selector |After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Node forced scheduling |If this option is enabled, you can configure the policy for selecting node labels. The core workload of the add\-on is forcibly scheduled to compliant nodes according to the scheduling policy. |
   |Resource configuration |CPU and memory requests and limits for the add\-on controller itself. We recommend adjusting the specifications of the controller based on your business requirements. |
   |**E2B configuration** ||
   |Enable E2B Server |If you enable this option, E2B is enabled. You also need to configure all parameters below. |
   |Service Account Name |ServiceAccount name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |E2B Domain |E2B service domain suffix. It is used to generate the access domain names for the E2B control plane and data plane. We recommend keeping the default value.<br><br><br>* **Control\-Plane**: The E2B API control plane component. It is a stateless management component that serves as the entry point for E2B protocol execution, handling API requests such as sandbox creation and deletion.<br><br>* **Data\-Plane**: The E2B API data plane component. It is a stateless component that forwards API requests for operations such as code instruction execution and command execution to sandboxes.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">After deploying the application template, configure ALB Ingress rules in the VKE cluster to point <code>e2b.com</code> to the control plane workload and <code>*.e2b.com</code> to the data plane workload. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Installation_guide#tvYM2kxn">Exposing the E2B service via an Ingress</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you have performance requirements, we recommend using APIG for data plane forwarding, in which case you do not need to point <code>*.e2b.com</code> to the data plane workload. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/apig/Accessing_VCI_Agent_Sandbox_via_APIG">Accessing VCI Agent Sandbox via APIG</a>.</div><br> |
   |Enable Control\-Plane Auth |Whether to enable Control\-Plane authentication. If you enable this option, API requests to E2B will be validated against the provided API key. |
   |Admin Key |The E2B API key. You can specify a custom string or leave it unspecified.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you use E2B SDK v2.25.0 or later, we recommend using an E2B API Key in the <code>e2b_xxxxx</code> format.</div><br><br><br>If you do not specify it, a random API key will be generated and saved in the Secret named `e2b-key-store` under the `agent-sandbox-system` namespace. |
   |Control\-Plane Name |Control\-Plane component name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |Control\-Plane Service Name |Control\-Plane service name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |Control\-Plane Replicas |The number of Control\-Plane replicas. You can adjust the number of replicas based on the file size and file/code operation frequency. |
   |Idle Timeout |Idle connection timeout.<br><br><br>* Format: Go duration string.<br><br>* Value range: Positive integers.<br><br>* Default value: 600s. We recommend keeping the default value. |
   |Write Timeout |Response write timeout.<br><br><br>* Format: Go duration string.<br><br>* Value range: Positive integers.<br><br>* Default value: 600s. Setting this too low may cause long\-running requests to be terminated prematurely. We recommend keeping the default value. |
   |Sandbox Timeout |Sandbox lifecycle timeout.<br><br><br>* Format: Go duration string.<br><br>* Value range: Positive integers.<br><br>* Default value: 600s. Setting this too low may cause the APIs for creating or modifying a sandbox to exit before the call completes. We recommend keeping the default value. |
   |Rest Client QPS |The QPS limit for Kubernetes API access.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 50. We recommend keeping the default value. |
   |Rest Client Burst |The maximum burst requests to the Kubernetes API.<br><br><br>* Value range: Positive integers.<br><br>* Default value: 100. We recommend keeping the default value. |
   |Control\-Plane Service Port |The Control\-Plane service port. We recommend keeping the default value 8081. |
   |Control\-Plane Resource Configuration |CPU/Memory requests and limits for the Control\-Plane. You can adjust this configuration based on the file size and the frequency of file or code operations. |
   |Data\-Plane Name |The Data\-Plane component name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |Data\-Plane Service Name |Data\-Plane service name. We recommend keeping the default value. If you want to specify a custom name, make sure that the name format meets the requirements of Kubernetes. |
   |Data\-Plane Replicas |The number of Data\-Plane replicas. You can adjust the number of replicas based on the file size and file/code operation frequency. |
   |Data\-Plane Service Port |The Data\-Plane service port. We recommend keeping the default value 8080. |
   |Data\-Plane Resource Configuration |CPU/Memory requests and limits for the Data\-Plane. You can adjust this configuration based on the file size and the frequency of file or code operations. |
   

5. Click **Confirm** to finish configuration.


<span id="QedmFDVx"></span>
## Upgrading add\-ons

&nbsp;

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="OxsiWFeE"></span>
## Related documentation


* [Introduction to VCI Agent Sandbox](https://docs.byteplus.com/en/docs/vke/Feature_introduction)

* [Lifecycle management of VCI Agent Sandbox](https://docs.byteplus.com/en/docs/vke/Lifecycle_management)

* [Managing VCI Agent Sandbox based on the E2B protocol](https://docs.byteplus.com/en/docs/vke/E2B-based_management)
