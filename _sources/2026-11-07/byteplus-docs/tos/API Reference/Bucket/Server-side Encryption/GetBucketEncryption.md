---
title: "GetBucketEncryption"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketencryption"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface retrieves the server\-side encryption configuration for a specified bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* The GetBucketEncryption interface can only be called using the HTTPS protocol.

* Only users with the `tos:GetBucketEncryption` permission can call the GetBucketEncryption interface. By default, the bucket owner has the `tos:GetBucketEncryption` permission directly, and the bucket owner can grant this permission to other users.

* HNS buckets do not currently support the GetBucketEncryption interface.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?encryption HTTPS
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses public request headers; see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|encryption |Query |String |Yes |\- |Special identifier representing the GetBucketEncryption request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers; see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements


|**Name** |**Type** |**Sample value** |**Note** |
|---|---|---|---|
|Rule |Array |\- |Bucket encryption rule information. |
|ApplyServerSideEncryptionByDefault |Array |\- |Server\-side encryption configuration information. |
|SSEAlgorithm |String |AES256 |The default server\-side encryption method and its values are as follows:<br><br><br>* `kms`: uses SSE\-KMS encryption.<br><br>* `AES256`: uses SSE\-TOS encryption and the AES256 algorithm.<br><br>* `SM4`: uses SSE\-TOS encryption and the SM4 algorithm.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using SSE\-KMS for server\-side encryption generates API call fees, and creating KMS keys generates key management fees. These fees are charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/kms/BytePlus_KMS_Pricing">KMS Billing Overview</a>.</div><br> |
|KMSDataEncryption |String |AES256 |Encryption algorithm used with SSE\-KMS encryption method, with the following values:<br><br><br>* `AES256`: AES256 encryption algorithm.<br><br>* `SM4`: SM4 encryption algorithm. |
|KMSMasterKeyID |String |trn:kms:cn\-beijing:200000\*\*\*\*\*:keyrings/ring\-test/keys/key\-test |The master key used for SSE\-KMS encryption.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>KMSMasterKeyID</code> parameter is returned only when the <code>SSEAlgorithm</code> value is <code>kms</code>.</div><br> |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?encryption HTTPS
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTPS 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 143

{
    "Rule":{
        "ApplyServerSideEncryptionByDefault":{
            "SSEAlgorithm":"kms",
            "KMSMasterKeyID":"trn:kms:cn-beijing:200000****:keyrings/ring-test/keys/key-test"
        }
    }
}
```
