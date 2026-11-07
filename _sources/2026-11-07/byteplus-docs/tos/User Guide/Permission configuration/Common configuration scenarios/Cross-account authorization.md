---
title: "Cross-account authorization"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-cross-account-authorization"
---

This topic describes common scenarios and instructions for cross\-account authorization. We recommend using bucket policies for cross\-account authorization.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you only need to grant a single main account read or write permissions on a bucket or its ACL, you can also set the bucket ACL. For detailed steps, see <a href="https://docs.byteplus.com/en/docs/tos/docs-configuring-a-bucket-acl">Configuring bucket ACLs</a>.</div>


<span id=".6Leo6LSm5Y-35o6I5LqI5qG255qE6K-75YaZ5p2D6ZmQ"></span>
## Cross\-account authorization of bucket read and write permissions


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Bucket List**. On the **Bucket List** page, click the target bucket name.

3. In the left navigation pane, select **Permission Management \> Bucket Authorization Policy Management**.

4. On the **Bucket Authorization Policy Management** page, under the **Visual View** tab, click **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Bucket Read and Write** template, then click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information as prompted.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this scenario, set the following parameters and leave others default.   </div>
   

   
   |**Type** |**Description** |
   |---|---|
   |Authorized User |Select **Specified Account**, click **Other Primary Account**, and perform the corresponding actions based on the authorization target as described below:<br><br><br>* Authorize another primary account: enter the other primary account ID without any further action.<br><br>* Authorize an IAM user under another primary account: enter the other primary account ID, click **Add Field**, and enter the sub\-user name of the other primary account. |
   

7. After completing the settings, click **Next** to confirm the current policy configuration.

8. After confirming the information is correct, click **OK** to complete the policy creation.

   A created authorization policy will appear in the policy management list.


<span id=".6Leo6LSm5Y-35o6I5LqI5qG255qE5oyH5a6a5p2D6ZmQ"></span>
## Cross\-account authorization of specified bucket permissions


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation panel, click **Bucket List**, then click the target bucket name on the **Bucket List** page.

3. In the left navigation panel, select **Permission Management \> Bucket Authorization Policy Management**.

4. On the **Bucket Authorization Policy Management** page, under the **Visual View** tab, click **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Bucket Read and Write** template and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information according to the interface prompts.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this scenario, set the following parameters and leave others default.   </div>
   

   
   |**Type** |**Description** |
   |---|---|
   |Authorized User |Select **specified account**, click **other main accounts**, and perform operations based on the authorized object as follows:<br><br><br>* Authorization for other main accounts: enter the other main account ID with no further operations required.<br><br>* Authorization for IAM users under other main accounts: enter the other main account ID, click **add field**, and enter the sub\-user name of the other main account. |
   |Action |Select the generic actions to authorize. For detailed action descriptions, see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
   

7. After configuring, click **Next** to confirm the current policy settings.

8. After verifying the information is correct, click **Confirm** to complete the policy creation.

   A created authorization policy will appear in the policy management list.


<span id=".6Leo6LSm5Y-35o6I5LqI5oyH5a6a6LWE5rqQ55qE6K-75YaZ5p2D6ZmQ"></span>
## Cross\-account authorization of read and write permissions on specified resources


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Bucket List**, then click the target bucket name on the **Bucket List** page.

3. In the left navigation bar, select **Permission Management \> Bucket Authorization Policy Management**.

4. On the **Bucket Authorization Policy Management** page, under the **Visual View** tab, click **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Folder Read/Write** template and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information according to the interface prompts.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this scenario, set the following parameters and leave others default.   </div>
   

   
   |**Type** |**Description** |
   |---|---|
   |Authorized User |Select **specified account**, click **other main accounts**, and perform operations based on the authorized object as follows:<br><br><br>* Authorize another primary account: enter the other primary account ID without any further action.<br><br>* Authorize an IAM user under another primary account: enter the other primary account ID, click **Add Field**, and enter the sub\-user name of the other primary account. |
   |Resource |Select the **specified object** and click the **Add Field** icon to set the specified resource fields. |
   

7. After setting, click **Next** to confirm the configured policy information.

8. After confirming the information is correct, click **Confirm** to complete the policy creation.

   A created authorization policy will appear in the policy management list.


<span id=".6Leo6LSm5Y-35o6I5LqI5oyH5a6a6LWE5rqQ55qE5oyH5a6a5p2D6ZmQ"></span>
## Cross\-account authorization of specified permissions on specified resources


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Bucket List**, then click the target bucket name on the **Bucket List** page.

3. In the left navigation bar, select **Permission Management \> Bucket Authorization Policy Management**.

4. On the **Bucket Authorization Policy Management** page, under the **visual view** tab, click **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **folder read/write** template and click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information according to the interface prompts.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In this scenario, set the following parameters and leave others default.   </div>
   

   
   |**Type** |**Description** |
   |---|---|
   |Authorized User |Select **Specified Account**, click **Other Primary Account**, and perform the corresponding actions based on the authorization target as described below:<br><br><br>* Authorize another primary account: enter the other primary account ID without any further action.<br><br>* Authorize an IAM user under another primary account: enter the other primary account ID, click **Add Field**, and enter the sub\-user name of the other primary account. |
   |Resource |Select **specified object**, click the **add field** icon, and set the specified resource field. |
   |Action |Select the actions to authorize. For detailed descriptions of the actions, see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
   

7. After setting, click **Next** to confirm the current policy configuration.

8. After confirming the information is correct, click **Confirm** to complete the policy creation.

   A created authorization policy will appear in the policy management list.
