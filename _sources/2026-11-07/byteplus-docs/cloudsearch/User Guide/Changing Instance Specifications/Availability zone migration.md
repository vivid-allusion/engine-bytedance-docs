---
title: "Availability zone migration"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Availability_zone_migration"
---

If the instance's availability zone lacks resources, you can use the availability zone migration feature to smoothly move the instance within the same region from one availability zone to another, alleviating resource pressure in a single availability zone. This article explains how to migrate an availability zone.

## Prerequisites

Please ensure that you have completed the data backup before migrating the availability zone. For more information, see [Manually create a snapshot](https://docs.byteplus.com/en/docs/cloudsearch/manual-snapshots).

## Precautions

* Single\-node instances do not support availability zone migration.

* If there is no data backup, any data loss during migration will not be counted as service downtime. For details, see [Cloud Search service level agreement](https://docs.byteplus.com/en/docs/cloudsearch/SLA).

* When migrating availability zones, select a target zone with sufficient resources; zones with sold\-out resources cannot be selected.

* The migration process involves data transfer, and the expected duration depends on the data volume.

* Read and write operations will not be interrupted during migration, but performance may degrade, and cross\-zone disaster recovery capability may temporarily decline. It is recommended to perform the operation during off\-peak hours.

## Procedure

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, in the **actions** column of the target instance, select  **...**   **\> Availability zone migration→**

4. In the **Availability zone migration** dialog, confirm the instance’s current deployment method and availability zone, select a new availability zone, then read and agree to the related agreement before clicking **OK**.

   The instance enters the **Changing** status. After migration completes, the instance will return to the **Running** status. You can check the migration progress in the task center. For specific operations, see [view task progress](https://docs.byteplus.com/en/docs/cloudsearch/task-progress).
