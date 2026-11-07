---
title: "Permanently delete recycle bin files"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Permanently-delete-recycle-bin-files"
---

TOS provides multiple mechanisms to permanently delete files in the recycle bin through lifecycle rules, recycle bin recovery policies, and manual methods. This article explains how to permanently delete recycle bin files for irreversible data removal. 

<span id="fd2a5b26"></span>
## Background information

Permanently deleting means removing files from the bucket permanently and making them unrecoverable. After enabling the recycle bin feature, files deleted by lifecycle rules, object expiration, or manual operation automatically move to the recycle bin directory without permanent deletion. To reduce storage costs, you may need to permanently delete files in the recycle bin. 

<span id="755c8ab8"></span>
## Manually permanently delete recycle bin files


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. On the **Buckets** page, click the name of the target tiered bucket.

3. On the **Objects** page, click the Recycle Bin directory.

4. Click **Permanently Delete** under the **Actions** column of the target file.

5. In the pop\-up dialog, enter permanently delete, then click **Permanently Delete**.


<span id="7769a031"></span>
## Use a retention policy to permanently delete files from the Recycle Bin

The Recycle Bin supports configuring a retention policy to automatically delete files. The retention policy counts from the time an object is moved to the Recycle Bin and permanently deletes files after the specified duration. The retention policy triggers based on the storage duration in the Recycle Bin and cannot selectively delete files based on name, size, or other conditions. The steps to configure the recycle policy are as follows:


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. On the **Buckets** page, click the name of the target tiered bucket.

3. In the left navigation pane, click **Recycle Bin**.

4. In the **Recycle Policy** section, click **Edit** under the **Actions** column of the default policy.

5. In the **Edit default policy** dialog, set the cleanup time, and click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default cleanup time is 7 days, with a minimum of 1 day. If you want to permanently delete files from the recycle bin as soon as possible, it is recommended to set the cleanup time to 1 day.   </div>
   

<span id="9c195eb5"></span>
## Delete recycle bin files permanently through lifecycle rules

After enabling the recycle bin feature, files deleted by lifecycle rules or object expiration time automatically move to the recycle bin directory instead of being permanently deleted. Only after disabling the recycle bin feature can lifecycle rules or object expiration time take effect directly to achieve permanent deletion. The steps to disable the recycle bin are as follows:


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**. On the **Buckets** page, click the name of the target tiered bucket.

3. In the left navigation pane, click **Recycle Bin**.

4. On the **Recycle Bin** page, in the **Basic configurations** section, disable the **Withdrawn station status**.

5. In the **Close the Recycling Bin** dialog box, click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After disabling the recycle bin, the original recycle bin directory will remain as a regular object and will no longer support file recovery. You can configure lifecycle rules or object expiration times to permanently delete files under the original recycle bin directory. For detailed information on lifecycle rules, refer to the <a href="https://docs.byteplus.com/docs/tos/Lifecycle-rules-overview">lifecycle overview</a>.   </div>
