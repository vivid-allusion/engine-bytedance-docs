---
title: "Release notes"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-Release-notes"
---

This topic describes the latest updates to the features in VCI. New features will be available regionally in the future for trials.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Tips</div>



* <div data-tips="true" data-tips-type="tip"><strong>Release region </strong>refers to the region where the feature was first released. The release regions added later will not affect the historical release notes. For the regions where features are actually available, please refer to the information on the console pages.</div>


* <div data-tips="true" data-tips-type="tip">The historical records of beta testing will not change after <strong>beta </strong>features are officially released to the public. The iteration information of features is always contained in the latest release notes.</div>


* <div data-tips="true" data-tips-type="tip">The release notes on this page cover the records of features released in VCI <strong>this year</strong>. For the historical release notes, see <a href="https://docs.byteplus.com/en/docs/vke/VCI_History_feature_release_notes">Historical release notes</a>.</div>



<span id="aNFpqOue"></span>
## August 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Pod fail\-fast |Supports the Pod fail\-fast capability. When a VCI instance fails to be created due to insufficient inventory, unavailable specifications, or other reasons, the system promptly returns the failure result. This helps users detect issues in a timely manner and switch to alternative solutions, preventing prolonged, ineffective waiting. |All |[VCI Pod fail-fast](https://docs.byteplus.com/en/docs/vke/VCI_Pod_fail-fast) |
|NetworkPolicy\-based network access control for VCI Pods |VCI provides a Kubernetes\-compatible NetworkPolicy solution for the nodeless architecture, enabling NetworkPolicy\-based network access control for VCI Pods and improving workload security. |All |[Using a NetworkPolicy to implement network access control for VCI Pods](https://docs.byteplus.com/en/docs/vke/Using_a_NetworkPolicy_to_implement_network_access_control_for_VCI_Pods) |
|General availability of inventory\-aware scheduling |The VCI inventory\-aware scheduling feature has completed beta testing and is now generally available. Inventory\-aware scheduling incorporates real\-time VCI inventory information into scheduling decisions, improving the success rate of Pod creation in specified availability zones and reducing creation failures and repeated retries caused by insufficient inventory. |All |[VCI inventory-aware scheduling](https://docs.byteplus.com/en/docs/vke/VCI-inventory-aware-scheduling) |
|Tag\-based and project\-based cost allocation supported for the image cache feature |Storage costs incurred by image cache usage support cost allocation by tag and by project, making cost management and allocation easier. |All |[Creating VCIs by using manually created image caches](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache) |


<span id="xYckAp5E"></span>
## July 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|VCI Agent Sandbox upgrades |Provides a new version of VCI Agent Sandbox, to which the existing VCI Agent Sandbox can be upgraded to obtain the latest features and optimized performance. |All |* [Version change log](https://docs.byteplus.com/en/docs/vke/Version_change_log)<br><br>* [Upgrading VCI Agent Sandbox](https://docs.byteplus.com/en/docs/vke/Upgrading_VCI_Agent_Sandbox) |
|Warm pools supported by VCI Agent Sandbox |VCI Agent Sandbox supports warm pools (SandboxWarmPool). Ready Pods are pre\-created and cached in the pools. This achieves instant delivery upon claim. This is applicable to scenarios that are extremely sensitive to startup latencies, such as real\-time AI Agent interactions. |All |[Startup acceleration](https://docs.byteplus.com/en/docs/vke/Startup_acceleration) |
|VCI Agent Sandbox enables snapshots not to be automatically created when sandboxes are suspended |VCI Agent Sandbox enables snapshots not to be automatically created when sandboxes are suspended. This allows you to control and manage snapshots to meet flexible requirements in different scenarios. |All |[Suspend sandboxes with no snapshots created](https://docs.byteplus.com/en/docs/vke/Lifecycle_management?lang=en#T7Yza9tu) |
|VCI Agent Sandbox supports in\-place image updates |When sandbox images are updated via VCI Agent Sandbox, container\-level in\-place restart is supported. This allows the images to be updated without Pod recreation, which shortens the update duration. |All |[Update sandboxes in place](https://docs.byteplus.com/en/docs/vke/Lifecycle_management?lang=en#D00NSH1g) |


<span id="Q4RBkJFM"></span>
## May 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|VCI Agent sandbox supports E2B |Supported the management of the VCI Agent Sandbox based on E2B. This achieves the feature of writing code once and running it across platforms and addresses industry pain points such as sandbox API fragmentation and inconsistency. |All |[E2B-based management](https://docs.byteplus.com/en/docs/vke/E2B-based_management) |


<span id="eXbH3Wb5"></span>
## March 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Provides the VCI Agent Sandbox features |VCI is built on the Community Agent Sandbox. It is integrated with BytePlus's public cloud general product capabilities and deeply developed to serve as a carrier for running AI Agents at scale. It provides an Agent management solution under the Kubernetes technical architecture: VCI Agent Sandbox. |All |[Introduction to VCI Agent Sandbox](https://docs.byteplus.com/en/docs/vke/Feature_introduction) |
|Supported Kubernetes v1.34 |VCI supported Kubernetes v1.34, which provides new features coming from this version.​ |All |[Release notes of VKE based on Kubernetes v1.34](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_34) |


<span id="HPVJSW3S"></span>
## February 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Support for deleting VCI subnets |Configured VCI Pod subnets can be deleted when they are not being used by any VCI Pod. This enables you to flexibly manage subnets in your business clusters and control the number of virtual nodes as needed. |All |[Managing virtual nodes](https://docs.byteplus.com/en/docs/vke/Managing_virtual_nodes) |


<span id="L8yWfJ9e"></span>
## January 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Supported Kubernetes v1.32 |VCI supports Kubernetes v1.32, which provides the features of the latest Kubernetes version. |All |[Release notes of VKE based on Kubernetes v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32) |


<span id="IhtslsRB"></span>
## November 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Added system labels related to instance specifications |A system label related to instance specifications is added for VCI pods that are created through VKE: `sys:vke:instance-type`. This facilitates you in querying VCIs and performing bill splitting based on system labels. |All |[Tag-based bill splitting](https://docs.byteplus.com/en/docs/vke/Tag-based-bill-splitting-for-instances) |


<span id="YDbgcoH6"></span>
## September 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Selecting multiple specifications during the creation of a VCI in the console |When you create a VCI in the VKE console, you can select multiple specifications to enhance your user experience. |All |[Creating general-purpose instances by specifying container vCPUs and memory](https://docs.byteplus.com/en/docs/vke/Creating-a-general-purpose-instance-based-on-specified-container-vCPUs-and-memory) |


<span id="qksRwo7E"></span>
## June 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Pulling images from self\-built image repositories |You can create VCIs or image caches in a self\-built image repository by using HTTP and self\-signed certificates. This resolves the ErrImagePull warning event and image pull failures that may occur when images are pulled from a self\-built image repository. |China (Beijing) |[Pulling images from self-built image registries during instance creation](https://docs.byteplus.com/en/docs/vke/Pull_images_from_a_self-hosted_Container_Registry_when_creating_an_instance) |
|||China (Shanghai) ||
|||China (Guangzhou) ||


<span id="V1HUkamO"></span>
## April 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Kubernetes v1.30 |VCI supports Kubernetes v1.30. The features of the latest Kubernetes version are available. |China (Beijing) |[Release notes of VKE based on Kubernetes v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30) |
|||China (Shanghai) ||
|||China (Guangzhou) ||


<span id=".XzIwMjTlubQxMuaciA=="></span>
## February 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Incrementally creating image caches in the console |When you create an image cache in the console, you can specify an existing image cache and enable incremental image cache creation. This shortens image cache creation duration and optimizes performance. |China (Beijing) |* [General-purpose instance](https://docs.byteplus.com/en/docs/vke/Create_General_purpose_instance) |
|||China (Shanghai) ||
|||China (Guangzhou) ||


<span id="ozFrrPyI"></span>
## More records

For the historical release notes, see [Historical release notes](https://docs.byteplus.com/en/docs/vke/VCI_History_feature_release_notes).
