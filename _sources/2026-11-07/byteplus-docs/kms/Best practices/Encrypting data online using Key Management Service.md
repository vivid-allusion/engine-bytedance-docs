---
title: "Encrypting data online using Key Management Service"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Encrypting_data_online_using_Key_Management_Service"
---

Key Management Service (KMS) allows you to encrypt the sensitive data of services deployed on the cloud. If the data object you need to encrypt is less than 4,096 bytes, you can call the specified KMS API to directly encrypt and decrypt the data online.

**Encryption process**:

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3256e8b78bedaf14dcc59a187da26022.png) </span>


1. The user calls the [CreateKey](https://docs.byteplus.com/en/docs/kms/CreateKey) API to create a CMK.

2. The user calls the [Encrypt](https://docs.byteplus.com/en/docs/kms/Encrypt) API to encrypt the plaintext data. Ciphertext data is returned.

3. The user deploys the ciphertext data in the server.

4. When the service side needs to use the data, the service side calls the [Decrypt](https://docs.byteplus.com/en/docs/kms/Decrypt) API to decrypt the ciphertext data to obtain the plaintext data.
