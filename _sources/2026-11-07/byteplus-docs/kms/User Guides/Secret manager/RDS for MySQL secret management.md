---
title: "RDS for MySQL secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/RDS_for_MySQL_secret_management"
---

<span id="rds-for-mysql-secret"></span>
## RDS for MySQL secret

An RDS for MySQL secret can store logon account and password combinations and SSH keys of BytePlus RDS for MySQL instances. You can enable the automatic rotation feature for an RDS for MySQL secret and set the rotation interval to 1 to 365 days.

<span id="single-and-dual-account-hosting"></span>
### Single\- and dual\-account hosting

RDS secrets support the dual\-account hosting mode and the single\-account hosting mode. In the single\-account hosting mode, the connection to the database may fail during automatic rotation. In the dual\-account hosting mode, the connection will not be interrupted and the business will not be affected during automatic rotation. The following figure shows how automatic rotation works in the dual\-account hosting mode.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7061536cdf54dce2e323c8755631adcc.png) </span>

In other words, in the dual\-account hosting mode, only the account and password tagged as OLDER are rotated, and after they are updated, the CURRENT and OLDER tags are switched.

<span id="creating-a-secret"></span>
### Creating a secret


|**Pane** |**Parameter** |**Description** |
|---|---|---|
|**Basic Information** |**Secret type** |The current secret management feature supports generic secrets, Identity and Access Management (IAM) secrets, Elastic Compute Service (ECS) secrets, RDS secrets, and Cache for Redis secrets. To create an RDS secret, select **RDS secret** from the drop\-down list. |
||**Secret name** |Set a name for the secret. |
||**Encryption key** |An encryption master key stores keys that are used to encrypt secret data. You can use the default system master key or select a symmetric key that you manage in the key management feature.<br><br>**Note: When you use a symmetric key that you manage by using Key Management Service (KMS), make sure that the encryption master key has not expired and is not mistakenly deleted. Otherwise, the secret will be unavailable.**  |
||**Description** |Enter a description of the secret. |
||**Project** |Select the project to which you want to add the secret. Only one project can be selected.<br><br>The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to IAM roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security. For more information on projects, refer to [Project management](https://www.volcengine.com/docs/6649/94333#%E9%A1%B9%E7%9B%AE%E7%AE%A1%E7%90%86). |
|**Secret value configuration** |**Secret value** |RDS instance: Select the RDS instance whose secret you want to host.<br><br>Account hosting: Select the single\- or dual\-account hosting mode as required.<br><br>Set secret value:<br><br><br>1. Import existing account: Select an existing account and password of the RDS instance.<br><br>2. Create account: You can create a new RDS account when creating an RDS secret. In the dual\-account hosting mode, the second database account is cloned in the format "Entered account name + _cloned", and both accounts have the same permissions.<br><br><br>After creating the database account, you can log on to the RDS console to view the information about the new account on the account management page. |


<span id="rotating-the-secret"></span>
### Rotating the secret

You can enable immediate rotation or automatic rotation on the console or through an API call.


* Automatic rotation: You can set the automatic rotation interval to 1 to 365 days. On the **Secret detail** page, click **Rotation setting** above the version list, enable or disable periodic automatic rotation, and click **Confirm**.

* Immediate rotation: On the **Secret detail** page, click **Immediately rotate** above the version list. In the dialog box that appears, click **Confirm**.
