---
title: "Encryption function"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-encryption"
---

These functions use the AES (Advanced Encryption Standard) algorithm for data encryption and decryption.

The key length depends on the encryption mode. For \-128\-, \-196\-, and \-256\- modes, the key lengths are 16, 24, and 32 bytes respectively.

The length of the initialization vector is always 16 bytes (parts exceeding 16 bytes will be ignored).

<span id="918c137e"></span>
### encrypt

This function encrypts data using the following modes:


* aes\-128\-ecb, aes\-192\-ecb, aes\-256\-ecb

* aes\-128\-cbc, aes\-192\-cbc, aes\-256\-cbc

* aes\-128\-ofb, aes\-192\-ofb, aes\-256\-ofb

* aes\-128\-gcm, aes\-192\-gcm, aes\-256\-gcm

* aes\-128\-ctr, aes\-192\-ctr, aes\-256\-ctr


**Syntax**

```SQL
encrypt('mode', 'plaintext', 'key' [, iv, aad])
```


**Param**


* **`mode`**— Encryption Mode. String.

* **`plaintext`**— The text that needs to be encrypted. String.

* **`key`**— The encryption key. String.

* **`iv`**— Initialization vector. Required for `-gcm` mode, optional for other modes. String.

* **`aad`**— Additional authentication data. While not encrypted, it impacts decryption. Only valid in `-gcm` mode; raises an exception in other modes. String.


**Return value**


* Ciphertext binary string. String.


**Example**

Create table:

```SQL
CREATE TABLE encryption_test
(
    `comment` String,
    `secret` String
)
ENGINE = Memory;
```


Insert some data (avoid storing keys/ivs in databases as it defeats the entire concept of encryption), storing "reminders" is also unsafe and is used here only for explanatory purposes:

```SQL
-- Insert
INSERT INTO encryption_test VALUES('aes-256-ofb no IV', encrypt('aes-256-ofb', 'Secret', '12345678910121314151617181920212')),\
('aes-256-ofb no IV, different key', encrypt('aes-256-ofb', 'Secret', 'keykeykeykeykeykeykeykeykeykeyke')),\
('aes-256-ofb with IV', encrypt('aes-256-ofb', 'Secret', '12345678910121314151617181920212', 'iviviviviviviviv')),\
('aes-256-cbc no IV', encrypt('aes-256-cbc', 'Secret', '12345678910121314151617181920212'));
```


```SQL
-- Query
SELECT comment, hex(secret) FROM encryption_test;
```


As a result:

```Plain
┌─comment──────────────────────────┬─hex(secret)──────────────────────┐
│ aes-256-ofb no IV                │ B4972BDC4459                     │
│ aes-256-ofb no IV, different key │ 2FF57C092DC9                     │
│ aes-256-ofb with IV              │ 5E6CB398F653                     │
│ aes-256-cbc no IV                │ 1BC0629A92450D9E73A00E7D02CF4142 │
└──────────────────────────────────┴──────────────────────────────────┘
```


**`Example: -gcm`**:

```SQL
-- Insert
INSERT INTO encryption_test VALUES('aes-256-gcm', encrypt('aes-256-gcm', 'Secret', '12345678910121314151617181920212', 'iviviviviviviviv')), \
('aes-256-gcm with AAD', encrypt('aes-256-gcm', 'Secret', '12345678910121314151617181920212', 'iviviviviviviviv', 'aad'));

SELECT comment, hex(secret) FROM encryption_test WHERE comment LIKE '%gcm%';
```


As a result:

```Plain
┌─comment──────────────┬─hex(secret)──────────────────────────────────┐
│ aes-256-gcm          │ A8A3CCBC6426CFEEB60E4EAE03D3E94204C1B09E0254 │
│ aes-256-gcm with AAD │ A8A3CCBC6426D9A1017A0A932322F1852260A4AD6837 │
└──────────────────────┴──────────────────────────────────────────────┘
```


<span id="279f7b47"></span>
### aes_encrypt_mysql

Compatible with MySQL encryption, the generated ciphertext can be decrypted via the AES_DECRYPT function.

Under the same input, the same ciphertext as encryption will be produced. But when the `key` or `iv` is longer than the normal length, `aes_encrypt_mysql` follows MySQL's `aes_encrypt` behavior: "folding" the `key` and ignoring the excess bits of the `iv`.

Supported Encryption Modes:


* aes\-128\-ecb, aes\-192\-ecb, aes\-256\-ecb

* aes\-128\-cbc, aes\-192\-cbc, aes\-256\-cbc

* aes\-128\-ofb, aes\-192\-ofb, aes\-256\-ofb


**Syntax**

```SQL
aes_encrypt_mysql('mode', 'plaintext', 'key' [, iv])
```


**Parameters**


* **`mode`**— Encryption Mode. String.

* **`plaintext`**— The text that needs encryption. String.

* **`Key`**— Encryption Key. If the length of the key exceeds the required length for the mode, perform MySQL\-specific key folding. String.

* **`iv`**— Initialization Vector. Optional, only consider the first 16 bytes of the string.


**Return Value**


* Ciphertext binary string. String.


**Example**

Given the same input `encrypt` and `aes_encrypt_mysql` generate the same ciphertext:

```SQL
SELECT encrypt('aes-256-ofb', 'Secret', '12345678910121314151617181920212', 'iviviviviviviviv') = aes_encrypt_mysql('aes-256-ofb', 'Secret', '12345678910121314151617181920212', 'iviviviviviviviv') AS ciphertexts_equal;
```


As a result:

```Plain
┌─ciphertexts_equal─┐
│                 1 │
└───────────────────┘
```


But when it is longer than expected `encrypt`, it fails: `keyiv`

```SQL
-- Query
SELECT encrypt('aes-256-ofb', 'Secret', '123456789101213141516171819202122', 'iviviviviviviviv123');
```


As a result:

```Plain
Received exception from server (version 22.6.1):
Code: 36. DB::Exception: Received from localhost:9000. DB::Exception: Invalid key size: 33 expected 32: While processing encrypt('aes-256-ofb', 'Secret', '123456789101213141516171819202122', 'iviviviviviviviv123').
```


Produces an output compatible with `aes_encrypt_mysql`MySQL:

```SQL
-- Query
SELECT hex(aes_encrypt_mysql('aes-256-ofb', 'Secret', '123456789101213141516171819202122', 'iviviviviviviviv123')) AS ciphertext;
```


As a result:

```Plain
┌─ciphertext───┐
│ 24E9E4966469 │
└──────────────┘
```


Note, even if the supply time is longer, `IV` will produce the same result

```SQL
-- Query
SELECT hex(aes_encrypt_mysql('aes-256-ofb', 'Secret', '123456789101213141516171819202122', 'iviviviviviviviv123456')) AS ciphertext
```


As a result:

```Plain
┌─ciphertext───┐
│ 24E9E4966469 │
└──────────────┘
```


Its binary result is the same as the result generated by MySQL under the same input:

```SQL
mysql> SET  block_encryption_mode='aes-256-ofb';
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT aes_encrypt('Secret', '123456789101213141516171819202122', 'iviviviviviviviv123456') as ciphertext;
+------------------------+
| ciphertext             |
+------------------------+
| 0x24E9E4966469         |
+------------------------+
1 row in set (0.00 sec)
```


<span id="7a75f11e"></span>
### decrypt

This function uses the following mode to decrypt ciphertext into plaintext:


* aes\-128\-ecb, aes\-192\-ecb, aes\-256\-ecb

* aes\-128\-cbc, aes\-192\-cbc, aes\-256\-cbc

* aes\-128\-ofb, aes\-192\-ofb, aes\-256\-ofb

* aes\-128\-gcm, aes\-192\-gcm, aes\-256\-gcm

* aes\-128\-ctr, aes\-192\-ctr, aes\-256\-ctr


**Grammar**

```SQL
decrypt('mode', 'ciphertext', 'key' [, iv, aad])
```


**Parameter**


* **`mode`**— Decryption mode. String.

* **`ciphertext`**— The ciphertext that needs to be decrypted. String.

* **`Key`**— Decryption Key. String.

* **`iv`**— Initialization Vector. It's necessary for `-gcm` Mode, but optional for other modes. String.

* **`aad`**— Additional Authentication Data. If this value is incorrect, decryption will not occur. Only valid in `-gcm` Mode, other modes will raise an exception. String.


**Return value**


* Decrypted string. String.


**Example**

Reuse the encryption table.

```SQL
SELECT comment, hex(secret) FROM encryption_test;
```


Result:

```Plain
┌─comment──────────────┬─hex(secret)──────────────────────────────────┐
│ aes-256-gcm          │ A8A3CCBC6426CFEEB60E4EAE03D3E94204C1B09E0254 │
│ aes-256-gcm with AAD │ A8A3CCBC6426D9A1017A0A932322F1852260A4AD6837 │
└──────────────────────┴──────────────────────────────────────────────┘
┌─comment──────────────────────────┬─hex(secret)──────────────────────┐
│ aes-256-ofb no IV                │ B4972BDC4459                     │
│ aes-256-ofb no IV, different key │ 2FF57C092DC9                     │
│ aes-256-ofb with IV              │ 5E6CB398F653                     │
│ aes-256-cbc no IV                │ 1BC0629A92450D9E73A00E7D02CF4142 │
└──────────────────────────────────┴──────────────────────────────────┘
```


Now, let’s try to decrypt all the data.

```SQL
-- Query
SELECT comment, decrypt('aes-256-cfb128', secret, '12345678910121314151617181920212') as plaintext FROM encryption_test
```


Result:

```Plain
┌─comment──────────────┬─plaintext──┐
│ aes-256-gcm          │ OQ�E
                             �t�7T�\���\�   │
│ aes-256-gcm with AAD │ OQ�E
                             �\��si����;�o�� │
└──────────────────────┴────────────┘
┌─comment──────────────────────────┬─plaintext─┐
│ aes-256-ofb no IV                │ Secret    │
│ aes-256-ofb no IV, different key │ �4�
                                        �         │
│ aes-256-ofb with IV              │ ���6�~        │
 │aes-256-cbc no IV                │ �2*4�h3c�4w��@
└──────────────────────────────────┴───────────┘
```


Please note that only a part of the data is correctly decrypted, while the rest remains garbled because the `mode`, `key`, or `iv` varied during encryption.

<span id="60427d2e"></span>
### tryDecrypt

Similar to `decrypt`, but returns NULL if decryption fails due to the use of an incorrect key.

**Example**

Let's create a table where `user_id` is the unique user ID, `encrypted` is the encrypted string field, and `iv` is the initial vector for decryption/encryption. Assume users know their ID and the key to decrypt the encrypted field:

```SQL
CREATE TABLE decrypt_null (
  dt DateTime,
  user_id UInt32,
  encrypted String,
  iv String
) ENGINE = Memory;
```


Insert some data:

```SQL
INSERT INTO decrypt_null VALUES
    ('2022-08-02 00:00:00', 1, encrypt('aes-256-gcm', 'value1', 'keykeykeykeykeykeykeykeykeykey01', 'iv1'), 'iv1'),
    ('2022-09-02 00:00:00', 2, encrypt('aes-256-gcm', 'value2', 'keykeykeykeykeykeykeykeykeykey02', 'iv2'), 'iv2'),
    ('2022-09-02 00:00:01', 3, encrypt('aes-256-gcm', 'value3', 'keykeykeykeykeykeykeykeykeykey03', 'iv3'), 'iv3');
```


Search

```SQL
SELECT
    dt,
    user_id,
    tryDecrypt('aes-256-gcm', encrypted, 'keykeykeykeykeykeykeykeykeykey02', iv) AS value
FROM decrypt_null
ORDER BY user_id ASC
```


Result:

```Plain
┌──────────────────dt─┬─user_id─┬─value──┐
│ 2022-08-02 00:00:00 │       1 │ ᴺᵁᴸᴸ   │
│ 2022-09-02 00:00:00 │       2 │ value2 │
│ 2022-09-02 00:00:01 │       3 │ ᴺᵁᴸᴸ   │
└─────────────────────┴─────────┴────────┘
```


<span id="5eb2c933"></span>
### aes_decrypt_mysql

Compatible with mysql encryption and decrypts data encrypted using the AES_ENCRYPT function.

`decrypt` will produce the same plaintext as the equal input. But when `Key` or `iv` is longer than normal, `aes_decrypt_mysql` will follow the practice of MySQL's `aes_decrypt`: "Fold" `key` and ignore the excess `IV` Digits.

Supported decryption modes:


* aes\-128\-ecb, aes\-192\-ecb, aes\-256\-ecb

* aes\-128\-cbc, aes\-192\-cbc, aes\-256\-cbc

* aes\-128\-cfb128

* aes\-128\-ofb, aes\-192\-ofb, aes\-256\-ofb


**Syntax**

```SQL
aes_decrypt_mysql('mode', 'ciphertext', 'key' [, iv])
```


**Parameter**


* `mode`— Decryption mode. String.

* `Ciphertext`— The ciphertext that needs to be decrypted. String.

* `Key`— The decryption key. String.

* `IV`— Initialization vector. Optional. String.


**Return value**


* The decrypted string. String.


**Example**

Before we decrypt the data encrypted with MySQL:

```SQL
mysql> SET  block_encryption_mode='aes-256-ofb';
Query OK, 0 rows affected (0.00 sec)

mysql> SELECT aes_encrypt('Secret', '123456789101213141516171819202122', 'iviviviviviviviv123456') as ciphertext;
+------------------------+
| ciphertext             |
+------------------------+
| 0x24E9E4966469         |
+------------------------+
1 row in set (0.00 sec)
```


Search

```SQL
SELECT aes_decrypt_mysql('aes-256-ofb', unhex('24E9E4966469'), '123456789101213141516171819202122', 'iviviviviviviviv123456') AS plaintext
```


As a result:

```Plain
┌─plaintext─┐
│ Secret    │
└───────────┘
```
