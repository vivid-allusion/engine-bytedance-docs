---
title: "Image cache overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview"
---

During container creation, image pulling often takes a long time. To address this problem, you can use an image cache solution to accelerate VCI creation.

## Background

In traditional workflows, during the container development and testing phase, container images need to be downloaded locally, decompressed, and then used to start container instances. This results in a lengthy overall process. To accelerate container instance creation, VCI provides the image cache feature to accelerate VCI creation.

If you use the image cache feature, additional storage fees will be incurred for image cache snapshots. For details, refer to [Product billing](https://docs.byteplus.com/en/docs/vke/Pay-as-you-go).

## Image caching solutions

The image cache feature allows you to pre\-download images to data disks, create cache snapshots, and then use these snapshots to create VCIs. This solution allows images to be mounted directly when a container starts, reducing or eliminating image layer downloads, lowering read and write pressure on image repositories and cloud disks, and significantly shortening image download and instance startup time.

VCI supports two image caching methods: manual image caching and automatic image caching. Their workflows are similar, but they are used differently. For details, see **Manual image caching** and **Automatic image caching** in this topic.

![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0c47f37127f64b36e2ab75c09aba0050.png)

> **tip**

> VCI image caches support the instant snapshot availability capability of EBS. This capability is in beta for EBS. To use it, contact your account manager of BytePlus.

### Manual image caching

In this solution, you manually create an image cache in advance and then use the image cache during container creation.

Manual image caching supports the following usage methods:

* Use the console. For details, see [Creating VCIs by using a manually created image cache](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache).

* Use the APIs:

   * Create an image cache: [CreateImageCache](https://docs.byteplus.com/en/docs/vke/CreateImageCache)

   * Update an image cache: [UpdateImageCache](https://docs.byteplus.com/en/docs/vke/UpdateImageCache)

   * Query image caches: [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches)

   * Delete an image cache: [DeleteImageCache](https://docs.byteplus.com/en/docs/vke/DeleteImageCache)

   * Batch\-update expiration time of image caches: [UpdateImageCacheRetentionDays](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays)

### Automatic image caching

Automatic image caching supports automatically creating and using image caches during the container creation process.

Automatic image caching is disabled by default. To enable it, To enable it, add the annotation `vci.vke.volcengine.com/enable-auto-create-imc: "true"`. For details, see [Creating VCIs by using an automatically created image cache](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Automatic-Image-Cache).

### Comparison of image caching solutions

|Aspect |Manual image caching |Automatic image caching |
|---|---|---|
|Advantage |* It can be used through the console and OpenAPI, providing strong control and operational flexibility.<br><br>* It allows you to specify custom parameters for image cache resources, providing greater flexibility.<br><br>* Has a default image caching duration of 15 days and supports a longer duration. |* Requires little attention to image caching, offering excellent usability.<br><br>* It provides a complete end\-to\-end workflow that covers a variety of potential scenarios.<br><br>* Requires minimal setup and is easy to use. |
|Disadvantage |It has a learning curve and is less straightforward to operate than automatic image caching. |* When Pods are created in bulk for the first time in a business scenario, startup is slow and manual warm\-up is required.<br><br>* The image caching duration is relatively short (15 days). |

## Using image caches

When you create a VCI by using an automatically or manually created image cache, you can use two options:

* **Automatically match existing image caches**

   Automatically match the optimal image cache based on the matching strategy to create VCIs. The matching strategy is as follows:

   1. Filter all image caches of the BytePlus root user in the current region.

   2. Select the optimal image cache in the following priority order:

      1. Image matching degree: Prioritize image caches with high matching accuracy, including checking if the image repository address, image name, and image version (tag) meet the requirements.

      2. Creation time: Prioritize the most recently created image cache.

      3. Last matching time: Prioritize the image cache that was successfully matched and used most recently.

   > **tip**

   > If no existing image cache is matched, the system will determine the next operation based on whether automatic image caching is enabled for your BytePlus root user(namely, checking `vci.vke.volcengine.com/enable-auto-create-imc: "true"`):

   * > Automatic image caching enabled: The system will automatically create an image cache while creating the VCI.

   * > Automatic image caching disabled: The system will pull the image from the target image repository and use it to create the VCI.

* **Explicitly specify an existing image cache**

   When creating a VCI, explicitly specify a particular image cache by using the annotation. The image cache must be in the  **[Ready.Ok]**  state.
