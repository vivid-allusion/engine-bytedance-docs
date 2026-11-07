---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Cross-region-replication-overview"
---

Cross region replication refers to automatically copying files from one bucket to other buckets in different regions. It supports filtering the copied files as needed to view the replication progress.

<span id="d8694d43"></span>
## Usage scenario


* Compliance requirements

   TOS supports storing your data in multiple Availability Zones in the same geography, but some industries may have compliance requirements that require data to be stored in different geographies. With cross\-region replication, you can replicate data between geographies at a distance to meet compliance requirements.

* Data backup and disaster recovery

   In order to prevent data loss, you can backup data in different regions through cross\-regional replication to improve the disaster tolerance of data against various possible factors.

* Reduce access latency

   To minimize access latency, you need to reduce the physical distance your data needs to span, at which point you can use cross\-region replication to maintain a copy of the object in the bucket closest to the customer's geographic location.

* Data migration

   Due to business needs, data is migrated from one TOS region to another.

* Operational requirements

   If you have compute clusters in two different TOS geographies that need to analyze the same set of objects, you can use cross\-region replication to maintain copies of objects in those geographies.


<span id="57qaQhh1"></span>
## What does CRR replicate?

<span id="RXQDqbMu"></span>
### What is replicated with CRR?

CRR replicates the following information about objects: content, size, last modified time, creator, version number, user\-defined metadata, and storage type. The following types of objects can be automatically replicated via a CRR rule:


* Objects that exist before the CRR rule takes effect.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the CRR rule does not synchronize existing objects. To do so, turn on the "Sync historical object" option in the rule.   </div>
   

* Objects uploaded after the CRR rule takes effect.

* Object overwrite operations. If an object in the source bucket is overwritten after replication, the overwrite operation will be synchronized again with the destination bucket.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Only object overwrite operations will be synchronized again to the destination bucket for objects that have already been successfully replicated. Changes to object metadata, object access control lists (ACLs), and storage type will not be synchronized to the destination bucket.   </div>
   

<span id="2Rg6sePf"></span>
### What is not replicated with CRR?


* Object ACLs. By default, an object is set to private after it is replicated to the destination bucket.

* Appendable objects.

* Objects stored in Archive, Cold Archive, or Deep Cold Archive.

* Objects with deletion marks.

* Object delete operations.

* RenameObject operations.

* Lifecycle rules.

* Expiration times of objects.

* Null objects.


<span id="33e2c83b"></span>
## Replication state

Replication status can help you understand the current state of the object being copied. You can view the cross\-region replication status on the **File details** page, as follows:


* If the file is a source object copied across regions, the **Waiting for copy** , **Failed to copy, Copy complete** status is displayed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The ability to view the replication status of cross\-region replicated source objects is currently available for beta testing. If you need to use this feature, please contact your account manager.   </div>
   

* If the file is a target object copied across regions, the copied object is displayed.

* Displays  **\-**  if the file is not the source or destination object copied across regions.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can also use the GetObject and HeadObject interfaces to query the cross\-region replication status of an object. For details, see <a href="https://docs.byteplus.com/docs/tos/reference--getobject">GetObject</a> and <a href="https://docs.byteplus.com/docs/tos/reference-headobject">HeadObject</a>.</div>


<span id="5e401348"></span>
## Precautions


|**Category** |**Precautions** |
|---|---|
|Billing |For each file synchronized by the cross\-region replication function, TOS will calculate the number of requests and generate the corresponding request fee, and will also charge the outflow traffic fee of the source bucket. For billing details, see [Request Fee](https://docs.byteplus.com/docs/tos/docs-request-fee) and [Traffic Fee](https://docs.byteplus.com/docs/tos/docs-traffic-fee). |
|Number of rules |The total number of cross\-region replication rules and same\-region replication rules for a bucket cannot exceed 100. |
|Permission |During the replication process, do not remove the TOS service's read and write permissions to the source and destination buckets, as this will cause object replication to fail. |
|File size |When copying across regions, the file size cannot exceed a certain limit, as follows:<br><br><br>* Non\-sharding objects: can replicate up to 5GiB.<br><br>* Sharding objects: can replicate up to 48.8TiB (maximum 5GiB per sharding, maximum number of shardings 10,000). |
|Operational restrictions |* Version control<br><br>   * Cross\-regional replication rules can only be created if the source and target buckets have the same version control state, and both are in the unopened or on state. In the suspended state, cross\-regional replication rules are not supported. If both the source and target buckets have versioning enabled, copying multiple versions of objects to the target bucket is supported.<br><br>   * After enabling cross\-region replication, do not modify the version control status of the source and destination buckets, as this may result in synchronization failures and other issues. If you want to modify the versioning state of the source bucket, you should delete the replication rule before modifying it.<br><br>* Multi\-AZ<br><br>   When you copy a file to a single AZ bucket using cross\-region copy, the file becomes a single AZ file, and when you copy to multiple AZ buckets, the file becomes a multi\-AZ file.<br><br>* Server level encryption<br><br>   Only objects encrypted with SSE\-TOS are supported in the North China 2 (Beijing) and East China 2 (Shanghai) regions. Copying SSE\-C, SSE\-KMS encrypted objects is not supported. If the file in the source bucket is encrypted with SSE\-TOS, the server level encryption method of the target bucket is SSE\-KMS, and the file will be encrypted with SSE\-TOS after being copied to the target bucket.<br><br>* RenameObject<br><br>   Cross\-region replication is not supported when RenameObject is enabled.<br><br>* Copy operation<br><br>   * Copy transfer between buckets is not supported, that is, if you create a rule that A buckets are copied to B buckets and B buckets are copied to C buckets, objects copied from A buckets to B buckets will not be copied to C buckets.<br><br>   * Replication between buckets is not supported, that is, if you create a rule that copies A buckets to B buckets and B buckets to A buckets, objects copied from A buckets to B buckets will no longer be copied to A buckets. |
|File overwrite risk |If you operate on both the source bucket and the target bucket, the object with the same name written by the target bucket may be overwritten by the object with the same name in the source bucket. |
|File copy order |When copying files, you cannot control the order in which the files are copied. It is recommended that you verify the integrity of the data by comparing the number of files in the directory. |
|Bandwidth and QPS limits |The default bandwidth of the cross\-regional replication link between the Chinese mainland and the Chinese mainland is 10Gbps and the QPS is 10000; the default bandwidth of the cross\-regional replication transmission acceleration link between the Chinese mainland and the Chinese mainland is 2Gbps and the QPS is 5000. If your business has greater bandwidth requirements, please contact technical support by submitting a ticket . |
|Replication between the Chinese mainland and other locations |Before replicating objects between the Chinese mainland and other locations, you must first enable transfer acceleration on the source bucket. For instructions, see [Enabling transfer acceleration](https://docs.byteplus.com/en/docs/tos/Transfer_acceleration?lang=en#e67c338c). |


<span id="97e9e8ac"></span>
## Same\-account and cross\-account CRR

Within the same account, you can copy objects across regions. You can also copy objects across different accounts. For instructions, see [Same-account cross-region replication](https://docs.byteplus.com/en/docs/tos/Cross-regional-replication-within-the-same-account) and [Cross-account cross-region replication](https://docs.byteplus.com/en/docs/tos/Cross-region-replication-across-account).

<span id="toOgel2P"></span>
## Related operations

After adding a CRR rule, you can use event notifications and logs to track new and updated objects in both the source and destination buckets. The instructions are as follows:


* Event notification: For an event notification rule, select `tos:ObjectReplication:ObjectCreated` and `tos:ObjectReplication:ObjectModified` as the event types. TOS will then deliver event notifications to the specified destination when a CRR rule adds or overwrites an object. For instructions, see [Configuring event notifications](https://docs.byteplus.com/en/docs/tos/Configuring-event-notifications).

* Logging: Use Torch Log Service to retrieve and analyze operation logs of objects. For instructions, see [Log analysis](https://docs.byteplus.com/en/docs/tos/Log-analysis).
