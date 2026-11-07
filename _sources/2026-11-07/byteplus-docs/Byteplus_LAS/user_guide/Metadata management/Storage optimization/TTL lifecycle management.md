---
title: "TTL lifecycle management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/TTL_lifecycle_management"
---

<span id="41f200c2"></span>
## Configure table lifecycle

When creating a table, you can configure lifecycle management. By default, table files are stored in TOS standard storage. By configuring the table's lifecycle, tables that are not used for extended periods can be moved to TOS archive storage to reduce your data storage costs.

Users should set the lifecycle based on actual business needs. Setting a lifecycle that is too short is not recommended, because retrieving data from TOS archive storage back to standard storage requires you to perform a thaw operation in TOS and will incur the applicable retrieval fees. For retrieval fees, see: [Data retrieval fees](https://www.volcengine.com/docs/6349/104494).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34aa37ab6bd34e5bb1403e5fb5f6ce06~tplv-goo7wpa0wc-image.image) </span>

**Parameter description**:


* Partition change time: The last update time of the table or partition.

   * If you use insert overwrite for table data, old data will be deleted and new data will be uploaded. The upload time of the new data files is the partition modification time for the table. The countdown for the table's lifecycle will start from the last update time.

   * If you use insert into for table data, the update time of historical data will not change, and the update time for newly inserted data will be the latest time. This may result in a situation where old partition data in the table meets the archiving criteria and is moved to archive storage, while new partition data remains in standard storage.

* Archive data: Move data to TOS "archive" storage. For information about TOS storage types, see: [Storage Type](https://docs.byteplus.com/en/docs/tos/docs-storage-type).


<span id="5008ee0e"></span>
## Delete table lifecycle

There are two ways to delete the lifecycle of a table.

**Method 1**:

In the left navigation bar of the LAS console, click **Catalog\>Database name \> Table**, select the corresponding data table, and click **Delete**. The table's lifecycle rules will be deleted along with the table.

**Method 2**:

In the left navigation bar of the LAS console, click **Catalog\>Database name \> Table**, select the corresponding data table, click **Edit**, enter the data table, and disable the table lifecycle.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, TOS lifecycle management has certain constraints, and LAS follows these constraints as well, for example:</div>



* <div data-tips="true" data-tips-type="warning">: After a lifecycle rule is created, it does not immediately take effect for all objects in the bucket; there will be a certain delay. Within 24 hours after the lifecycle rule is created, TOS will load the rule. After the rule is loaded, TOS will begin execution within 24 hours.</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-overview#f65aa113">Rule execution priority</a>: The execution priority of lifecycle rules varies depending on the prefix overlap status.</div>


* <div data-tips="true" data-tips-type="warning"><a href="https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-overview#0a0be877">Quantity</a>: The maximum number of lifecycle rules for a single bucket is 1,000, and the total size of the JSON descriptions for all lifecycle rules in a bucket must not exceed 20 KB. The prefix length of a rule (that is, the table storage path) must not exceed 1,024 bytes.</div>


* <div data-tips="true" data-tips-type="warning">Limitations after archiving data: Before using the CopyObject, GetObject, SetObjectMeta, or UploadPartCopy interfaces to set archived storage objects, or before moving, renaming, or downloading archived storage objects, the object must first be restored; otherwise, the operation will fail.</div>



<span id="c377ac9d"></span>
## Frequently asked questions

<span id="10443bf9"></span>
### How to configure the lifecycle if the number of tables exceeds 1,000


1. It is recommended to prioritize setting the lifecycle at the database level, that is, on the TOS lifecycle management page, configure a lifecycle rule with the database storage path as the prefix. This effectively provides a default lifecycle rule at the database granularity. If the table's lifecycle rule differs from the database, then enable the table's lifecycle rule.

2. A single bucket is limited to 1,000 rules. You may consider using multiple buckets.


<span id="2b86d2f4"></span>
### Error: Found two rules with same prefix

Prefix overlap must be enabled. For detailed instructions, refer to: [Configure prefix overlap](https://www.volcengine.com/docs/6349/1160440).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb3ea3a82a4843ea815d2a9aae36c5c0~tplv-goo7wpa0wc-image.image" width="2616px" /></div>


<span id="112157c0"></span>
### Error: The operation is not valid for the object's storage class

Archived data cannot be moved or read; that is, operations such as table rename or select will be restricted. The data must be restored to standard storage before it can be used. For detailed instructions, refer to: [Restore files](https://www.volcengine.com/docs/6349/302315).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cec2357e9e5145f389b656c2ea832552~tplv-goo7wpa0wc-image.image" width="2544px" /></div>
