---
title: "New feature release notes"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/New-feature-release-notes"
---

This topic introduces the feature releases of various ECS instance versions. New features will be gradually released in each region. We welcome you to explore them.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The "Beta" products or features are not available to all users. To help you understand the products, some documents for "Beta" products or features have been made available to all users. Note that certain documents for "Beta" products or features are only accessible to users with access permission to such products. If you need to use Beta products or features, please contact your account manager to apply.</div>



<span id="xVJXTmHU"></span>
## September 2026


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Instance |Offsetting resources \- RSC supports projects and tags. |All |GA |[Purchase Reserved Storage Capacity (RSC)](https://docs.byteplus.com/en/docs/ecs/Purchase-a-reserved-storage-capacity) |
|2 ||Added support for managing files in ECS instances via Terminal, including preview, upload, download, rename, and delete operations. |All |Beta |[Managing files in ECS instances via Terminal](https://docs.byteplus.com/en/docs/ecs/Managing_files_in_ECS_instances_via_Terminal) |
|3 |Security |Official launch of resetting the instance login password online. |All |GA |[Resetting login password](https://docs.byteplus.com/en/docs/ecs/Resetting-passwords) |
|4 |Deployment set |Official launch of instance deployment at rack and switch granularity through the "Availability Group policy" feature. |All |GA |[Managing deployment sets](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview) |


&nbsp;

<span id="1yxCqFXJ"></span>
## July 2026


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Performance burst |Supports enabling performance burst for ESSD FlexPL volumes during instance creation. |All |Beta |[Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) |


<span id="Tjc4bZ6R"></span>
## March 2026


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Network |* Supports managing network interface MTU value.<br><br>* Launch of the jumbo frame feature. It is applicable for bulk data transfers and have strict limitations on traffic path and instance type. |All |GA |* [Managing MTU values of network interfaces](https://docs.byteplus.com/en/docs/ecs/Modify-the-MTU-of-the-Network-Interface)<br><br>* [Enabling/disabling jumbo frames](https://docs.byteplus.com/en/docs/ecs/Enabling_or_Disabling_jumbo_frames) |


<span id="dHJFUAl7"></span>
## February 2026


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Image |The image inspection feature supports detection of O11yAgent plugin information. |All |GA |[Check item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description) |


<span id="JO9HC7R9"></span>
## January 2026


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Event monitoring |Added a scheduled maintenance window to enable flexible and automated O&M. |All |Beta |[Scheduled maintenance window overview](https://docs.byteplus.com/en/docs/ecs/Overview_of_Planned_Maintenance_Windows) |


<span id="CjsybVIw"></span>
## December 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Instance |Supports more resolution options for instances running Windows Server and Ubuntu operating systems. |All |Beta |[Changing the screen resolution](https://docs.byteplus.com/en/docs/ecs/Overview_05) |
|2 |Event |Discontinuation of the event notification subscription feature. |All |GA |* [Configure event monitoring notifications](https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications?lang=en)<br><br>* [Announcement on discontinuation of the "Subscribe to event notifications" feature](https://docs.byteplus.com/en/docs/ecs/Announcement_on_discontinuation_of_the_Subscribe_to_event_notifications_feature?lang=en) |
|3 |Image |Supports copying a custom image from a region in the Chinese mainland to Asia Pacific (Johor). |All |Beta |[Copying custom images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) |
|4 ||Official launch of the features of copying and sharing images within the same region. |All |GA |[Copying shared images](https://docs.byteplus.com/en/docs/ecs/Copy_shared_image) |


<span id="KAwXh1Wa"></span>
## November 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Snapshot |Up to 256 manual snapshots and 1,024 automatic snapshots can be created for each volume. |All |GA |* [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots)<br><br>* [Create snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot)<br><br>* [Creates an auto snapshot policy](https://docs.byteplus.com/en/docs/ecs/Create-an-auto-snapshot-policy)<br><br>* [Creates a snapshot consistency group](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot-consistency-group) |
|2 |Storage placement group |Supports associating a volume with a storage placement group and specifying a sub\-placement group ID via the console. Based on metrics such as cluster health and resource utilization, the system deploys volumes with different sub\-placement group IDs to separate physical clusters, thereby achieving data isolation and protection. |All |GA |[Managing placement groups](https://docs.byteplus.com/en/docs/ecs/Manage-placement-group) |
|3 |Instance |Supports using an instance created based on a whole image to create another instance with the same configurations. |All |GA |[Purchasing an instance with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration) |
|4 |Image |Custom image detection: Supports one\-click repair of high\-risk issues in Windows images. Additionally, new detection items for Linux and Windows images have been added. ||Beta |[Checking custom images and addressing risk items](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images) |
|5 |ESSD FlexPL volume |By default, the average random write latency of newly created ESSD_FlexPL volumes in some availability zones is within 0.2 ms, and in other regions, the latency ranges from 0.3 to 0.5 ms. |China (Beijing), China (Shanghai), and Asia Pacific (Johor) |GA |* [Volume specification](https://docs.byteplus.com/en/docs/ecs/Volume-specifications)<br><br>* [ESSD FlexPL volume](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume#.5Z-65YeG5oCn6IO9) |
|6 |Instance diagnosis |Supports comprehensive instance diagnosis. |All |GA |[Instance diagnosis](https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status) |
|7 |Monitoring |Supports second\-level monitoring for operating system\-related metrics. |All ||[Viewing basic monitoring data/operating system monitoring data](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |


<span id="crRIFVyu"></span>
## October 2025

<span id="crRIFVyu"></span>
## September 2025


|Serial number |Feature |Feature description |Release regions |Phase |Documentation |
|---|---|---|---|---|---|
|1 |Snapshot chain capacity |Supports viewing snapshot chain capacity. |All |GA |* [Viewing snapshot chains](https://docs.byteplus.com/en/docs/ecs/View-a-snapshot-chain)<br><br>* [DescribeSnapshotChains](https://docs.byteplus.com/en/docs/ecs/Describesnapshotchains) |
|2 |Instance diagnosis |Instance device detection is updated to GA. ||GA |[Instance diagnosis](https://docs.byteplus.com/en/docs/ecs/Diagnose_instance_health_status?TagIDs=2,288,70,69) |
|3 |Instance |When creating an instance with the same configuration as a custom image\-based instance, you can use the preconfigured credentials (key pair or password) from the image to log in to the new instance. ||GA |[Purchasing an instance with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration) |
|4 |Image |Custom image detection feature supports one\-click repair of **items for which fixing is strongly recommended** identified in Linux images, and supports detection of  NVIDIA, OFED, and DOCA versions installed within an image. ||Beta |[Checking custom images and addressing risk items](https://docs.byteplus.com/en/docs/ecs/Detect_Custom_Images) |
|5 |Monitoring |Supports monitoring disk space utilization at the granularity of disk mount points. ||GA |[Viewing basic monitoring data/operating system monitoring data](https://docs.byteplus.com/en/docs/ecs/View-basic-and-operating-system-monitoring-data) |
|6 |Event |Supports configuring the nofail parameter in`/etc/fstab` for an instance. ||GA |[Method 2: Resolve local volume failures through instance redeployment](https://docs.byteplus.com/en/docs/ecs/Redeploying-instances) |
|7 |Launch template |Supports selecting "Spots" as the billing method during creation of a launch template/version. ||GA |* [Creating instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-templates)<br><br>* [Creating versions of instance launch templates](https://docs.byteplus.com/en/docs/ecs/Creating-launch-template-versions) |
|8 |O&M orchestration |Supports creating custom templates. |All |GA |[Create custom templates](https://docs.byteplus.com/en/docs/ecs/Creating_custom_templates) |
|9 ||Supports creating orchestration plans via custom templates. ||GA |[Creating orchestration plans](https://docs.byteplus.com/en/docs/ecs/Create_an_orchestration_plan) |


<span id="k5xrzc35"></span>
## August 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Volume anti\-affinity |Supports associating a volume with a storage placement group and specifying a sub\-placement group ID via API. Based on metrics such as cluster health and resource utilization, the system deploys volumes with different sub\-placement group IDs to separate physical clusters, thereby achieving data isolation and protection. |All |GA |* [CreateVolume](https://docs.byteplus.com/en/docs/ecs/Createvolume)<br><br>* [CreatePlacementGroup](https://docs.byteplus.com/en/docs/ecs/Createplacementgroup)<br><br>* [DescribePlacementGroups](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroups)<br><br>* [DescribePlacementGroupDetails](https://docs.byteplus.com/en/docs/ecs/Describeplacementgroupdetails)<br><br>* [ModifyPlacementGroup](https://docs.byteplus.com/en/docs/ecs/Modifyplacementgroup)<br><br>* [DeletePlacementGroup](https://docs.byteplus.com/en/docs/ecs/Deleteplacementgroup) |
|2 |Instance metadata |Supports accessing instance metadata through security hardening mode. |All |Beta |[Viewing instance metadata](https://docs.byteplus.com/en/docs/ecs/Viewing-instance-metadata) |
|3 |Additional performance |Supports modifying the additional performance of TSSD volumes and ESSD FlexPL volumes in a batch. |All |GA |* [TSSD volume](https://docs.byteplus.com/en/docs/ecs/Volume-specification-tssd-tl0-Volume)<br><br>* [ESSD FlexPL volume](https://docs.byteplus.com/en/docs/ecs/essd_flexpl_volume) |
|4 |Volume specification |Supports modifying specifications of volumes in a batch. |All |GA |[Modifies the specifications of a volume](https://docs.byteplus.com/en/docs/ecs/Modify-volume-type) |


<span id="k5xrzc35"></span>
## July 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Image |Supports copying and sharing images within the same region. |All |Beta |[Copying shared images](https://docs.byteplus.com/en/docs/ecs/Copy_shared_image) |
|2 ||Supports selecting a whole image to replace the operating system. ||GA |[Change the operating system](https://docs.byteplus.com/en/docs/ecs/Changing-OS) |
|3 ||Supports copying a custom image from a region in the Chinese mainland to Asia Pacific (Johor). ||Beta |[Copying custom images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) |
|4 |Network and security group |Supports replacing instance VPCs or subnets in a batch. ||GA |[Changing VPC or subnet](https://docs.byteplus.com/en/docs/ecs/Changing-the-VPC-or-subnet-of-an-ECS-instance) |
|5 ||Supports batch adding, replacing, or removing multiple instances to/from security groups. ||GA |[Changing security groups](https://docs.byteplus.com/en/docs/ecs/Changing-security-groups) |
|6 |Instance diagnosis |Supports new diagnostic items related to network service monitoring, including those targeted at network PPS, BPS, and session limits. |Asia Pacific (Johor), China (Shanghai), China (Guangzhou), China (Beijing) |GA |[Diagnosis item overview](https://docs.byteplus.com/en/docs/ecs/Diagnosis_summary) |
|7 ||Added diagnostic capabilities for OpenSSL, connectivity of key instance\-dependent components, and other aspects. ||GA ||
|8 |O&M orchestration |Supports the orchestration plan feature. |China (Shanghai), China (Beijing), China (Guangdong), Asia Pacific (Johor), China (Hong Kong) |GA |[Orchestration overview](https://docs.byteplus.com/en/docs/ecs/Overview_of_Process_Orchestration) |
|9 |Monitoring |Windows supports process monitoring. |All |<div style="text-align: center"><br>GA</div><br> |[Managing process monitoring data](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics) |
|10 ||Supports viewing metrics such as GPU encoder usage, GPU decoder usage, and GPU memory usage of instance GPU/RDMA. |||[Viewing GPU/RDMA monitor​ing data of instances](https://docs.byteplus.com/en/docs/ecs/View-instance-GPU-and-RDMA-monitoring-data) |
|11 |Event |Added InstanceDiskStalled (Seriously impaired disk performance for instance) event. |||[Event type overview](https://docs.byteplus.com/en/docs/ecs/Event-type-overview) |
|12 ||Supports event levels, including critical, warning, and informational levels. |||[Querying and handling events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events) |
|13 ||Certain events support restoring normal operation by restarting the instance. Certain events support root cause operations for instance exceptions. ||||


<span id="GzCvESXe"></span>
## June 13, 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Monitoring |Supports manually adding custom processes. |China (Shanghai), China (Beijing), China (Guangdong), Asia Pacific (Johor), China (Hong Kong) |GA |[Managing process monitoring data](https://docs.byteplus.com/en/docs/ecs/Instance-processes_TCP-connection-metrics?TagIDs=2,70,69) |


<span id="YYWFCgAO"></span>
## June 10, 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Instance |The instance deletion protection capability was launched. |All |GA |[Instance deletion protection](https://docs.byteplus.com/en/docs/ecs/Instance_delete_protection) |
|2 |O&M orchestration |New ECS batch operations that are dependent on O&M orchestration have been added. ||GA |* [Batch Send remote commands](https://docs.byteplus.com/en/docs/ecs/Batch_send_remote_commands)<br><br>* [Downloading files to multiple instances](https://docs.byteplus.com/en/docs/ecs/Download_files_to_multiple_instances)<br><br>* [Changing instance hostname](https://docs.byteplus.com/en/docs/ecs/Changing-the-hostname-of-an-instance)<br><br>* [Add multiple instances to a scaling group](https://docs.byteplus.com/en/docs/ecs/Add_multiple_instances_to_the_scaling_group) |
|3 |Image |Supports detecting OFED driver version information via the image inspection feature. ||GA |[Check item description](https://docs.byteplus.com/en/docs/ecs/Detect_item_description) |
|4 ||Supports copying custom images between regions outside the Chinese mainland. ||Beta |[Copying custom images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images) |
|5 ||Official launch of the features of importing and exporting full machine images. ||GA |* [Importing custom images](https://docs.byteplus.com/en/docs/ecs/Importing-custom-images-1)<br><br>* [Exporting custom images](https://docs.byteplus.com/en/docs/ecs/Exporting-custom-images) |
|6 |Event monitoring |Supports automatic cancellation of events upon host machine changes (such as manual hot or cold migration, evacuation, type changes, power\-on, and restart). ||GA |[Querying and handling events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events?TagIDs=2,70,69) |


<span id="kYf16Re6"></span>
## June 04, 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |O&M orchestration |Common O&M tasks (such as batch operations on instances and images) support configuring a maximum error count. |<div style="text-align: center"><br>China (Beijing), China (Shanghai), China (Guangdong), Asia Pacific (Johor), Asia Pacific (Jakarta)</div><br> |GA |[Creating tasks for batch instance operations](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task) |


<span id="MUHiXWR3"></span>
## April 29, 2025


|Serial number |Feature |Feature description |Release regions |Stage |Documentation |
|---|---|---|---|---|---|
|1 |Instance diagnosis |Added diagnostic items for Linux\-related configuration and instance configuration management. |Asia Pacific (Johor), China (Shanghai), China (Guangzhou), China (Beijing) |GA |[Diagnosis item overview](https://docs.byteplus.com/en/docs/ecs/Diagnosis_summary) |


&nbsp;
