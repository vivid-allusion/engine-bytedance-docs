---
title: "IAM secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/IAM_secret_management"
---

<span id="iam-secret"></span>
## IAM secret

An Identity and Access Management (IAM) secret can store AccessKey IDs and AccessKey Secrets of IAM sub\-accounts. You can enable the automatic rotation feature for an IAM secret and set the rotation interval to 1 to 365 days.

&nbsp;

<span id="creating-a-role"></span>
### Creating a role

**Step 1: Create a custom policy**


1. Log on to the [IAM console](https://console.byteplus.com/iam/identitymanage/role) as an IAM administrator.

2. On the left navigation pane, choose **Policy management**.

3. On the **Policy management** page, click **Create policy**.

4. Select **JSON Editor** and input the following script:


```json
{
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:UpdateAccessKey",
                "iam:DeleteAccessKey",
                "iam:ListAccessKeys",
                "iam:CreateAccessKey"
            ],
            "Resource": [
                "*"
            ]
        }
    ]
}
```



5. Set **Policy name** to **SecretsManagerManagedIAMSecretsRolePolicy**.

6. Click **Submit**.


**Step 2: Create an IAM role**


1. Log on to the [IAM console](https://console.byteplus.com/iam/identitymanage/role) as an IAM administrator.

2. On the **Role** page, click **Create new Role**.

3. On the **Create new role** page, select **Services** for the trusted identity type.

4. Select **kms**, clear **Create as a service\-associated role**, and click **Next**.

5. Set **Role name** to **SecretsManagerManagedIAMSecretsRole** and click **Next**.

6. Select the policy named **SecretsManagerManagedIAMSecretsRolePolicy** and click **Submit**.


For more information on how to create an IAM role, refer to [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles).

&nbsp;

<span id="creating-a-secret"></span>
### Creating a secret


|**Pane** |**Parameter** |**Description** |
|---|---|---|
|**Pane** |**Parameter** |**Description** |
|:\-\- |:\-\- |:\-\- |
|**Basic Information** |**Secret type** |The current secret management feature supports generic secrets, Identity and Access Management (IAM) secrets, ECS secrets, RDS secrets, and Cache for Redis secrets. To create an IAM secret, select **IAM secret** from the drop\-down list. |
||**Secret name** |Set a name for the secret. |
||**Encryption key** |An encryption master key stores keys that are used to encrypt secret data. You can use the default system master key or select a symmetric key that you manage in the key management feature.<br><br>**Note: When you use a symmetric key that you manage by using Key Management Service (KMS), make sure that the encryption master key has not expired and is not mistakenly deleted. Otherwise, the secret will be unavailable.**  |
||**Description** |Enter a description of the secret. |
||**Project** |Select the project to which you want to add the secret. Only one project can be selected.<br><br>The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to Identity and Access Management (IAM) roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security. For more information on projects, refer to [Project management](https://docs.byteplus.com/docs/byteplus-platform/docs-editing-a-project). |
|**Secret Value Configuration** |**Secret value** |Perform a fuzzy search for IAM usernames. From the drop\-down list, select the username for the AccessKey ID and AccessKey Secret that you want to store. Then, enter the AccessKey Secret of the AccessKey ID.<br><br>**Note: If the SecretsManagerManagedIAMSecretsRole role is not created, you must create a policy and the role according to the preceding role creation process before you can store the AccessKey ID and AccessKey Secret in Secret Manager.** <br><br>To query the AccessKey Secret, go to [User management - Access control](https://console.byteplus.com/iam/identitymanage/user/). On the **User detail** page, you can view the AccessKey Secret on the **Access Key** tab. |


<span id="rotating-the-secret"></span>
### Rotating the secret

You can enable immediate rotation or automatic rotation on the console or through an API call.


* Automatic rotation: You can set the automatic rotation interval to 1 to 365 days. On the **Secret detail** page, click **Rotation setting** above the version list, enable or disable periodic automatic rotation, and click **Confirm**.

* Immediate rotation: On the **Secret detail** page, click **Immediately rotate** above the version list. In the dialog box that appears, click **Confirm**.
