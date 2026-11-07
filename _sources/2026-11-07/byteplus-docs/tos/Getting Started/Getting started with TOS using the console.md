---
title: "Getting started with TOS using the console"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-quick-start_1"
---

This topic provides a quick start guide for TOS. It includes steps for creating buckets and uploading, downloading, and sharing objects through the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before you begin using TOS, make sure you have signed up for a BytePlus account and completed real name verification. For instructions, see [Account registration](https://docs.byteplus.com/en/docs/Account/sign-up-and-verify-byteplus-account) and [Real Name Verification](https://docs.byteplus.com/en/docs/Account/real-name-verification).

<span id=".5q2l6aqk5LiA77ya5byA6YCaLXRvcy3mnI3liqE="></span>
## Step 1: Activate TOS

The first time you use TOS, you need to activate the service to access its full functionality.

Log in to the [TOS console](https://console.byteplus.com/tos). In the dialog box, check the box that says **I have read and agree to Storage products and service terms** and click **Activate now**.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Skip this step if you have activated TOS.</div>


<span id=".5q2l6aqk5LqM77ya5Yib5bu65a2Y5YKo5qG2"></span>
## Step 2: Create a bucket

Buckets are containers that hold your files or objects in TOS. You must create a bucket before uploading any objects.


1. Log in to [the TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. Then, in the upper\-left corner of the displayed page, click **Create bucket**.

3. Set the bucket parameters and click **Create**.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |Basic configurations |Name |Enter the name of the bucket. After you create the bucket, you cannot change its name. The bucket name must:<br><br><br>* Be globally unique within TOS, meaning no duplication is allowed across all regions and accounts.<br><br>* Consist only of numbers, hyphens (\-), and lowercase letters (a\-z).<br><br>* Start and end with a number or letter.<br><br>* Be between 3 and 63 characters long. |
   ||Region |Select the region where you want to create a bucket. After you create a bucket, you cannot change its region. |
   ||Versioning |Enable this feature to keep historical versions of overwritten and deleted objects. |
   ||Bucket policy |The following options are available for the bucket policy:<br><br><br>* **Private** (Default): Only the bucket owner and authorized accounts have read and write permissions to objects. This is the recommended setting.<br><br>* **Public read**: All users have read access to objects and will incur data transfer charges. Allowing all users to read objects can cause data leaks and financial losses. We recommend setting the policy to **Private** instead.<br><br>* **Public read/write**: All users have full read and write access to objects and will incur data transfer charges. Allowing all users to read and write objects can cause data leaks and financial losses. We recommend setting the policy to **Private** instead. |
   ||Object ACL default policy |Enable **Object ACL default policy** to ensure newly uploaded objects inherit the bucket's ACL by default. If **Object ACL default policy** is not enabled, the object ACL policy will default to **Private**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For details on the relationship between object ACL and bucket ACL, see <a href="https://docs.byteplus.com/en/docs/tos/docs-overview_4#9b50293d">Managing object permissions using bucket ACLs</a>.</div><br> |
   ||Project |(Optional) Select the project to which the bucket belongs from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that comprises a set of resources, users, and roles. It provides a unified view of and access to resources, as well as control over user and role permissions within the project. For more information, see <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Product_Overview">Resource management</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To create a project, click <strong>Create new projects</strong> on the right. This will take you to the <a href="https://console.byteplus.com/iam/resourcemanage/project">IAM console</a>.</div><br> |
   |Advanced settings |Multi\-AZ redundancy |Expand **Advanced settings** to enable **Multi\-AZ Redundancy**. If you enable multi\-AZ redundancy, TOS will store your data across multiple availability zones in the same region. This ensures that your storage service will be stable even if one zone fails. Learn more in [Multi-AZ redundancy](https://docs.byteplus.com/docs/tos/Multi-az-redundancy).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Multi\-AZ redundancy is currently only available in China (Beijing), China (Shanghai), China (Guangzhou), and Asia Pacific (Johor).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For buckets with hierarchical namespace enabled, check the console to see if multi\-AZ redundancy is available.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Multi\-AZ storage costs more than single\-AZ storage. Once enabled, multi\-AZ redundancy cannot be disabled. For details on how much it costs to store data in more than one AZ, check out <a href="https://docs.byteplus.com/docs/tos/docs-storage-fee">Storage</a>.</div><br> |
   ||Default storage type |Expand **Advanced settings** to configure the bucket's storage type. The storage types available in TOS are as follows:<br><br><br>* **Standard Storage** (Default): High availability, reliability, and performance, suitable for frequently accessed data.<br><br>* **Infrequent Access Storage**: Designed for less frequently accessed data with a minimum storage duration of 30 days.<br><br>* **Intelligent Tiering**: Automatically moves data between tiers based on how it is accessed, ideal for data with unpredictable access patterns.<br><br>* **Flashback Archive**: Optimized for rarely accessed data with a minimum storage duration of 90 days.<br><br>* **Archive**: Suited for long\-lived, rarely accessed data with flexible latency requirements. The minimum storage duration is 90 days.<br><br>* **Cold Archive**: Suited for long\-lived, rarely accessed data with flexible latency requirements. The minimum storage duration is 180 days.<br><br>* **Deep Cold Archive**: Cost\-effective storage for extremely cold data with ultra\-long retention needs. The minimum storage duration is 180 days.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). Deep Cold Archive is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-storage-type">Storage type</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have enabled multi\-AZ redundancy, you can only choose the storage type from the following options: Standard Storage (Multi\-AZ), Infrequent Access Storage (Multi\-AZ), and Flashback Archive (Multi\-AZ). For more information on multi\-AZ, see <a href="https://docs.byteplus.com/docs/tos/Multi-az-redundancy">Multi\-AZ redundancy</a>.</div><br> |
   ||Server\-Side encryption |Expand **Advanced settings** to configure the bucket's server\-side encryption method. Once configured, all objects uploaded to the bucket will automatically inherit its encryption settings, unless otherwise specified. The available encryption options are:<br><br><br>* **None**: No encryption applied.<br><br>* **SSE\-TOS**: TOS\-managed encryption. Objects are encrypted automatically upon upload and decrypted during download using TOS\-hosted keys. For more information, see [Server-side encryption](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>* **SSE\-KMS**: Uses keys managed by BytePlus's Key Management Service (KMS) to encrypt and decrypt objects. For more information, see [Server-side encryption](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">SSE\-TOS and SSE\-KMS are only available in China (Beijing), China (Shanghai), China (Guangzhou), China (Hong Kong), Asia Pacific (Johor), and Asia Pacific (Jakarta).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are using SSE\-KMS for server\-side encryption for the first time, you must first <a href="https://console.byteplus.com/finance/opening-service/CloudKMS/?return_url=/kms/region:kms+cn-beijing/primary">activate KMS</a>. Although activating KMS is free, using the service incurs charges. Using SSE\-KMS for server\-side encryption generates API call fees, and creating KMS keys generates key management fees. These fees are charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">KMS billing overview</a>.</div><br> |
   ||Encryption algorithm |Expand **Advanced settings** and select the encryption algorithm for the key. Options include **AES256** and **SM4**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This parameter only appears when <strong>SSE\-KMS</strong> or <strong>SSE\-TOS</strong> is selected for<strong> Server\-Side encryption</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The AES\-256 algorithm is only available in China (Beijing), China (Shanghai), China (Guangzhou), China (Hong Kong), Asia Pacific (Johor), and Asia Pacific (Jakarta). The SM4 algorithm is only available in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br> |
   ||Encryption Key Type |Expand **Advanced settings** to set the encryption key. The default setting is **Custom Key**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when <strong>SSE\-KMS</strong> is selected for <strong>Server\-Side encryption</strong>.</div><br> |
   ||Custom Key |Expand **Advanced settings** and select a key created in KMS. If you have not created a key yet, proceed to the KMS console to do so. For instructions, see [KMS Quickstarts](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when <strong>SSE\-KMS</strong> is selected for <strong>Server\-Side encryption</strong>.</div><br> |
   ||Log analysis |Expand **Advanced settings** to enable **Log analysis**.<br><br>TOS offers free real\-time queries of the most recent seven days of TOS activity through the log analysis feature, which is based on Torch Log Service (TLS). Once you have enabled log analysis, you can query and analyze access logs for your bucket in real time. By default, logs are saved for seven days. This period is customizable. However, TLS will charge you extra for logs kept beyond seven days. For more information on TLS pricing, see [TLS Billable items](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">First\-time users must grant TOS permission to access BytePlus TLS.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Learn more in <a href="https://docs.byteplus.com/docs/tos/Log-analysis">Log analysis</a>.</div><br> |
   ||RenameObject |Expand **Advanced settings** to enable **RenameObject**.<br><br>Once you have enabled RenameObject, you can rename objects by calling the RenameObject API. Learn more in [Using RenameObject](https://docs.byteplus.com/docs/tos/Use-renameobject).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">RenameObject does not work with versioning. You cannot use this feature if versioning is enabled on your bucket.</div><br> |
   ||Tag |Expand **Advanced settings** to add tags to your bucket. For more information, see [Tagging buckets](https://docs.byteplus.com/docs/tos/Set-bucket-tag). |
   ||Retention policy |Expand **Advanced settings** to enable the retention policy feature. For more information, see [Configuring retention policies (WORM)](https://docs.byteplus.com/docs/tos/Configure-retention-policy). |
   


<span id=".5q2l6aqk5LiJ77ya5LiK5Lyg5paH5Lu2"></span>
## Step 3: Upload an object to the bucket

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before uploading any objects, make sure you have created a bucket.</div>



1. Log in to [the TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the bucket you want to manage.

5. On the **Objects** page, click **Upload file**.

6. Set the object parameters on the **Upload file** page.

   
   |**Parameter** |**Description** ||
   |---|---|---|
   |Upload to |Specify the TOS bucket directory to which the object will be uploaded.<br><br><br>* **Current Directory**: Uploads the object to the current directory.<br><br>* **Specified Directory**: Customizes the directory name and upload the object to this directory. When naming the directory, be aware of the following:<br><br>   * Directory names can contain Chinese characters, letters, numbers, and common symbols.<br><br>   * You can use forward slashes (/) to quickly create subfolders. However, the folder name cannot start with a forward slash (/) or backslash (\) and cannot contain consecutive forward slashes (/).<br><br>   * `..` cannot be used as a folder name. ||
   |To be uploaded |Select or drag and drop files or folders from your local device.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You cannot have duplicate filenames in the same bucket. If you upload a file with the same name as an existing file, the system will process it according to the following rules:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If versioning is disabled: The uploaded file will replace the existing file.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If versioning is enabled: The uploaded file will become the latest version, and the existing file will be kept as a previous version. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-overview">Versioning</a>.</div><br> ||
   |Advanced settings |Storage type |Expand **Advanced settings** to specify the storage type for the object to be uploaded. By default, objects use the storage type of the bucket they are stored in. The options are as follows:<br><br><br>* **Inherit Bucket** (Default): Objects use the storage type of the bucket they are stored in.<br><br>* **Standard Storage**: High availability, reliability, and performance, suitable for frequently accessed data.<br><br>* **Intelligent Tiering**: Designed for data with unpredictable access patterns, which will incur object monitoring charges. For more information, see [Intelligent Tiering](https://docs.byteplus.com/docs/tos/docs-overview_1).<br><br>* **Infrequent Access Storage**: Designed for frequently accessed data with a minimum storage duration of 30 days.<br><br>* **Flashback Archive**: Optimized for rarely accessed data with a minimum storage duration of 90 days.<br><br>* **Archive**: Suited for long\-term storage of rarely accessed data with a minimum storage duration of 90 days. You need to restore data in Archive before reading it.<br><br>* **Cold Archive**: Suited for long\-lived, rarely accessed data with flexible latency requirements. The minimum storage duration is 180 days. You need to restore data in Cold Archive before reading it.<br><br>* **Deep Cold Archive**: Cost\-effective storage for extremely cold data with ultra\-long retention needs. The minimum storage duration is 180 days. You need to restore data in Deep Cold Archive before reading it.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). Deep Cold Archive is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-storage-type">Storage type</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have enabled multi\-AZ redundancy for the bucket, you can only choose the storage type from the following options: Inherit Bucket, Standard Storage (Multi\-AZ), Intelligent Tiering (Multi\-AZ), Infrequent Access Storage (Multi\-AZ), and Flashback Archive (Multi\-AZ). For more information on multi\-AZ, see <a href="https://docs.byteplus.com/docs/tos/Multi-az-redundancy">Multi\-AZ redundancy</a>.</div><br> |
   ||Server\-Side encryption |Expand **Advanced settings** to configure the server\-side encryption method. The available encryption options are:<br><br><br>* **Inherit Bucket Encryption Configuration** (Default): An object gets the server\-side encryption method from its bucket. You can find the server\-side encryption method of the bucket in the **Basic information** section of the bucket's **Overview** page. You can also change the bucket's server\-side encryption method. For instructions, see [Setting bucket encryption](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket).<br><br>* **None**: No encryption applied.<br><br>* **SSE\-TOS**: TOS\-managed encryption. Objects are encrypted automatically upon upload and decrypted during download using TOS\-hosted keys. For more information, see [Server-side encryption](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br>* **SSE\-KMS**: Uses keys managed by BytePlus's Key Management Service (KMS) to encrypt and decrypt objects. For more information, see [Server-side encryption](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">SSE\-TOS and SSE\-KMS are only supported in China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta).</div><br><br><br>* <div data-tips="true" data-tips-type="tip">You can only set the server\-side encryption method when uploading objects. You cannot change the encryption settings of uploaded objects.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you are using SSE\-KMS for server\-side encryption for the first time, you must first <a href="https://console.byteplus.com/finance/opening-service/CloudKMS/?return_url=/kms/region:kms+cn-beijing/primary">activate KMS</a>. Although activating KMS is free, using the service incurs charges. Using SSE\-KMS for server\-side encryption generates API call fees, and creating KMS keys generates key management fees. These fees are charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">KMS billing overview</a>.</div><br> |
   ||Encryption algorithm |Expand **Advanced settings** and select the encryption algorithm for the key. Options include **AES256** and **SM4**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The <strong>encryption algorithm</strong> parameter only appears when <strong>SSE\-KMS</strong> or <strong>SSE\-TOS</strong> is selected for <strong>Server\-Side encryption</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The AES\-256 algorithm is only supported in China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta). The SM4 algorithm is only supported in China (Beijing) and China (Shanghai).</div><br> |
   ||Encryption Key Type |Expand **Advanced settings** to set the encryption key. The default setting is **Custom Key**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when <strong>SSE\-KMS</strong> is selected for <strong>Server\-Side encryption</strong>.</div><br> |
   ||Custom Key |Expand **Advanced settings** and select a key created in KMS. If you have not created a key yet, proceed to the KMS console to do so. For instructions, see [KMS Quickstarts](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter only appears when <strong>SSE\-KMS</strong> is selected for <strong>Server\-Side encryption</strong>.</div><br> |
   ||Metadata |Expand **Advanced settings** and click Add Field to configure object metadata. For more information on user\-defined object metadata, see [Managing object metadata](https://docs.byteplus.com/docs/tos/docs-managing-file-metadata). |
   ||Access permission |The following options are available when setting the access control list (ACL) policy for objects to be uploaded to the bucket:<br><br><br>* **Inherit bucket**: An object inherits the permissions from its bucket, meaning the object's ACL will mirror the bucket's. For details on the relationship between object ACL and bucket ACL, see [Managing object permissions using bucket ACLs](https://docs.byteplus.com/en/docs/tos/docs-overview_4).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To allow newly uploaded objects to automatically adopt the bucket's ACL policy, turn on the Object ACL default policy switch. For instructions, see <a href="https://docs.byteplus.com/en/docs/tos/docs-configuring-an-object-acl">Enabling objects to automatically apply bucket ACL</a>.   </div><br>   <br><br>* **Private** (Default): Only the object owner and authorized accounts have read and write permissions. This is the recommended setting.<br><br>* **Public read**: All users, including those making anonymous requests, can read the object. However, only the owner and authorized accounts can modify it.<br><br>* **Public read/write**: All users, including those making anonymous requests, can have full read and write access to the object. |
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Description   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After setting the parameters and adding the files, you can view the list of files that will be uploaded on the <strong>Upload file</strong> page.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To cancel the upload of a selected file, click <strong>Remove</strong> in the <strong>Actions</strong> column. To cancel the upload of all files, click <strong>Clear list</strong> above the file list.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Do not refresh or close the page while uploading. Otherwise, the upload task will be interrupted and the list will be cleared.   </div>
   

7. Verify the files you want to upload, and click **Upload**.

   Then, you are redirected to the **Task progress management** page. To view task progress and status, you can also click **Task center** in the upper\-right corner of the console.


<span id=".5q2l6aqk5Zub77ya5LiL6L295paH5Lu2"></span>
## Step 4: Download an object

After uploading an object to a bucket, you can download the object to your local computer via the console. Objects will be saved to your browser's default download location.


1. Log in to [the TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. On the **Objects** page, click **Download** in the **Actions** column of the object you want to download.


<span id=".5q2l6aqk5LqU77ya6I635Y-W5paH5Lu2LXVybA=="></span>
## Step 5: Share the object

From the TOS console, you can obtain a publicly accessible URL for an uploaded object and share it with third parties for downloading or previewing the object.


1. Log in to [the TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the bucket you want to manage.

5. On the **Objects** page, click **Details** in the **Actions** column of the object you want to share.

6. In the Basic information section of the panel that appears, click the copy button next to the **URL** field.
