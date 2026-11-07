---
title: "GetBucketInfo"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketinfo"
---

<span id="b59e4254"></span>
## Description

This API is used to query the configuration information of the storage bucket.

<span id="47798713"></span>
## **Request syntax**

```JSON
GET /?bucketInfo HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="33df7704"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|bucketInfo |Query |String |Is |\- |Represents the special identifier for a GetBucketInfo request. |


<span id="4efa916f"></span>
## **Request body elements**

This request does not use request message elements.

<span id="2e19f116"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="a4d4d428"></span>
## **Response body elements**


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Bucket |Object |\- |Bucket information. |
|Name |String |tos\-example |Name of the bucket.<br><br>Parent node: Bucket |
|Owner |Object |\- |Account information associated with the storage bucket.<br><br>Parent node: Bucket |
|ID |String |20012\*\*\*\* |Account ID to which the storage bucket belongs.<br><br>Parent node: Owner |
|DisplayName |String |user\-name |Name of the account that owns the bucket.<br><br>Parent node: Owner |
|CreationDate |String |2025\-01\-17T04:25:18.000Z |Creation time of the bucket, in UTC format.<br><br>Parent node: Bucket |
|StorageClass |String |STANDARD |Set the default storage class for the bucket.<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiered Storage<br><br>* `ARCHIVE_FR`: Flashback Archive Storage.<br><br>* `ARCHIVE`: Archived Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br><br>Parent node: Bucket |
|Type |String |fns |The type of bucket.<br><br>Parent node: Bucket |
|ProjectName |String |default |Project that owns the bucket.<br><br>Parent: Bucket |
|Location |String |ap\-southeast\-1 |Region where the bucket is located.<br><br>Parent: Bucket |
|AzRedundancy |String |single\-az |Types of AZ redundancy for the bucket.<br><br>Parent node: Bucket |
|ExtranetEndpoint |String |tos\-ap\-southeast\-1.bytepluses.com |The public network access domain name of the TOS protocol for the storage bucket.<br><br>Parent node: Bucket |
|IntranetEndpoint |String |tos\-ap\-southeast\-1.ibytepluses.com |The private network access domain name of the TOS protocol for the storage bucket.<br><br>Parent node: Bucket |
|ExtranetS3Endpoint |String |tos\-s3\-ap\-southeast\-1.bytepluses.com |The public network access domain name of the S3 protocol for the storage bucket.<br><br>Parent node: Bucket |
|IntranetS3Endpoint |String |tos\-s3\-ap\-southeast\-1.ibytepluses.com |The private network access domain name of the S3 protocol for the storage bucket.<br><br>Parent node: Bucket |
|Versioning |String |Enabled |Explanation of the bucket's versioning status is as follows:<br><br><br>* `Enabled`: Enable the versioning feature.<br><br>* `Suspended`: Suspend the versioning feature.<br><br>* Empty: Version control function not enabled.<br><br><br>Parent node: Bucket |
|CrossRegionReplication |String |Enabled |The cross\-region replication status of the bucket is described as follows:<br><br><br>* `Enabled`: Enable the cross\-region replication feature.<br><br>* `Disabled`: Disabled the cross\-region replication feature.<br><br><br>Parent node: Bucket |
|AccessMonitor |String |Enabled |The access tracking state of the bucket is explained as follows:<br><br><br>* `Enabled`: Enabled the access monitor feature.<br><br>* `Disabled`: Disabled the access monitor feature.<br><br><br>Parent node: Bucket |
|ServerSideEncryptionConfiguration |Object |\- |Information on the server\-side encryption configuration of the bucket.<br><br>Parent node: Bucket |
|Rule |Array |\- |Server\-side encryption rules.<br><br>Parent node: ServerSideEncryptionConfiguration |
|ApplyServerSideEncryptionByDefault |Array |\- |Server\-side encryption configuration information.<br><br>Parent node: Rule |
|SSEAlgorithm |String |AES256 |Server\-side encryption methods, explanation of values as follows:<br><br><br>* `kms`: Uses SSE\-KMS encryption method.<br><br>* `AES256`: Uses SSE\-TOS encryption method.<br><br>* None: Server\-side encryption feature not enabled.<br><br><br>Parent node: ApplyServerSideEncryptionByDefault |
|KMSMasterKeyID |String |trn:kms:cn\-beijing:200000\*\*\*\*\*:keyrings/ring\-test/keys/key\-test |The primary key used when encrypting with SSE\-KMS.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the <code>SSEAlgorithm</code> value is <code>kms</code>, the <code>KMSMasterKeyID</code> parameter is returned.</div><br><br><br>Parent node: ApplyServerSideEncryptionByDefault |


<span id="d78728ef"></span>
## **Sample request**

```JSON
GET /?bucketInfo HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="04cedf3e"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Wed, 09 Apr 2025 09:01:45 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 643
{
    "Bucket": {
        "Name": "test",
        "Owner": {
            "ID": "214748****",
            "DisplayName": "aaa"
        },
        "CreationDate": "2025-04-02T06:09:12.000Z",
        "StorageClass": "STANDARD",
        "ProjectName": "default",
        "Type": "fns",
        "Location": "ap-southeast-1",
        "AzRedundancy": "single-az",
        "ExtranetEndpoint": "tos-ap-southeast-1.bytepluses.com",
        "IntranetEndpoint": "tos-ap-southeast-1.ibytepluses.com",
        "ExtranetS3Endpoint": "tos-s3-ap-southeast-1.bytepluses.com",
        "IntranetS3Endpoint": "tos-s3-ap-southeast-1.ibytepluses.com",
        "Versioning": "",
        "CrossRegionReplication": "Disabled",
        "AccessMonitor": "Disabled",
        "ServerSideEncryptionConfiguration": {
            "Rule": {
                "ApplyServerSideEncryptionByDefault": {
                    "SSEAlgorithm": ""
                }
            }
        }
    }
}
```
