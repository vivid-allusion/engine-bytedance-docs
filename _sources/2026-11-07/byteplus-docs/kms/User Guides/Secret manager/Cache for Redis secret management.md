---
title: "Cache for Redis secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Cache_for_Redis_secret_management"
---

<span id="cache-for-redis-secret"></span>
## Cache for Redis secret

A Cache for Redis secret stores account and password combinations of a BytePlus Cache for Redis instance. It supports the single\- and dual\-account hosting modes and the automatic rotation feature.

&nbsp;

<span id="creating-a-secret"></span>
### Creating a secret


|**Pane** |**Parameter** |**Description** |
|---|---|---|
|**Basic Information** |**Secret type** |The current secret management feature supports generic secrets, Identity and Access Management (IAM) secrets, ECS secrets, RDS secrets, and Cache for Redis secrets. To create a Redis secret, select **Redis secret** from the drop\-down list. |
||**Secret name** |Set a name for the secret. |
||**Encryption key** |An encryption master key stores keys that are used to encrypt secret data. You can use the default system master key or select a symmetric key that you manage in the key management feature.<br><br>**Note: When you use a symmetric key that you manage by using Key Management Service (KMS), make sure that the encryption master key has not expired and is not mistakenly deleted. Otherwise, the secret will be unavailable.**  |
||**Description** |Enter a description of the secret. |
||**Project** |Select the project to which you want to add the secret. Only one project can be selected.<br><br>The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to Identity and Access Management (IAM) roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security. For more information on projects, refer to [Project management](https://docs.byteplus.com/docs/byteplus-platform/docs-editing-a-project). |
|**Secret Value Configuration** |**Secret value** |Redis instance: Select the Cache for Redis instance whose secret you want to host.<br><br>Account hosting: Select the single\- or dual\-account hosting mode as required.<br><br>Set secret value:<br><br><br>1. Import existing account: Select an existing account and password of the Cache for Redis instance.<br><br>2. Create account: You can create a new Cache for Redis account when creating a Cache for Redis secret. In the dual\-account hosting mode, the second database account is cloned in the format "Entered account name + _cloned", and both accounts have the same permissions.<br><br><br>After creating the database account, you can log on to the Cache for Redis console to view the information about the new account on the account management page. |


<span id="rotating-the-secret"></span>
### Rotating the secret

You can enable immediate rotation or automatic rotation on the console or through an API call.


* Automatic rotation: You can set the automatic rotation interval to 1 to 365 days. On the **Secret detail** page, click **Rotation setting** above the version list, enable or disable periodic automatic rotation, and click **Confirm**.

* Immediate rotation: On the **Secret detail** page, click **Immediately rotate** above the version list. In the dialog box that appears, click **Confirm**.
