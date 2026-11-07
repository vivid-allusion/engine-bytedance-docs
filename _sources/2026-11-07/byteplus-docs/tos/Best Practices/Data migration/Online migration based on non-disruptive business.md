---
title: "Online migration based on non-disruptive business"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Online-migration-based-on-non-disruptive-business"
---

This article introduces the solution and operation steps for migrating data from third\-party services to TOS without business loss.

<span id=".5Lia5Yqh5Zy65pmv"></span>
## Business scenario

If your business is running on other third\-party services and you need to migrate to TOS, you must ensure business stability and avoid damage caused by data migration. You can refer to this document and use the storage migration service and mirror origin rules to achieve lossless business migration.

<span id=".6L-B56e75rWB56iL6K-05piO"></span>
## Migration process


1. Use service tools like DMS or Rclone to migrate all existing data to BytePlus Object Storage TOS. At this point, the original business system still uses the original storage service.

2. Configure mirror origin on the BytePlus TOS bucket and set the access URL path of the source end.

3. Configure the business system to connect the business system's storage access to BytePlus TOS. After configuration, new data will be directly written to BytePlus TOS. Data not migrated before will be transferred from the source bucket to the BytePlus storage bucket through the mirror origin rule, ensuring normal operation of the business system.

4. Use service tools like DMS or Rclone to migrate incremental data generated during the previous business migration, completing the data and business migration.


<span id=".6L-B56e75q2l6aqk"></span>
## Migration steps

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites


1. Determine the migration tool based on the source object storage vendor and interface type.

2. Survey the source object storage's capacity, number of objects, business bandwidth, and QPS capability.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure

<span id=".5q2l6aqk5LiA77ya6YCa6L-H5a2Y5YKo6L-B56e75pyN5Yqh6L-B56e75YWo6YeP5pWw5o2u"></span>
#### Step 1: Migrate the full amount of data through the storage migration service

This article uses DMS for migration as an example. For a detailed explanation of migrating with Rclone, see [Rclone overview](https://docs.byteplus.com/docs/tos/docs-accessing-tos-with-rclone).

Currently, DMS supports data migration through public network and dedicated line. The migration sources can support object storage from multiple cloud providers, and also supports migration via **import** **URL** Data migration can be performed via **list** method.


1. Log in to the [DMS console](https://console.byteplus.com/dms).

2. On the **Migration task ** page, click **Create migration task**.

3. On the **Set the source and destination** page, configure the source and destination parameters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed parameter descriptions when creating a migration task, see <a href="https://docs.byteplus.com/docs/dms/Create-a-migration-task">Create Migration Task</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For descriptions of data sources supported by DMS, see <a href="https://docs.byteplus.com/docs/dms/Create-a-migration-task">Data Source</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For the initial migration, set <strong>Migration File Start Time</strong> to <strong>Migrate All</strong>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are concerned that data migration may consume your business bandwidth and affect normal operations. You can set <strong>traffic control</strong> parameters, defining the traffic control period and maximum rate for migration tasks. For detailed parameter descriptions, see <a href="https://docs.byteplus.com/docs/dms/Create-a-migration-task">Create Migration Task</a>.   </div>
   

4. After completing the settings, click **Submit**.


<span id=".5q2l6aqk5LqM77ya6YWN572u6ZWc5YOP5Zue5rqQ"></span>
#### Step 2: configure image origin retrieval

After configuring the image origin retrieval rule, when the requested object does not exist in the bucket, TOS pulls the file from the origin specified in the rule, returns it to the requester, and writes the file into the bucket.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. Click **Buckets** in the left navigation bar, then click the target bucket name on the **Buckets ** page.

3. Select **Basic configurations \> ** **Back\-to\-Origin rules** in the left navigation menu. On the **Back\-to\-Origin rules** page, click **Create rule**.

4. On the **Create Back\-to\-Origin Rule** ** Rule** page, configure the required parameters.

   
   |Parameter |Note |
   |---|---|
   |Back\-to\-Origin method |Select **Mirroring**. |
   |Back\-to\-Origin Condition |Currently only supports **HTTP status code 404**. |
   |Back\-to\-origin address |Set the address for mirrored origin retrieval. For third\-party cloud providers, set the corresponding bucket domain name.<br><br><br>* Protocol: Optional **https** or **http**.<br><br>* Domain: The value must be in the domain name format but cannot be an IP address.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Click <strong>Add Field</strong> to continue adding back\-to\-origin addresses. You can add up to five addresses.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you set multiple addresses, requests will be sent to one of them randomly. If a request fails, TOS automatically retries to send it to other addresses.</div><br> |
   |Whether to carry request parameter |Enable **Whether to carry request parameter**.<br><br> |
   |Whether to redirect based on the origin server<br><br> |Specifies whether to redirect the request based on the 3XX status code of the origin server. Such a request can be redirected only once. This option is disabled by default. |
   |HTTP Header Delivery Rules (client side to source) |Response headers that can be passed for TOS access to the specified origin server. The options are as follows:<br><br><br>* Transparently Transmit All HTTP Headers(default): All except the following headers are transmitted: Host, Content\-length, Date, Authorization.<br><br>* Transparently Transmit Specified HTTP Headers: Up to 10 headers can be specified.<br><br>* Transparently Transmit No HTTP Headers: No headers are transmitted when selected.<br><br>* Not Transparently Transmit Specified HTTP Headers: Up to 10 headers can be specified that will not be transmitted. |
   

5. After finishing, click **Submit**.


<span id=".5q2l6aqk5LiJ77ya5Lia5Yqh57O757uf5a-55o6l54Gr5bGx5byV5pOOLXRvcw=="></span>
#### Step 3: integrate the business system with BytePlus TOS

After migrating stored data to TOS, you can follow the steps below to switch your business to TOS:


1. Create an IAM user, grant the necessary permissions, and obtain AKSK. For detailed steps, refer to the following document:

   1. [Create an IAM user](https://docs.byteplus.com/docs/byteplus-platform/docs-creating-a-user)

   2. [Grant permissions to the IAM user](https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy)

   3. [View AK and SK information](https://docs.byteplus.com/docs/byteplus-platform/docs-managing-an-accesskey)

2. Choose the corresponding language TOS SDK integration for development based on your business needs. TOS supports SDK languages; please refer to the [SDK Overview](https://docs.byteplus.com/docs/tos/SDK-overview).

3. Use the TOS SDK for interface development and testing of business TOS.

4. After testing, upgrade the business system software version and switch to the TOS storage system during low business hours.


<span id=".5q2l6aqk5Zub77ya5L2_55So5a2Y5YKo6L-B56e75pyN5Yqh6L-B56e75aKe6YeP5pWw5o2u"></span>
#### Step 4: Use the storage migration service to migrate incremental data

The steps for migrating incremental data are the same as step one. For details, see [Create migration task](https://docs.byteplus.com/docs/dms/Create-a-migration-task).

The following recommendations apply when configuring a migration task:


* **Incremental migration interval**: For data volumes less than 100 TiB, an interval of 10 hours is recommended; for volumes over 100 TiB, set it to 24 hours.

* **Number of incremental migrations**: Set to 5 is recommended.

* **Override policy**: Choose **No override**.

* **Migration file start time**: Set this earlier than the first full migration task time point.
