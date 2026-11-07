---
title: "PutBucketEncryption"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketencryption"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface sets server\-side encryption for a bucket. Once configured, all objects uploaded to the bucket will automatically inherit its encryption settings, unless otherwise specified. Currently, server\-side encryption using KMS\-managed keys (SSE\-KMS) and TOS\-managed keys (SSE\-TOS) is supported for bucket configuration.

For more information on server\-side encryption, see [Server-Side Encryption Overview](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* PutBucketEncryption can only be called over HTTPS.

* Only users with `tos:PutBucketEncryption` permission can call PutBucketEncryption. By default, the bucket owner directly has `tos:PutBucketEncryption` permission, and the bucket owner can grant this permission to other users.

* HNS buckets do not support the PutBucketEncryption interface.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /?encryption HTTPS
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-MD5: OolRtfRnEQlFUQVcEd5Q****

{
    "Rule":{
        "ApplyServerSideEncryptionByDefault":{
            "SSEAlgorithm":"kms",
            "KMSMasterKeyID":"trn:kms:cn-beijing:200000****:keyrings/ring-test/keys/key-test"
        }
    }
}
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## **Request parameters and headers**

This request requires setting the Content\-MD5 value of the request body elements in the headers. It will be compared with the MD5 value of the uploaded request body elements. If they do not match, an error will be returned. For other common request headers, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|encryption |Query |String |Yes |\- |Special identifier representing the PutBucketEncryption request. |
|Content\-MD5 |Header |String |Yes |XrY7u+Ae7tCTyyK7j1rNww== |Base64\-encoded MD5 digest of the message body. |


<span id=".6K-35rGC5YWD57Sg"></span>
## **Request body elements**


|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Rule |Array |Yes |\- |Bucket encryption rule information. |
|ApplyServerSideEncryptionByDefault |Array |Yes |\- |Server\-side encryption configuration information. |
|SSEAlgorithm |String |Yes |AES256 |The default encryption method for server\-side encryption is described as follows:<br><br><br>* `kms`: use SSE\-KMS encryption.<br><br>* `AES256`: uses SSE\-TOS encryption with the AES256 algorithm.<br><br>* `SM4`: uses SSE\-TOS encryption with the SM4 algorithm.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Using SSE\-KMS for server\-side encryption generates API call fees, and creating KMS keys generates key management fees, which are charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">KMS Billing Overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The AES\-256 algorithm for SSE\-TOS is only supported in China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta); the SM4 algorithm for SSE\-TOS is only supported in China (Beijing) and China (Shanghai).</div><br> |
|KMSDataEncryption |String |No |AES256 |Set the encryption algorithm when using SSE\-KMS encryption. If not set, it defaults to the AES256 encryption algorithm. The values are explained as follows:<br><br><br>* `AES256`: AES256 encryption algorithm.<br><br>* `SM4`: SM4 encryption algorithm.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">AES\-256 algorithm under SSE\-KMS is only supported in China (Beijing), China (Shanghai), Asia Pacific (Johor), and Asia Pacific (Jakarta); SM4 algorithm under SSE\-KMS is only supported in China (Beijing) and China (Shanghai).</div><br> |
|KMSMasterKeyID |String |No |trn:kms:cn\-beijing:200000\*\*\*\*\*:keyrings/ring\-test/keys/key\-test |Specify the primary key for SSE\-KMS encryption in the format `trn:kms:<region>:<accountID>:keyrings/<keyring>/keys/<key>`, which is the TRN of the KMS primary key. Parameter details are as follows:<br><br><br>* `region`: the Region ID where the key is used.<br><br>* `accountID`: the account ID that owns the key.<br><br>* `keyring`: alias of the keyring.<br><br>* `key`: primary key alias.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can also create a primary key in the <a href="https://console.byteplus.com/kms/region:kms+cn-beijing/primary">KMS console</a>, then click the key name to get the KMSMasterKeyID under the <strong>key TRN and alias</strong> column on the <strong>key ring details</strong> page. For detailed information on KMS keys, refer to <a href="https://docs.byteplus.com/en/docs/kms/Getting_started_with_key_management">KMS quick start</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Set the <code>KMSMasterKeyID</code> parameter only when the <code>SSEAlgorithm</code> value is <code>kms</code>.</div><br> |


<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## **Response headers**

For the common response headers returned by this request, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## **Response body elements**

No elements are used.

<span id=".6K-35rGC56S65L6L"></span>
## **Sample request**

```JSON
PUT /?encryption HTTPS
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-MD5: OolRtfRnEQlFUQVcEd5Q****

{
    "Rule":{
        "ApplyServerSideEncryptionByDefault":{
            "SSEAlgorithm":"kms",
            "KMSMasterKeyID":"trn:kms:cn-beijing:200000****:keyrings/ring-test/keys/key-test"
        }
    }
}
```


<span id=".5ZON5bqU56S65L6L"></span>
## **Sample response**

```JSON
HTTPS 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
server: TosServer
Content-Length: 0
```
