---
title: "Viewing bucket details"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-exporting-bucket-information"
---

In the TOS console, you can view the basic information of buckets under your account. You can also export information of all buckets under your account locally, then view the bucket information on your local device.

<span id="GPHO17xJ"></span>
## Note

By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5):


* View bucket details: `tos:ListBuckets`

* View access permissions: `tos:GetBucketAcl` and `tos:GetBucketPolicy`

* View default storage type: `tos:HeadBucket`

* View redundancy type: `tos:HeadBucket`

* View capacity\-related metrics: `Volc_Observe:GetMetricsData`


<span id="sFJJtIo2"></span>
## Customize list fields

You can select the fields to view on the **Bucket List** page. After selection, the bucket list will display the corresponding fields according to your custom settings.

<span id="HYvXyamK"></span>
### Field description


|**Field** |**Description** |
|---|---|
|Bucket name |The bucket name is displayed by default and cannot be changed. |
|Actions |Operations supported on the **buckets ** page currently only include **Delete**. Displayed by default and cannot be selected. |
|Region |Bucket region. |
|visit |Bucket access permissions are as follows:<br><br><br>* **Public read**: Any user has read permission for the bucket, but only the bucket owner and authorized accounts have write permission.<br><br>* **Public Write**: Any user has write permission to the bucket, but only the bucket owner and authorized accounts have read permission.<br><br>* **Public Read\-Write**: Any user has read and write permissions to the bucket.<br><br>* **Private**: Only the bucket owner and authorized accounts have read and write permissions to the bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The bucket access permissions displayed on the bucket list page are calculated based on existing bucket policies and ACL permissions, excluding IAM permission configurations. If you have configured IAM permissions, the access permissions displayed on the page may be inaccurate.</div><br> |
|Tag |Bucket tags. For details, see [set bucket tags](https://docs.byteplus.com/docs/tos/Set-bucket-tag). |
|Bucket category |Bucket type. |
|Default Storage Type |Bucket's default storage type. |
|Redundancy type |Bucket redundancy type.  |
|Creation time |Bucket creation time. |
|Project |Bucket's project. For details, see [Project management](https://docs.byteplus.com/docs/tos/Project-management). |


<span id="OdmvzuWh"></span>
### Steps


1. Log in to the  [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets.**  Then click the settings icon at the top right of the page.

3. In the popup dialog, select the fields you want to display in the bucket list.

   After selecting a field, the bucket list page will display the corresponding field information.


<span id="WM691S7v"></span>
## View bucket details


1. Log in to the  [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click **Buckets**, then click the target bucket name on the right page.

3. In the left navigation bar, click **Overview**, then view the storage bucket's usage summary, basic information, and access domain on the right page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For detailed descriptions of storage bucket overview parameters, refer to <a href="https://docs.byteplus.com/docs/tos/docs-bucket-overview"> Bucket Overview</a>.   </div>
   

<span id="95HBdjPw"></span>
## Exporting Bucket Information

Object Storage TOS supports exporting bucket name, region, access, creation time, storage type, redundancy type, bucket tags, capacity, public network traffic this month, access count this month, standard storage capacity, infrequent storage billing capacity, archive retrieval storage billing capacity, archive storage billing capacity, cold archive storage billing capacity, deep cold archive billing capacity, and project.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**, then click the download icon at the top right of the page.

3. In the pop\-up dialog box, select the information categories you want to export, then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The table containing the exported bucket information will be named buckets_YYMMDD and saved in csv format to your local system. where YYMMDD indicates the year, month, and day, for example, 20230406.   </div>
   

<span id="e9g19ikO"></span>
## Sort buckets

**Sort by bucket name**


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets.** 

3. Click the sorting icon in the **Bucket name** column to sort buckets by name.

   * Sort ascending

      Click the upward triangle icon to sort buckets in ascending dictionary order by bucket name.

   * Sort descending

      Click the inverted triangle icon to sort buckets in descending dictionary order by bucket name.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the first character is the same, sort by the second character, and so on.   </div>
   

**Sort by creation time**


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets.** 

3. Click the sort icon in the **Creation time** column to sort buckets by creation time.

   * Ascending order

      Click the upright triangle icon to sort buckets from earliest to latest creation time.

   * Descending order

      Click the inverted triangle icon to sort buckets from latest to earliest creation time.
