---
title: "Key hosting"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Key_hosting"
---

Key hosting is a core feature of Key Management Service (KMS). KMS provides full key hosting and protection capabilities and allows you to conveniently encrypt data by calling cloud\-native APIs.

<span id="key-types"></span>
## Key types

When you call the [CreateKey](https://docs.byteplus.com/docs/kms/CreateKey) API to create a customer master key (CMK) for hosting, you can configure the type of the key. Key types are classified in the following dimensions:


* Key specifications (KeySpec)

* Key usage (KeyUsage)

* Key protection level (ProtectionLevel)

* Key origin (Origin)


Keys are classified into the following types:

**Symmetric Key**


|**Key type** |**Key specification** |**Key usage** |**Protection level** |**Algorithm** |**Key length** |**Data encryption mode** |**Supported regions** |
|---|---|---|---|---|---|---|---|
|Symmetric key |SYMMETRIC_256 |ENCRYPT_DECRYPT, GENERATE_VERIFY_MAC |SOFTWARE / HSM |AES |256 |GCM |All regions |
|Symmetric key |SYMMETRIC_128 |ENCRYPT_DECRYPT, GENERATE_VERIFY_MAC |SOFTWARE / HSM |SM4 |128 |GCM |Mainland China |


**Asymmetric Key**


|**Key type** |**Key specification** |**Key usage** |**Protection level** |**Algorithm** |**Key length** |**Supported regions** |
|---|---|---|---|---|---|---|
|Asymmetric Key |RSA_2048 |ENCRYPT_DECRYPT, SIGN_VERIFY |SOFTWARE / HSM |RSA |2048 |All regions |
|Asymmetric Key |RSA_3072 |ENCRYPT_DECRYPT, SIGN_VERIFY |SOFTWARE / HSM |RSA |3072 |All regions |
|Asymmetric Key |RSA_4096 |ENCRYPT_DECRYPT, SIGN_VERIFY |SOFTWARE / HSM |RSA |4096 |All regions |
|Asymmetric Key |EC_P256K |SIGN_VERIFY |SOFTWARE / HSM |ECC |256 |Mainland China |
|Asymmetric Key |EC_P256 |SIGN_VERIFY |SOFTWARE / HSM |ECC |256 |All regions |
|Asymmetric Key |EC_P384 |SIGN_VERIFY |SOFTWARE / HSM |ECC |384 |All regions |
|Asymmetric Key |EC_P521 |SIGN_VERIFY |SOFTWARE / HSM |ECC |521 |All regions |
|Asymmetric Key |EC_SM2 |ENCRYPT_DECRYPT, SIGN_VERIFY |HSM |SM2 |256 |Mainland China |


<span id="encryption-context"></span>
## Encryption context

As additional authenticated data (AAD), encryption context can be passed in as an optional parameter when a KMS symmetric key adopts the Galois/Counter Mode (GCM) of the block cipher. Encryption context provides additional integrity protection during encryption.

Encryption context is a JSON string in the Map<String, String\> format.

The following code shows an example of a valid encryption context:

```Plain Text
{"key1":"value1"}
{"name":"bob","path":"/path/to/plaintext.txt"}

```


The following APIs support the EncryptionContext parameter:


* [GenerateDataKey](https://docs.byteplus.com/docs/kms/GenerateDataKey)

* [Encrypt](https://docs.byteplus.com/docs/kms/Encrypt)

* [Decrypt](https://docs.byteplus.com/docs/kms/Decrypt)


<span id="key-states"></span>
## Key states

A CMK has five states:


* Enable

* Disable

* Archived

* PendingDelete

* PendingImport


Key states affect API calls, resource metering, and billing.

<span id="key-archival"></span>
## Key archival

Key archival is the process of archiving a CMK. An archived key can only be decrypted, and cannot be encrypted. When a CMK is archived, the key is still billed for storage and API calls.

You can enable or cancel key archival settings for a created CMK via the console or by calling the specified KMS API.

<span id="key-protection-levels"></span>
## Key protection levels

KMS provides two key protection levels to meet different security compliance and budget needs:


* Software

* Hardware security module (HSM)（To be released）


**Software**

Software\-protected keys are applicable to users with low security compliance requirements and limited budgets. They feature fast speed and low costs. Software\-protected CMKs and cryptographic operations are processed by the general\-purpose computing chip.

**HSM**

HSM\-protected keys enable you to store keys and perform cryptographic operations by using encryption devices that comply with the standards issued by China's State Cryptography Administration. Such keys have the following benefits:


* Security

   * Plaintext key material will be processed inside the HSM for cryptographic operations, and will be kept within the hardware security boundaries of the HSM. Note that ciphertext key material will be stored outside the HSM to improve availability.

   * Key material is generated based on a random number generation algorithm seeded with a high entropy value. This way, keys are protected from being restored or predicted by attackers.

* Ease of use

   * The HSM is fully hosted, freeing you from the associated procurement, deployment, and O&M work and greatly reducing costs.

* Availability

   * The HSM is deployed as a cluster, achieving high availability and scalability.

   * The system stores three copies of ciphertext keys for redundancy, maximizing the availability of stored keys.


<span id="key-origins"></span>
## Key origins

You can specify one of the following key origins when creating a CMK for hosting:


* BytePlus KMS (Default): The key material of the CMK is derived from BytePlus KMS.

* Outside BytePlus KMS: The key material of the CMK is securely imported into BytePlus KMS through the bring your own key (BYOK) feature.
