---
title: "Creating a bucket policy with a template"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-creating-a-bucket-policy-with-a-template"
---

Torch Object Storage (TOS) provides seven preset templates for you to quickly configure permissions in the console.

In some templates, you need to specify the authorized user or resource scope. In other templates, you can change the authorized user, resource scope, operation, and condition.

<span id="vhOQKxZb"></span>
## Notes

By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).


* Configure bucket policies: `tos:PutBucketPolicy`

* View bucket policy details: `tos:GetBucketPolicy`

* Delete bucket policies: `tos:DeleteBucketPolicy`


<span id="af57f34f"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission \> Bucket policies**.

4. On the **Visual view** tab of the **Bucket policies** page, click **Create policy**.

5. On the **Create Bucket Authorization Policy** page, select the target template and click **Next**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information on TOS templates, see <a href="https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#q6Rw9Wjw">Bucket policy templates</a>.   </div>
   

6. Set the parameters as prompted, including the authorized user and account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can modify parameters in the current template based on your business requirements, such as authorized operation and condition. For more information on policy parameters, see <a href="https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#4eZxSoDw">Bucket policy parameters</a>.   </div>
   

7. Then, click **Next**.

8. Confirm the information and click **Create**.

   A created authorization policy will appear in the policy management list.


<span id="d24afb6f"></span>
## Further operations


* **Editing a bucket policy**: In the policy management list, click **Edit** in the **Actions** column of the target policy.

* **Deleting a bucket policy**: In the policy management list, click **Delete** in the **Actions** column of the target policy and click **Delete** in the pop\-up dialog box.
