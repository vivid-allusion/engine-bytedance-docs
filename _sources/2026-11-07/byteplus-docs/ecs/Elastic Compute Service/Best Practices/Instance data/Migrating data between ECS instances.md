---
title: "Migrating data between ECS instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Transmitting-data-between-ECS-instances"
---

You may need to migrate business data to a new ECS instance due to business requirements or resource limits. This topic describes how to use the custom image and snapshot features to migrate data between ECS instances on BytePlus. For more information about snapshots and custom images, see [Snapshot overview](https://docs.byteplus.com/en/docs/ecs/Overview-of-snapshots) and [Image overview](https://docs.byteplus.com/en/docs/ecs/Image-overview).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Copying images feature is in Beta. If you need a trial, contact your account manager.</div>


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Before you migrate instance data, check resource associations and update them in a timely manner after migration is complete.

* You can only create snapshots for instances with ESSD volumes. For other instances, you cannot migrate their data by creating snapshots for the instances. Before you migrate instance data, we recommend that you use the snapshot feature to promptly back up business data.

* When you migrate instance data by using the snapshot and image features, the metadata of new instances may differ from that of the source instances. For more metadata information, see [Instance metadata](https://docs.byteplus.com/en/docs/ecs/Using-instance-custom-data-and-metadata).

* If you need to migrate instance data across regions, plan the destination regions for your resources in advance.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Li65rqQRUNT5a6e5L6L5Yib5bu66Ieq5a6a5LmJ6ZWc5YOP5LiO5b-r54Wn"></span>
### Step 1: Create a custom image and snapshot for the source ECS instance

Before you migrate data, you need to back up the data on the system volume and data volumes based on your migration requirements. The data you have backed up will then be migrated to the destination ECS instance.


* To migrate data on the system volume, you can back up the data by creating a custom image for the source instance. For more information, see [Creating custom images](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-1).

   > Before you create a custom image for an instance, you need to review the relevant precautions. For more information, see [Operation instructions for creating custom image from instance](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5pON5L2c6K-05piO).   
   

* To migrate data on data volumes, you can back up the data by creating snapshots for the data volumes mounted to the source instance. For more information, see [Creating snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).


<span id=".5q2l6aqk5LqM77ya5aSN5Yi26ZWc5YOP77yI5Y-v6YCJ77yJ"></span>
### Step 2: Copy image (optional)

> If you do not need to migrate data across regions, you can skip this step.


If you need to migrate data from a source ECS instance to a new ECS instance in another region, you can first use the image copy feature to copy the custom image to the destination region. For more information, see [Copying images](https://docs.byteplus.com/en/docs/ecs/Copying_custom_images).

After the image is copied, you can perform the subsequent operations in the new region to complete the cross\-region instance data migration.

<span id=".5q2l6aqk5LiJ77ya5L2_55So6Ieq5a6a5LmJ6ZWc5YOP5LiO5b-r54Wn5Yib5bu655uu5qCHRUNT5a6e5L6L"></span>
### Step 3: Use the custom image and snapshots to create an ECS instance in the destination region

In the destination region, you can use the custom image and snapshots of backup data to migrate data.


* Use the custom image of the source instance to create the target instance. After this, the system volume data can be migrated. For more information, see [Purchasing instances based on custom images](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images).

* To migrate data on the data volumes, create new volumes by using the snapshots of data volumes mounted to the source instance and mount the new volumes to the destination instance. For more information, see [Creating volumes by using snapshots](https://docs.byteplus.com/en/docs/ecs/Create-a-volume-through-snapshot).


<span id=".5q2l6aqk5Zub77ya5qOA5p-l5paw5Yib5bu655qE55uu5qCHRUNT5a6e5L6L5YaF55qE5pWw5o2u"></span>
### Step 4: Check the data in the destination ECS instance

After data is migrated from the source instance, check the data storage status and other relevant information in the destination instance based on your needs to ensure that business can run as expected after the migration is complete.

<span id=".5q2l6aqk5LqU77ya6YeK5pS-RUNT5a6e5L6L5Y-K55u45YWz6LWE5rqQ77yI5Y-v6YCJ77yJ"></span>
### Step 5: Release the source ECS instance and related resources (optional)

After you confirm that the instance data migration is successful and the business is running as expected, you can release or delete the relevant resources of the source ECS instance based on your needs. This helps prevent fees generated by redundant resources. Specific steps are as follows:


* For information about how to release an instance, see [Deleting instances](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).

* For information about how to delete a snapshot, see [Deleting snapshots](https://docs.byteplus.com/en/docs/ecs/Delete-a-snapshot).

* For information about how to delete a custom image, see [Deleting custom images](https://docs.byteplus.com/en/docs/ecs/Deleting-custom-images).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Deleted resources, such as instances, snapshots, and custom images cannot be recovered. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">After you delete a custom image, ECS instances created from it will no longer be able to reinitialize their system volumes. We recommend that you retain the custom image.</div>
