---
title: "Key"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Key"
---

**Key**


|**Name** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|ID |String |1d2baaf3\-d357\-46c2\-832e\-13560c2bd9cd |The unique ID of the key. The value is in the UUID format. |
|CreationDate |Long |1709789948 |The date when the key was created. |
|KeyName |String |example\-keyname |The alias of the key.<br><br>The alias must be 2 to 31 characters in length. |
|KeySpec |String |SYMMETRIC_256 |The algorithm used in the key.<br><br>Valid values for symmetric keys:<br><br><br>* SYMMETRIC_256<br><br>* SYMMETRIC_128<br><br><br>Valid values for asymmetric keys:<br><br><br>* RSA_2048<br><br>* RSA_3072<br><br>* RSA_4096<br><br>* EC_P256<br><br>* EC_P256K<br><br>* EC_P384<br><br>* EC_P521<br><br>* EC_SM2 |
|Description |String |Example description |The description of the key.<br><br>The description must be 0 to 8,192 characters in length. |
|ProtectionLevel |String |SOFTWARE |The protection level of the key. Valid values:<br><br><br>* SOFTWARE<br><br>* HSM |
|KeyState |String |Enable |The state of the key. Valid values:<br><br><br>* Enable<br><br>* Disable<br><br>* PendingDelete |
|KeyUsage |String |ENCRYPT_DECRYPT |The usage of the key. Valid values:<br><br><br>* ENCRYPT_DECRYPT<br><br>* SIGN_VERIFY |
|UpdateDate |Long |1709789948 |The date when the key was updated. |
|RotationState |string |Enable |The rotation configuration of the key. |
|LastRotationTime |string |2024\-05\-04T21:48:24.369005772+08:00 |The last time the key was rotated. |
|ScheduleRotationTime |string |2024\-05\-04T21:48:24.369005772+08:00 |The next time the key will be rotated. |
|Trn |string |trn:kms:cn\-beijing:2100001139:keyrings/111/keys/ecc256k\-hardwares |The name of the resource.<br><br>The name must be in the format trn:${Service}:${Region}:${AccountID}:${ResourcePath}. |
|VerifyToken |string | |The token of the key material. |
