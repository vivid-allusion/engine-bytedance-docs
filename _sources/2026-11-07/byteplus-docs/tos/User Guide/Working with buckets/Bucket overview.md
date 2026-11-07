---
title: "Bucket overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-bucket-overview"
---

From the bucket overview page, you can view a bucket's usage overview, basic information, and access domain.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A bucket has been created. For more information, see [Creating buckets](https://docs.byteplus.com/docs/tos/docs-create-a-bucket).

<span id="0tTv81dh"></span>
## Notes

To view usage overview, you must have read\-only access to Cloud Monitor. For authorization steps, see [Granting read-only access to Cloud Monitor](https://docs.byteplus.com/en/docs/tos/Grant_read-only_permission_for_account_cloud_monitoring).

<span id=".5p-l55yL5a2Y5YKo5qG25qaC6KeI"></span>
## Viewing bucket overview


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. 

3. In the top menu bar, select the project of the bucket you want to manage.

4. In the **Buckets** list, click the bucket you want to manage.

5. From the **Objects** page, click **Overview** in the left navigation pane.

   On the Overview page, you can view the following details:

   
   |**Category** |**Description** |
   |---|---|
   |Usage overview |* **Number of bucket objects**: Select a storage type from the drop\-down list to view the number of objects stored in that storage type. Select "total usage" to view the total number of objects stored in the bucket. The statistics include historical object versions but not parts. <br><br>* **Total capacity of bucket object**: The total storage capacity of the objects in the current bucket.<br><br>* **Total download traffic over the public network of the bucket today**: Outbound traffic from the beginning of the day (12:00:00 a.m.) to the present.<br><br>* **Total download traffic over the private network of the bucket today**: Outbound traffic from the beginning of the day (12:00:00 a.m.) to the present.<br><br>* **CDN back\-to\-origin traffic of the bucket today**: CDN back\-to\-origin traffic from the beginning of the day (12:00:00 a.m.) to the present.<br><br>* **Total number of requests for the bucket today**: The total number of requests from the beginning of the day (12:00:00 a.m.) to the present. |
   |Basic information |* **Bucket name**: The custom name given to the bucket when it was created.<br><br>* **Region**: The region where the bucket is located.<br><br>* **Multi\-AZ Redundancy**: Indicates whether the **Multi\-AZ Redundancy** feature is enabled for the bucket. Learn more in [Multi-AZ redundancy](https://docs.byteplus.com/en/docs/tos/Multi-az-redundancy).<br><br>* **Default storage type**: The storage type of the bucket.<br><br>* **Creation time**: The time when the bucket was created.<br><br>* **Lifecycle**: Indicates whether lifecycle rules are configured for the bucket.<br><br>   Click **Settings** to navigate to the **Lifecycle** page and set specific rules. For instructions, see [Configuring lifecycle rules](https://docs.byteplus.com/en/tos/docs/setting-lifecycle-rules?version=1.0.0).<br><br>* **Back\-to\-Origin rules**: Indicates whether back\-to\-origin rules are configured for the bucket.<br><br>   Click **Settings** to navigate to the **Back\-to\-Origin rules** page and set specific rules. For instructions, see [Back-origin overview](https://docs.byteplus.com/en/docs/tos/Overview9).<br><br>* **CORS**: Indicates whether cross\-region resource sharing (CORS) policies are configured for the bucket.<br><br>   Click **Settings** to navigate to the **CORS rules** page and set specific rules. For instructions, see [CORS rules](https://docs.byteplus.com/docs/tos/docs-cross-origin-resource-sharing-settings).<br><br>* **Versioning**: Indicates whether the versioning feature is enabled for the bucket.<br><br>   Click **Settings** to navigate to the **Versioning** page and set specific rules. For instructions, see [Enabling or suspending versioning](https://docs.byteplus.com/docs/tos/docs-enabling-and-suspending-versioning).<br><br>* **Tag**: The tags associated with the bucket.<br><br>* **Server\-Side encryption**: Indicates whether server\-side encryption is enabled for the bucket.<br><br>   Click **Settings** to navigate to the **Server\-Side encryption** page and set specific rules. For instructions, see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>* **RenameObject**: Indicates whether the RenameObject feature is enabled for the bucket.<br><br>   Click **Settings** to navigate to the **RenameObject** page and set specific rules. For instructions, see [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).<br><br>* **Project**: The project to which the bucket belongs.<br><br>* **Object ACL default policy**: The default ACL policy for objects uploaded to the bucket. For more information, see [Configuring object ACLs](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl). |
   |Access domain |* **Public Network Access**: Publicly accessible bucket domains, including **Endpoint**, **S3 endpoint**, and **Bucket domain**.<br><br>* **Private Network Access**: Bucket domains accessible within the VPC, including **Endpoint**, **S3 endpoint**, and **Bucket domain**. |
   


<span id=".5p-l55yL5a2Y5YKo5qG255So6YeP57uf6K6h"></span>
## Viewing bucket usage statistics


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the bucket you want to manage.

5. In the left navigation pane, select **Usage statistics \> Basic data** to view bucket usage statistics, including storage capacity, retrieve capacity, traffic, number of requests, bandwidth, and status codes.

   You can specify a reference period at the top of the **Basic data** page.


<span id="ae04e388"></span>
## FAQ

**The bucket overview page indicates "User is not authorized to perform" and cannot display content.** 

Your account lacks Cloud Monitor permissions. You must either add the `GetMetricsData` permission to or attach the `CloudMonitorReadOnlyAccess` policy to your users. For instructions, see [Authorizing IAM users](https://docs.byteplus.com/en/docs/cloudmonitor/Granting_permissions_to_an_IAM_user).
