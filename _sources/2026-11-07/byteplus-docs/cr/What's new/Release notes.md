---
title: "Release notes"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/release-notes"
---

This topic introduces the latest CR feature updates. New features are rolled out gradually across regions. Feel free to try them when they become available.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the release notes, the <strong>Region</strong> field refers to the regions where the feature was first released. The release regions added later will not be put in the historical release notes. For the regions where features are actually available, please refer to the information on the console pages.</div>


<span id="mi5YxSWS"></span>
## August 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Custom expiration time supported for temporary access credentials |The validity period of the temporary access credentials for an instance is no longer fixed at 1 hour. You can now set it to a value between 10 minutes and 12 hours. The default is 1 hour. |All |[Instance access credentials](https://docs.byteplus.com/en/docs/cr/Get-access-credentials) |


<span id="RTtGQygk"></span>
## July 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Instance monitoring information |Monitoring information is available for instances. This information includes runtime metrics such as public/private bandwidth, storage usage, request QPS, and QPS by API. Alert rules can be configured for metrics reported to VMP. |All |[View monitoring information](https://docs.byteplus.com/en/docs/6420/2608575?lang=en) |


<span id="f2xClwVg"></span>
## June 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Encrypted storage supported for image data |CR instances support server\-side encryption, which enables data to be stored in encrypted form on the server side to meet data security and compliance requirements in certain scenarios. |All |[Creating Standard instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance?lang=en) |
|Modification supported for image tag descriptions |CR supports adding descriptions to image tags to indicate images' purpose, status, or environment (for example, production or test). |All |[Editing image tag descriptions](https://docs.byteplus.com/en/docs/cr/Edit_image_tag_description?lang=en) |


<span id="KwksksHJ"></span>
## April 2026


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Container image signature | CR integrates with Key Management Service (KMS) asymmetric keys, enabling automatic namespace\-level signing and manual signing for individual image tags to ensure image integrity and source provenance trust. Signing rules can be created/deleted through both the Image signature page and the Namespace page. |All |* [Creating image signatures](https://docs.byteplus.com/en/docs/cr/Create_image_signature)<br><br>* [Deleting image signatures](https://docs.byteplus.com/en/docs/cr/Delete_image_signature) |


<span id="ZUCrXIs1"></span>
## December 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Docker Registry image migration supported |Docker Registry\-compatible images can be quickly migrated to CR to meet service migration requirements. |All |[Synchronizing external repositories to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry) |


<span id="ajq530KN"></span>
## November 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Upgrading from Micro Edition instances to Standard Edition instances |Micro Edition instances can be upgraded to Standard Edition instances for higher performance and SLA assurance. |All |[Upgrading from Micro Edition instances to Standard Edition instances](https://docs.byteplus.com/en/docs/cr/Upgrade_a_Micro_Edition_instance_to_a_Standard_Edition_instance) |


<span id="sCj952QU"></span>
## October 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Management of custom domain names |A custom domain name facilitates unified enterprise\-level service management and ensures domain name consistency after CR instance migration, maintaining service continuity. |All |[Domain management](https://docs.byteplus.com/en/docs/cr/Domain_name_management) |


<span id="6V7I2Llu"></span>
## September 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Automatic cleanup of OCI artifact repositories with empty image tags |When all image tags in an OCI artifact repository are cleared based on tag retention rules, the system will automatically delete the empty repository. |All |[Tag retention rules](https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule) |
|Micro Edition instances supported |Micro Edition instances are available on BytePlus. |All |[Micro Edition instances](https://docs.byteplus.com/en/docs/cr/Micro_Edition_instance) |
|Terraform supported |Instance creation and other operations can be implemented by using Terraform. |All |[Using CR with Terraform](https://docs.byteplus.com/en/docs/cr/Using_Container_Registry_with_Terraform) |


<span id="iunDDQ8R"></span>
## August 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Terminate a synchronization task ||All ||
|Connecting cross\-account VPCs |‌Instances and proxy cache registries now support cross\-region VPC connectivity. Pulling images and Helm charts over the internal network effectively boosts push and pull speeds while eliminating public network bandwidth costs. |All |[Connecting cross-account VPCs](https://docs.byteplus.com/en/docs/cr/Connect_VPCs_across_different_accounts) |
|Configuring resource capacity alerts |You can configure quota alerts for your CR resources based on usage quantity or percentage. These alerts provide early warnings, allowing you to manage resource capacity proactively and prevent task failures from resource exhaustion. |All |[Configuring resource capacity alerts](https://docs.byteplus.com/en/docs/cr/Configure_resource_capacity_alerts) |


<span id=".XzIwMjXlubQwNuaciA=="></span>
## July 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Image list display optimization |The image tag list supports drag\-based column width adjustment and can display longer image names/addresses. |All |None |
|Instance label search supported |Add tags to the instance. You can search for and select existing tags. You can also create custom ones if existing tags cannot meet your requirements. |All |[Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance) |


<span id=".XzIwMjXlubQwNuaciA=="></span>
## June 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|VPC access quota increase |The maximum VPC access quota is increased to 20. |All |[VPC access quota](https://docs.byteplus.com/en/docs/cr/vpc-quota) |
|Container image distribution and startup acceleration |As an efficient compression algorithm, zstd (Zstandard) achieves a better balance between compression ratio and speed than gzip. This balance optimizes image transmission and startup. |All |[Container Image Distribution and Startup Acceleration Based on Zstd Compression Algorithm](https://docs.byteplus.com/en/docs/cr/Image_distribution_and_startup_acceleration_based_on_Zstd) |



|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Tag retention rule optimization |Image push/pull conditional rules can be associated with regex matching rules using OR/AND logic, enabling more flexible retention of specified images. |Asia Pacific (Johor) |[Creating tag retention rules](https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule) |
|||Asia Pacific (Jakarta) ||


<span id=".XzIwMjXlubQwNOaciA=="></span>
## April 2025

<span id=".XzIwMjXlubQwM-aciA=="></span>
## March 2025


|**Feature name** |**Description** |**Region** |**Related documentation** |
|---|---|---|---|
|Pay\-as\-you\-go to mixed billing |Standard instance billing supports switching from pay\-as\-you\-go to partial subscription. |Asia Pacific (Johor) |[Switching from Pay-as-You-Go to Mixed Billing (Partial Subscription)](https://docs.byteplus.com/en/docs/cr/Switch_from_Pay-as-you-go_to_Mixed_Billing) |
|||Asia Pacific (Jakarta) ||
