---
title: "Product features"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Product_features"
---

<span id="key-lifecycle-management"></span>
## **Key lifecycle management**

Key Management Service (KMS) enables you to manage the entire lifecycle of keys through the following features:


* **Key group management:**  manages keys by group using keyrings.

* **Key distribution or injection:**  automatically distributes keys via the system to ensure security, implementing backup and storage mechanisms for keys that are used more than once.

* **Key update:**  updates keys according to a specified lifecycle and strength.

* **Key archival:**  archives keys with the same type or the same usage into the same keyring to facilitate management.

* **Key restoration:**  restores a CMK to the Enable state if the scheduled deletion of the CMK is canceled.


&nbsp;

<span id="key-auditing"></span>
## **Key auditing**

KMS records and audits key management activities. In the audit log of KMS, you can view the key use history of each system service.

&nbsp;

<span id="secret-lifecycle-management"></span>
## **Secret lifecycle management**


* **Secret management**: allows you or applications to create, retrieve, update, and delete secrets, uniformly managing the entire lifecycle of sensitive secrets with ease.

* **Secret version management (secure secret rotation)** : securely rotates sensitive secrets for application nodes through APIs and the console at specific intervals, which improves the system security.

* **Cloud\-native integration**: integrates secret management with cloud\-native systems, allowing you to host the secrets of IAM, RDS, Cache for Redis, and ECS instances and configure rotation intervals to make secrets dynamic. This feature helps you prevent security threats to the AccessKey IDs and AccessKey Secrets of IAM instances and account and password leaks of RDS, Cache for Redis, and ECS instances.


&nbsp;

<span id="secret-auditing"></span>
## **Secret auditing**

KMS records and audits secret management activities. In the audit log of KMS, you can view the secret use history of each system service.
