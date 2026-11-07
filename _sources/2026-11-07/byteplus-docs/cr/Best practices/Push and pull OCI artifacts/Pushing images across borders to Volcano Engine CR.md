---
title: "Pushing images across borders to Volcano Engine CR"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/Push_images_across_borders_to_the_Volcano_Engine_Container_Registry"
---

This topic describes how to quickly push and pull images in cross\-border scenarios.

## Scenario introduction

When images are pushed from third\-party registries outside the Chinese mainland, such as GitHub, to CR instances in the Chinese mainland, image pulls may be slow. BytePlus supports features including service nodes outside the Chinese mainland, such as Johor, and dedicated lines for image synchronization.

## Procedure

### Step 1: Create instance A in the Asia Pacific (Johor) region

1. Log in to the [CR console](https://console.byteplus.com/cr).

2. Select the target region in the top navigation bar.

3. In the left navigation bar, click **Instances**. Then, in the **Instances** area on the right page, click **Create Registry Instance**.

4. On the **Create Registry Instance** page, fill in the **Purchase Information**. For detailed settings and subsequent operations, see [Creating Standard Edition instances](https://docs.byteplus.com/en/docs/cr/create-a-container-registry-enterprise-edition-instance).

### Step 2: (Optional) Create instance B in the target region in the Chinese mainland

> **tip**

> If a CR instance already exists in the Chinese mainland, you do not need to create another one.

Refer to **Step 1** and create a CR instance in a region in the Chinese mainland, such as China (**Beijing**).

### Step 3: Push GitHub images to instance A

Use the push command on the instance overview page to push GitHub images to instance A in the Asia Pacific (Johor) region. For instructions, see [Pushing and pulling artifacts](https://docs.byteplus.com/en/docs/cr/Push_and_pull_artifacts).

### Step 4: Synchronize images from instance A to instance B

After the images are pushed, use registry replication and dedicated lines under the same BytePlus root user that owns the CR instance. Replicate images from the instance in the Asia Pacific (Johor) region to an instance in the Chinese mainland, such as China (Beijing). This enables fast pulls of images from outside the Chinese mainland. For instructions on cross\-region image replication within the same root user, see [Synchronizing images within or across regions](https://docs.byteplus.com/en/docs/cr/Synchronize_images_within_the_same_region_or_across_regions).
