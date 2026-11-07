---
title: "Authorizing IAM users of an account"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-authorizing-iam-users-of-an-account"
---

This topic describes typical authorization scenarios and instructions for IAM users. You can complete the authorization based on the appropriate scenario according to your actual needs.

<span id=".5o6I5LqILWlhbS3nlKjmiLfmiYDmnInotYTmupDmlK_mjIHnmoTmiYDmnInliqjkvZzmnYPpmZA="></span>
## Granting IAM users the permissions to perform all operations on all supported resources

To grant IAM users all permissions on all Torch Object Storage (TOS) resources in the current account, use IAM system policies.

For steps to grant IAM system permissions, see [Editing a system default policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-system-default-policy). Select the **TOSFullAccess** system policy during authorization.

<span id=".5o6I5LqILWlhbS3nlKjmiLfliJvlu7rmobblj4rliJfkuL7miYDmnInmobbnmoTmnYPpmZA="></span>
## Granting IAM users the permissions to create buckets and list all buckets

To grant IAM users permissions to create buckets and list all buckets, use IAM custom policies.

For steps to grant IAM users custom policies, see [Creating a user custom policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

Below is a sample policy:

```Plain
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:CreateBucket",
        "tos:ListBuckets"
      ],
      "Resource": [
        "trn:tos:::*"
      ]
    }
  ]
}
```


<span id=".5o6I5LqILWlhbS3nlKjmiLfmjIflrprotYTmupDnmoTnm7jlhbPmnYPpmZA="></span>
## Granting IAM users permissions on specified resources

To grant IAM users permissions on specified resources, use IAM custom policies or bucket policies.


* IAM policy: For steps to grant IAM users custom policy permissions, see [Creating a user custom policy](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-user-custom-policy).

   Below is a sample policy:


```Plain
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "tos:List*"
      ],
      "Resource": [
        "trn:tos:::test"
      ]
    }
  ]
}
```



* Bucket policy

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. Click **Bucket List** in the left navigation bar, then click the target bucket name on the **Bucket List** page.

   3. Select **Permission Management \> Bucket Authorization Policy Management** in the left navigation bar.

   4. On the **Bucket Authorization Policy Management** page, under the **Visual View** tab, click **Create Policy**.

   5. On the **Create Bucket Authorization Policy** page, select the **Folder Read/Write** template, then click **Next**.

   6. On the **Create Bucket Authorization Policy** page, follow the interface prompts to complete the policy information. The parameter description for this scenario is as follows.

      
      |**Type** |**Description** |
      |---|---|
      |Authorized user |Select **specified account** and choose the main account to authorize. Description as follows<br><br><br>* **Current main account**: Used to authorize IAM users (subusers) under the current main account. No need to enter the main account ID. Click **Add Field** to select the IAM user name from the dropdown under **Subuser Name**.<br><br>* **Other main account**: used to authorize IAM users (subusers) of another main account. You need to enter the other main account ID. Click **Add Field** and enter the subuser name of the other main account. |
      |Resource |Select **Specified Object**, then click the **Add Field** icon to set the specified resource field. |
      |Action |Select the generic actions to authorize. For detailed action descriptions, see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
      

   7. After completing the setup, click **Next** to confirm the current policy configuration.

   8. After confirming the information is correct, click **Confirm** to complete the policy creation.

      A created authorization policy will appear in the policy management list.


<span id=".5o6I5LqILWlhbS3nlKjmiLfmjIflrprotYTmupDmjIflrprmnaHku7bnmoTmnYPpmZA="></span>
## Granting IAM users permissions on specified resources with specified conditions


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. Click **Bucket List** in the left navigation, then click the target bucket name on the **Bucket List** page.

3. Select **Permission Management \> Bucket Authorization Policy Management** in the left navigation.

4. On the **Bucket Authorization Policy Management** page, under the **Visual View** tab, click **Create Policy**.

5. On the **Create Bucket Authorization Policy** page, select the **Folder Read/Write** template, then click **Next**.

6. On the **Create Bucket Authorization Policy** page, complete the policy information according to the prompts. The parameter description for this scenario is listed as follows.

   
   |**Type** |**Description** |
   |---|---|
   |Authorized User |Select **Specified Account** to choose the main account to authorize. Details are as follows<br><br><br>* **Current main account**: used to authorize IAM users (subusers) under the current main account. No need to enter the main account ID. Click **Add Field** to select the IAM user name from the dropdown under **Subuser Name**.<br><br>* **Other main account**: used to authorize IAM users (subusers) of another main account. You need to enter the other main account ID. Click **Add Field** and enter the IAM user name of the other main account. |
   |Resource |Select **specified object**, click the **add field** icon, and set the specified resource fields. |
   |Action |Select the generic actions to authorize. For detailed action descriptions, see [Supported actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |
   |Condition |Click the **add field** icon to set the required condition and value. For the parameter details of conditions, refer to [Conditions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC). |
   

7. After setting is complete, click **Next** to confirm the current configured policy information.

8. After verifying the information is correct, click **Confirm** to complete the policy creation.

   A created authorization policy will appear in the policy management list.
