---
title: "Billing items and prices"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/charge_items_and_price"
---

This topic describes the billing items and price details of RDS for MySQL.

<span id=".6K6h6LS56aG5"></span>
## Billing items

RDS for MySQL's billing items include instance specification charges, data storage charges, backup storage charges, database proxy service charges, and extranet network traffic charges.


|Billing items |Description |Billing method |
|---|---|---|
|Instance specification |Fees for primary, secondary, or read\-only node specifications of MySQL. |Pay\-as\-you\-go and subscription |
|Storage space |Fees for the storage space of MySQL instances. |Pay\-as\-you\-go and subscription |
|Backup storage space |The cost of the storage space occupied by the backup files. The billing of the backup storage space is differentiated according to the backup type, and is divided into basic backup storage space and deleted instance backup storage space.<br><br><br>* RDS for MySQL provides each instance with a certain amount of free storage space for basic backups. The portion of the basic backup file that exceeds the free space will be billed according to the billing standard of the basic backup storage space.<br><br>   * For instances with local disks, the size of the free basic backup storage space is the same as the storage space of the instance's primary node.<br><br>   * For volume instances, the free basic backup storage space is twice the size of the instance's primary node storage space.<br><br>* Backups of deleted instances are stored free of charge for 30 days after creation. After 30 days, they are billed according to the billing standard for storage space for backups of deleted instances.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Both system and user\-created backups occupy backup storage space.</div><br> |Pay\-as\-you\-go |
|Database proxy service |The database proxy service is charged according to the number of CPU cores configured for the proxy service.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Each instance has two free proxy cores. The number of cores charged = the actual number of proxy cores \- 2.</div><br> |Pay\-as\-you\-go |
|Auto\-scaling node CPU |After configuring automatic or manual specification volume expansion and contraction rules for an instance, MySQL will automatically expand and shrink the node specification for the instance after the instance triggers the rule.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">RDS for MySQL automatically expands the number of node cores in minutes, and is billed according to the number of cores and duration.</div><br> |Pay\-as\-you\-go |
|Backup external network download traffic |The traffic consumed by downloading backups through the external network.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently free to use, no fees are incurred. We will issue an announcement before starting to charge, see the announcement for the specific start time and price of charging.</div><br> |\- |
|External network traffic (optional) |MySQL supports applying for external network addresses and using external network addresses for access. The external network address will be bound to the [public network IP](https://docs.byteplus.com/en/docs/eip/What-is-EIP) (Elastic IP Address, referred to as EIP), and the use of EIP will incur fees. For more information about public IP billing, see [Public IP Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview). |Depends on the billing method selected when purchasing EIP. |
|Cross\-region backup traffic |Enabling cross\-region snapshot backup and cross\-region Binlog log backup for cloud disk instances will incur additional storage and traffic fees. |Pay\-as\-you\-go |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For more information about billing methods, see <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/price_overview">Overview</a>.</div>


* <div data-tips="true" data-tips-type="tip">Backup storage space and database proxy services have been charged starting from 00:00:00 Beijing Time on December 30, 2024. For more details, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/billing_for_backup_storage_space_and_proxy_service">Billing for backup storage space and proxy service starting on December 30, 2024</a>.</div>



<span id=".5Lu35qC8"></span>
## Price

<span id="GBvXStSR"></span>
### Node specification and storage space


|Billing items |||Region |Price |Unit |
|---|---|---|---|---|---|
|* Local SSD<br><br>* FlexPL<br><br>* PL0 |||For detailed pricing information on instance specifications and data storage space, see [MySQL price calculator](https://www.byteplus.com/en/pricing?product=RDS+for+MySQL&tab=2). |||
|High performance cloud disk<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">High\-performance cloud disk instances are subject to a maximum IOPS limit and come with complimentary IOPS quotas. Charges are incurred only for the portion exceeding the free quota, and this extra portion will be billed solely when the actual IOPS of the instance surpasses the maximum IOPS threshold and further exceeds the complimentary quota.</div><br><br><br><div data-tips="true" data-tips-type="default">The free quota for IO performance burst is specified as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Single node instance: 300,000 IO/hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Double node instance: 800,000 IO/hour.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Multiple node instance: 900,000 IO/hour.</div><br> |Node specification and storage space ||For detailed pricing information on instance specifications and data storage space, see [MySQL price calculator](https://www.byteplus.com/en/pricing?product=RDS+for+MySQL&tab=2). |||
||IO performance burst<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The IO performance burst is the sum of the IO performance bursts of all nodes in the instance. For example, the IO performance burst of a multi\-node instance is <code>the sum of the IO performance burst of the primary node and the IO performance burst of all secondary nodes</code>.</div><br> |General type |China (Beijing) |0.0015 |USD/10,000 IOs/hour |
|||Dedicated type ||0.0015 ||
|||General type |China (Shanghai) |0.0015 ||
|||Dedicated type ||0.0015 ||
|||General type |China (Guangzhou) |0.0015 ||
|||Dedicated type ||0.0015 ||
|||General type |China (Hong Kong)<br><br> |0.0015 ||
|||Dedicated type ||0.0015 ||
|||General type |Asia Pacific (Johor) |0.0015 ||
|||Dedicated type ||0.0015 ||
|||General type |Asia Pacific (Jakarta) |0.0015 ||
|||Dedicated type ||0.0015 ||


&nbsp;

<span id="LWlhtdJA"></span>
### Backup storage space


|Billing items ||Region |Price |Unit |
|---|---|---|---|---|
|Backup storage space |Basic backup storage space |China (Beijing) |0.0001 |USD/GiB/Hour |
|||China (Shanghai) |0.0001 ||
|||China (Guangzhou) |0.0001 ||
|||China (Hong Kong) |0.0001 ||
|||Asia Pacific (Johor) |0.0001 ||
|||Asia Pacific (Jakarta) |0.00012 ||
||Deleted backup storage space |China (Beijing) |0.000025 ||
|||China (Shanghai) |0.000025 ||
|||China (Guangzhou) |0.000025 ||
|||China (Hong Kong) |0.000025 ||
|||Asia Pacific (Johor) |0.000025 ||
|||Asia Pacific (Jakarta) |0.000025 ||


<span id="V670jdWX"></span>
### Database proxy service


|Billing items |Region |Price |Unit |
|---|---|---|---|
|Database proxy service |China (Beijing) |0.035 |USD/GiB/Hour |
||China (Shanghai) |0.035 ||
||China (Guangzhou) |0.035 ||
||China (Hong Kong) |0.084 ||
||Asia Pacific (Johor) |0.068 ||
||Asia Pacific (Jakarta) |0.0684 ||


<span id="kmoxS4Ub"></span>
### Auto\-scaling node CPU


|Billing items ||Region |Price |Unit |
|---|---|---|---|---|
|Auto\-scaling node CPU<br><br> |Dedicated type |China (Beijing)<br><br> |0.060 |USD/GiB/Hour |
||General type ||0.040 ||
||Dedicated type |China (Shanghai) |0.060 ||
||General type ||0.040 ||
||Dedicated type |China (Guangzhou) |0.060 ||
||General type ||0.040 ||
||Dedicated type |China (Hong Kong) |0.074 ||
||General type ||0.049 ||
||Dedicated type |Asia Pacific (Johor) |0.090 ||
||General type ||0.060 ||
||Dedicated type |Asia Pacific (Jakarta) |0.090 ||
||General type ||0.060 ||


<span id="H3rsw2T5"></span>
### Cross\-region backup traffic

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Only cloud disk instances are billed for cross\-region backup traffic.</div>



|**Billing items** |**Source region** |**Target region** |**Price** |**Unit** |
|---|---|---|---|---|
|Cross\-region backup traffic |Chinese mainland regions |Chinese mainland regions |0.072 |&nbsp;<br><br>USD/GiB |


&nbsp;
