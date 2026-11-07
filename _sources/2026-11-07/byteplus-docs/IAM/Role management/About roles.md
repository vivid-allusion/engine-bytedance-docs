---
title: "About roles"
product: "BytePlus IAM"
product_code: "IAM"
source: "https://docs.byteplus.com/en/docs/IAM/about-roles"
---

"Role" is an identity type. Roles do not have access to cloud resources. These roles are assigned to other identities, like users. These role\-assigned identities can user AssumeRole to generate temporary security tokens to accessing cloud resources.

Roles can be assigned to the following identities:


* **User**: A user can be a real user or a backend service. After a role has been assigned to a user, the user can access cloud resources through the generation of temporary security tokens.

* **Account**: Roles can be assigned to the current account or other accounts.

* **Cloud service**: After a role has been assigned to a BytePlus cloud service, this service can access other cloud resources as an account.
