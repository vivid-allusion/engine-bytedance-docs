---
title: "Registry replication overview"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Registry_replication_overview"
---

Registry replication is the image distribution capability provided by CR, supporting automatic synchronization of images and Helm Charts across different instances, regions, and repositories to meet the requirements of multi\-region deployment, disaster recovery, migration, and other scenarios.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This action applies only to Standard instance and is not applicable to proxy repository.</div>


<span id="mjQpy8cm"></span>
## Feature introduction

The registry replication feature enables images and Helm Charts in the source repository to be synchronized automatically or manually to the target repository by creating synchronization rules. After a synchronization rule is created, each time a new image is pushed to the source repository and matches the rule, the system will automatically trigger a synchronization task. You can also manually trigger a full synchronization.<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e7a69d18dfd6d5172932d366a0d769fa.png) </span>

<span id="0dtYkyIf"></span>
## Synchronization type

CR supports the following synchronization types for different scenarios:


|**Synchronization type** |**Description** |**Source side** |**Target side** |
|---|---|---|---|
|[Synchronization within the same region or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions?lang=en) |Synchronize images between Standard Edition instances under the same BytePlus root user, supporting both intra\-region and cross\-region synchronization. Applicable to multi\-region deployment, disaster recovery, and backup scenarios. |Standard Edition instance |Standard Edition instance (same account) |
|[Synchronize from CR to external repository](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions?lang=en) |Synchronize images from a CR Standard Edition instance to an external self\-built repository (such as a self\-built Harbor or other cloud vendor image repositories). Applicable to hybrid cloud deployment, cross\-cloud distribution, and other scenarios. |Standard Edition instance |External repository (Harbor, ACR, ECR, and more) |
|[Synchronizing external repositories to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry?lang=en) |Synchronize images and Helm Charts from a third\-party image repository to a CR instance. Applicable to image migration, unified management of external images, and other scenarios. |External repository (AWS ECR, Harbor, Docker Hub, and more) |Standard Edition instance / Micro Edition instance |


<span id="5fostQpz"></span>
## Usage limits


* Supported artifact types for synchronization: Docker images, Helm Charts.

* Each account supports a maximum of 5 enabled registry replication rules at the same time.

* After a rule is deleted, historical logs cannot be viewed.

* By default, the last 1,000 synchronization logs are retained for each rule.

* Once a registry replication rule is triggered, the current synchronization task cannot be terminated.
