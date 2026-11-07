---
title: "Key management scenarios"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Key_management_scenarios"
---

<span id="key-hosting"></span>
## **Key hosting**


* The Key Management Service (KMS) is primarily used in key hosting scenarios. It provides full key hosting and protection capabilities and allows you to encrypt data by calling cloud\-native APIs.

* The software\-protected key hosting features fast speed and low costs. It is applicable to users with low security compliance requirements and limited budgets. Software\-protected customer master keys (CMKs) and cryptographic operations are processed by the general\-purpose computing chip.


<span id="encrypting-data-online-using-kms"></span>
## **Encrypting data online using KMS**

KMS allows you to encrypt the sensitive data of services deployed on the cloud. If the data object you need to encrypt is less than 4,096 bytes, you can call the specified KMS API to directly encrypt and decrypt the data online.

<span id="typical-scenarios"></span>
### **Typical scenarios**


* Encrypt configuration files.

* Encrypt SSH keys, logon passwords of virtual machines, and SSL certificates.


<span id="encryption-process"></span>
### **Encryption process**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_4776ab548abaf5412db98e520ec0dda2.png) </span>


1. The user calls the [CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) API to create a CMK.

2. The user calls the [Encrypt](https://docs.byteplus.com/en/docs/kms/Encrypt) API to encrypt the plaintext data. Ciphertext data is returned.

3. The user deploys the ciphertext data in the server.

4. When the service side needs to use the data, the service side calls the [Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt) API to decrypt the ciphertext data to obtain the plaintext data.


<span id="encrypting-and-decrypting-data-locally-based-on-envelope-encryption"></span>
## **Encrypting and decrypting data locally based on envelope encryption**

KMS allows you to encrypt the sensitive data of services deployed on the cloud. If the data object you need to encrypt is greater than 4,096 bytes, you can call the specified KMS API to protect the data using the envelope encryption technology.

<span id="typical-scenarios"></span>
### **Typical scenarios**


* Encrypt business data.

* Encrypt disk data.


<span id="encryption-process"></span>
### **Encryption process**

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_979aacf227fe68a73581f17002dffc6a.png) </span>


1. The user calls the [CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) API to create a CMK.

2. The user calls the [GenerateDataKey](https://docs.byteplus.com/en/docs/kms/GenerateDataKey) API to create a data key, which can be used to encrypt data.

3. The service side encrypts the plaintext data by using the plaintext of the data key, to obtain the ciphertext of the data.

4. The service side persists both the ciphertext of the data key and the ciphertext of the data.


<span id="decryption-process"></span>
### **Decryption process**


1. The service side calls the [Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt) API to decrypt the ciphertext of the data key by using the CMK.

2. KMS decrypts the ciphertext data by using the ciphertext of the data key to obtain the plaintext data.
