---
title: "Creating VCIs by using manually created image caches"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Manual-Image-Cache"
---

During container creation, image pulling often takes a long time. To address this problem, you can use the manual image caching solution to accelerate VCI creation.

## Usage limits

* Each BytePlus root user, including IAM users, can have up to 1000 image caches, excluding image caches that are being deleted (status:  **[Deleting,\*]** ). If this upper limit is reached, new image caches cannot be created. You can delete image caches that are no longer used, or [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) to apply for a quota increase.

* VCI supports instant availability of EBS to shorten the time from image cache creation to availability. This feature is currently in **beta** in EBS. To use it, contact your account manager of BytePlus.

## Usage methods

### Step 1: Prepare a container image

Prepare the container image to be used for creating a VCI. You can use images from BytePlus CR as well as images from third\-party container registries. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

### Step 2: Create an image cache

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Vital Container Instance** \> **Image Cache**. On the page that appears, click **Create Image Cache**.

3. On the **Create Image Cache** page, complete **Image Cache configuration** according to the system prompts.

   |Parameter |Description |
   |---|---|
   |**Basic configuration** ||
   |Name |Set the image cache name based on the on\-screen prompts. The image cache name must be unique within the same region. |
   |VPC |Select a VPC for the image cache. A VPC provides an isolated, self\-configurable, and self\-managed virtual network environment for image caches. If no VPC is available, follow the steps described in [Creating VPC](https://docs.byteplus.com/en/docs/vpc/Creating-a-VPC) to create one. |
   |Subnet |Select a subnet within the selected VPC to provide a subnet CIDR block for the image cache. If no subnet is available, click **Create subnet** to create one. For details, see [Creating subnets](https://docs.byteplus.com/en/docs/vpc/Creating-a-subnet).<br><br>> **tip**<br><br><br>> The first subnet is used by default to create the temporary pod resources required for the image cache.<br> |
   |Security group |To ensure that the image cache and related features can function normally, associate the security groups of the selected VPC. |
   |Image Cache capacity |Set the size of the image cache. The default is 40 GiB, and the size range is 40 GiB to 500 GiB. |
   |**Container image settings** ||
   |Container image |Select or enter the container image that will be used to create the image cache. The following image sources are supported:<br><br><br>* If the container registry is BytePlus CR, enter the CR image address or click **Choose your own image** to select an image from the target CR instance in the panel that pops up on the right.<br><br>   > **warning**<br>   <br><br>   > After selecting the target CR image, you also need to specify an **image tag**. If no tag is selected, the image with the tag `latest` will be pulled by default. If no image with the `latest` tag exists, the image cache creation will fail.<br>   <br><br>* If the container registry is a third\-party container registry, enter the address of the third\-party container registry. The entered image address can include a tag (such as `example.com/namespace/repository:v1`), or the tag can be entered in the **Image tag** field.<br><br><br>Click **Add container image** to add multiple images. |
   |**Container Registry configuration** ||
   |Container Registry access credentials |When the added container image is **private**, click **Add access credentials** to configure container registry access credentials.<br><br><br>* Access domain name: The domain name of the container registry. Note that you should not include the `http://` or `https://` prefix. An example is `cr-cn-beijing.volces.com`.<br><br>* Username: The username for accessing the container registry.<br><br>* Password: The password of the username for accessing the container registry. |
   |**Advanced settings** ||
   |Annotation |Configure an annotation for the image cache. You can only configure the following two annotations to configure bill splitting for the image cache:<br><br><br>* **`vci.volcengine.com/image-cache-resource-tags`**: Add tags for the image cache to perform bill splitting based on tags. The requirements for custom tags are as follows:<br><br>   * The supported format is string.<br><br>   * Each tag consists of a key\-value pair in the `key:value` format. Multiple tags are separated by commas (`,`). For example, "`k1:v1,k2:v2`" means that two tags are set for the image cache: `k1:v1` and `k2:v2`.<br><br>   * The requirements for a tag key are as follows:<br><br>      * It cannot start with `volc:` in ‌any case variation‌.<br><br>      * It can only contain characters, digits, spaces, and special characters `_.:/=+-@`.<br><br>      * The length is limited to 1 to 128 characters.<br><br>   * The requirements for a tag value are as follows:<br><br>      * This can be left blank.<br><br>      * It can only contain characters, digits, spaces, and the following special characters: `_.:/=+-@`.<br><br>      * Its length does not exceed 256 characters.<br><br>   * A single image cache supports up to 50 tags.<br><br>   * If a tag with the same key already exists for the image cache, adding the tag key again through this annotation overwrites the original tag value.<br><br>   * Tag keys and values do not allow leading or trailing spaces.<br><br>   > **warning**<br>   <br><br>   > After adding tags for the image cache, you need to **enable** bill tags in the billing center console at [Billing management \- Bill tags](https://console.byteplus.com/finance/bill/tag/) and apply the corresponding tags to the bill details. For details, see [Cost tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags) and [Tag\-based bill splitting](https://docs.byteplus.com/en/docs/6649/189384).<br>   <br><br>* **`vci.volcengine.com/image-cache-project-name`**: Associate a project with the image cache to perform bill splitting based on projects. Take note of the following items when you enter the project name:<br><br>   * If you enter a project name that does not exist, an error is reported when you create the image cache.<br><br>   * If this annotation is not configured, which means that no project is associated, the image cache uses the **default** project by default.<br><br><br>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_722be5232cbd9a3c8119927ae912002f.png) |
   |Image Cache incremental production |If you select **Enable**, specify an existing **base image cache** and enable incremental image cache creation. The newly created image cache will reuse the image layer of the specified image cache, which accelerates cache creation. |

4. Click **Next: Configuration confirmation** to confirm the image cache configuration and read the terms of service.

5. If you confirm that the configuration is correct and have no objections to the terms of service, check **I have read and agree to Vital Kubernetes Engine Specific Terms of Service** and click **Confirm** to create the image cache.

   > **tip**

   > After the image cache is created, its default expiration time is 15 days. If the image cache is used for creation of a VCI, the expiration time is refreshed to "Time of matching + 15 days." If it is not used for 15 consecutive days, it is automatically cleaned up. To modify the expiration time of an image cache, call the API [UpdateImageCacheRetentionDays](https://docs.byteplus.com/en/docs/vke/UpdateImageCacheRetentionDays).

### Step 3: Accelerate VCI creation with manual image caching

After confirming that the target image cache is available, you can use it to create a large number of VCI pods. You can use the following methods:

> **tip**

* > To ensure that a VCI created using an image cache can function normally, manually specify the system disk size by adding a pod annotation when creating the VCI. This practice helps ensure enough space for storing the image cache and deploying VCI system components. For more information, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).

   > The annotation key is `vci.vke.volcengine.com/desired-system-storage`, and the annotation value should be set according to the following principles:

   * > Automatic image cache matching: `Image size × 2 to image size × 2.5`. For example, if the image size selected for VCI creation is 20 GiB, you need to specify a system volume size of 40 GiB to 50 GiB.

   * > Manually specified image cache: `Image cache capacity + 20 GiB`. For example, if your image cache size is 60 GiB, you need to specify a system volume size of 80 GiB.

* > The capability of manually specifying the system volume size is in **beta**. To use this capability, [submit an application](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features).

**Automatically matching image caches**

When creating a VCI, select an image that has already been cached. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

The system automatically matches the optimal image cache based on the matching strategy to create VCIs. For the strategy of automatically matching image caches, see [Using image caches](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview#.5L2_55So6ZWc5YOP57yT5a2Y).

**Manually matching image caches**

Add a specific annotation to `spec·template·metadata` of the VCI. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance). The specified image cache will be used to create the VCI.

> **warning**

> VCI will perform pre\-checks on the status of the image cache specified by `vci.vke.volcengine.com/image-cache-id`. Ensure the specified image cache is in the **Available** or **[Ready.Ok]** state. Otherwise, an error will occur and the VCI pod cannot be created.

|Annotation key |Annotation sample value |Description |Required |
|---|---|---|---|
|vci.vke.volcengine.com/image\-cache\-id |imc\-3uqroqkx0i3j\*\*\*\*\*\*\*\* |Image cache ID specified for creating the VCI. |No |
|vci.vke.volcengine.com/ignore\-image\-cache\-unavailable |false |During VCI creation, if the image cache identified by the image cache ID does not exist or is unavailable, the image cache configuration is ignored.<br><br><br>* **true**: (Default) Ignore it.<br><br>* **false**: Do not ignore it. If the image cache with the corresponding ID does not exist or is unavailable, the VCI creation fails. |No |

## Related documentation

* [Managing image caches](https://docs.byteplus.com/en/docs/vke/Image-Cache)

* [CreateImageCache](https://docs.byteplus.com/en/docs/vke/CreateImageCache)
