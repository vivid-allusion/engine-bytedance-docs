---
title: "Secret management scenarios"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Secret_management_scenarios"
---

<span id="database-accounts-and-passwords"></span>
## Database accounts and passwords

[RDS for MySQL secret management](https://docs.byteplus.com/en/docs/kms/RDS_for_MySQL_secret_management)

[Cache for Redis secret management](https://docs.byteplus.com/en/docs/kms/Cache_for_Redis_secret_management)

You can store the account and password of a database in the secrets of Key Management Service (KMS). When a business application needs to access the database, you can integrate the business application to the KMS SDK or call the specified KMS API to dynamically obtain the database account and password from KMS.

<span id="account-and-password-combinations-and-ssh-keys-of-ecs-instances"></span>
## Account and password combinations and SSH keys of ECS instances

[ECS secret management](https://docs.byteplus.com/en/docs/kms/ECS_secret_management)

You can store the account and password or public and private keys of an Elastic Compute Service (ECS) instance in the secrets of KMS. When a business application needs to log on to the ECS instance, you can integrate the business application to the KMS SDK or call the specified KMS API to dynamically obtain the logon secrets from KMS.

<span id="accesskey-ids-and-accesskey-secrets"></span>
## AccessKey IDs and AccessKey Secrets

[IAM secret management](https://docs.byteplus.com/en/docs/kms/IAM_secret_management)

When a business application uses a BytePlus AccessKey as an access secret, you can store the AccessKey in the secrets of KMS. The business application can dynamically obtain the AccessKey from KMS.

<span id="generic-secrets"></span>
## Generic secrets

[Generic secret management](https://docs.byteplus.com/en/docs/kms/Generic_secret_management)

As a basic type of secret supported in KMS, generic secrets can store any sensitive data, such as custom accounts and passwords, access keys, OAuth keys, and tokens. In addition, generic secrets support multiple secret versions, making it easier to update secret values and preventing data leaks caused by hard\-coded secrets.
