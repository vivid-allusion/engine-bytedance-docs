---
title: "Log batch delivery"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/log-batch-delivery_en-us"
---

Log Batch Delivery is a BytePlus CDN service that allows you to automatically transfer hourly packaged request logs to a bucket in your specified object storage service. This feature supports various destinations, including BytePlus Object Storage (TOS), Alibaba Cloud Object Storage (OSS), Tencent Cloud Object Storage (COS), AWS S3, or any S3\-compatible service, enabling centralized log management and analysis.

For differences between "Log Batch Delivery" and the other two CDN log acquisition methods, see [Logs Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/logs-overview_en-us).

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cc9274170bbd84a8443797019bf373ff.png) </span>

When configuring "Log Batch Delivery", you need to create a delivery task. In the delivery task, you provide access settings for the bucket and specify which domains' request log packages CDN should transfer.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The log packages transferred by CDN are identical to the log packages that can be queried and downloaded in the <strong>Log Download</strong> tab.</div>



* <div data-tips="true" data-tips-type="tip">For information about log timeliness, naming rules for log packages, descriptions of log fields, etc., see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs-logs">Log Download</a>.</div>



<span id="log-batch-delivery-billing"></span>
## Log Batch Delivery Billing

"Log Batch Delivery" is a paid service. The fees consist of the following parts:


* Log delivery fees. CDN charges for delivered logs. The billing unit is 10,000 log entries. For detailed information about log delivery billing, see [CDN Pricing](https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-pricing-cn).

* Object storage service fees. Based on the delivery destination, see

   * [BytePlus TOS Pricing](https://docs.byteplus.com/en/docs/tos/docs-billing-overview).

   * [AWS S3 Pricing](https://aws.amazon.com/s3/pricing/).

   * For pricing of other object storage services, visit the service provider's website.


<span id="steps"></span>
## Steps


1. Log in to the [BytePlus CDN Console](https://console.byteplus.com/cdn).

2. In the left navigation pane, click **Tools** \> **Logs**.

3. On the **Logs** page, click the **Log Batch Delivery** tab.

4. On the **Log Batch Delivery** tab, click **Create Task** to create a delivery task.

5. On the **Create Task** page, configure **Destination** and **Domains (Log Source)**  according to the [Configuration Instructions](https://docs.byteplus.com/en/docs/18/48157#configuration-instructions).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you specify <strong>Destination</strong> as <strong>BytePlus Torch Object Storage (TOS)</strong>, you need to first authorize CDN to access TOS. Please follow the page prompts. If you have previously authorized CDN to access TOS, the status of <strong>Service Authorization</strong> will be <strong>Authorized</strong>.   </div>
   

6. After completing the task configuration, click **Submit**.


<span id="screenshots"></span>
### Screenshots


|**Destination** is **BytePlus TOS** |**Destination** is **AWS S3 or S3\-compatible Storage** |
|---|---|
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_e92428442c8fc95c6229a981cafbf64f.png) </span><br><br>See [corresponding configuration instructions](https://docs.byteplus.com/en/docs/18/48157#destination-is-byteplus-tos). |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3e4f4f3ff83d8198323024f7eba26347.png) </span><br><br>See [corresponding configuration instructions](https://docs.byteplus.com/en/docs/18/48157#destination-is-aws-s3-or-s3-compatible-storage). |



|**Domains (Log Source)**  is **Selected Domains** |**Domains (Log Source)**  is **All Domains** |
|---|---|
|<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_0be020ab8a079a7757f11ba56bd52c93.png) </span><br><br>See [corresponding configuration instructions](https://docs.byteplus.com/en/docs/18/48157#domains-log-source). |<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_60ba81358dc49f92bedc897737e1c2d5.png) </span><br><br>See [corresponding configuration instructions](https://docs.byteplus.com/en/docs/18/48157#domains-log-source). |


<span id="configuration-instructions"></span>
## Configuration Instructions

<span id="destination-is-byteplus-tos"></span>
### **Destination** is **BytePlus TOS**


|**Configuration** |**Description** |
|---|---|
|Bucket |The name of a bucket in TOS. Select a bucket from the list, which contains all buckets in your account.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Logs collected by CDN may be delayed. For delayed logs, CDN will append them to the corresponding log package in the TOS bucket. Therefore, when selecting a bucket, you can only choose buckets with storage type "Standard Storage" because only this type of bucket supports appending content to existing files.</div><br> |
|Bucket Directory |Represents a directory path under the bucket. Log packages will be transferred to this directory path. For example, `mylogs/cdn-logs`.<br><br>&nbsp;<br><br>The directory path cannot start or end with a slash (/), and cannot exceed 256 characters. If the directory path does not exist, CDN will create it in the bucket.<br><br>&nbsp;<br><br>If you do not specify this configuration, log packages will be transferred to the root directory of the bucket. |
|Require Authentication |Indicates whether the bucket is publicly accessible. This configuration is disabled by default.<br><br><br>* If this configuration is enabled, it means the bucket is privately accessible. When CDN transfers log packages to this bucket, CDN will use your BytePlus account credentials to access the bucket.<br><br>* If this configuration is disabled, it means the bucket is publicly accessible. |
|Remarks |Represents the remarks for this task, with a length of 3\-45 characters, which can include Chinese characters, letters, and numbers, but cannot start or end with an underscore (_). One Chinese character counts as 3 characters.<br><br>&nbsp;<br><br>After the task is created, these remarks will be displayed below the task ID.<br><br><span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b289ab034b791c2628681b94ba645467.png) </span> |


<span id="destination-is-aws-s3-or-s3-compatible-storage"></span>
### **Destination** is **AWS S3 or S3\-compatible Storage**


|**Configuration** |**Description** |
|---|---|
|Bucket Endpoint |The S3\-compatible access endpoint for the destination bucket.<br><br>&nbsp;<br><br>The endpoint must start with `https://`, must not include the bucket name, and cannot exceed 1,024 characters. For example: `https://oss-ap-southeast-1.aliyuncs.com`. |
|Region |Represents the region code of the bucket, such as `ap-southeast`. Please consult the object storage service provider of the bucket to obtain the region of the bucket.<br><br>&nbsp;<br><br>The region cannot exceed 64 characters. |
|Bucket |Represents the bucket name, which cannot exceed 256 characters. For example: `mybucket`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Logs collected by CDN may be delayed. For delayed logs, CDN will append them to the corresponding log package in the TOS bucket. Therefore, the bucket you specify must support appending content to existing files.</div><br> |
|Bucket Directory |Represents a directory path under the bucket. Log packages will be transferred to this directory path. For example, `mylogs/cdn-logs`.<br><br>&nbsp;<br><br>The directory path cannot start or end with a slash (/), and cannot exceed 256 characters. If the directory path does not exist, CDN will create it in the bucket. |
|Require Authentication |Indicates whether the bucket is publicly accessible. This configuration is disabled by default.<br><br><br>* If this configuration is enabled, it means the bucket is privately accessible. You need to provide credentials for CDN to access the bucket.<br><br>* If this configuration is disabled, it means the bucket is publicly accessible. |
|AccessKey ID |For the credentials used by CDN to access the bucket, this configuration represents the AccessKey ID in the credentials.<br><br>&nbsp;<br><br>This configuration only appears when **Require Authentication** is enabled. |
|Secret Access Key |For the credentials used by CDN to access the bucket, this configuration represents the AccessKey Secret in the credentials.<br><br>&nbsp;<br><br>This configuration only appears when **Require Authentication** is enabled. |
|Remarks |Represents the remarks for this task, with a length of 3\-45 characters, which can include Chinese characters, letters, and numbers, but cannot start or end with an underscore (_). One Chinese character counts as 3 characters.<br><br>&nbsp;<br><br>After the task is created, these remarks will be displayed below the task ID. |


<span id="domains-log-source"></span>
### **Domains (Log Source)** 

In this configuration, you specify which domains' log packages CDN should transfer. This configuration has the following options:


* Selected Domains: Specify up to 200 domains under your account.

* All Domains: Represents all domains under your account.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">A domain can only be included in one task.</div>


* <div data-tips="true" data-tips-type="tip">If there is already a task with <strong>Domains (Log Source)</strong> set to <strong>Selected Domains</strong>, you cannot create a task with <strong>Domains (Log Source)</strong> set to <strong>All Domains</strong>, and vice versa.</div>



<span id="more-information"></span>
## More Information

<span id="delivery-task-list"></span>
### Delivery Task List

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_81da2c5e303aee45f265d418b027039b.png) </span>

The delivery task list displays the delivery tasks you have created.


* Hover over the **Task Details** column to view detailed bucket information.

* Hover over the **Domains** column to view the domains associated with that task.


<span id="start-stop-task"></span>
### Start/Stop Task

If you want to pause a task, you can click **Stop** in the **Actions** column of that task. After the task is stopped, CDN stops transferring log packages for all domains associated with that task. Later, you can click **Start** at any time to resume log transfers for these domains.

<span id="error-notifications-for-failed-transfers"></span>
### Error Notifications for Failed Transfers

When configuring bucket information, if any configuration is incorrect, the delivery task will fail. Additionally, if the bucket reaches certain limits during the execution of the delivery task, the delivery task will also fail.

If a delivery task cannot transfer log packages to the target bucket, an exclamation mark will appear on the left side of the task. When you click this exclamation mark, the page will display the time and reason for the most recent transfer failure. You can refer to the failure reason to troubleshoot the issue.
