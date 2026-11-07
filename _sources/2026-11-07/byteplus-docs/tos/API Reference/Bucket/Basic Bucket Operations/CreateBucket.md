---
title: "CreateBucket"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-createbucket"
---

<span id="cb9d4418"></span>
## **Description**

This API is used to create a TOS bucket. To create a bucket, you must register with BytePlus and have a valid TOS Access Key ID (AK) for request validation. Anonymous users cannot create buckets, and a user can create up to 100 buckets globally. You assume ownership of a bucket when you create it.

<span id="2714ff4e"></span>
## **Storage types**

When creating a bucket, you can specify the default storage type for the bucket by providing the `x-tos-storage-class` header. The following storage types are currently supported:


* STANDARD (Standard Storage): suitable for scenarios where data is frequently accessed, such as social media images, popular videos, and big data analytics.

* IA (Infrequent Access Storage): suitable for scenarios where data is infrequently accessed (once or twice per month on average), such as data backup and file synchronization. It offers lower storage costs than Standard Storage but incurs a data retrieval fee for access. For details, see [Billing Overview](https://docs.byteplus.com/en/tos/docs/billing-overview).

* ARCHIVE_FR (Flashback Archive): suitable for scenarios where data is rarely accessed. The minimum storage duration is 90 days. Files can be read (flashed back) directly and transitioned to another storage type. Accessing the data incurs a data retrieval fee. For details, see [Billing Overview](https://docs.byteplus.com/en/tos/docs/billing-overview).

* ARCHIVE (Archive Storage): suitable for scenarios where data is rarely accessed and stored in the long run. The minimum storage duration is 90 days, and data needs to be restored before they can be accessed. For details, see [Billing Overview](https://docs.byteplus.com/en/tos/docs/billing-overview).

* COLD_ARCHIVE(Cold Archive Storage): suitable for business scenarios where data is rarely accessed and needs to be stored long\-term. The minimum storage duration is 180 days; data must be restored before accessing cold archive data. For details, see [Billing Overview](https://docs.byteplus.com/en/tos/docs/billing-overview).

* DEEP_COLD_ARCHIVE: suitable for extremely cold data that needs to be stored for ultra\-long periods. The minimum storage duration is 180 days; data must be restored before accessing deep cold archive data. For details, see [Billing Overview](https://docs.byteplus.com/en/tos/docs/billing-overview).


<span id="026e6fb7"></span>
## **Request syntax**

```Plain
PUT / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Authorization: authorization string
Date: GMT Date
x-tos-acl: ACL
x-tos-grant-full-control: GrantFullControl
x-tos-grant-read: GrantRead
x-tos-grant-read-acp: GrantReadACP
x-tos-grant-write: GrantWrite
x-tos-grant-write-acp: GrantWriteACP
x-tos-storage-class: STANDARD
```


<span id="9f6d265e"></span>
## **Request parameters and headers**


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-acl |Header |String |No |private |Bucket ACL. Valid values:<br><br><br>* `private`: private permission. This is the default value.<br><br>* `public-read`: publicly readable.<br><br>* `public-read-write`: publicly readable and writable.<br><br>* `authenticated-read`: Authenticated users have read access.<br><br>* `bucket-owner-read`: The bucket owner has read access.<br><br>* `bucket-owner-full-control`: The bucket owner has full control. |
|x\-tos\-grant\-full\-control |Header |String |No |id=123 |Grants the READ, WRITE, READ_ACP, and WRITE_ACP permissions of the bucket.<br><br>Format: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=123 |Allows grantee to list the objects in the bucket.<br><br>Format: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=123,id=456 |Allows grantee to read the bucket ACL.<br><br>Format: id=account1,id=account2. |
|x\-tos\-grant\-write |Header |String |No |id=123,id=456 |Allows grantee to create objects in the bucket. The bucket/object owner can delete and overwrite existing objects.<br><br>Format: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=123,id=456 |Grants WRITE_ACP permission.<br><br>Format: id=account1,id=account2. |
|x\-tos\-storage\-class |Header |String |No |STANDARD |The default storage type of the bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage, which is the default value.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>    |
|x\-tos\-az\-redundancy |Header |String |No |single\-az |The redundancy type of the bucket's availability zone. Possible values are explained as follows:<br><br><br>* `single-az`: Single AZ redundancy; default value.<br><br>* `multi-az`: Multi\-Availability Zone redundancy.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Multi\-AZ redundancy is supported only in North China 2 (Beijing), East China 2 (Shanghai), South China 1 (Guangzhou), and Asia Pacific Southeast (Johor) regions. For detailed information, refer to <a href="https://docs.byteplus.com/docs/tos/Multi-az-redundancy">Multi\-AZ redundancy</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please refer to the information displayed in the console for the support status of the multi\-AZ redundancy feature for HNS buckets.   </div><br>    |
|x\-tos\-project\-name |Header |String |No |default |Project name associated with the bucket. The possible values are explained as follows:<br><br><br>* If the request includes the specified request header and specifies a project name, the bucket created will belong to that project.<br><br>* When the specified project name is 'default', the created bucket will belong to the default project.<br><br>* If the request does not include this request header, the bucket created will belong to the default project. |
|x\-tos\-tagging |Header |String |No |key1=value1&key2=value2 |Add tags to the bucket in the format `{Key}={Value}`. Separate multiple tags with &. Each storage bucket can be bound to up to 50 tags. The constraints and limitations for tag keys and tag values are as follows:<br><br><br>* Label Key<br><br>   * The length must be between 1 and 128 characters.<br><br>   * Supports letters or characters from any language (for example, Chinese, English letters, etc.), numbers, spaces, and special characters: `_.:/+-@`.<br><br>   * Labels must not begin with `volc:` in any letter case. Keys starting with `volc:` are reserved by the system and must not be created.<br><br>* Label Value<br><br>   * The length must be between 0 and 256 characters, and the label value may be left empty.<br><br>   * Supports letters or characters from any language (such as Chinese, English letters, etc.), numbers, and spaces; supports special characters: `_.:/+-@`. |
|x\-tos\-bucket\-type |Header |String |No |hns |Set the bucket type. The parameter type is string. This is an optional parameter. The possible values are described as follows:<br><br><br>* `fns`: flat barrel.<br><br>* `hns`: Tiered bucket.<br><br><br>If this message header is not included, an fns bucket will be created by default. |
|x\-tos\-bucket\-object\-lock\-enabled |Header |String |No |true |Whether to enable the retention policy feature; only the value `true` is supported, which indicates that the retention policy is enabled. Once enabled, it cannot be disabled. |


<span id="ff4a7703"></span>
## **Request body elements**

No elements are used.

<span id="c1892767"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|Location |String |A forward slash ( / ) followed by the bucket name. |


<span id="a8d1db91"></span>
## **Response body elements**

No elements are used.

<span id="c9b99999"></span>
## **Sample request**

```Plain
PUT / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: authorization string
x-tos-acl: public-read
Content-Length: 0
```


<span id="e5b0c62c"></span>
## **Sample response**

```Plain
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 06:45:39 GMT
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Location: /bucketname  
server: TosServer
Content-Length: 0
```
