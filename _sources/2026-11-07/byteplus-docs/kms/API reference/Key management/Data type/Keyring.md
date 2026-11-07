---
title: "Keyring"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Keyring"
---

**Keyring**


|**Name** |**Type** |**Example Value** |**Description** |
|---|---|---|---|
|ID |String |1d2baaf3\-d357\-46c2\-832e\-13560c2bd9cd |The unique ID of the keyring. The value is in the UUID format. |
|CreationDate |Long |1709789948 |The date when the keyring was created. |
|UpdateDate |Long |1709789948 |The date when the keyring was updated. |
|KeyringName |String |Example keyring name |The alias of the keyring.<br><br>The alias must be 2 to 31 characters in length. |
|KeyringType |String |ManagedKeyring |The type of the key. Valid values:<br><br><br>* ManagedKeyring<br><br>* CustomKeyring |
|Description |String |Example description |The description of the keyring.<br><br>The description must be 0 to 8,192 characters in length. |
|UID |String |1234567890 |The tenant ID of the creator who created the keyring. |
