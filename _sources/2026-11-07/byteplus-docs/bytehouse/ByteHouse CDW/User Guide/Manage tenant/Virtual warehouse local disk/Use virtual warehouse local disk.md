---
title: "Use virtual warehouse local disk"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/intelligent-cache"
---

ByteHouse Cloud Data Warehouse provides you with virtual warehouse local disl features, allowing the caching of cold data in object storage to increase the likelihood of hot reads. For scenarios that demand high performance and high QPS, this can greatly enhance the user's querying efficiency. This article provides guidance on the use of local disk features.

<span id="e9531551"></span>
# Background Information

In scenarios such as user queries (logs, etc.), insufficient local caching often leads to severe performance degradation and may even fail to produce results. To avoid this problem, ByteHouse supports adding local storage to the compute groups and scaling the local storage as the compute groups are scaled.

<span id="ea96466e"></span>
# Notice

Local disk is a value\-added paid service. For details, refer to [Specifications and pricing](https://docs.byteplus.com/docs/bytehouse/specifications-and-pricing).

<span id="7e5bb110"></span>
# Enable local disk

<span id="97de6fcf"></span>
## Enable local disk: create a new virtual warehouse

Users can select the "Local disk" function when creating a virtual warehouse; for detailed operations, refer to [Create⧸Edit virtual warehouse](https://docs.byteplus.com/docs/bytehouse/create-edit-virtual-warehouse).

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After activating the local disk function, if you need to reduce the virtual warehouse size later, the system will also clear the existing cache synchronously. Please proceed with caution.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c9ef1f7d16a4c0abf976b7b1476d840~tplv-goo7wpa0wc-image.image) </span>

<span id="0a0df37a"></span>
## Enable local disk: existing virtual warehouse

Users can also configure the local disk function by clicking the "Enable now" (or the "Edit" button) in the "local disk" column on the right side of the virtual warehouse management page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfb04f6fda7342d5953af32b652ad032~tplv-goo7wpa0wc-image.image) </span>

<span id="3b36e2a9"></span>
## Subsequent actions: Cache loading

After enabling local disk, you can configure cache loading tasks to preload data into cache resources, enhancing subsequent query speeds. For instructions on creating cache loading tasks, refer to [Preload ](https://docs.byteplus.com/docs/bytehouse/docs-query-acceleration-preload).

<span id="2c825b62"></span>
# Adjust the local disk TTL

You can adjust the local diskTTL at the table level by modifying the table setting parameter. A usage example is provided below. When using this example, use the actual database and table names, and refer to the parameter descriptions below to replace the setting parameter value with the actual value.

```SQL
ALTER TABLE demo_db.demo_table
MODIFY SETTING
  partition_time_key = 'toDate(time)',
  local_disk_cache_partition_ttl = '7d';
```


Setting parameter descriptions are as follows:


|Setting parameters |Type |Configuration instructions |
|---|---|---|
|partition_time_key |String |It is used to specify the time field expression relied upon for table TTL filtering. It must be set to the field that represents time among the table's partition fields.<br><br><br>* If this value is left empty (the default), the first Date field in the partition will be used for table TTL filtering. If there is no Date field, the first time field will be used as the default filtering key.<br><br>* If you customize this field, table TTL filtering will ignore the time field in the table partition and use the time field expression you have set. For example, when configured as `toDate(time)`, the table TTL will be determined based on the date converted from the `time` field. Replace the `time` field with the actual time field name in your table. |
|local_disk_cache_partition_ttl |String |The table TTL value can be set to `d` (days), `h` (hours), `m` (minutes), or `s` (seconds), and must be enclosed in single quotation marks when used.<br><br>Example: `'7d'` indicates that the cache is retained for 7 days, and `'12h'` indicates that it is retained for 12 hours. |


<span id="28c18709"></span>
# View local disk monitoring

After creating a local disk, you can view the monitoring metric data of the local disk on **Tenant management** \> **Cloud monitor** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a44a98737c94bbd8fa50b3ae6bf7bde~tplv-goo7wpa0wc-image.image) </span>

For details about the currently supported local disk monitoring metrics and operation guidelines for creating monitoring and alarms via BytePlus Cloud Monitor, please refer to [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).

<span id="4b5325bd"></span>
# Disable local disk


1. Enter the virtual warehouse management page and click the "**Edit**" button on the right side of the virtual warehouse.

2. Unselect the "Local disk" button and click **Confirm**.

3. The system enters the fee adjustment confirmation page, click **Next** to complete the operation.
