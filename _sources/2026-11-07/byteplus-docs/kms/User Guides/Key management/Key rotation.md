---
title: "Key rotation"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Key_rotation"
---

BytePlus Key Management Service (KMS) provides the automatic transparent key rotation feature. After this feature is enabled, the system will rotate the key material of a customer master key (CMK) at a specified interval, which is one year by default. The rotation of the CMK does not affect the user business associated with the key, and the CMK can still be used to decrypt data that was encrypted before the rotation.

Periodic CMK rotation improves the protection level of encrypted data and helps enterprises meet various compliance requirements.

<span id="rotation-states"></span>
## Rotation states

The rotation state of a CMK may be:


* Enable

* Disable


The key rotation state determines whether the CMK will be rotated after the specified interval. When a CMK is created, key rotation is enabled for the key by default. You can change the key rotation state on the console or by calling the specified KMS API.

<span id="related-apis"></span>
## Related APIs

**API calls**

The following table lists the key\-related APIs available for different key rotation states.


|**Key Rotation State** |**Available API** |**Description** |
|---|---|---|
|Enable |[EnableKeyRotation](https://docs.byteplus.com/en/docs/kms/EnableKeyRotation) |ENables the rotation of the CMK. |
|Disable |[DisableKeyRotation](https://docs.byteplus.com/en/docs/kms/DisableKeyRotation) |Disables the rotation of the CMK. |
