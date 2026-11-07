---
title: "Data encryption"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/data-encryption"
---

ByteHouse cloud data warehouse edition supports transparent data encryption, allowing encryption of entire tables or specific columns. This enhances core data security and meets your regulatory and compliance requirements. This tutorial introduces ByteHouse’s encryption mechanism and how to use data encryption in ByteHouse.

<span id="501c8a1c"></span>
# Usage restrictions


* This function is in Beta. To use it, submit a ticket or contact the ByteHouse team to obtain whitelist access.

* Only the main account or the sub\-account with the SystemAdmin or AccountAdmin role and the privilege to access the ByteHouse console can activate the ByteHouse data encryption feature.


<span id="1368a0db"></span>
# Cautions


* After activating ByteHouse data encryption, table performance may decrease by more than 10% due to encryption and decryption operations during data processing.

* Once enabled, ByteHouse data encryption cannot be disabled. Proceed with caution. If you no longer want to encrypt a table or column, refer to [Modify encrypted tables and columns](https://docs.byteplus.com/docs/bytehouse/data-encryption#cc4d18e1) to adjust the table/column settings without disabling the ByteHouse data encryption feature.

* After activating ByteHouse data encryption, the BytePlus key management service (KMS), which the ByteHouse encryption feature depends on, will start charging. Do not disable the BytePlus KMS service, incur arrears, or delete ByteHouse\-related keys, as this will cause data read and write errors. If you plan to stop using this service, first contact the ByteHouse team to avoid issues where encrypted data becomes inaccessible.

* Please ensure that the BytePlus key management service you use is in the same region as the ByteHouse cloud data warehouse service.


<span id="27ca1197"></span>
# Feature overview

ByteHouse relies on [BytePlus Key Management Service KMS](https://docs.byteplus.com/en/docs/kms/What_is_Key_Management_Service) and integrates ClickHouse community’s table\-level and column\-level encryption mechanisms to achieve transparent encrypted storage, protecting underlying static data. Database transparent encryption means encrypting data when writing to ByteHouse and automatically decrypting data when querying to return results. When using KMS for ByteHouse key management, the key hierarchy includes customer master keys (CMK) and data encryption keys (DEK). The complete encryption and decryption process is as follows:


1. Users create a master key in the KMS service and use CMK to generate data keys (DEK plaintext and ciphertext).

2. The DEK plaintext key encrypts plaintext data to generate ciphertext data; the ciphertext data key and the encrypted data are persistently saved.

3. When reading data, if the system detects that the data is encrypted, it requests the plaintext data key from the CMK based on the encrypted data key within the data block, then decrypts the data ciphertext and returns the decrypted data to the user. The decryption process requires no user intervention and completes automatically by the system.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ed3c76298a9426189796244df988e00~tplv-goo7wpa0wc-image.image) </span>


The specific data encryption mechanism is as follows:


* ByteHouse adopts transparent encryption, supporting AES\-128\-GCM\-SIV and AES\-256\-GCM\-SIV encryption algorithms.

* To use it, first activate the BytePlus KMS service and ByteHouse data encryption function, then enable encryption and configure encryption parameters for tables/columns via SQL commands (DDL). After configuration, data encrypts automatically on write and decrypts automatically on query, with no need to manually handle keys or encryption logic in subsequent operations, ensuring normal data read and write habits remain unaffected.

* BytePlus KMS service supports KMS\-derived keys and Bring Your Own Key (BYOK). You can create keys through BytePlus KMS and enable KMS services in ByteHouse for data encryption. Before using data encryption features, ensure the KMS service is activated in your region. For instructions, refer to [Key Management Quick Start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).

* ByteHouse encrypts or decrypts stored data at the table and column units using KMS.

* After creating a user keyring (CustomKeyring) on BytePlus KMS, the KMS managed service will be used. Meanwhile, during data read/write operations, ByteHouse calls KMS APIs to obtain related key information, which incurs KMS\-related fees when using data encryption features. For KMS pricing details, refer to [KMS Pricing Description](https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing). If the key ring type you create in BytePlus KMS is a cloud service managed key ring (ManagedKeyring), BytePlus will only charge for API calls. Related management fees will be borne by the cloud service that created the key. Actual billing depends on the billing rules of the service you use.


<span id="19cc4e57"></span>
# Enable ByteHouse data encryption


1. Activate the ByteHouse data encryption service which depends on the BytePlus KMS service.

   Log in to the ByteHouse cloud data warehouse console. On the **Tenant management** \> **Data encryption** page, click **Activate KMS** in Step 1. The system will jump to the BytePlus KMS service activation page. You can refer to [Quick Start for Key Management](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management) to activate and configure BytePlus KMS service. When activating, ensure that the KMS service you use is in the same region as ByteHouse.

   After activation, return to the ByteHouse cloud data warehouse console and check if the KMS service in the process guide shows **Opened**.

2. Click **Activate** in Step 2 to activate the ByteHouse data encryption function. Carefully read the prompt and then click **Confirm**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After data encryption is turned on, the table performance will be reduced by 10% or more. It cannot be turned off after it is turned on. Please operate with caution.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After data encryption is turned on, it cannot be turned off! Forcibly turning off the KMS service after turning it on will cause data reading and writing to fail!   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data encryption is not charged, only the KMS service fee (billed by volume) is charged, and the billing rules are detailed in the help document.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data encryption can be turned on through SQL; after encryption is turned on for tables with historical data, only new data is encrypted.   </div>
   

3. When the page shows “**Activated data encryption successfully**”, it means the function is successfully activated, as shown below.

   Please use SQL to create, modify, and delete data encryption tables/columns. For more information, please refer to the help documentation.


<span id="29314790"></span>
# Use data encryption

ByteHouse supports enabling table/column encryption through SQL commands. You can create encrypted tables/columns or convert existing non\-encrypted tables/columns into encrypted ones via commands. For tables with historical data, enabling encryption only encrypts newly written data.

<span id="2f658704"></span>
## Create encrypted tables/columns

When creating tables, you can use the following parameters to set encryption for the entire table or columns:


* Encrypt a table: Set the setting parameter `encrypt_table` to 1, which enables table encryption, i.e., `SETTINGS encrypt_table=1`.

* Encrypt columns: You can use AES_128_GCM_SIV or AES_256_GCM_SIV algorithms to encrypt columns. For example, setting the parameter `Codec(LZ4, AES_256_GCM_SIV)` for a column indicates that the Codec uses a compression algorithm (LZ4) combined with an encryption algorithm (AES_256_GCM_SIV).


<span id="c4e60ebd"></span>
### Example 1: Create an encrypted table

After executing this command, the target table will have full table encryption enabled, and subsequently inserted data will be encrypted automatically. Replace the table name with your actual table name when using.

```SQL
CREATE TABLE test.new_encrypted_table
(
    `A` Int64
)
ENGINE = CnchMergeTree()
ORDER BY A
SETTINGS encrypt_table=1 
```


<span id="58d2147a"></span>
### Example 2: Create an encrypted column

After running this command, the system encrypts the target column, and all subsequent data written to that column will be automatically encrypted. Replace the table name and column name with your actual table and column names when using.

```SQL
CREATE TABLE test.new_encrypted_column_table
(
    `A` Int64 Codec(LZ4, AES_256_GCM_SIV)
)
ENGINE = CnchMergeTree()
ORDER BY A 
```


<span id="cc4d18e1"></span>
## Modify encrypted tables and columns

For existing data tables, you can use `Alter table... MODIFY...` to set data encryption:


* Encrypt a table: Set the parameter `encrypt_table` to 1, which activates table encryption, i.e., `SETTINGS encrypt_table=1`. Setting it to 0 disables encryption.

* Encrypt a column: You can use AES_128_GCM_SIV or AES_256_GCM_SIV algorithms to encrypt a column. For example, set the `Codec(LZ4, AES_256_GCM_SIV)` parameter in the corresponding column, indicating that the Codec parameter consists of a compression algorithm (LZ4) and an encryption algorithm (AES_256_GCM_SIV).


<span id="810c829f"></span>
### Example 1: Change an unencrypted table to an encrypted table

After running this command, the table will activate full\-table encryption. Newly written data will be encrypted automatically, but historical data will not be encrypted. Replace the table name with your actual table name when using this command.

```SQL
ALTER TABLE test.new_encrypted_table 
MODIFY SETTING encrypt_table=1;
```


<span id="6f1d1ca0"></span>
### Example 2: Change an unencrypted column to an encrypted column

After running this command, the system will encrypt the target column. Newly written data will be encrypted automatically, but historical data will not be encrypted. Replace the table name and column name with your actual table and column names when using this command.

```SQL
ALTER TABLE test.new_encrypted_column_table
MODIFY COLUMN A Codec(LZ4, AES_256_GCM_SIV)
```


<span id="2f109f67"></span>
### Example 3: Change an encrypted table to an unencrypted table

After running this command, the column will disable encryption. Newly written data will no longer be encrypted, but existing encrypted data will remain encrypted. Replace the table name and column name with your actual table and column names when using this command.

```SQL
ALTER TABLE test.new_encrypted_table
MODIFY SETTING encrypt_table=0;
```


<span id="875eda94"></span>
### Example 4: Change encrypted column to non\-encrypted column

After running this command, the column is decrypted; new data written will no longer be encrypted, while previously encrypted historical data remains encrypted. Please replace the table name and column name with your actual table and column names when using this.

```SQL
ALTER TABLE test.new_encrypted_column_table
MODIFY COLUMN A Int64 REMOVE CODEC
```
