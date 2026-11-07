---
title: "Creating a custom bucket policy in visual view"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-customizing-a-bucket-policy-in-the-visual-view"
---

You can customize a bucket policy if preset policy templates in Torch Object Storage (TOS) do not meet your needs. TOS allows you to customize a bucket policy in the visual or JSON view. This topic describes how to customize a bucket policy in the visual view.

<span id="65546ff8"></span>
## Background


* For more information on authorized operations in a bucket policy, see [Actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8).

* For more information on the parameters of a bucket policy, see [Bucket policy parameters](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#4eZxSoDw).


<span id="tAeJzlD3"></span>
## Notes

By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).


* Configure bucket policies: `tos:PutBucketPolicy`

* View bucket policy details: `tos:GetBucketPolicy`

* Delete bucket policies: `tos:DeleteBucketPolicy`


<span id="632d4a0f"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission \> Bucket policies**.

4. On the **Visual view** tab of the **Bucket policies** page, click **Create policy**.

5. At the bottom of the **Create Bucket Authorization Policy** page, select **Custom Policy** and click **Next**.

6. On the **Create Bucket Authorization Policy** page, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Policy configuration method |Click **Basic configuration** and select **Visual view**.<br><br>For more information on how to configure a bucket policy in the JSON view, see [Creating a custom bucket policy in JSON view](https://docs.byteplus.com/en/tos/docs/customizing-a-bucket-policy-in-the-json-view?version=1.0.0). |
   |Policy name |Click **Basic configuration** and set the policy name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The policy name must be unique in a bucket.</div><br> |
   |Effect |Select a policy effect.<br><br><br>* **Allow**: Allows requests.<br><br>* **Deny**: Denies requests. |
   |Authorized user |* **Specified account**: If you select **Specified account**, you need to add the ID of the account to be authorized.<br><br>   * **Current main account**：Used to authorize IAM users (sub\-users) under the current account. No need to enter the account ID, simply click on the **Add Field**, you can select the sub\-user name from the drop\-down menu of the sub\-user name.<br><br>   * **Other main account**：Used to authorize other accounts and IAM users (sub\-users) of other accounts. You need to enter the other account ID and the name of the sub\-user of the other account.<br><br>* **All users**: All users (including anonymous users) can execute the bucket policy without authentication. If you set **Effect** to **Allow**, this may pose security risks for data storage. Proceed with caution. |
   |User Policy |Set user authorization method, only when **Effect** is **Deny**, can you set the **User Policy** parameter. When **Effect** is **Deny**, the parameters mean the following:<br><br><br>* **Includes the above users**: Deny specified users certain permissions.<br><br>* **Excludes the above users**: Deny permissions to other users except the specified ones.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Excluding the above user functions is only used to deny permissions and does not grant authorizations. If you want to specify certain permissions for a user, you also need to create the corresponding permission policies. For a detailed introduction, please see <a href="https://docs.byteplus.com/en/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction">Using NotPrincipal, NotResource, and NotAction</a>.</div><br> |
   |Resource Scope |* **Current bucket**: The policy takes effect on the current bucket. You can configure bucket operations in **Action**.<br><br>* **Objects in bucket**: The policy takes effect on objects in the bucket. You can configure object operations in **Action**.<br><br>   * **All objects**: The policy takes effect on all objects in the bucket.<br><br>   * **Specified object(s)** : If you select **Specified object(s)** , click the **Add Field** icon to set the object field.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The Specified Object is to be filled as follows:      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Chinese, English, digits, and common characters are supported.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Cannot start with "/" or "", and cannot use consecutive "/".      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You cannot name a directory "..".      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Supports specifying the resource path as an entire bucket, object, or directory. When you authorize a directory, please end with wild\-card,<em> </em>such as test/\*.      </div><br>       |
   |Resource strategy |Set the method of resource authorization. Only when **Effect** is **Deny**, you can set **resource strategy** parameters. When **Effect** is **Deny**, the meanings of the parameters are as follows:<br><br><br>* **Include the above resources**: Denies users' access to the specified resources.<br><br>* **Exclude the above resources**: Apart from designated resources, deny users access to any other resources.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature to exclude the above resources is solely used to deny users certain resource permissions and does not grant authorization by itself. If you want users to have permissions for specified resources, you also need to create a corresponding permission policy. For a detailed introduction, please refer to <a href="https://docs.byteplus.com/en/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction">Using NotPrincipal, NotResource, and NotAction</a>.</div><br> |
   |Action |Select the operations to be authorized. For more information, see [Actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
   |Operational strategy |Set the method of action authorization; different strategies have different effects and implications.<br><br><br>* When **Effect** is **Deny**, the meaning of the operational strategy is as follows:<br><br>   * **Include the above actions**: Deny users the permission to perform designated actions.<br><br>   * **Exclude the above actions**: Apart from designated actions, deny users the permission to perform any other actions.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Exclusion actions are solely for denying users the permission to perform certain actions and do not grant authorization by themselves. If you want users to have the permission to perform specified actions, you need to create the corresponding permission policy as well.      </div><br>      <br><br>* When **Effect** is **Allow**, the meaning of the operational strategy is as follows:<br><br>   * **Includes the above actions**: Allows the user to have the permission to perform specified actions.<br><br>   * **Excludes the above actions**: Apart from the specified actions, allows the user to have the permission to perform all other actions. For detailed case descriptions, please see [Using NotPrincipal, NotResource, and NotAction](https://docs.byteplus.com/en/docs/tos/Typical-authorization-scenarios-for-notprincipal-notresource-and-notaction). |
   |Condition |Click the **Add Field** icon and set the condition and value. For more information, see [Conditions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC). |
   

7. Then, click **Next**.

8. Confirm the information and click **Create**.

   A created authorization policy will appear in the policy management list.


<span id="914cabe2"></span>
## Further operations


* **Editing a bucket policy**

   * In the policy management list, select the **Visual view** tab. Then, click **Edit** in the **Actions** column of the target policy.

   * In the policy management list, select the **JSON view** tab. Then, click **Edit** and find the target policy in the text box.

* **Deleting a bucket policy**

   In the policy management list, select the **Visual View** tab. Then, click **Delete** in the **Actions** column of the target policy and click **Delete** in the pop\-up dialog box.
