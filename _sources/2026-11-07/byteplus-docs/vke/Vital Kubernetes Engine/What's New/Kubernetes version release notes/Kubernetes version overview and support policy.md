---
title: "Kubernetes version overview and support policy"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy"
---

VKE provides enterprise\-grade container management capabilities with high performance, high reliability, and extreme elasticity based on community Kubernetes. As community Kubernetes versions continue to upgrade, VKE will periodically release the supported Kubernetes versions. This topic introduces the overview of the Kubernetes versions supported by VKE and its support policy.

<span id=".54mI5pys5Y-36K-05piO"></span>
## Version number description

The Kubernetes version number format supported by VKE is as follows.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0fada2ef7b52ff5e0f4b6610f10e69d0.png) </span>


* **Kubernetes version**: follows the community Kubernetes version format, expressed as **x.y.z**, where **x** is the major version, **y** is the minor version, and **z** is the patch version. For more information, see [Community Kubernetes version policy](https://kubernetes.io/zh-cn/releases/version-skew-policy/#supported-versions).

* **VKE version**: The patch version released by VKE, in the format of **vke.(n)** .


<span id="fJaAbE6L"></span>
## Version lifecycle


* After the Kubernetes community releases even\-numbered minor versions (e.g., v1.36 and v1.38), VKE gradually begins supporting these Kubernetes minor versions within 30 business days.

* Each supported Kubernetes minor version goes through the GA phase, EOM phase, and EOS phase from the start of support to the end of service. The phases are described in the table below.

   
   |**Phase** |**Introduction** |
   |---|---|
   |GA (General Availability) |General Availability (GA) phase. VKE provides patch and service support for Kubernetes minor versions in the GA phase, which is defined as 18 months. |
   |EOM (End of Marketing) |End of Marketing (EOM) phase. The EOM phase is defined as 6 months. During this period, VKE does not support the creation of new clusters on this version, and no longer assumes responsibility for the stability of existing clusters on this version, nor does it commit to the [SLA](https://docs.byteplus.com/en/docs/vke/BytePlus-VKE_Service-Level-Agreement). For more risk descriptions, see [Risks from expired versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy#.6L-H5pyf54mI5pys6aOO6Zmp) section below in this document. |
   |EOS (End of Service) |The phase in which all services will be unavailable. The EOS phase begins after the EOM phase ends. VKE no longer provides any security issue fixes for Kubernetes minor versions in the EOS phase, and O&M support is reduced to the minimum level. For more risk descriptions, see [Risks from expired versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy#.6L-H5pyf54mI5pys6aOO6Zmp) section below in this document. |
   |EOL (End of Life) |The nodes with a special lifecycle. Only v1.28 (and earlier) versions use EOL to describe nodes, indicating that the version has expired. Versions v1.30 and above use the EOM and EOS to describe nodes rather than EOL.<br><br>For Kubernetes minor versions that have already reached EOL, clusters of this version cannot be created, and such versions may pose risks such as unstable operation and cluster upgrade failures. VKE does not guarantee the quality or effectiveness of technical support. For more risk descriptions, see [Risks from expired versions](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy#.6L-H5pyf54mI5pys6aOO6Zmp) section below in this document. |
   


<span id="PneEuucQ"></span>
## Version release calendar


<Tabs>
<Tab zoneid="cPdGNGotED" title="Current running version">
<TabTitle>Current running version</TabTitle>

The list of Kubernetes versions currently supported by managed VKE clusters is as follows.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For versions that are about to enter EOM, we recommend planning ahead for an upgrade window.</div>



|Kubernetes version |GA time |EOM time |EOS time |
|---|---|---|---|
|[v1.36](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_36) |June 2026 |December 2027 |June 2028 |
|[v1.34](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_34) |February 2026 |November 2027 |May 2028 |
|[v1.32](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_32) |November 2025 |October 2027 |April 2028 |
|[v1.30](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30) |February 2025 |October 30, 2026 |April 30, 2027 |



</Tab>
<Tab zoneid="XGSTPWqUI6" title="Expired version">
<TabTitle>Expired version</TabTitle>

The list of expired versions among the Kubernetes versions released by VKE is as follows.

<div data-tips="true" data-tips-type="danger">Outdated versions may pose risks such as unstable operation and cluster upgrade failures, and VKE does not guarantee the quality or effectiveness of technical support for expired versions. To ensure the normal operation of your business, please upgrade the Kubernetes versions of the relevant clusters as soon as possible. For instructions on how to upgrade a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Cluster upgrade operation</a>.</div>



|Kubernetes version |Status |GA time |EOL time |
|---|---|---|---|
|[v1.28](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28) |No longer maintained |August 2024 |June 30, 2026 |
|[v1.26](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26) |No longer maintained |December 2023 |March 9, 2026 |
|[v1.24](https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_24) |No longer maintained |June 2023 |April 30, 2025 |



</Tab>
</Tabs>


<span id=".54mI5pys5pSv5oyB"></span>
## Version support policy

The Kubernetes version policy supported by VKE is as follows.


* Since November 2022, VKE has only released even\-numbered Kubernetes minor versions.

* VKE ensures the stable operation of the latest three Kubernetes minor versions. Clusters with outdated versions may face risks such as unstable operation and cluster upgrade failures. We recommend upgrading your Kubernetes version promptly.

* VKE provides technical support for the latest three Kubernetes minor versions that are under active maintenance. The support includes Q&A, online guidance, troubleshooting, and issue diagnosis. However, for clusters running outdated Kubernetes versions, the quality and effectiveness of technical support are not guaranteed.


<span id=".54mI5pys5Y-R5biD5ZGo5pyf"></span>
## Version constraints


* The version upgrade feature only supports upgrading between adjacent minor versions released by VKE. Cross\-version upgrades that skip multiple minor versions are not supported. For example, upgrading directly from v1.32 to v1.36 is not supported. You must first upgrade v1.32 to v1.34, and then upgrade to v1.36.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Patch version upgrades are not subject to this restriction.   </div>
   

* For patch versions, in principle, technical support is only provided for the latest patch version. For older patch versions, please upgrade to the latest patch version as soon as possible to receive full technical support.


<span id=".6L-H5pyf54mI5pys6aOO6Zmp"></span>
## Risks from outdated versions

After your cluster's Kubernetes version expires, you will no longer have access to the latest features released by the Kubernetes community and VKE, and will also face the following risks:


|Phase |Risk description |
|---|---|
|EOM |* Creation of new clusters on this version is not supported.<br><br>* Clusters of this version that have already been created can still be used, but VKE no longer assumes responsibility for their stability, nor does it commit to the [SLA](https://docs.byteplus.com/en/docs/vke/BytePlus-VKE_Service-Level-Agreement).<br><br>* VKE provides limited maintenance at a minimum level, handling only very few critical security issues.<br><br>* No further patch versions will be released for this version, and no new features will be added to clusters running this version.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Before entering the EOM phase, VKE will send a notification 90 days in advance. There will be at least 3 rounds of notifications, covering SMS, email, Feishu, in\-site messages, and official website product announcements.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The coverage of advance notifications depends on the message notification channels bound to your BytePlus account.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Upon receiving the EOM advance notification, please upgrade your business as soon as possible to protect your own interests. For instructions on how to upgrade a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Cluster upgrade operation</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The cluster upgrade must be completed by the end of the EOM phase (6 months). <strong>Any risks arising from the inability to upgrade due to the user's own reasons shall be borne by the user.</strong></div><br> |
|EOS and EOL |* Creation of new clusters on this version is not supported.<br><br>* No further patch versions will be released for this version, and no new features will be added to clusters running this version.<br><br>* Clusters on this version will not receive Kubernetes bug fixes or security vulnerability patches.<br><br>* VKE does not guarantee the timeliness of technical support.<br><br>* VKE makes no guarantees regarding the normal operation or any other aspects of clusters running this version.<br><br>* Based on considerations of cluster availability and security, VKE reserves the right to forcibly upgrade clusters on expired versions, meaning the expired cluster version will be forcibly upgraded to the minimum version currently supported by VKE.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Before performing a forced upgrade, VKE will send relevant notifications via SMS, email, or in\-site messages at least one month in advance. Please pay attention to these notifications and plan your upgrade. For information on cluster upgrades, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Cluster upgrade operation</a>.</div><br> |
