---
title: "Generic secret management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Generic_secret_management"
---

<span id="generic-secret"></span>
## Generic secret

A generic secret can store any sensitive data, such as custom accounts and passwords, access keys, OAuth keys, and tokens.

<span id="creating-a-secret"></span>
### Creating a secret


|**Pane** |**Parameter** |**Description** |
|---|---|---|
|**Basic Information** |**Secret type** |The current secret management feature supports generic secrets, Identity and Access Management (IAM) secrets, ECS secrets, RDS secrets, and Cache for Redis secrets. To create a Generic secret, select **Generic secret** from the drop\-down list. |
||**Secret name** |Set a name for the secret. |
||**Encryption key** |An encryption master key stores keys that are used to encrypt secret data. You can use the default system master key or select a symmetric key that you manage in the key management feature.<br><br>**Note: When you use a symmetric key that you manage by using Key Management Service (KMS), make sure that the encryption master key has not expired and is not mistakenly deleted. Otherwise, the secret will be unavailable.**  |
||**Description** |Enter a description of the secret. |
||**Project** |Select the project to which you want to add the secret. Only one project can be selected.<br><br>The project management feature is provided by BytePlus to allow you to manage resources of different services or projects by group. You can grant permissions to Identity and Access Management (IAM) roles and users by project, where a project represents a group of resources. This ensures resource isolation and data security. For more information on projects, refer to [Project management](https://docs.byteplus.com/docs/byteplus-platform/docs-editing-a-project). |
|**Secret Value Configuration** |**Secret value** |You can set a secret value to a key/value pair or text only.<br><br><br>1. Key/Value: The secret is stored as a key/value pair. Each key corresponds to one value. You can add multiple key/value pairs.<br><br>2. Plain text: The secret is stored as text only.<br><br><br>The text can be up to 30,720 bytes in length. |


<span id="rotating-the-secret"></span>
### Rotating the secret

Rotating a generic secret involves storing a new secret value. Secrets can be rotated manually only via the console or APIs. You can store a secret value by specifying the key/value or entering the value as text.
