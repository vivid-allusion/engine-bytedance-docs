---
title: "Billing for backup storage space and proxy service starting on December 30, 2024"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/billing_for_backup_storage_space_and_proxy_service"
---

To provide you with more professional and stable services, we plan to start charging for the backup file storage space and database proxy service of RDS for MySQL from 00:00:00 Beijing time on December 30, 2024. The details of the charging policy are as follows.

<span id="charging-regions"></span>
## Charging regions

All BytePlus public cloud regions.

<span id="backup-file-storage-space-charging-policy-description"></span>
## Backup file storage space charging policy description

<span id="free-storage-space"></span>
### Free storage space

We will give a certain amount of backup storage space to each instance as a gift. The size of the gifted space is equal to the storage space size of the primary node of the instance.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">注意</div>


<div data-tips="true" data-tips-type="warning">The free storage space quota can only be used for basic backup files and is not applicable to backups of deleted instances.</div>


<span id="charged-storage-space"></span>
### Charged storage space

The part of the basic backup file that exceeds the gifted storage space will be charged according to the charging standard for backup storage space.

The storage space for cross\-region backup files will be charged according to the charging standard for backup storage space.

Backups of deleted instances are stored for free within 7 days after their creation. After more than 7 days, they will be charged according to the charging standard for backup storage space.

For detailed information on the charging standard for backup storage space, please refer to [Charging Items and Prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<span id="service-activation-notice"></span>
### Service activation notice

We will add charging items related to backup storage space to the accounts of users of RDS for MySQL. During this period, you will receive a text message notification of service activation. Please note that receiving a text message notification only means that the service has been activated and there will be no charging before December 30, 2024.

<span id="usage-suggestions"></span>
### Usage suggestions

It is recommended that you adjust the backup retention policy in advance and use the backup storage space reasonably.

<span id="database-proxy-service-charging-policy-description"></span>
## Database proxy service charging policy description

<span id="free-proxy-resources"></span>
### Free proxy resources

We give 2 cores of proxy resources to each instance for free.

If an instance has enabled the database proxy service before December 30, 2024 and has not adjusted the proxy configuration, the database proxy service of this instance will not be charged temporarily.

<span id="charged-proxy-resources"></span>
### Charged proxy resources

If an instance enables the database proxy service after 00:00:00 on December 30, 2024, it will be charged according to the charging standard for database proxy service.

For detailed information on the charging standard for database proxy service, please refer to [Charging Items and Prices of RDS for MySQL](https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price).

<span id="service-activation-notice"></span>
### Service activation notice

We will add charging items related to the database proxy service to the accounts of users of RDS for MySQL. During this period, you will receive a text message notification of service activation. Please note that receiving a text message notification only means that the service has been activated and there will be no charging before December 30, 2024.

<span id="usage-suggestions"></span>
### Usage suggestions

Confirm whether your instance has enabled the database proxy service and confirm whether your business needs to use the related features of the database proxy service. If not, please refer to the document [Disable database proxy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disable_database_agent) and turn off the database proxy service before December 30, 2024.
