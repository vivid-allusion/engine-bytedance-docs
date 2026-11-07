---
title: "Partition lifecycle management"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Partition_lifecycle_management"
---

The AI Data Lake Service (LAS) provides a variety of storage optimization features, including partition lifecycle management, to help users manage partitions of metadata tables and optimize storage resources. The following provides a detailed description and instructions for the partition lifecycle management feature within storage optimization.

<span id="11ae3b2d"></span>
# Notes and limitations


* Currently, only Hive\-type tables support the storage optimization—partition lifecycle management feature.

* After configuring lifecycle rules, partition data cleanup is performed as an asynchronous task and will take effect within 24 hours after the rule is set.

* Partition data cleanup will incur queue resource fees.

   * The billing item is: cpu_hour_{region}, which refers to the queue resource fee billed by the hour (pay\-as\-you\-go, billed hourly).

   * The resource consumption for executing partition cleanup tasks for each customer does not exceed 10 CU/hour.


<span id="ec12a178"></span>
# Configure partition lifecycle management

<span id="ce0008fa"></span>
## Enable and configure


1. Log in to the [LAS Console](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home?), select the region in the upper left corner as needed, select Lake management \> Metadata in the left navigation bar, select the corresponding **Database \> Table**, and go to the table list page.

2. Select the target table, go to the **Table Details \>** Storage optimization page, enable the partition lifecycle management feature, and configure the relevant parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ee4bdb9467540b3a0a2a1db8acf1079~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameters |Configuration instructions |
   |---|---|
   |partition archive rule configuration |Configure the partition archiving rules to retain partitions. Currently, the following are supported:<br><br><br>* By partition name: Retain the corresponding partitions according to the partition name rules configured below. Partitions that do not meet the rule requirements will be deleted.<br><br>* Create time by partition/Change time by partition: Retain the corresponding partitions according to the partition creation/modification time rules configured below. Partitions that do not meet the rule requirements will be deleted.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Partition cleanup is an asynchronous task, and the partition lifecycle rules will take effect within 24 hours after configuration.</div><br> |
   |partition field &date format<br><br>(Required when By partition name is configured) |When partition archive rule configuration is set to By partition name, you need to configure the name of the grouping field and the date format for the corresponding partition field. |
   |reserved partition range |Set the partition range to be retained for tables that meet the partition archiving rules. |
   


<span id="dd25455c"></span>
## View optimization results

After enabling and configuring the feature, partition cleanup is an asynchronous task. The partition lifecycle rules will take effect within 24 hours after being set. You can view optimization records and results on the partition lifecycle rules page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4504f7eca8346f7b8d66100e3dd0ebb~tplv-goo7wpa0wc-image.image) </span>
