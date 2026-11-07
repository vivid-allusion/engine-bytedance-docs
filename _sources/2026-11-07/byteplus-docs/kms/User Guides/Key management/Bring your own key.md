---
title: "Bring your own key"
product: "BytePlus Key Management Service"
product_code: "kms"
source: "https://docs.byteplus.com/en/docs/kms/Bring_your_own_key"
---

BytePlus Key Management Service (KMS) supports the bring your own key (BYOK) feature, allowing you to import your own key material into a customer master key (CMK) for hosting.

&nbsp;

<span id="supported-key-types"></span>
## Supported key types


|**Key type** |**Key specification** |**Key usage** |**Protection level** |**Key length** |
|---|---|---|---|---|
|Symmetric key |SYMMETRIC_256 |ENCRYPT_DECRYPT |SOFTWARE |256 |
|Asymmetric key |RSA_2048 |ENCRYPT_DECRYPT and SIGN_VERIFY |SOFTWARE |2048 |
||RSA_3072 |ENCRYPT_DECRYPT and SIGN_VERIFY |SOFTWARE |3072 |
||RSA_4096 |ENCRYPT_DECRYPT and SIGN_VERIFY |SOFTWARE |4098 |
||EC_P256 |SIGN_VERIFY |SOFTWARE |256 |
||EC_P384 |SIGN_VERIFY |SOFTWARE |384 |
||EC_P521 |SIGN_VERIFY |SOFTWARE |521 |


&nbsp;

<span id="step-1-create-a-customer-master-key"></span>
## Step 1: Create a customer master key

Call the [CreateKey](../6476/1337064) API to create a customer master key (CMK) for hosting. During the creation, you must set the key origin to **External**, so that KMS creates a CMK but does not generate key material for the CMK. The initial state of a CMK with the key origin set to **External** is PendingImport. You can import your own key material into the CMK. After the import is complete, the state of the CMK changes to Enable.

&nbsp;

**Note**

When you import external key material, note the following:


* Use a random source that meets the requirements to generate key material.

* Each CMK can have only one imported key material. After you import the key material for the first time, the CMK will be associated with the key material. No more key material can be imported, even if the imported key material expires or is deleted.

* CMKs are independent of each other. Data encrypted with a CMK cannot be decrypted by other CMKs, even if they use the same key material as the CMK.

* When importing key material, you can set the expiration time of the key material. The key material will be automatically deleted after expiration, or you can manually delete it when you no longer need it. When the key material expires or is deleted, the CMK is not deleted.

* After the key material expires or is deleted, you can import the same key material again. Copies of the key material can only be manually stored.

* A CMK with external key material cannot be automatically rotated. If you need to use new key material, you can only create a CMK and then import the new key material.


&nbsp;

<span id="step-2-import-key-material"></span>
## Step 2: Import key material

<span id="obtaining-import-parameters"></span>
### Obtaining import parameters

Parameters used for importing key material include a public key for encrypting the key material and an import token. In this topic, a public key of the RSA_2048 type and the encryption algorithm RSAES_OAEP_SHA_256 are used as examples.


1. Find the specified CMK and click **Get import parameters** in the **Actions** column.

2. In the **Get import parameters** dialog box, select values from the **Public key type** and **Encryption algorithm** drop\-down lists, and click **Obtain**.

3. Download the public key and the import token.


When downloading the public key, you can select a format for the public key:


* PEM format: suffixed by .pem, such as publickey_7a20e103\-0871\-437a\-a120\-985102c9c57b.pem

* DER format: suffixed by .der, such as publickey_7a20e103\-0871\-437a\-a120\-985102c9c57b.der


&nbsp;

**Note**


* Public keys of the RSA_2048 type support RSAES_OAEP_SHA_256 and RSAES_OAEP_SHA_1 encryption algorithms.

* Public keys of the EC_SM2 type support SM2PKE encryption algorithms.

* The public key and import token in the import parameters must be used in pairs.

* The import parameters obtained from a CMK cannot be used to import key material of other CMKs.

* The import token is valid for 24 hours and can be reused within the validity period. After expiration, you need to obtain new import parameters.


&nbsp;

<span id="encrypting-the-key-material"></span>
### Encrypting the key material

After downloading the public key and the import token, you can encrypt your key material by using the public key and the encryption algorithm you selected when obtaining the import parameters. In the following example, the key material is encrypted using OpenSSL. Run the following command in OpenSSL 3.0 or later.


1. Create key material for a SYMMETRIC\_256 key.


```bash
openssl rand -out KeyMaterial.bin 32
```



2. Encrypt the key material by using the RSAES_OAEP_SHA_256 algorithm:


```bash
openssl pkeyutl \
    -in KeyMaterial.bin \
    -out EncryptedKeyMaterial.bin \
    -inkey PublicKey.der \
    -keyform DER -pubin \
    -encrypt \
    -pkeyopt rsa_padding_mode:oaep \
    -pkeyopt rsa_oaep_md:sha256
```



* Replace PublicKey.der with the public key that you downloaded when obtaining the import parameters.

* In the example, the public key is in the DER format. If you have downloaded the public key in the PEM format, replace "\-keyform DER" with "\-keyform PEM".



&nbsp;

3. If the key material is in the Binary format, you can directly upload EncryptedKeyMaterial.bin. If the key material is in the Base64 format, you need to encode the key material in Base64.


```bash
openssl enc -e -base64 -A -in EncryptedKeyMaterial.bin -out EncryptedKeyMaterial_base64.txt
```


&nbsp;

<span id="importing-the-key-material"></span>
### Importing the key material

Import the key material file generated after the encrypted key material is uploaded, and import the import token file obtained when you obtained import parameters:


1. Find the specified CMK and click **Import key material** in the **Actions** column.

2. In the **Import key material** dialog box, upload the files in the **Key material** and **Import token** panes, set **Key expiration time**, and click **Import**.


&nbsp;

**Note**

When you import the private key of an asymmetric key into KMS, make sure that the private key is DER\-encoded in the PKCS #8 ASN.1 format.

Note: During functional verification, you can use the [ASN.1 JavaScript decoder](https://lapo.it/asn1js/#) to check the key format. We do not recommend that you use your own private key directly on BytePlus sites without a full understanding of the relevant features.

Example of RSA 2048 PKCS#8 ASN.1 DER private key in Base64:

```bash
MIIEvQIBADANBgkqhkiG9w0BAQEFAASCBKcwggSjAgEAAoIBAQDTmr8aEJbDU4KAQEFt6gSKFIBvKZfUM0WnwPB/zKB3PDuLc4+se776zs5sB4lggKT7JHFuLHPodTJrVT9iA8cxfXznrXCk0Ti1d01gqf6iPQOqC9bLnDMOj+2Jfzz0TeNyf10al/545CgYVW6y58WspdbRuL7BHxiqW7LV0DjaO7nwc1IHfwW/vqU5jiiz6GYpGyipNUCHC4tYW+U5n24MvcuI8ekAVhdJSeodSt/A9llAdQryJHCWv23p4eH7MlGxBlt6PZJmuarfVSgCHYbteiDGWQgp9xlS/gaWUvKqVoOVCUCKaGEdliQok8QcxZRw87ejzbXX0q1eW4B4SI1/AgMBAAECggEAWU2dKjhnEC8ty8eSdXtGiCnH3GI+4AD1fCtKtHzdGgUzEhLmx0IAYyQlbOUvXqlcN1t1faxIDIptiWvUUJ7Mkb/ml3YUrJJZ7wfXAZ0syDac1caiU5Lr31DxzE4FIQvAGmHTHraX4FhV7ZMcoWd8fvUMeL0R0Do59Ce4DVGPtNWsioP2OKlZrEEYxlzPZsIYzne+8rhj/jsKxudyj21sN8mAY0FCRoeytkIroCYG0TaIGfm4J20HYunFDmUt4cZVQsgoIzpZrvs20JI+3qtrlWzAj89RZ4fH7CN1er1HCeb3jptZKwKx2qQyhTA6NDhxuzPH90l7zsuhLDMXuL4kXQKBgQDutyY88W2mpwgPY4VyAcIXojLCEp9aOplVajRNR9aK/Ti958nvYqFWoe7+QSwsFVrOTkyIUxqY8mv3aFg9nczWNoNFRGdD3zfjkbp17yec8QOq+yaQWyoBamyytJVmuJjjZUZWeUrQ5Q4YEUDCjYbfyx/mp9Zxwj3vGU2wZt5IvQKBgQDi7RDuhWB0PrSfcHTCFZ8Co3dHHndLI4pAnKawaca+Lw1RvqqvNNkVb87SpO0wRNoKDOUmfitrV0n9bOsWraam1gY8nQsdwMvb1/fEbKMGxxFfp0bWgTaRUkmzdGxOcV49tGuTF4kdyfiZp3Yu/LrSLUaeUCNZpck9+2mtP9to6wKBgFFESqE+s8yjWowanmh0jsYK8uq8+kD2aBL7B/kzNqe0kyebjFSRqElc8YbfWxFa58IKR+W1HP3qsbTVcgzv9rcKceAX7GvfxyATEX5qv3qfVldUDwnf70nyGDUyYxZIS8xGQw7XVhANmqG45eoV0k/H0AFvLAMoVHtciuU97/ilAoGBAKlrdsWtfHqtSirzSaiRfdr5chb9zvChQxnEGssA3emltVr/b+1JFn3jsNUhXxg3f1YblIWtkvsb+1iilc2jrhVHGvbsBJ2dEFY9InVa6kgoHXd9quyBId1TQ0Ugua/DAiotZlc2Lh+4Z8tH9HtWIqDCPsP5brsChIGrD5XSZBwrAoGAUAIw4qr0FpFGpDYkLYY03k614kmDJskFG+jO2RdXQc58HK5QvkhquMoT12mASfMknb2Kn5su4iGB8uirjMCtdVeQK0ztjmmWUhJsu5VsA1Dn5dQeBhpUikXR5flgdzLmJqIFtHLgx0EqNusO4iuUrl20ftGyZK4k8aysfhYbPq8=
```


Example of ECC 256 PKCS#8 ASN.1 DER private key in Base64:

```bash
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgDwgzMkOu2yCJekAO70mYCUS0mySg9KW95Fd1pVdUybChRANCAASvXfyC9XmUlW6Kq4TQXHJiUcg4CtlzEj9I+RlkQo6wQWLTFjBW9b6VUFwNwC56yDN7QDN+yndS9pgUh5+kxEom
```


On the console, you can upload private keys encoded in Base64 or binary. In API calls, the private keys must be encoded in Base64.

&nbsp;

**Related APIs**

[ImportKeyMaterial](https://docs.byteplus.com/en/docs/kms/ImportKeyMaterial)

&nbsp;

<span id="step-3-delete-the-key-material"></span>
## Step 3: Delete the key material

You can directly delete the key material. After the key material is deleted, the state of the CMK changes to PendingImport, in which state the CMK cannot be used to encrypt or decrypt data. If the current state of the CMK is PendingDelete, the state of the CMK does not change after the key material is deleted. You can import the same key material again to re\-enable the CMK. We recommend that you store a copy of the key material.


1. Find the specified CMK and click **Delete key material** in the **Actions** column.

2. In the deletion confirmation message, click **Confirm**.


&nbsp;

**Related APIs**

[DeleteKeyMaterial](https://docs.byteplus.com/en/docs/kms/DeleteKeyMaterial)

&nbsp;

&nbsp;

&nbsp;
