---
title: "Getting started with key management"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management"
---

**Step 1: Activate the service**

Prerequisites: You have registered a BytePlus account and passed real\-name authentication.

When you go to the [Key Management Service (KMS) console](https://console.byteplus.com/kms/region:kms+ap-southeast-1/kms) for the first time, KMS is automatically activated. The service activation process will take several minutes.

**Step 2: Create a keyring**

Prerequisites: KMS is activated.

Click **Create keyring** to create the first keyring.

Procedure:


* Click **Create keyring**. The **Create keyring** dialog box appears.

* Enter an alias in the **Alias** box (required) and the description in the **Description** box (optional).

* Click **Create**.


After the process is complete, you can view the new keyring on the console.

**Step 3: View the keyring**

Prerequisites: The keyring is created.

Find the specified keyring, and click **Detail** in the **Actions** column or directly click the keyring ID. On the **Detail**, you can preview and modify the information about the keyring.

Procedure:


* To modify the description of the keyring, click the Pencil icon next to **Description**.


**Step 4: Create a key**

Prerequisites: A keyring is selected.

Click **Create key** to create a customer master key (CMK).

Procedure:


* Select a key type from the **Key Type** drop\-down list.

* Select a key usage from the **Key usage** drop\-down list.

* Select a protection level from the \*\* Protection level\*\* drop\-down list.

* Enter an alias in the **Alias** box.

* (Optional) Enter the description of the key in the **Description** box.


**Step 5: View the key**

Prerequisites: A key is created.

On the **Detail**, you can view the CMK you created.

**Step 6: Generate a data key**

Prerequisites: A key with the key type set to **Symmetric key** is created.

Find the specified key and click **Generate data key** in the **Actions** column to generate a data key for envelope encryption.

Procedure:


* Click the **Copy** icon next to **Plaintext** to copy the plaintext of the data key.

* Click the **Copy** icon next to **Ciphertext** to copy the ciphertext of the data key.


**Step 7: Copy and download the public key**

Prerequisites: A key with the key type set to **Asymmetric key** is created.

On the **Detail** page, click **Copy public key** to copy the public key or click **Download public key** to download the public key.

**Step 8: Delete a data key**

Prerequisites: A key is created.

If you no longer need to use a CMK you created, you can click **Set deletion time** to set a scheduled deletion time for the CMK.

Procedure:


* Set **Set deletion time** to specify the number of days after which the key will be automatically deleted.

* Click **Confirm**.


**Step 9: Cancel scheduled deletion**

Prerequisites: A deletion schedule is configured for the key.

To cancel the scheduled deletion for a key, click **Revoke delete plan**.

**Step 9: Archive a key**

Prerequisites: A key is created.

An archived key can only be decrypted, and cannot be encrypted. To archive a key, click **Archive**.

**Step 10: Cancel archiving a key**

Prerequisites: The key is archived.

To restore an archived key, click **Undo archive**.
