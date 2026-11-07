---
title: "Historical release notes (2024)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-Historical-release-notes-2024"
---

This topic describes the updates to the features of VCI released in 2024.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">For the latest release notes of VCI, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-Release-notes">Release notes</a>.</div>


<span id="epI25wYC"></span>
## Note


* **Region** refers to the region where the feature was first released. The release regions coming up afterward will not affect the historical release notes. For the regions where features are actually available, please refer to the information on the console pages.

* The historical records of beta testing will not change after **beta ** features are officially released to the public. The iteration information of features is always contained in the latest release notes.


<span id="X1Nq4Iea"></span>
## December 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|Enhanced VCI scheduling capability |The scheduling capability of VCI is enhanced to specify multiple instance families at the same time. This helps you reduce concern about VCI resource limitations, such as instance family and subnet, and enables automatic resource scheduling based on the distribution of resources, such as instance family and subnet, without modifying business pods. |China (Beijing) |2024\-12\-10 |* [General-purpose instance](https://docs.byteplus.com/en/docs/vke/Create_General_purpose_instance) |
|||China (Shanghai) |2024\-12\-09 ||
|||China (Guangzhou) |2024\-12\-04 ||
|Added CPU metrics |The CPU metric `container_cpu_load_average_10s` is added. This metric allows you to obtain the average CPU load of a container in the last 10 seconds. It helps you understand the CPU resource usage of processes in the container and plan resources appropriately. |China (Beijing) |2024\-12\-10 |[Obtaining VCI metrics through virtual nodes](https://docs.byteplus.com/en/docs/vke/Getting-VCI-metrics-through-virtual-nodes#cpu) |
|||China (Shanghai) |2024\-12\-09 ||
|||China (Guangzhou) |2024\-12\-04 ||
|Incremental creation of image caches |In the API used to create an image cache, a new parameter has been added, which allows you to specify the image in an existing image cache as the base image to create a new image cache. This reduces redundant download operations for existing image layers and accelerates the creation and use of image caches. |China (Beijing) |2024\-12\-10 |[Create image cache](https://docs.byteplus.com/en/docs/vke/CreateImageCache) |
|||China (Shanghai) |2024\-12\-09 ||
|||China (Guangzhou) |2024\-12\-04 ||


<span id="qJeZc4iS"></span>
## November 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|Scheduling pods to VCI by using annotations in self\-built or cross\-cloud clusters |Self\-built or cross\-cloud Kubernetes clusters support scheduling pods to VCI through the annotation `vke.volcengine.com/burst-to-vci`. This improves the efficiency of using VCI for self\-built and cross\-cloud clusters, and maintains consistency with the usage method of VKE clusters. |China (Beijing) |2024\-11\-06 |[Elastically using VCI for self-managed or cross-cloud Kubernetes clusters](https://docs.byteplus.com/en/docs/vke/Elastically-using-VCI-for-self-managed-Kubernetes-clusters) |
|||China (Shanghai) |2024\-11\-07 ||
|||China (Guangzhou) |2024\-11\-05 ||
|Image caches support the instant availability feature of EBS. |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Image caches can use the instant availability feature of EBS, which shortens the time from creation to availability, reduces business waiting periods, and improves resource turnover efficiency. |China (Beijing) |2024\-11\-06 |[VCI image cache overview](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview) |
|||China (Shanghai) |2024\-11\-07 ||
|||China (Guangzhou) |2024\-11\-05 ||


<span id="YfvbxTyS"></span>
## October 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|New GPU metrics |GPU\-accelerated instances support the DCGM_FI_PROF_NVLINK_\* and DCGM_CUSTOM_XID_ERRORS_\* metrics. This provides GPU users with more comprehensive metrics monitoring capabilities. |China (Beijing) |2024\-10\-16 |[VCI GPU metrics](https://docs.byteplus.com/en/docs/vke/VCI-GPU-metrics) |
|||China (Shanghai) |2024\-10\-15 ||
|||China (Guangzhou) |2024\-10\-10 ||


<span id="utrlbRLw"></span>
## September 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|In\-place restart of VCI pods when partial container `metadata` is updated |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VCI supports in\-place upgrade of pods when you update the container image, as well as the `annotation` or the `label` of the `metadata` for the container. In business update scenarios, pod upgrades and business recovery are accelerated. When some containers are being upgraded, others can continue running, ensuring business continuity. |China (Beijing) |2024\-09\-09 |[In-place restart of VCI pods](https://docs.byteplus.com/en/docs/vke/VCI-Pod-in-place-restart) |
|||China (Shanghai) |2024\-09\-05 ||
|||China (Guangzhou) |2024\-09\-04 ||
|Instance families supported by RCI are specific to the availability zone level |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] When you select an availability zone on the RCI purchase page, instance families that are unavailable in the availability zone are dimmed. This helps you quickly purchase RCIs and improves user experience. |China (Beijing) |2024\-09\-11 |[RCI](https://docs.byteplus.com/en/docs/vke/VCI-Reserved-Container-Instance) |
|||China (Shanghai) |2024\-09\-10 ||
|||China (Guangzhou) |2024\-09\-12 ||
|Binding a VCI to multiple EIPs |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] Multiple EIPs can be bound to a single VCI. You can replace a multi\-ISP BGP EIP with multiple single\-ISP EIPs, which reduces business costs. |China (Beijing) |2024\-09\-03 |No |
|||China (Shanghai) |2024\-09\-03 ||
|||China (Guangzhou) |2024\-08\-29 ||
|VCI adapting to FlexPL to configure additional performance |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VCI supports PVs of the FlexPL cloud disk type with extra performance configurations. Cloud disks of the FlexPL type with extra performance configurations can provide higher IOPS and throughput performance. |China (Beijing) |2024\-09\-03 |[Using EBS as dynamic PersistentVolume](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes) |
|||China (Shanghai) |2024\-09\-03 ||
|||China (Guangzhou) |2024\-08\-29 ||
|Ignoring the resource requirements of specific containers during automatic adjustment of pod instance specifications |When VCI adjusts pod instance specifications based on container limits and requests, the resource requirements of specific containers can be ignored. In this way, exclusive resources are not allocated to some containers that do not affect your business in certain scenarios. |China (Beijing) |2024\-09\-11 |[Creating instances by ignoring specific container resource requirements](https://docs.byteplus.com/en/docs/vke/Creating-instances-by-ignoring-specific-container-resource-requirements) |
|||China (Shanghai) |2024\-09\-10 ||
|||China (Guangzhou) |2024\-09\-12 ||
|Optimized automatic cleanup policies for image caches |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] The default retention period for a manually created image cache has changed from permanent retention to 15 days. In addition, an API is provided to update image cache retention periods. This helps you reduce long\-unused image caches. It ensures sufficient image cache quota for your BytePlus root user. It also improves service feature performance. |China (Beijing) |2024\-09\-11 |* [Creating VCIs by using manually created image caches](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache)<br><br>* [UpdateImageCacheRetentionDays](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays) |
|||China (Shanghai) |2024\-09\-10 ||
|||China (Guangzhou) |2024\-09\-12 ||
|Specifying part of the kernel parameters for VCIs |You can specify the `vm.watermark_scale_factor` kernel parameter of the VCI. You can adjust the memory reclaim watermark proportionally to ensure that sufficient system resources are reserved. |China (Beijing) |2024\-09\-03 |[Pod annotation descriptions](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations) |
|||China (Shanghai) |2024\-09\-03 ||
|||China (Guangzhou) |2024\-08\-29 ||


<span id="Bedjfn76"></span>
## August 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|Integrating RCI with the Cost Center standard solution of BytePlus |RCI is integrated with the Cost Center standard solution of BytePlus, which supports features such as automatic renewal and periodic deduction. This standardizes instance deduction rules and improves the user experience. |China (Beijing) |2024\-08\-13 |[RCI](https://docs.byteplus.com/en/docs/vke/VCI-Reserved-Container-Instance) |
|||China (Shanghai) |2024\-08\-13 ||
|||China (Guangzhou) |2024\-08\-12 ||
|Automatically adding system labels during VCI creation |When you create a VCI, system labels, such as the cluster ID, namespace, and availability zone ID, are automatically added to the VCI. This facilitates you in querying the VCI and managing bill splitting by using these system labels. |China (Beijing) |2024\-08\-13 |[Label bill splitting](https://docs.byteplus.com/en/docs/vke/Tag-based-bill-splitting-for-instances) |
|||China (Shanghai) |2024\-08\-13 ||
|||China (Guangzhou) |2024\-08\-12 ||


<span id="RVDf4evg"></span>
## July 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|Project bill splitting |VCI integrates with the project management feature of BytePlus. You can specify the project a VCI belongs to and split VCI bills by project.<br><br>This helps you centrally manage VCI resources and costs by project.<br><br> |China (Beijing) |2024\-06\-30 |[Pod annotation description](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations) |
|||China (Shanghai) |2024\-07\-02 ||
|||China (Guangzhou) |2024\-06\-26 ||
|Supported time zone synchronization feature |You can specify time zones for virtual nodes. VCI pods can synchronize with the time zones of the virtual nodes or use hostPath to directly mount the time zone file to the container to modify the time zone of the container. This resolves the inconsistency between the time zone of the container image and the system time zone when you obtain system time for operations, such as log recording. |China (Beijing) |2024\-06\-30 |[Using VCIs by configuring vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile) |
|||China (Shanghai) |2024\-07\-02 ||
|||China (Guangzhou) |2024\-06\-26 ||


<span id="jeGgYysA"></span>
## June 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|RCI supports renewal and more GPU instance families |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] RCI supports the renewal feature, which can meet the requirements of general\-purpose scenarios and enhance the capabilities of RCI. |China (Beijing) |2024\-06\-03 |[RCI](https://docs.byteplus.com/en/docs/vke/VCI-Reserved-Container-Instance) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Label bill splitting |VCI supports the label bill splitting feature, which achieves bill splitting by label after you classify instances by adding labels. |China (Beijing) |2024\-06\-03 |[Label bill splitting](https://docs.byteplus.com/en/docs/vke/Tag-based-bill-splitting-for-instances) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Optimized automatic matching capability for VCI types |When you only specify the request for containers in VCI without specifying the limit, appropriate instance specifications can still be assigned. The automatic matching capability for VCI types is improved, which reduces the adaptation cost for migrating pods to VCI. |China (Beijing) |2024\-06\-03 |[Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|In\-place container image restart during update |When you update container images, you do not need to re\-create pods. This enables in\-place image updates, accelerating the process without interrupting business operations. |China (Beijing) |2024\-06\-03 |[In-place restart of VCI pods](https://docs.byteplus.com/en/docs/vke/VCI-Pod-in-place-restart) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|VCI supporting vePFS storage |[[Beta · Apply for Trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] VCI supports using vePFS\-type storage services via the standard CSI method. This further expands VCI's application scenarios. |China (Beijing) |2024\-06\-03 |[Using Parallel File Storage as PersistentVolumes](https://docs.byteplus.com/en/docs/vke/vePFS-Volumes) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|DNSCache solution |VCI supports the DNSCache solution, which provides the DNS cache proxy feature for virtual nodes. This eliminates the impact of large\-scale pods on CoreDNS in clusters. |China (Beijing) |2024\-06\-03 |* [Using NodeLocal DNSCache as DNS cache proxies](https://docs.byteplus.com/en/docs/vke/Using-NodeLocal-DNSCache)<br><br>* [node-local-dns](https://docs.byteplus.com/en/docs/vke/node-local-dns) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Supported network and storage performance burst for the n3i instance family |The network bandwidth, cloud disk bandwidth, and cloud disk IOPS metrics of the General\-purpose n3i (vci.n3i) instance family support burst transmission. This improves the network and storage performance of VCIs and meets your requirements for high concurrency. |China (Beijing) |2024\-06\-03 |[General-purpose n3i](https://docs.byteplus.com/en/docs/vke/VCI-General-purpose#.6YCa55So5Z6LLW4zaQ==) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Configuring the startup and exit priorities of containers |You can configure the startup and exit priorities for each container in a VCI by using environment variables. |China (Beijing) |2024\-06\-03 |[Configuring the startup and exit priorities of containers](https://docs.byteplus.com/en/docs/vke/Configuring-the-startup-and-exit-priorities-of-containers) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Improved GPU metrics |Eight GPU metrics are supported. This allows you to monitor more pod GPU status by using VMP in VCI. |China (Beijing) |2024\-06\-03 |[VCI GPU metrics](https://docs.byteplus.com/en/docs/vke/VCI-GPU-metrics) |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||
|Added VCI usage information in the VKE console |VCI resource usage information is added on the **Overview** page in the VKE console and the **Overview** page on the cluster details page. The pages clearly display VCI specifications, computing resource usage, and other information, which helps you collect statistics on VCI resources at the cluster level. |China (Beijing) |2024\-06\-03 |No |
|||China (Shanghai) |2024\-05\-30 ||
|||China (Guangzhou) |2024\-06\-04 ||


<span id="i8NdNwyk"></span>
## May 2024


|**Feature name** |**Description** |**Region** |**Release date** |**Related documentation** |
|---|---|---|---|---|
|Vital Container Instance (VCI) |Vital Container Instance (VCI) is released for the first time. VCI is a serverless and containerized computing service that supports capabilities such as second\-level startup, high\-concurrency creation, and security isolation between sandboxed containers. |Asia Pacific (Johor) |2024\-05\-30 |[What is Vital Container Instance](https://docs.byteplus.com/en/docs/vke/What-is-Vital-Container-Instance) |
