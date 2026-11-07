---
title: "Data encryption"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Data_encryption"
---

TLS supports encrypted data storage and uses Key Management Service (KMS) from BytePlus to encrypt log topic\-level data. This topic describes the steps to encrypt TLS data using customer\-managed keys (SSE\-KMS).

<span id="91e0b039"></span>
## Data encryption overview


|Encryption method |Description |
|---|---|
|Service Key (SSE\-TLS) |It is the default encryption method provided by TLS. It requires no additional configuration from users, enabling seamless encryption during usage. |
|Customer Key (SSE\-KMS) |It can generate, manage, and protect encryption keys via [Key management service (KMS)](https://docs.byteplus.com/en/docs/kms/What_is_Key_Management_Service) from BytePlus **;**  offers secure key storage, key generation, encryption operations, and key rotation. Features include:<br><br><br>* Full lifecycle control:<br><br>   Users have complete control over keys, independently managing their entire lifecycle—from creation and periodic rotation to final deletion; users will no longer need to rely on third\-party. This ensures autonomy and security in key management.<br><br>* Proactive management attribute:<br><br>   It requires active user involvement in key management, such as creating master keys in the KMS console and precisely configuring usage permissions (e.g., authorizing specific roles or restricting operational scope) to ensure compliant and controlled key usage. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Notice</div>



* <div data-tips="true" data-tips-type="default">User keys (SSE\-KMS) are used to generate and protect data encryption keys, but do not directly encrypt log content.</div>


* <div data-tips="true" data-tips-type="default">Log content is encrypted using the default TLS data encryption algorithm (envelope encryption, fixed 32\-byte encryption key). Changing the data key length or encryption algorithm is not supported.</div>



<span id="57be0bbb"></span>
## Limits

The following limitations apply when using customer\-managed keys (SSE\-KMS):


|Category |Supported operations |Unsupported operations |
|---|---|---|
|Region |The primary key and TLS must be in the same region. |Do not support that the primary key and TLS are in different regions. |
|IAM permissions |You must grant the user role permission for KMS encryption and decryption operations, KMS read\-only access, and configure TLS trust relationships. |Encryption and decryption requests will fail due to insufficient permissions, invalid trust relationship, or deleted role. |
|Types of key |KMS symmetric primary key is required.<br><br>The specification must be `SYMMETRIC_256`. |Asymmetric keys such as `RSA_2048` or `EC_SM2`are not supported. |
|Key status |The status of the key must be enable. |Keys in the following states are not supported to bind:<br><br>Disabled, Archived, Pending Delete, or Pending Import. |
|Binding method |The key must be bound using user_cmk_id (Customer Master Key ID). |Binding a key by Keyring name or Keyring ID is not supported. |
|Modify encryption |Only enabling or disabling data encryption is supported. |* Modifying the encryption method is not supported. This means switching between service keys (SSE\-TLS) and customer keys (SSE\-KMS) is not supported.<br><br>* Modifying the encryption algorithm or bound user key information is not supported.<br><br>   If performing key rotation within KMS, ensure that the primary key ID remains unchanged.<br><br>   TLS does not support switching to a new primary key ID via `ModifyTopic`. |
|Delete/disable key |After the primary key is deleted or disabled, the CMK becomes invalid, and all read and write requests for the corresponding log topic will fail. |\- |
|Non\-KMS key |When using external keys such as BYOK or CustomKeyring, you must complete CustomKeyring creation, key import, and activation in KMS in advance, and obtain the key ID. |TLS does not provide the capability to import key material, create Keyrings, or manage Keyrings. |


<span id="9dfbdb64"></span>
## Billing notes


|Encryption method |Description |
|---|---|
|Service Key (SSE\-TLS) |No billing item is generated. |
|Customer Key (SSE\-KMS) |First\-time users need to activate the KMS service. Although activating KMS is free, using the service incurs fees.<br><br>Using KMS for server\-side encryption will incur API call fees. Creating KMS keys will incur key hosting fees, which are charged by KMS. For details, see [KMS billing description](https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing). |


<span id="353927a0"></span>
## Use cases


|Encryption method |Use cases |
|---|---|
|Service Key (SSE\-TLS) |* Quickly deploy data encryption.<br><br>* No need to manage keys (managed by the service provider), suitable for scenarios requiring long\-term key stability. |
|Customer Key (SSE\-KMS) |* Suitable for scenarios requiring self\-managed keys to meet security and compliance requirements.<br><br>* Suitable for scenarios requiring regular permission audits to reduce key leakage risks. |


<span id="d997fcf9"></span>
## Encryption configuration steps

When using TLS service\-managed keys (SSE\-TLS) for encryption, you can simply add the `EncryptConf` structure parameter to your API request to complete the encryption setup.

When using customer\-managed keys (SSE\-KMS) for encryption, you can follow these steps to configure the Key Management System.

<span id="d6e256df"></span>
### 1 Configure the key management system


1. Enable Key Management System (KMS) in the same region as TLS.

2. Create a customer master key and obtain the key ID. For details, refer to [Key Management Quick Start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management) and [Bring Your Own Key](https://docs.byteplus.com/en/docs/kms/Bring_your_own_key).


<span id="8deaf5f0"></span>
### 2 Configure TLS

Configure TLS cross\-service access to KMS. For details, see [Cross-service access authorization](https://docs.byteplus.com/docs/tls/Authorizing_cross-service_access).

<span id="8c71f931"></span>
### 3 Configure the permission policy

Grant user roles KMS encryption/decryption permissions and KMS read\-only permissions, configure TLS trust relationships, and record the role TRN.


1. Log in to the [IAM console](https://console.byteplus.com/iam/).

2. In the left navigation bar, click **Role Management**.

3. Locate the role to be authorized, and in the **Actions** column, click **Authorize**.

4. Under **Service**, search for **Key Management Service** and click the `KMSCryptoUserAccess` and `KMSReadOnlyAccess` policies. And then click **Submit**.

5. Click the name of the role to be authorized. Then go to the **Trust relationships** tab and click **Edit trust policy**. Add the following content, and click **Save**.

   ```YAML
   {
       "Statement": [
           {
               "Effect": "Allow",
               "Action": [
                   "sts:AssumeRole"
               ],
               "Principal": {
                   "Service": [
                       "TLS"
                   ]
               }
           }
       ]
   }
   ```
   

6. Under **Basic information**, record the role TRN.


<span id="1720421d"></span>
### 4 Configure data encryption

Only supported via API calls. When calling the API, add the `EncryptConf` structure parameter to the request to complete encryption settings. Supported API:


|API |API Description |
|---|---|
|CreateTopic |Create a TLS topic. For details, refer to [CreateTopic](https://docs.byteplus.com/en/docs/tls/api-createtopic). |
|ModifyTopic |Modify the log topic information. For details, refer to [ModifyTopic](https://docs.byteplus.com/en/docs/tls/api-modifytopic).<br><br><br>* If `EncryptConf` is not included: The encryption settings for this log topic remain unchanged, and the server continues to process other modifiable parameters in the request.<br><br>* If `EncryptConf` is included:<br><br>   * `enable`: (Optional) This parameter can be modified. You should explicitly enter the corresponding Boolean value; otherwise, it will default to `false`, disabling data encryption.<br><br>   * `encrypt_type`:  (Optional) This parameter can not be modified. If provided, it must match the original configuration; otherwise, the request will fail.<br><br>   * `user_cmk_info`:  (Optional) This parameter can not be modified. If provided, it must match the original configuration; otherwise, the request will fail. |


<span id="6fe3063b"></span>
### Request parameter description


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|EncryptConf |Object of EncryptConf |NOT |[API request example](https://docs.byteplus.com/en/docs/tls/Data_encryption#bbcc138d) |Data encryption structure.<br><br>When not configured, the data encryption feature is disabled. |


EncryptConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|enable |Boolean |NOT |true |Enable data encryption.<br><br><br>* true: Yes.<br><br>* false: No. |
|encrypt_type |String |NOT |default |Encryption algorithm. Only `default` is supported. |
|user_cmk_info |Object of EncryptUserCmkConf<br><br> |NOT |/ |Configure key information. Takes effect when `enable` is `true`.<br><br><br>* Not configured: Uses service key (SSE\-TLS) encryption.<br><br>* Configure user key: uses user key (SSE\-KMS) encryption. |


EncryptUserCmkConf


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|trn |string |NOT |trn:iam::123456789:role/service_role_for_tls |The TRN of the user IAM role.<br><br>Log in to [the IAM console](https://console.byteplus.com/iam/). Click the role name under the **Role Management** tab and obtain the **Role TRN** in the **Basic Information** section. |
|region_id |string |NOT |ap\-southeast\-1 |Region ID where the user master key is located. |
|user_cmk_id |string |NOT |fc227edb\-3682\-4577\-a3b5xxxxxxxxx |User main key ID.<br><br>The **Key ID** of the key created through Key Management Service (KMS). |


<span id="bbcc138d"></span>
### API request example

Using user\-managed keys (SSE\-KMS) encryption as an example.

```JSON
EncryptConf = {
    "enable" : true,            
    "encrypt_type" : "default"  
    "user_cmk_info" :           
    {
          "trn" :  "trn:iam::123456789:role/service_role_for_tls"         
          "region_id" : "ap-southeast-1"      
          "user_cmk_id" : "fc227edb-3682-4577-a3b5xxxxxxxxx"     
    }
}
```
