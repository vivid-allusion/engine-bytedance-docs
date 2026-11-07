---
title: "BytePlus KMS Pricing"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing"
---

The KMS service provides a set of standard capabilities to generate and manage your keys and secrets. It supports the pay\-as\-you\-go billing model, which allows you to pay based on your usage.

<span id="billing-model"></span>
### Billing Model

The KMS service supports the pay\-as\-you\-go billing model. You are charged based on your KMS resource usage. Fees are deducted from the balance of your BytePlus account after bills are generated at the end of each service cycle.

<span id="pricing-details"></span>
### Pricing Details

<span id="key-manager"></span>
#### Key Manager

Key Manager includes two billing items: key management fee and API usage fee.


1. Key management fee: Each key you create is charged at a price of 0.033 USD per day.



|**Item** |**Pricing(USD)**  |**Unit** |**Note** |
|---|---|---|---|
|Key management fee |$ 0.033 |Per Day |1. All types of keys are at the same price (symmetric/asymmetric/HMAC keys, software protection keys, hardware protection keys, externally imported keys)<br><br>2. If the storage time is less than one day, it will be calculated as one day. |



2. API usage fee: The cost of each API request sent to KMS (Open API requests and console requests are included).



|**Item** |**Pricing(USD)**  |**Unit** |**Note** |
|---|---|---|---|
|Normal key API call count |$ 0.03 |Per 10,000 API calls |All API calls using keys of two specifications, SYMMETRIC_256 (AES_256) and RSA_2048.<br><br>Other types of key API calls for management. |
|Asymmetric key API call count |$ 0.15 |Per 10,000 API calls |The following API calls belong to the key specifications of asymmetric requests (RSA_3072, RSA_4098, EC_P256K, EC_P256, EC_P384, EC_P521):<br><br><br>5. GetPublicKey<br><br>6. CreateKey<br><br>7. AsymmetricDecrypt<br><br>8. AsymmetricEncrypt<br><br>9. AsymmetricSign<br><br>10. AsymmetricVerify |


<span id="secret-manager"></span>
#### Secret Manager

Secret Manager includes two billing items: secret management fee and API usage fee.


1. Secret management fee: Each secret you create is charged at a price of 0.0133 USD/day.



|**Item** |**Pricing(USD)**  |**Unit** |**Note** |
|---|---|---|---|
|Secret management fee |$ 0.0133 |Per Day |1. All types of Secrets are priced at this price<br><br>2. If the storage time is less than one day, it will be calculated as one day |



2. API usage fee: The cost of each API request sent to KMS.



|**Item** |**Pricing(USD)**  |**Unit** |**Note** |
|---|---|---|---|
|API call count |$ 0.04 |Per 10,000 API calls |Open API requests and console requests are both included in the statistics. |


<span id="pricing-example"></span>
### Pricing Example

**Encryption and decryption program example**

1 AES_256 key (created on Dec 1, 2024, still in use on Dec 31, 2024), generated 100,000 data keys through KMS OpenAPI operations.

**Cost items:** 


* 1 key

* 100,000 GenerateDataKey API calls


**Total cost：** 

Key management fee = 1 \* 31 \* 0.33 = 1.023 USD

API usage fee = 10 \* 0.03 = 0.3 USD

Total cost = 1.023 + 0.3 = 1.323 USD

&nbsp;

**Signature Program Example**

1 RSA_3072 key (created on Dec 1, 2024, still in use on Dec 31, 2024), signed 10,000 binary files through KMS OpenAPI operation.

**Cost items:** 


* 1 Key

* 10,000 Sign API calls


**Total cost：** 

Key management fee = 1 \* 31 \* 0.33 = 1.023 USD

API usage fee = 1 \* 0.15 = 0.15 USD

Total cost = 1.023 + 0.15 = 1.173 USD

&nbsp;

**ECS** **Secret management Example**

100 ECS instances' SSH keys are hosted by Secret Manager (Started creating in secret manager on Dec 15, 2024, still in use as of Dec 31, 2024.). These 100 SSH keys in the program connect to the instances once a day.

**Cost items:** 


* 100 Secrets

* 10,000 GetSecretValue API calls


**月度成本：** 

Secret management fee = 100 \* 17 \* 0.133 = 226.1 USD

API usage fee = 1 \* 100 \* 17 \* 0.04 = 68 USD

Total cost = 226.1 + 68 = 294.1 USD
