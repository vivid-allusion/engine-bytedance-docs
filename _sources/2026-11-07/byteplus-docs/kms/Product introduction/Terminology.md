---
title: "Terminology"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Terminology"
---

**KMS**


|**Term** |**Acronym** |**Description** |
|---|---|---|
|**keyring** |\- |A keyring is a collection of customer\-managed keys. Keys with the same type or the same usage can be stored in the same keyring to facilitate management. You can call the [CreateKeyring](https://docs.byteplus.com/en/docs/kms/CreateKeyring) API to create a keyring. |
|**customer master key** |CMK |A CMK encrypts data keys (DKs) and generates an envelope. In addition, a CMK can encrypt short data, which is less than 4,096 bytes in length. You can call the [CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) API to create a CMK. |
|**data key** |DK |A data key can encrypt and decrypt data of any length. |
|**envelope encryption** |\- |You can call the [GenerateDataKey](https://docs.byteplus.com/en/docs/kms/GenerateDataKey) API to generate the plaintext and ciphertext of a data key. Then, you can encrypt your data using the plaintext of the data key, after which the plaintext of the data key is discarded. The encrypted data is stored with the ciphertext of the data key. When you need to decrypt the data, you can call the [Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt6) API to decrypt the ciphertext of the data key. After decryption, the plaintext of the data key is obtained and can be used to decrypt the encrypted data to obtain the plaintext of the data. |
|**hardware security module** |HSM |A hardware security module is a hardware device that performs cryptographic operations and securely generates and stores keys. KMS protects and performs related cryptographic operations on customer\-managed keys based on the HSM. |
|**bring your own key** |BYOK |The BYOK feature allows you to securely import your own keys into KMS as key material for the CMK, and then encrypt DKs or short data based on the CMK. |


&nbsp;

**Secret Manager**


|**Term** |**Description** |
|---|---|
|**secret** |A secret is sensitive information used to authenticate application users, such as database account passwords, SSH keys, sensitive addresses, AccessKey, and other sensitive data. |
|**ECS secret** |An Elastic Compute Service (ECS) secret can host a username and password combination and an SSH key pair that are used to log on to an ECS instance. |
|**IAM secret** |An Identity and Access Management (IAM) secret can host the AccessKey of an IAM user. |
|**generic secret** |A generic secret is a basic type of secret. It can store any sensitive data, such as accounts and passwords, access keys, OAuth keys, tokens, and API keys. |
|**RDS secret** |An RDS secret can host accounts and passwords of various database instances, such as RDS instances and Cache for Redis instances. |
|**encryption master key** |An encryption master key encrypts the stored secret data. |
