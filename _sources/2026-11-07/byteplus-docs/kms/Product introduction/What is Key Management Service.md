---
title: "What is Key Management Service"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/What_is_Key_Management_Service"
---

<span id="what-is-a-key-management-system"></span>
## What Is a Key Management System?

BytePlus Key Management System is a comprehensive security service that includes **Key Management Service (KMS)**  and **Secret Manager**, providing centralized management and protection for cryptographic keys and credentials.

In Mainland China regions, the service is built on **Hardware Security Modules (HSMs)**  that have obtained certifications from the relevant national commercial cryptography authorities, ensuring compliance with China’s commercial cryptography regulations.

&nbsp;

In regions outside Mainland China, the service is built on **Hardware Security Modules (HSMs)**  certified to **FIPS 140\-3 Level 3**, meeting internationally recognized high\-level security and compliance standards and providing a strong security foundation for your keys and credentials.

<span id="core-components"></span>
## Core Components

**Key Management Service** (KMS) is an all\-in\-one key management and data encryption service platform provided by BytePlus. With easy\-to\-use encryption APIs, KMS allows you to conveniently manage keys and protect the security of your core data on the cloud. In addition, KMS greatly reduces your procurement costs and R&D costs when deploying cryptographic infrastructure and helps your business meet regulatory and compliance requirements.

**Secret Manager** is a secret management service developed based on BytePlus KMS. It stores accounts and passwords, access keys, and other secret information that you need to use in your business applications. You can integrate your business applications with the KMS SDK or KMS APIs to securely and dynamically obtain secret information from the Secret Manager. This prevents data leaks, unintended modifications, or other risks caused by storing sensitive information in plaintext.

&nbsp;


|**Business Module** |**Feature Description** |**Main Functions** |
|---|---|---|
|KMS |KMS focuses on the generation, management, and protection of encryption keys. It provides secure key storage, key generation, encryption, and key rotation capabilities. KMS manages the keys used during encryption, ensuring the security of encrypted data. |Encrypts data, protects data integrity, and performs digital signing and other security operations. This service is commonly used to encrypt the data of applications and services. |
|Secret Manager |Secret Manager focuses on the management and storage of sensitive secrets, such as API keys, database passwords, and certificates. It provides secure storage, access control, automatic rotation, and auditing capabilities to ensure the security of sensitive information during storage and use. |Stores sensitive information required by applications and provides convenient access and management methods, ensuring data security and compliance. |


With security keys provided by **KMS**, **Secret Manager** can encrypt and decrypt the sensitive data it stores. In other words, Secret Manager can enhance its security capabilities by leveraging the powerful key management capabilities of KMS to properly encrypt the sensitive information stored in the Secret Manager.
