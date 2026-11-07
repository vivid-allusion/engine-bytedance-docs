---
title: "Quick start"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Quick_start"
---

This topic describes the workflow for using Elastic File Storage (EFS) to help you quickly get started with EFS.

<span id="bUtNQWl3"></span>
## Product definition

EFS is a next\-generation cloud\-native elastic file storage service launched by BytePlus, designed for AI while meeting traditional NAS requirements. EFS, based on standard POSIX semantics, provides a high\-performance file storage client FSX for AI business scenarios, and mainstream protocols NFSv3 and NFSv4.1 for traditional NAS scenarios. It seamlessly integrates with various AI training and inference frameworks, operating systems, and applications, providing a user experience consistent with local file systems. For more information, see [What is Elastic File Storage (EFS)](https://docs.byteplus.com/en/docs/nas/What_is_Elastic_File_Storage).

<span id="6SqQuFDI"></span>
## Product specifications

To meet different file storage needs, EFS offers two types of instance specifications: Premium Tier and Basic Tier. For more information, see [Product specifications](https://docs.byteplus.com/en/docs/nas/Product_specifications).


|Specifications |Features |Applicable scenarios |
|---|---|---|
|Premium Tier |Premium Tier features ultra\-large capacity and file count limits, ultra\-high bandwidth and IOPS, as well as ultra\-low latency, delivering robust support for AI training & inference and enterprise\-critical services. |* It is primarily tailored for AI training and inference scenarios, such as autonomous driving and large language model training & inference. With support for hundreds of billions of files, up to 10 PiB of storage capacity, and flexibly configurable performance, it satisfies the diverse and high\-performance file storage demands of such scenarios.<br><br>* It supports standard NFSv4.1 and NFSv3 protocols, meeting the needs of traditional businesses for high\-performance shared file storage (e.g., performance\-optimized NAS). |
|Basic Tier |The Base Tier offers ultra\-large capacity, providing ultimate cost\-effectiveness for massive file storage requirements. |It adopts standard NFSv4.1 and NFSv3 protocols to fulfill traditional business demands for large\-capacity shared file storage (e.g., capacity\-optimized NAS). |


<span id="pWG8jxK1"></span>
## Product Billing

EFS uses pay\-as\-you\-go mode. You can use the service first and pay later. By default, EFS is billed based on storage capacity. When you use provisioned bandwidth, provisioned bandwidth cost is generated. If you enable burst bandwidth, burst bandwidth cost is generated. For more information, see [Billing Overview](https://docs.byteplus.com/en/docs/nas/Billing_overview).

<span id="Kp7TFhE3"></span>
## How to use EFS

<span id="wVroNtRM"></span>
### Prerequisites

Before using EFS, make sure you have completed the following steps:


1. You have registered a BytePlus account and completed enterprise verification. For specific steps, see [Signing up for BytePlus accounts](https://docs.byteplus.com/byteplus-platform/docs/signing-up-your-account).

2. You have created a project for the file system (or you can use the default project). For more information about projects and steps to create a project, see [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

3. You have created a VPC. If you have not created a VPC or want to create a new one, see [Creating a VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC).

4. You have created an ECS instance within the VPC. For detailed steps, see [Creating ECS instances](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Both the VPC and ECS must be in the same region as the file system.   </div>
   

<span id="q3nMfPdv"></span>
### Workflow


1. Select the file system specification.

   Select the appropriate file system specification based on your using scenario. For more information, see [Product specifications.](https://docs.byteplus.com/en/docs/nas/Product_specifications)

2. Create a file system.

   After selecting the file system specification, you can create a file system. For details, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

3. Mount the file system.

   Select a client access method and mount the file system. Steps:

   * If mount via NFS

      1. Create a mount target.

         A mount target serves as the access entry for ECS instances to the file system. You need to create a mount target before you can mount the file system. For details, see [Creating mount targets](https://docs.byteplus.com/en/docs/nas/efs_Managing_mount_targets#ZRe0cMNq).

      2. Mount the file system.

         File systems must be mounted to ECS instances before they can be used. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_NFS).

   * If mount via FSX

      1. Create an access point.

         An access point provides directory\-level access to file systems in BytePlus EFS. You need to create an access point before you can mount a file system. For more details, see [Creating access points](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW).

      2. Mount the file system.

         File systems must be mounted to ECS instances before they can be used. For more information, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX).
