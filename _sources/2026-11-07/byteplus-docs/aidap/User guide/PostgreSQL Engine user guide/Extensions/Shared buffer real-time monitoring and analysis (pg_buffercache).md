---
title: "Shared buffer real-time monitoring and analysis (pg_buffercache)"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-pg_buffercache"
---

<span id="kTGI7HCM"></span>
## Introduction

supabase_vault is a PostgreSQL extension designed to securely store and manage sensitive strings (such as API keys and access tokens) within the database.

The extension achieves this by persisting encrypted ciphertext into the `vault.secrets` table and decrypting it on demand during queries through the `vault.decrypted_secrets` view to return plaintext, enabling:


* **Static data encryption**: only ciphertext is stored in disk files, backups, and replication streams;

* **Controlled runtime access**: plaintext is dynamically decrypted and returned only in authorized queries;

* **Minimal exposure surface**: business users can securely use sensitive information without directly handling encryption implementation details.


<span id="zNrYtpnY"></span>
## Prerequisites

Before using the supabase_vault extension, it must be added to the PostgreSQL configuration parameter `shared_preload_libraries`. After updating this parameter, the PostgreSQL instance must be restarted for the configuration to take effect.

<span id="zkiUvmRl"></span>
## Create and delete extension

<span id="qtyKqnBS"></span>
### Create extension

```SQL
CREATE EXTENSION supabase_vault;
```


<span id="yWhHldII"></span>
### Delete extension

```SQL
DROP EXTENSION supabase_vault;
```


<span id="VgVkkMww"></span>
## Basic usage

<span id="Cna1JMXf"></span>
### **Create secret**

Create a new key using the `vault.create_secret()` function. This function writes the ciphertext into the `vault.secrets` table and returns the universally unique identifier (UUID) of the newly created key.

```SQL
SELECT vault.create_secret('secret');
            create_secret
--------------------------------------
 0957e0d7-081e-400e-833f-922526e14df2
(1 row)
```


Optionally attach a unique name and description when creating, to facilitate subsequent identification and management.

```SQL
SELECT vault.create_secret(
    'sk_live_abcdefghijklmnopqrstuvwxyz', 
    'stripe_production_key', 
    '用于生产环境的 Stripe API Key'
);

            create_secret
--------------------------------------
 5ced3759-473d-48e0-b109-4f1d13124dd3
(1 row)
```


Among them:


* The first parameter is the actual sensitive string to be saved;

* The second parameter is the unique name of the key (`name`);

* The third parameter is the description for easier understanding (`description`).


<span id="M1TwIWNH"></span>
### Query secret

When decrypting an access key, query through the `vault.decrypted_secrets` view. This view decrypts the ciphertext instantly during the query phase and returns the plaintext in the `decrypted_secret` column.

```SQL
-- Query a specific secret by name
SELECT id, name, decrypted_secret,created_at FROM vault.decrypted_secrets WHERE name = 'stripe_production_key';

                  id                  |         name          |          decrypted_secret          |          created_at
--------------------------------------+-----------------------+------------------------------------+-------------------------------
 5ced3759-473d-48e0-b109-4f1d13124dd3 | stripe_production_key | sk_live_abcdefghijklmnopqrstuvwxyz | 2025-12-24 01:12:40.382076+08
(1 row)
```


In the above query:


* The `decrypted_secret` column returns the plaintext key;

* The `secret` column in the `vault.secrets` table is always stored as ciphertext and is not directly exposed in the view.


It is recommended to strictly control access permissions to `vault.decrypted_secrets` at the application layer, granting only roles or service accounts that truly need to read plaintext keys.

<span id="Zere5inb"></span>
### Update secret

Use `vault.update_secret(secret_id, new_secret, new_name, new_description)` to update an existing secret.

```SQL
SELECT vault.update_secret(
    '5ced3759-473d-48e0-b109-4f1d13124dd3',
    new_secret := 'sk_live_new_updated_secret_key',
    new_name := 'stripe_prod_key_rotated',
    new_description := '已轮替的 Stripe 生产环境 API Key'
);
```


Parameter description:


* `secret_id`: UUID of the secret to update;

* `new_secret`: new secret value;

* `new_name`: new name;

* `new_description`: new description.


Except for `secret_id`, other parameters are optional and will update the corresponding fields only if provided. Fields not explicitly passed will remain unchanged.

After updating, verify the change by querying the `vault.decrypted_secrets` view.

```SQL
SELECT name, description, decrypted_secret 
FROM vault.decrypted_secrets 
WHERE id = '5ced3759-473d-48e0-b109-4f1d13124dd3';
          name           |           description            |        decrypted_secret
-------------------------+----------------------------------+--------------------------------
 stripe_prod_key_rotated | 已轮替的 Stripe 生产环境 API Key | sk_live_new_updated_secret_key
(1 row)
```


<span id="szJka1jh"></span>
### Delete secret

supabase_vault does not provide a dedicated delete function. To delete unused keys, perform the standard `DELETE` operation on the `vault.secrets` table.

```SQL
DELETE FROM vault.secrets WHERE id = '5ced3759-473d-48e0-b109-4f1d13124dd3';
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">Delete operations are <strong>irreversible</strong>. Once removed from the vault.secrets table, the corresponding encrypted information is permanently lost and cannot be recovered.</div>


* <div data-tips="true" data-tips-type="warning">Confirm that the key is no longer referenced by any application, service, or scheduled task before deletion to avoid causing production issues;</div>


* <div data-tips="true" data-tips-type="warning">It is recommended to combine audit records or change management processes for necessary approval and traceability of key deletion operations.</div>
