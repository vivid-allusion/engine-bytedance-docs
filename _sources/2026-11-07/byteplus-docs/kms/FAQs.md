---
title: "FAQs"
product: "BytePlus Key Management Service"
product_code: "kms"
section: "Document"
source: "https://docs.byteplus.com/en/docs/kms/FAQs"
---

<span id="UZ7xnRO1"></span>
## Which KMS key types are certified to FIPS 140\-3 Level 3?

The following KMS key types are protected by **Hardware Security Modules (HSMs)**  that are certified to **FIPS 140\-3 Level 3** in the regions listed below.


|**Protection Level** |**Symmetric Keys** |**Asymmetric Keys** |**Regions** |
|---|---|---|---|
|HSM |SYMMETRIC_256 |RSA_2048, RSA_3072, RSA_4096, EC_P256, EC_P384, EC_P521 |Johor, Jakarta, Hong Kong (China) |


<span id="j0Lzh5EG"></span>
## How are my keys protected in KMS? Is there any risk of key exposure?

Your plaintext keys are designed to **never leave the secure boundary of HSMs** that meet high\-assurance security certification requirements. KMS protects your keys through multiple layers of security controls:

<span id="CcdbrhMN"></span>
### Cryptographic Boundary Protection

Keys are generated inside HSMs and are always stored outside the HSM in encrypted form. When cryptographic operations are requested, only the encrypted key material, the data to be encrypted, and the operation instructions are sent to the HSM. The plaintext key material never leaves the hardware security boundary.

<span id="KYrkqCEm"></span>
### Physical Security Protection

HSM devices are designed with strong physical tamper\-resistance capabilities. Any attempt at physical intrusion—such as drilling, casing removal, or abnormal environmental conditions—is detected and triggers built\-in key zeroization mechanisms within the HSM.

<span id="Xc7yaJVC"></span>
### Logical Access Control

All access to and operations on keys must be authorized through strict authentication and authorization controls, including identity verification and fine\-grained permission policies (IAM/RBAC). All key\-related operations are fully logged and auditable.
