---
title: "Encrypting and decrypting data locally based on envelope encryption"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Encrypting_and_decrypting_data_locally_based_on_envelope_encryption"
---

Key Management Service (KMS) allows you to encrypt the sensitive data of services deployed on the cloud. If the data object you need to encrypt is greater than 4,096 bytes, you can call the specified KMS API to protect the data using the envelope encryption technology.

**Typical scenarios**:

\*Encrypt business data.

\*Encrypt disk data.

**Encryption process**:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_411fdf78386cd9baa61c7faf954410cb.png) </span>


1. The user calls the [CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) API to create a customer master key (CMK).

2. The user calls the [GenerateDataKey](https://docs.byteplus.com/en/docs/kms/GenerateDataKey) API to create a data key, which can be used to encrypt data.

3. The service side encrypts the plaintext data by using the plaintext of the data key, to obtain the ciphertext of the data.

4. The service side persists both the ciphertext of the data key and the ciphertext of the data.


**Decryption process**


1. The service side calls the [Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt) API to decrypt the ciphertext of the data key by using the CMK.

2. KMS decrypts the ciphertext data by using the ciphertext of the data key to obtain the plaintext data.
