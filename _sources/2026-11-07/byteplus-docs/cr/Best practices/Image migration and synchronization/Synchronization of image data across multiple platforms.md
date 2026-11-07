---
title: "Synchronization of image data across multiple platforms"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/replicate-images-across-platforms"
---

In hybrid cloud environments, image pushes and pulls often occur across multiple registries. These registry services may span regions, platforms, accounts, and editions. This topic describes best practices for image data synchronization scenarios in hybrid cloud environments.

## Feature introduction

To support these scenarios, CR provides features such as registry replication, image migration, and custom domain names.

* **Image synchronization**: Allows you to synchronize **all or part** of your image data based on replication rules. For details, see [Replication between registry instances](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions).

* **Image migration**: Allows you to migrate image data from **multiple container registries**. For details, see [Synchronizing external registries to CR](https://docs.byteplus.com/en/docs/cr/replicate-images-from-a-third-party-registry-to-the-container-registry).

* **Custom domain names**: If you migrate from an open\-source or third\-party registry service to CR, you can configure a custom domain for your CR instance. This allows you to keep using the original domain name and ensure service continuity. For details, see [Creating custom domain names](https://docs.byteplus.com/en/docs/cr/Creating_custom_domain_names).

## Prerequisites

* A Standard Edition instance has been created. For details, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

* If you use an IAM user, authorization management has been completed. For details, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/cr/Adding_system_policies).

## Procedure

### Scenario 1: Cross\-region image synchronization

> **warning**

> After registry replication, the target image address and access credentials usually differ from the source image. When pulling images, update the related information.

* > Image address: It changes based on the target region and instance name in the replication rule.

* > Access credentials: For private images, use the access credentials of the target instance.

> **tip**

> Registry replication does not consume public network traffic.

**Image synchronization across regions in the Chinese mainland**

If your workloads span regions, you can use **registry replication**. For details, see [Synchronizing images within or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions).

**Cross\-country image synchronization**

Cross\-country registry replication is similar to registry replication across regions in the Chinese mainland. You can use the **registry replication feature**. For details, see [Synchronizing images within or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions).

### Scenario 2: Cross\-platform image migration

When you use registries from multiple public cloud vendors, cross\-platform image migration or synchronization is often required. CR allows you to migrate repositories external to BytePlus to Standard Edition instances with one click. This provides you with professional and stable hosting services and technical support, reduces the O&M and management costs associated with self\-built and self\-managed environments, and meets the delivery requirements of low\-complexity businesses. CR integrates with Vital Kubernetes Engine (VKE) by default. It supports pulling images over private networks. This helps reduce bandwidth costs.

The following third\-party registry services are supported for migration:

* AWS ECR (**private** repositories)

* Harbor

* Docker

For the workflow of synchronizing images from a self\-managed Harbor to a CR Standard Edition instance, see [Migrating self-managed Harbor to CR Standard Edition](https://docs.byteplus.com/en/docs/cr/Pull_images_into_Harbor_from_the_Volcano_Engine_Container_Registry).

> **tip**

> In cross\-platform scenarios, you can use the CR custom domain name feature. With a single configuration, you can enable unified access across platforms and ensure service continuity. For details, see [Creating custom domain names](https://docs.byteplus.com/en/docs/cr/Creating_custom_domain_names).

### Scenario 3: Cross\-account image migration

> **warning**

> When you implement cross\-root\-user registry replication through registry replication rules, ensure the target instance has a namespace and an OCI artifact repository with the same names as in the source instance.

Configure cross\-root\-user registry replication by selecting the **Custom** replication type. Other operations are similar to same\-account registry replication. For details, see [Synchronizing images within or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions).
