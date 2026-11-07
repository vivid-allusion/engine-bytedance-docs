---
title: "Database-native JWT generation and verification (pgjwt)"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/JWT"
---

<span id="JOK3mSdm"></span>
## Introduction

pgjwt is a PostgreSQL\-based JSON Web Token (JWT) extension that allows you to generate and verify JWTs directly within the database. This extension relies on the encryption functions provided by the pgcrypto extension and uses only the HMAC symmetric signing algorithms (e.g., HS256, HS384, and HS512). The entire process requires no external services, achieving secure and efficient authentication token management.

<span id="irpylRkh"></span>
## Applicable scenarios


* **Serverless architecture:**  perform user authentication directly through the database in environments like function computing, simplifying the authentication process.

* **API gateway integration:**  combine with tools like PostgREST to handle request authentication at the database level, protecting API endpoint security.

* **Application logic simplification:**  move JWT generation and verification into the database to reduce code complexity and dependencies at the application layer.


<span id="fNkKXTgm"></span>
## Prerequisites

Before using the pgjwt extension, ensure that the pgcrypto extension is installed and enabled in your database instance.

```SQL
-- check if pgcrypto extension is installed
SELECT * FROM pg_extension WHERE extname = 'pgcrypto';

-- if not installed, execute the following command to create
CREATE EXTENSION IF NOT EXISTS pgcrypto;
```


<span id="uHxCL3P0"></span>
## Create and delete extension

<span id="MhxiXkZM"></span>
### Create extension

Execute the following SQL command to enable the pgjwt extension. If pgcrypto is not yet enabled, using `CASCADE` automatically handles dependencies.

```SQL
CREATE EXTENSION pgjwt;  -- or use CASCADE: CREATE EXTENSION pgjwt cascade;
```


<span id="1ZFcdxWY"></span>
### Delete extension

If no longer needed, execute the following command to uninstall it.

```SQL
DROP EXTENSION pgjwt;
```


<span id="WxH9vHQ1"></span>
## Basic usage

<span id="bS7fzZrh"></span>
### Generate JWT (`sign` function)

The `sign` function generates a JWT. It accepts three parameters:


* `payload` (json): required, a valid JSON object containing claims to encode.

* `secret` (text): required, the key used for signing.

* `algorithm` (text): optional, signing algorithm, supports `HS256` (default), `HS384`, `HS512`.


**Example: generate a token using the default algorithm (HS256)** 

```SQL
SELECT sign(
    '{"sub":"1234567890","name":"John Doe","admin":true}',
    'your-super-secret-key'
);
```


**Response results:** 

```Plain Text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```


**Example: generate a token using the HS384 algorithm**

```SQL
SELECT sign(
    '{"sub":"1234567890","name":"John Doe","admin":true}',
    'your-super-secret-key',
    'HS384'
);
```


<span id="8jD0ftlt"></span>
### Verify JWT (`verify` function)

`verify` function validates JWT and parses its content. It accepts three parameters:


* `token` (text): required, the JWT string to be verified.

* `secret` (text): required, the key used to verify the signature.

* `algorithm` (text): optional, the signature algorithm, must be consistent with the one used when creating the token.


The function returns a record containing three fields, namely, `header` (json), `payload` (json), and `valid` (boolean).

**Example: verifying a valid token**

```SQL
SELECT * FROM verify(
    'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ',
    'your-super-secret-key'
);
```


**Response results:** 


|header |payload |valid |
|---|---|---|
|{"alg":"HS256","typ":"JWT"} |{"sub":"1234567890","name":"John Doe","admin":true} |true |


**Example: verifying a token with an incorrect key**

If the key does not match, the `valid` field will return `false`.

```SQL
SELECT * FROM verify(
    'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ',
    'wrong-secret'
);
```


**Response results:**  the `valid` field will be `false`.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">In practical use, the <code>secret</code> should be sufficiently complex and managed securely. For example, using environment variables or dedicated key management services to avoid hardcoding it in code or the database.</div>
