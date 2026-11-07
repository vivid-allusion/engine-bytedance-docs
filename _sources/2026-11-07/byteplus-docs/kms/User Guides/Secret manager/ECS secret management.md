---
title: "ECS secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/ECS_secret_management"
---

<span id="ecs-secret"></span>
## ECS secret

An Elastic Compute Service (ECS) secret can store logon account and password combinations and SSH keys of BytePlus ECS instances. You can enable the automatic rotation feature for an ECS secret and set the rotation interval to 1 to 365 days.

<span id="creating-a-secret"></span>
### Creating a secret


|**Pane** |**Parameter** |**Description** |
|---|---|---|
|**Basic Information** |**Secret type** |The current secret management feature supports generic secrets, Identity and Access Management (IAM) secrets, ECS secrets, RDS secrets, and Cache for Redis secrets. To create an ECS secret, select **ECS secret** from the drop\-down list. |
||**Secret name** |Set a name for the secret. |
||**Encryption key** |An encryption master key stores keys that are used to encrypt secret data. You can use the default system master key or select a symmetric key that you manage in the key management feature.<br><br>**Note: When you use a symmetric key that you manage by using Key Management Service (KMS), make sure that the encryption master key has not expired and is not mistakenly deleted. Otherwise, the secret will be unavailable.**  |
||**Description** |Enter a description of the secret. |
||**Project** |Select the project to which you want to add the secret. Only one project can be selected.<br><br>The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to Identity and Access Management (IAM) roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security. For more information on projects, refer to [Project management](https://docs.byteplus.com/docs/byteplus-platform/docs-editing-a-project). |
|**Secret Value Configuration** |**Secret value** |**Managed ECS**: Select the ECS instance whose secret you want to host.<br><br>**ECS username**: Specify the username that will host the secret. The user can be an administrator with high permissions, such as **root** or **Administrator**, or a created user. You can perform a fuzzy search to find usernames and select one from the drop\-down list.<br><br>**Login method**: If an ECS instance runs on Linux, you can host passwords and SSH keys of the ECS instance. If an ECS instance runs on Windows, you can only host passwords of the ECS instance.<br><br>**Note:** <br><br><br>1. If the hosting username is incorrect, the ECS secret can still be created, but cannot be manually or automatically rotated. We recommend that you call the RotateSecret API to rotate the secret after creation. This helps you verify the rotation feature and allows you to replace the initial password with a strong password immediately.<br><br>2. After you host the account and password or public and private keys of an ECS instance in the secret management feature, do not change or delete them on the ECS console. |


<span id="rotating-the-secret"></span>
### Rotating the secret

You can enable immediate rotation or automatic rotation on the console or through an API call.


* Automatic rotation: You can set the automatic rotation interval to 1 to 365 days. On the **Secret detail** page, click **Rotation setting** above the version list, enable or disable periodic automatic rotation, and click **Confirm**.

* Immediate rotation: On the **Secret detail** page, click **Immediately rotate** above the version list. In the dialog box that appears, click **Confirm**.
