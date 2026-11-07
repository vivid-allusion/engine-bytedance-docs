---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Same-region-replication-overview"
---

Same\-region replication (SRR) refers to automatically copying objects from one bucket to another in the same region, allowing users to filter the objects to be copied as needed and view the replication progress.

<span id="8bb9fbfc"></span>
## Use cases

SRR enables local data redundancy backup by copying data to other buckets in the same region, with no traffic fees currently charged, resulting in lower costs.

<span id="7Dc5L2ez"></span>
## What does SRR replicate?

<span id="HMKFaUlz"></span>
### What is replicated with SRR?

SRR replicates the following information about objects: content, size, last modified time, tag, creator, version number, user\-defined metadata, and storage type. The following types of objects can be automatically replicated via an SRR rule:


* Objects that exist before the SRR rule takes effect.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the SRR rule does not synchronize existing objects. To do so, turn on the "Sync historical object" option in the rule.   </div>
   

* Objects uploaded after the SRR rule takes effect.

* Object overwrite operations. If an object in the source bucket is overwritten after replication, the overwrite operation will be synchronized again with the destination bucket.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only object overwrite operations will be synchronized again to the destination bucket for objects that have already been successfully replicated. Changes to object metadata, object access control lists (ACLs), and storage type will not be synchronized to the destination bucket.   </div>
   

<span id="FY7rAcV3"></span>
### What is not replicated with SRR?


* Object ACLs. By default, an object is set to private after it is replicated to the destination bucket.

* Appendable objects.

* Objects stored in Archive, Cold Archive, or Deep Cold Archive.

* Objects with deletion marks.

* Object delete operations.

* Lifecycle rules.

* Expiration times of objects.


<span id="34QOthne"></span>
## Precautions


|Category |Precautions |
|---|---|
|Billing |SRR will calculate the number of requests and generate corresponding request fees for each synchronized object, without charging traffic fees. For billing details, please refer to the [Requests](https://docs.byteplus.com/docs/tos/docs-request-fee). |
|Permissions |During the copying process, do not delete the read and write permissions of the source and destination buckets by TOS service, otherwise it will cause the object copying to fail. |
|Number of rules |The total number of SRR rules for a bucket cannot exceed 100. |
|Object size |When copying within the same region, the object size cannot exceed a certain limit, as explained below:<br><br><br>* Non\-multipart object: can replicate up to 5GiB.<br><br>* Multipart object: Maximum copy size is 48.8TiB (each chunk maximum 5GiB, maximum 10000 chunks). |
|Operation restriction |* Versioning<br><br>   * Only when the versioning status of the source and destination buckets is the same, and both are in either disabled or enabled state, can a SRR rule be created. It is not supported to create a SRR rule when the buckets are in a paused state. If both the source and destination buckets have versioning enabled, multiple versions of objects can be replicated to the destination bucket.<br><br>   * After enabling cross\-region replication, do not modify the versioning status of the source and destination buckets, as this may cause synchronization failures and other issues. If you want to modify the versioning status of the source bucket, you should delete the replication rule first before making any changes.<br><br>* Behavior restrictions<br><br>   * Copying transfer between buckets is not supported, meaning if you create a rule to copy objects from bucket A to bucket B, and then from bucket B to bucket C, the objects copied from bucket A to bucket B will not be copied to bucket C.<br><br>   * Inter\-bucket replication is not supported, meaning if you create a rule to replicate objects from bucket A to bucket B, and then from bucket B to bucket A, objects copied from bucket A to bucket B will not be replicated back to bucket A. |
|Object overwrite risk |If you operate both the source bucket and the destination bucket at the same time, the same\-named objects written to the destination bucket may be overwritten by the same\-named objects in the source bucket. |
|Object replication order |When copying objects, the order of object copying cannot be controlled. It is recommended that you verify the integrity of the data by comparing the number of objects in the directory. |


<span id="acb0830d"></span>
## Instructions for use

You can copy objects from one bucket to another within the same account, or from one account to another. For specific instructions, please refer to [Same-account same-region replication](https://docs.byteplus.com/docs/tos/Same-region-replication-within-the-same-account) and [Cross-account same-region replication](https://docs.byteplus.com/docs/tos/Same-region-replication-across-accounts).
