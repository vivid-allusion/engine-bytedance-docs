---
title: "Creating a custom bucket policy in JSON view"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-customizing-a-bucket-policy-in-the-json-view"
---

You can customize a bucket policy if preset policy templates in Torch Object Storage (TOS) do not meet your needs. TOS allows you to customize a bucket policy in the visual or JSON view. This topic describes how to customize a bucket policy in the JSON view.

<span id="6ca096bb"></span>
## Note


* A bucket can contain policy descriptions up to a total size of 20 KB in JSON format.

* By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

   * Configure bucket policies: `tos:PutBucketPolicy`

   * View bucket policy details: `tos:GetBucketPolicy`

   * Delete bucket policies: `tos:DeleteBucketPolicy`


<span id="b8827820"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission \> Bucket policies**.

4. On the **Bucket Policies** page, click **JSON view** tab, and then set the policy content. For more information, see [Parameters](https://docs.byteplus.com/en/tos/docs/templates-and-parameters?version=1.0.0).

5. Then, click **Select**.

   A created authorization policy will appear in the policy management list.


<span id="6300f9b1"></span>
## Further operations


* **Editing a bucket policy**

   * In the policy management list, select the **Visual View** tab. Then, click **Edit** in the **Actions** column of the target policy.

   * In the policy management list, select the **JSON View** tab. Then, click **Edit** and find the target policy in the text box.

* **Deleting a bucket policy**

   In the policy management list, select the **Visual View** tab. Then, click **Delete** in the **Actions** column of the target policy and click **Delete** in the pop\-up dialog box.
