---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview"
---

With server\-side encryption, TOS encrypts your uploaded data at the object level before storing it. When you download these objects, TOS automatically decrypts the data and sends it back to you.

<span id=".5L2_55So5Zy65pmv"></span>
## Use cases

Server\-side encryption is ideal for applications that need to encrypt stored data or comply with regulatory requirements. It provides effective data protection, and encrypted objects are automatically decrypted when accessed. Accessing encrypted and unencrypted objects is identical.

<span id=".5Yqg5a-G5pa55byP"></span>
## Encryption methods

TOS offers several server\-side encryption methods. Select the appropriate method based on your use case.


|**Encryption method** |**Description** |**Use cases** |Cost |**Supported regions** |
|---|---|---|---|---|
|Server\-side encryption with TOS\-managed keys (SSE\-TOS) |TOS manages encryption keys. TOS uses a unique key to encrypt each object with AES\-256, and it regularly rotates the master key. |When basic encryption is enough and self\-managed keys are not necessary |Free |China (Beijing), China (Shanghai), China (Hong Kong), Asia Pacific (Johor), and Asia Pacific (Jakarta) |
|Server\-side encryption with customer\-provided keys (SSE\-C) |Users manage encryption keys. TOS uses customer\-provided keys to encrypt data with AES\-256 during the upload process. |When you need to encrypt data using keys that you manage yourself |Free |All regions |
|Server\-side encryption with BytePlus KMS keys (SSE\-KMS) |Key Management Service (KMS) manages encryption keys. TOS uses customer master keys, hosted by KMS, to generate unique data keys. These keys are then used to encrypt data with AES\-256 algorithm. |When you need the cloud service provider to manage the keys while retaining the ability to create, manage, and designate your own customer master keys for data encryption |Charged. For more information, see [BytePlus KMS Pricing](https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing). |China (Beijing), China (Shanghai), China (Hong Kong), Asia Pacific (Johor), and Asia Pacific (Jakarta) |


<span id="0crYgczL"></span>
## Using server\-side encryption with TOS\-managed keys (SSE\-TOS)

SSE\-TOS is an encryption method where TOS manages the keys. SSE\-TOS employs strong multi\-factor encryption to ensure that each object is encrypted with a unique key. SSE\-TOS supports the AES\-256 algorithm for encrypting data. The keys themselves are encrypted using a regularly rotated master key. There are several ways to apply SSE\-TOS to your objects.

<span id=".5L2_55So5a-56LGh5a2Y5YKo5o6n5Yi25Y-w"></span>
### Using the TOS console


* You can enable SSE\-TOS when uploading objects. For instructions, see [Uploading objects](https://docs.byteplus.com/docs/tos/docs-uploading-a-file).

* You can enable SSE\-TOS for a bucket when you create it or after it is created. For instructions, see [Creating buckets](https://docs.byteplus.com/docs/tos/docs-create-a-bucket) or [Setting bucket encryption](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket).

   When you set a bucket's encryption to SSE\-KMS, all objects uploaded to that bucket will automatically inherit its encryption settings, unless otherwise specified.


<span id=".5L2_55SoLXJlc3QtYXBp"></span>
### Using REST APIs

When uploading objects with server\-side encryption via API, you must include the` x-tos-server-side-encryption` header in the request. The following APIs support this header:


* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When uploading a large object via multipart upload, you can specify the server\-side encryption method by adding the <code>x-tos-server-side-encryption</code> header to the <code>CreateMultipartUpload</code> request.</div>


* <div data-tips="true" data-tips-type="tip">When copying an existing object, the target object will not be encrypted, regardless of whether the source object is encrypted, unless you explicitly specify the server\-side encryption method in the request.</div>



When an object's encryption method is set to SSE\-TOS, the following REST APIs include the `x-tos-server-side-encryption` header in their responses.


* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart)

* [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy)

* [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload)

* [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject)

* [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When using a POST operation to upload an object, instead of providing the request header, you provide the same information in the form fields. For more information, see PostObject.</div>


* <div data-tips="true" data-tips-type="warning">If your object uses SSE\-TOS, do not include the <code>x-tos-server-side-encryption</code> header in GET and HEAD requests. Including this header results in an HTTP 400 Bad Request error.</div>



<span id=".5L2_55So55So5oi35o-Q5L6b5a-G6ZKl55qE5pyN5Yqh56uv5Yqg5a-G77yIc3NlLWPvvIk="></span>
## Using server\-side encryption with customer\-provided keys (SSE\-C)

SSE\-C uses customer\-managed keys to encrypt data. You provide the key, and then TOS encrypts the data using AES\-256 during the upload process. To use SSE\-C, you must provide encryption key information in the following request headers.


|Header |**Description** |
|---|---|
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Specifies the encryption algorithm. The value must be "AES256". |
|x\-tos\-server\-side\-encryption\-customer\-key |Specifies the 256\-bit, Base64\-encoded encryption key used to encrypt or decrypt your data. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Specifies the Base64\-encoded, 128\-bit MD5 digest of the encryption key according to [RFC 1321](http://tools.ietf.org/html/rfc1321).<br><br>TOS uses this header to perform a message integrity check and ensure that the encryption key was transmitted without error. |


<span id=".5L2_55SoLXJlc3QtYXBp"></span>
### Using REST APIs

You can apply SSE\-C to objects by providing the `x-tos-server-side-encryption-customer-*` headers in PUT and POST requests. To decrypt objects encrypted with SSE\-C in GET or HEAD requests, you must provide the `x-tos-server-side-encryption-customer-*` headers. The following APIs support these headers:


* [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject)

* [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject)

* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)

* [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy)


When you copy an object, you have both a source object and a target object.


* To encrypt the target object with SSE\-C, provide the necessary encryption information using the three headers described in the above table.

* If the source object is encrypted with SSE\-C, provide the encryption key information using the following headers so that TOS can decrypt the object for copying.



|Header |**Description** |
|---|---|
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-algorithm |Specifies the algorithm used to decrypt the source object. The value must be "AES256". |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key |Specifies the Base64\-encoded encryption key used to decrypt the source data. The key must match the one used when creating the source object. |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key\-MD5 |Specifies the Base64\-encoded, 128\-bit MD5 digest of the encryption key according to [RFC 1321](http://tools.ietf.org/html/rfc1321).<br><br>TOS uses this header to perform a message integrity check and ensure that the encryption key was transmitted without error. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You must use HTTPS when specifying SSE\-C headers in your requests.</div>


* <div data-tips="true" data-tips-type="warning">TOS never stores the encryption keys you provide. Instead, it stores an HMAC value of the key along with randomly generated data. This value is then used to validate access requests. TOS cannot derive the encryption key or decrypt the object content from the HMAC value and random data. Therefore, if you lose the encryption key, you will not be able to retrieve the object.</div>


* <div data-tips="true" data-tips-type="warning">When using a POST operation to upload an object, instead of providing the <code>x-tos-server-side-encryption-*</code> header, you provide the same information in the form fields. For more information, see <a href="https://docs.byteplus.com/docs/tos/reference-postobject">PostObject</a>.</div>


* <div data-tips="true" data-tips-type="warning">SSE\-C can only be used via the API and is not supported in the console.</div>



<span id=".5L2_55So54Gr5bGx5byV5pOOLWttcy3nmoTmnI3liqHnq6_liqDlr4bvvIhzc2Uta21z77yJ"></span>
## Using server\-side encryption with BytePlus KMS keys (SSE\-KMS)

TOS uses customer master keys, which are managed by KMS, to generate unique data keys. These keys are then used to encrypt data with AES\-256 algorithm. SSE\-KMS uses envelope encryption to secure user data. First, TOS encrypts the data with the plaintext data key. Then, the plaintext key is discarded and only the encrypted data key is retained.

<span id=".a21zLeivtOaYjg=="></span>
### What is KMS

KMS is an all\-in\-one key management and data encryption platform powered by BytePlus. It provides user\-friendly encryption interfaces that help you securely manage keys and protect critical cloud data. KMS implements access control and log tracking for all key operations. This ensures that usage records are maintained for each key, thus satisfying auditing and compliance requirements. You can create keys independently via the [KMS console](https://console.byteplus.com/kms/region:kms+cn-beijing/primary) or import external keys into KMS. Learn more in [KMS Quick start](https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management).

<span id=".5rOo5oSP5LqL6aG5"></span>
### Notes


* If you are using SSE\-KMS for server\-side encryption for the first time, you must first [activate KMS](https://console.byteplus.com/finance/opening-service/CloudKMS/?return_url=/kms/region:kms+cn-beijing/primary). Although activating KMS is free, using the service incurs charges. Using SSE\-KMS for server\-side encryption generates API call fees, and creating KMS keys generates key management fees. These fees are charged by KMS. For more information, see [BytePlus KMS Pricing](https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing).

* Currently, SSE\-KMS only supports custom KMS keys and does not support default keys managed by TOS.

* SSE\-KMS only encrypts object data, not metadata.

* To upload objects with SSE\-KMS, you need the `kms:GenerateDataKey` permission. To download SSE\-KMS\-encrypted objects, you need the `kms:Decrypt` permission.

* SSE\-KMS\-encrypted objects do not support anonymous access. To access SSE\-KMS\-encrypted objects, you must activate KMS and have permission to access the master key. Requests must also be signed using valid credentials.


<span id=".5L2_55So5a-56LGh5a2Y5YKo5o6n5Yi25Y-w"></span>
### Using the TOS console


* You can enable SSE\-KMS when uploading objects. For instructions, see [Uploading objects](https://docs.byteplus.com/docs/tos/docs-uploading-a-file).

* You can enable SSE\-KMS for a bucket when you create it or after it is created. For instructions, see [Creating buckets](https://docs.byteplus.com/docs/tos/docs-create-a-bucket) or [Setting bucket encryption](https://docs.byteplus.com/docs/tos/Set-server-side-encryption-for-the-bucket).

   When you set a bucket's encryption to SSE\-KMS, all objects uploaded to that bucket will automatically inherit its encryption settings, unless otherwise specified.


<span id=".5L2_55SoLXJlc3QtYXBp"></span>
### Using REST APIs

To apply SSE\-KMS to objects via REST APIs, you must provide the `x-tos-server-side-encryption`, `x-tos-server-side-data-encryption`, and `x-tos-server-side-encryption-kms-key-id` headers in the requests.

The following APIs support SSE\-KMS headers:


* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When uploading a large object via multipart upload, you can specify SSE\-KMS by adding the <code>x-tos-server-side-encryption</code>, <code>x-tos-server-side-data-encryption</code>, and <code>x-tos-server-side-encryption-kms-key-id</code> headers to the <code>CreateMultipartUpload</code> request.</div>


* <div data-tips="true" data-tips-type="tip">When copying an existing object, the server\-side encryption method of the source object will not be automatically applied to the target object. You must explicitly specify the server\-side encryption method in the <code>CopyObject</code> request.</div>



When an object's encryption method is set to SSE\-KMS, the following REST APIs include the `x-tos-server-side-encryption` and `x-tos-server-side-encryption-kms-key-id` headers in their responses.


* [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)

* [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)

* [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)

* [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)

* [UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart)

* [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy)

* [CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload)

* [GetObject](https://docs.byteplus.com/docs/tos/reference--getobject)

* [HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject)


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You must use HTTPS when specifying SSE\-KMS headers in your requests.</div>


* <div data-tips="true" data-tips-type="warning">When using a POST operation to upload an object, instead of providing the request header, you provide the same information in the form fields. For more information, see <a href="https://docs.byteplus.com/docs/tos/reference-postobject">PostObject</a>.</div>


* <div data-tips="true" data-tips-type="warning">If your object uses SSE\-KMS, do not include the <code>x-tos-server-side-encryption</code> header in GET and HEAD requests. Including this header results in an <code>HTTP 400 Bad Request</code> error.</div>
