---
title: "FetchObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Fetchobject"
---

<span id="1211ce54"></span>
## Feature description

Call the FetchObject interface to fetch resources from the specified URL and store them in the designated bucket.

<span id="70ad6032"></span>
## Server\-side encryption

With server\-side encryption enabled, TOS encrypts the data you upload at the file level and stores the encrypted data permanently. When you download a file, TOS automatically decrypts and returns the data to you. For more details about server\-side encryption, see [server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

<span id="c065e39f"></span>
## ACL

You can set the object's ACL through headers. All objects are private by default. You can grant specific permissions to an account or predefined group. For more details about ACL, see [ACL policy overview](https://docs.byteplus.com/docs/tos/docs-overview_4).

<span id="0f5ca9d7"></span>
## Storage type

TOS stores objects in Standard Storage by default. This storage type features high availability, reliability, and performance. You can also choose another storage type according to the use case. For more details about storage types, see [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type).

<span id="97753912"></span>
## Notes


|**Category** |**Notes** |
|---|---|
|Object count |* Only one object can be fetched at a time.<br><br>* The maximum supported size is 5 GiB. Fetching objects larger than 5 GiB will fail. |
|URL |Only publicly accessible URL resources are supported for fetching. |
|Permissions |Please ensure your BytePlus account has permission to upload objects to the corresponding bucket; otherwise, calling FetchObject to fetch resources will fail. |


<span id="96e56fd7"></span>
## Request syntax

```JSON
POST /objectName?fetch HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
<Optional Additional Header>

{
    "URL": "http://abc.123/"
}
```


<span id="aa0f0fa8"></span>
## Request parameters and headers

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|fetch |Query |String |Yes |\- |Represents a special identifier for the FetchObject request. |
|x\-storage\-class |Header |string |No |STANDARD |Specifies the storage type of the copy. If this parameter is unset, the copy inherits the default storage type of its containing bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering Storage.<br><br>* `ARCHIVE_FR`: Archive Flashback Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive is only supported in China (Beijing), China (Shanghai), and China (Guangzhou). Deep Cold Archive is currently in closed beta. Please contact your account manager for access.   </div><br>    |
|x\-tos\-acl |Header |string |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: private.<br><br>* `public-read`: public read.<br><br>* `public-read-write`: public read\-write.<br><br>* `authenticated-read`: authenticated user read.<br><br>* `bucket-owner-read`: bucket owner read.<br><br>* `bucket-owner-full-control`: bucket owner full control.<br><br>* `default`: inherit bucket ACL, meaning the object's ACL policy matches the bucket ACL policy. |
|x\-tos\-grant\-full\-control |Header |string |No |id=123,id=456 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object during object creation. Format: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |string |No |id=123,id=456 |Allows the grantee to read the object and its metadata. Format: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |string |No |id=123,id=456 |Allows the authorized user to read the object ACL. Format: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |string |No |id=123,id=456 |Allows the grantees to modify the object ACL. Format: id=account1,id=account2. |
|x\-tos\-meta\-\* |Header |string |No |x\-tos\-meta\-key: value |Used to add custom metadata for personalized object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |
|x\-tos\-server\-side\-encryption |Header |String |No |AES256 |Specifies the method used for encrypting the object. If this parameter is unset, the object is not encrypted by default. Valid values:<br><br><br>* `AES256`: uses SSE\-TOS encryption with the AES256 algorithm.<br><br>* `SM4`: uses SSE\-TOS encryption with the SM4 algorithm.<br><br>* `kms`: uses SSE\-KMS encryption.<br><br><br>For detailed explanations of SSE\-TOS and SSE\-KMS encryption methods, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using SSE\-KMS for server\-side encryption generates API call fees. Creating a KMS key incurs key management fees charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">BytePlus KMS Pricing</a>.</div><br> |
|x\-tos\-server\-side\-data\-encryption |Header |String |No |AES256 |Set the encryption algorithm when using SSE\-KMS encryption. Description:<br><br><br>* `AES256`: AES256 encryption algorithm.<br><br>* `SM4`: SM4 encryption algorithm.<br><br><br>Default is `AES256` algorithm. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |Header |String |No, but yes if SSE\-KMS is used. |trn:kms:cn\-beijing:20000111:keyrings/ring\-test/keys/key\-test |Specify the master key used for SSE\-KMS encrypted target objects in the following format:<br><br>`trn:kms:<region>:<accountID>:keyrings/<keyring>/keys/<key>`: the TRN of the KMS master key, where `region` is the Region ID of the key, `accountID` is the account ID owning the key, `keyring` is the keyring alias, and `key` is the master key alias.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Default master key is not supported currently. If SSE\-KMS encryption is specified without providing this header, the server returns a <code>400 InvalidRequest</code> error.</div><br> |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm for SSE\-C encrypting the object. Valid value:<br><br>`AES256`: encrypt the object using the AES256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |YWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFh\*\*\*\* |Used with `x-tos-server-side-encryption-customer-algorithm`, specifies the SSE\-C encrypted target object's key, formatted as a base64\-encoded 256\-bit encryption key. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4\*\*\*\* |Used with `x-tos-server-side-encryption-customer-key`, this header represents the MD5 value of the key used to encrypt the object. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |


<span id="f6740010"></span>
## Request body elements


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|URL |Body |String |Yes |http://abc/obj |URL to be fetched.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only a single URL is supported at present.</div><br> |
|IgnoreSameKey |Body |Bool |No |true |Fetch strategy when a file with the same name exists in the bucket. The values are as follows:<br><br><br>* `true`: if a file with the same name already exists in the bucket, skip this fetch.<br><br>* `false`: if a file with the same name already exists in the bucket, still fetch the object and overwrite the existing object when uploading.<br><br><br>default is `false`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The same\-name file is determined by the file key; file content is not compared.</div><br> |
|ContentMD5 |Body |String |No |XrY7u+Ae7tCTyyK7j1rN\*\*\*\* |Base64 value of the MD5 of the file to upload. After setting this, TOS calculates the MD5 of the uploaded file and checks it against the MD5 carried by FetchObject. If the verification fails, the fetch will fail. |


<span id="3448f63a"></span>
## Response headers

The common response headers returned by this request. See [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Parameter type** |**Sample value** |**Note** |
|---|---|---|---|
|x\-tos\-server\-side\-encryption |String |kms |Server\-side encryption method of the object, which is returned if the object is SSE\-TOS or SSE\-KMS encrypted. Valid values:<br><br><br>* `AES256`: uses SSE\-TOS encryption with the AES256 algorithm.<br><br>* `SM4`: uses SSE\-TOS encryption with the SM4 algorithm.<br><br>* `kms`: uses SSE\-KMS encryption.<br><br><br>For detailed explanations of SSE\-TOS and SSE\-KMS encryption methods, see [Server-Side Encryption Overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |trn:kms:cn\-beijing:2000\*\*\*\*:keyrings/ring\-test/keys/key\-test |ID of the KMS master key, which is returned if the object is SSE\-KMS encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |AES256 |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |0gYVWExOAz67jX5A6qY4+A== |MD5 value of the encryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-version\-id |String |57AF1A32CECB56721267 |Version ID of the object. This header will not appear in the response if the object has no version ID. |
|x\-qos\-delay\-time |String |5 |The expected delay time. The `x-qos-delay-time` header is calculated and added only when `AvgQosDelayTime` is not 0. If this value is 0, this header is not added, indicating that flow control is not in effect. |


<span id="a88f0358"></span>
## Response body elements


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|ETag |String |883abc8623528daf10b7e1bb1b2774ba |Uniquely identifies the content of an object. |


<span id="60fe4e28"></span>
## Sample request

```JSON
POST /objectName?fetch HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
<Optional Additional Header>

{
    "URL": "http://abc.123/",
}
```


<span id="5ba2a51e"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Transfer-Encoding: chunked
{
    "ETag": "883abc8623528daf10b7e1bb1b2774ba"
}
```
