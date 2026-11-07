---
title: "Features"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/features"
---

This article introduces the product features of BytePlus CR.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">✅ indicates that it is supported.</div>


* <div data-tips="true" data-tips-type="default">A hyphen (\-) indicates not supported.</div>



&nbsp;


|Category |Feature |Feature description |Standard instance ||Related documentation |
|---|---|---|---|---|---|
||||Standard |Micro Edition ||
|**Instance management** |Dedicated Registry service |Each instance has an independent registry service, providing stable image management capabilities. |✅ |\- |[Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance) |
||Dedicated data storage backend |Each instance has an independent storage backend, with data stored in isolation to ensure data security. |✅ |\- |\- |
||Dedicated service access domain name |Each instance is assigned an independent service domain name for image push and pull. The system domain name is composed of instance name, region, and other information. |✅ |✅ |\- |
||Temporary/long\-term access credential |Supports logging in to an instance using both temporary token and long\-term password methods, suitable for different security scenarios. |✅ |✅ |[Standard Edition instance access credentials](https://docs.byteplus.com/en/docs/cr/Get-access-credentials) |
||Instance upgrade |Support one\-click upgrade of instance specification without manual data migration. |\- |✅ |[Micro Edition Instance upgrade to Standard Edition Instance](https://docs.byteplus.com/en/docs/cr/Upgrade_a_Micro_Edition_instance_to_a_Standard_Edition_instance) |
||Instance Overview |Shows instance basic information and resource usage state (storage capacity, public network traffic, resource quota, and more). |✅ |✅ |\- |
|**Access control** |Public NAT for internet endpoint |Access instance via public network. |✅ |✅<br><br>Enabled by default |[Enabling public network access](https://docs.byteplus.com/en/docs/cr/enable-public-network-access) |
||VPC private network connectivity |Access instance via private network VPC to ensure internal network transmission security. Supports connectivity for this account, cross\-product, and cross\-account VPCs. |✅ |✅ |[Connecting to the VPC of the current account](https://docs.byteplus.com/en/docs/cr/connect-vpcs-under-the-same-account) |
||VPC access quota |Supports increasing the maximum number of VPCs that can connect to a single instance. |✅ |\- |[Increasing instance quotas](https://docs.byteplus.com/en/docs/cr/increase-instance-quota) |
||IAM Authorizations |Use IAM policy to grant fine\-grained permissions to sub\-users, distinguishing resource control permissions. |✅ |✅ |[Authorizing IAM users](https://docs.byteplus.com/en/docs/cr/authorize-iam-users) |
||Robot account |Create a dedicated robot account for image push and pull operations in CI/CD and other automated scenarios. |✅ |\- |[Creating robot accounts](https://docs.byteplus.com/en/docs/cr/Create-robot-accounts) |
|**Artifact repository** |OCI artifact repository management |The OCI artifact repository is used to store container images or Helm Charts and other artifacts that comply with the OCI standard, supporting both public and private access types. |✅ |✅ |[Creating OCI artifact repositories](https://docs.byteplus.com/en/docs/cr/create-an-OCI-repository) |
||tag management |Manage image tags in the artifact repository to distinguish different build artifacts of the same base image. |✅ |✅ |\- |
||Helm Chart hosting |Store and manage Kubernetes application packages in Helm Chart format, and support versioned management. |✅ |✅ |\- |
|**Artifact push and pull**<br><br> |Image push and pull |Push and pull images. |✅ |✅ |[Push and pull image](https://docs.byteplus.com/en/docs/cr/push-and-pull-images-in-an-enterprise-instance) |
||Helm Chart push and pull |Push and pull Helm Chart artifacts. |✅ |✅ |[Pushing and Pulling Helm Charts](https://docs.byteplus.com/en/docs/cr/push-and-pull-Helm-charts-in-an-enterprise-instance) |
||Batch modify artifact public/private type |Supports batch switching between public and private access types for OCI artifact repositories. |✅ |✅ |[Batch modifying public/private types of OCI artifacts](https://docs.byteplus.com/en/docs/cr/Bulk_modify_the_public_or_private_type_of_OCI_artifacts) |
||Viewing image layer information |View image layer details to understand the image building process. |✅ |\- |[Viewing image layer information](https://docs.byteplus.com/en/docs/cr/View_image_layer_information) |
|**Image Security** |Image malicious file scanning |Detect malicious files and unexpected files in images to ensure business security. |✅ |\- |[Image scanning](https://docs.byteplus.com/en/docs/cr/scan-container-images) |
||Image signature |Integrates BytePlus Key Management Service (KMS) asymmetric keys to enable automatic signing at the namespace level and manual signing for individual image tags. |✅ |\- |[Create image signature](https://docs.byteplus.com/en/docs/cr/Create_image_signature) |
|**Image Distribution** |External registry migration |Synchronize images and Helm Charts from third party image repositories (AWS ECR, Harbor, ...) to CR Instance. |✅ |✅ |[Synchronizing external repositories to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry) |
||Inter\-instance synchronization |Within the same root user account, instances support image synchronization within the same region and across regions. |✅ |\- |[Synchronizing images within or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions) |
||P2P acceleration |Utilize internal network bandwidth between compute nodes for peer\-to\-peer image distribution, improving image pull efficiency in large\-scale clusters and saving public network bandwidth. |✅ |\- |[P2P acceleration overview](https://docs.byteplus.com/en/docs/cr/p2p-acceleration-overview) |
||Image lazy loading |Pre\-generate accelerated image replicas in Nydus format for on\-demand loading, significantly improving container start speed. |✅ |\- |[Creating image lazy loading conversion rules](https://docs.byteplus.com/en/docs/6420) |
||Proxy repository acceleration |Proxy external image sources such as Docker Hub, GHCR, or self\-built Docker Registry, cache images locally and accelerate pulls, reducing dependency on overseas networks. |\- |\- |[Create proxy cache registry](https://docs.byteplus.com/en/docs/cr/Create_proxy_cache_registry_Docker_Hub_type) |
|**Artifact life cycle management** |tag immutability rule |Prevents pushed image tags from being overwritten, ensuring tag consistency and release traceability. |✅ |✅ |[Creating tag immutability rules](https://docs.byteplus.com/en/docs/cr/create-a-version-immutable-rule) |
||tag retention rules |Supports configuring tag retention rules, regularly cleaning image tags, and automatically deleting versions outside the policy. |✅ |✅ |[Creating tag retention rules](https://docs.byteplus.com/en/docs/cr/create-a-tag-retention-rule) |
||Event notification |Configure notification rules for image push and other events, and support automatic triggering of downstream CI/CD processes. |✅ |\- |[Creating image push notification rules](https://docs.byteplus.com/en/docs/cr/Create_notification_rules) |
|**Domain management** |Default domain name settings |Set custom domain name as the instance default domain name, replacing the system domain name. |✅ |\- |[Setting default domain names](https://docs.byteplus.com/en/docs/cr/Set_the_default_domain_name) |
||Custom access domain name |Support binding user\-owned domain names as instance access domain names, ensuring domain name consistency before and after business changes and business continuity. |✅ |\- |[Creating custom domain names](https://docs.byteplus.com/en/docs/cr/Create_a_custom_domain_name) |
|**Operations and audit** |Resource capacity alarm |Set alert thresholds for storage capacity and ResourceQuota to monitor resource levels in real time and avoid service interruptions. |✅ |\- |[Configuring resource capacity alerts](https://docs.byteplus.com/en/docs/cr/Configure_resource_capacity_alerts) |
||Log audit |Supports displaying logs of image push and pull operations through the audit log feature to understand the state of image push and pull. |✅ |\- |[Enabling log audit](https://docs.byteplus.com/en/docs/6420/1356487) |
