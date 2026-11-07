---
title: "Creating VCIs by using automatically created image caches"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Automatic-Image-Cache"
---

During container creation, image pulling often takes a long time. To address this problem, you can use the automatic image caching solution to accelerate VCI creation.

## Usage limits

The following limits apply when you use the automatic image caching solution to accelerate VCI creation.

|Limitation item |Restriction |
|---|---|
|Image cache disks (cloud disks) |By default, only 40 GiB of storage space is provided. If the required cache capacity for the target container image exceeds 40 GiB, you need to specify the required storage space separately. Otherwise, image cache creation may fail. |
|Image cache snapshots |The validity period of an image cache is 15 days. After the cache expires, creating a cloud disk by using the image takes longer or may fail.<br><br>> **tip**<br><br><br><br>* > We recommend that you manually create a cloud disk based on the image cache in advance and trigger the cloud disk to warm up and cache snapshot data.<br><br><br>* > Cache warm\-up must be performed in the target region and availability zone where the image cache will be used.<br> |
|Image cache capabilities |* Automatic image caching is disabled by default and needs to be enabled by using a particular annotation.<br><br>* If you use an automatically created image cache to create a VCI, the system disk capacity of the VCI must be greater than or equal to the size of the matched or used image cache.<br><br>* APIs for automatic image caching are not yet provided.<br><br>* To use automatic image caching, you need to create a small number of pods in advance to trigger and complete image cache creation. You can use it to create a large number of business pods after the cache enters the  **[Ready.Ok]**  state.<br><br>* Unused automatically created image caches are retained for a maximum of 15 days. If an image cache is used during VCI creation, its expiration time is refreshed to "matching time + 15 days". If it remains unused for 15 consecutive days, it is automatically cleaned up.<br><br>* Each BytePlus root user, including IAM users, can have up to 20 image caches, excluding image caches that are being deleted (status:  **[deleting,\*]** ). If this upper limit is reached, new image caches cannot be created. You can delete image caches that are no longer needed or request a quota increase in the [Quota Center](https://console.byteplus.com/quota/productList). For details, see [Viewing and applying for quotas](https://docs.byteplus.com/en/docs/vke/VCI-limits#.6YWN6aKd5p-l55yL5ZKM55Sz6K-3).<br><br>* VCI supports the instant availability capability of EBS to shorten the time from image cache creation to availability. This capability is an independent beta feature. To use it, submit an additional [application](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features).<br><br>   > **tip**<br>   <br><br>   > If you apply for a trial of the VCI image cache feature for the first time and simultaneously need the instant availability feature of EBS, request access to these features in the same [application](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features).<br>    |

## Procedure

### Step 1: Prepare a container image

Prepare the container image to be used for creating a VCI. You can use images from BytePlus CR as well as images from third\-party container registries.

This topic uses an image from CR as an example. To upload an image to CR, see [Pushing and pulling images](https://docs.byteplus.com/en/docs/cr/push-and-pull-images).

### Step 2: (Optional) Automatically cache and warm up the image

Before creating a VCI, confirm whether the container image to be used is a new image. If it is a new image, you need to add the image to the cache and warm it up in advance.

> **tip**

> A new image refers to a container image whose image name, image tag, image layer data, and other attributes are different from those of existing images.

We recommend first creating a small number of pod instances to trigger and complete creation of an image cache. The following example demonstrates how to create a Deployment that contains one pod instance and is deployed by using VCI. For details, see [Creating general-purpose instances by specifying container vCPUs and memory](https://docs.byteplus.com/en/docs/vke/Creating-a-general-purpose-instance-based-on-specified-container-vCPUs-and-memory).

**Using the console**

1. [Create a VCI-related cluster](https://docs.byteplus.com/en/docs/vke/Using-VCI-in-Vital-Kubernetes-Engine#.5q2l6aqk5LiA77ya5Yib5bu6LXZwYy1jbmkt5a655Zmo572R57uc5qih5Z6L55qE6ZuG576k).

2. [Create a Deployment](https://docs.byteplus.com/en/docs/vke/Creating-a-Deployment). When you create the Deployment, configure some parameters as described below.

   a. **Basic information**: Select **Vital Container Instance** for the **Computing power type** parameter.

   b. **Container configuration**: Select the prepared new image.

   c. **Advanced settings**: In the **Instance annotation** field, add the following annotation: `vci.vke.volcengine.com/enable-auto-create-imc:"true"`.

   > **warning**

   > By default, VCI provides only 40 GiB of storage space for an image cache. If a larger cache capacity is required for the target container image, you need to add an additional annotation in this step: `vci.vke.volcengine.com/auto-imc-disk-size: "specific capacity size (GiB)"`to specify the required image cache disk size. For example, if 80 GiB is needed, also add the `vci.vke.volcengine.com/auto-imc-disk-size: "80"` annotation.

3. Click **Confirm** to create the VCI Deployment.

**Using YAML**

1. [Connect to the cluster through kubectl](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

2. Create a YAML file for the VCI Deployment. The following `vci-deployment.yaml` file serves as an example:

   ```yaml
   apiVersion: apps/v1
   kind: Deployment
   metadata:
     name: vci-deployment  # The name of the Deployment.
     namespace: default # The namespace to which the Deployment belongs.
   spec:
     replicas: 2  # The number of replicas for the Deployment.
     selector:
       matchLabels:
         app: vci-deployment
     template:
       metadata:
         annotations:
           vke.volcengine.com/burst-to-vci: enforce  # Force the use of VCI.
           vci.vke.volcengine.com/enable-auto-create-imc: "true"  # Enable automatic image caching.
           vke.volcengine.com/preferred-subnet-ids: subnet-3tispp1nai**** # Specify the ID of the subnet.
           vci.vke.volcengine.com/preferred-instance-family: vci.n2i # Specify the instance family of VCI.
         labels:
           app: vci-deployment
       spec:
         containers:
         - name: nginx
           image: vke-cn-beijing.cr.volces.com/vke/nginx:latest # The address and version of the container image. Replace the value with your actual information.
           ports:
           - containerPort: 80
           resources:
             requests:  # Specify the vCPU and memory of the container.
               cpu: "500m"      
               memory: "1024Mi"
             limits:
               cpu: "1"      
               memory: "2048Mi"
   ```

2. Run the following command to create the VCI Deployment.

   ```bash
   kubectl apply -f vci-deployment.yaml
   ```

### Step 3: Confirm image cache availability

Use the OpenAPI interface [ListImageCaches](https://docs.byteplus.com/en/docs/vke/ListImageCaches) to query all image cache files that belong to the current BytePlus root user.

> **warning**

> An automatically created image cache can be properly matched and used to create VCIs only when its status is **[Ready.Ok]**.

### Step 4: Accelerate VCI creation with automatic image caching

After confirming that the target image cache is available, you can use it to create a large number of VCI pods. You can use the following methods:

> **tip**

* > To ensure that a VCI created using an image cache can function normally, manually specify the system disk size by adding a pod annotation when creating the VCI. This practice helps ensure enough space for storing the image cache and deploying VCI system components. For more information, see [Pod annotations](https://docs.byteplus.com/en/docs/vke/VCI-Pod-annotations).

   > The annotation key is `vci.vke.volcengine.com/desired-system-storage`, and the annotation value should be set according to the following principles:

   * > Automatic image cache matching: `Image size × 2 to image size × 2.5`. For example, if the image size selected for VCI creation is 20 GiB, you need to specify a system volume size of 40 GiB to 50 GiB.

   * > Manually specified image cache: `Image cache size + 20 GiB`. For example, if your image cache size is 60 GiB, you need to specify a system volume size of 80 GiB.

* > The capability of manually specifying the system disk volume is in **beta**. To use this capability, [submit an application](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features).

**Automatically matching image caches**

When creating a VCI, select an image that has already been automatically cached. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

The system automatically matches the optimal image cache based on the matching strategy to create VCIs. For the strategy of automatically matching image caches, see [Using image caches](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache-overview#.5L2_55So6ZWc5YOP57yT5a2Y).

> **tip**

> If you have not performed [Step 2](https://docs.byteplus.com/en/docs/vke/Creating-a-VCI-instance-using-Automatic-Image-Cache#.5q2l6aqk5LqM77ya77yI5Y-v6YCJ77yJ6Ieq5Yqo57yT5a2Y5Y-K6aKE54Ot6ZWc5YOP), you need to add the `vci.vke.volcengine.com/enable-auto-create-imc:"true"` annotation to the `spec·template·metadata` of the VCI to enable automatic image caching.

**Manually matching image caches**

Add the `vci.vke.volcengine.com/image-cache-id:imc-3uqroqkx0i3j********` annotation to the `spec·template·metadata` of the VCI to specify the image cache ID. For details, see [Creating instances](https://docs.byteplus.com/en/docs/vke/Creating-an-instance).

The specified image cache will be used to create the VCI.

> **warning**

> VCI performs pre\-checks on the status of the image cache specified by `vci.vke.volcengine.com/image-cache-id`. Ensure the specified image cache is in **[Ready.Ok]** state. Otherwise, an error will occur and the VCI pod cannot be created.

## Related documentation

* [Managing image caches](https://docs.byteplus.com/en/docs/vke/Image-Cache)

* [CreateImageCache](https://docs.byteplus.com/en/docs/vke/CreateImageCache)
