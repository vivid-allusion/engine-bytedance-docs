---
title: "Basic bucket operations"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-bucket-operation"
---

You can use the TOS Browser tool to perform bucket\-related operations, such as creating buckets and viewing bucket details.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


1. [Install TOS Browser](https://docs.byteplus.com/docs/tos/Install-tos-browser)

2. [Log in to TOS Browser](https://docs.byteplus.com/docs/tos/Log-in-to-tos-browser)


<span id=".5pSv5oyB5pON5L2c"></span>
## Supported operations

After signing in to TOS Browser, you can perform the following bucket operations.


|Supported actions |Note |
|---|---|
|Creating a bucket |1. Click **Create bucket** in the upper\-left corner of the page.<br><br>2. Set the bucket parameters in the pop\-up dialog, then click **Create**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">For explanations of bucket creation parameters, see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Create Bucket</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TOS Browser supports different parameters for bucket creation compared to the console; please follow the Browser interface.</div><br> |
|Viewing bucket overview |On the **Bucket list** page, click **Details** in the **Actions** column of the target bucket to view detailed information about the bucket, including **Bucket name**, **Creation time**, **Region**, and **Bucket** **Domain**. |
|Bucket ACLs |1. On the **Bucket list** page, click the  **...**   **\> ACL permission ** in the **Actions** column of the target bucket.<br><br>2. Set ACL permissions in the pop\-up panel.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information on ACL permissions, see <a href="https://docs.byteplus.com/docs/tos/docs-overview_4">Bucket ACL Overview</a>.</div><br> |
|View parts |1. On the **Bucket list** page, click  **... \> Parts** in the **Actions** column of the target bucket.<br><br>2. View shard information in the **Parts** panel.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">TOS Browser currently only supports viewing shards. To clear shards in a bucket, please log in to the <a href="https://console.byteplus.com/tos">TOS Console</a> and follow the instructions in <a href="https://docs.byteplus.com/docs/tos/docs-managing-parts#deleting-parts">Clearing Shards</a>.</div><br> |
|Delete a bucket |1. On the **Bucket list** page, click **Delete** in the **Actions** column of the target bucket.<br><br>2. In the pop\-up dialog, click **Delete**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed information on deleting buckets, see <a href="https://docs.byteplus.com/docs/tos/docs-deleting-a-bucket">Delete Bucket</a>.</div><br> |
|Switch bucket |In the bucket list display on the left side of any page, click the target bucket name to enter another bucket. |
