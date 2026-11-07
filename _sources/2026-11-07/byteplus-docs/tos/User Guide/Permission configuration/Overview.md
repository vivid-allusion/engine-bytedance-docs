---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs--overview"
---

By default, Torch Object Storage (TOS) buckets and objects are private. However, you can grant other users relevant permissions on these resources if you want them to access or manage your resources. TOS provides multiple authorization methods, including bucket policies, Identity and Access Management (IAM) policies, and Access Control Lists (ACLs). You can select appropriate methods based on your business requirements to ensure the security of your resources.

<span id="9199a01d"></span>
## Authorization methods

This topic describes how to configure permissions in different scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In general, we recommend that you configure permissions by using IAM policies or bucket policies.</div>


* <div data-tips="true" data-tips-type="tip">We also recommend that you select the same type of policies to facilitate further maintenance.</div>


* <div data-tips="true" data-tips-type="tip">If a configured permission does not take effect, we recommend that you retry later, as there is a delay.</div>




|**Authorization Method** |**Authorized User** |**Authorized Operation** |**Condition Supported** |**Applicable Scenario** |
|---|---|---|---|---|
|IAM policy |IAM user |All operations supported by TOS. |No |* Grant IAM users permissions on multiple cloud resources.<br><br>* Set the same permissions for multiple buckets.<br><br>* Authorize an IAM user to create buckets or obtain a list of buckets. |
|Bucket policy |* Account ID<br><br>* All users |All operations except for creating buckets and obtaining a list of buckets. For more information, see [Actions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#WhABJky8). |Yes. For more information, see [Conditions](https://docs.byteplus.com/en/docs/tos/docs-templates-and-parameters#nk9G2rUC). |* Authorize users of another account or all users.<br><br>* Set authorization conditions. |
|Bucket ACL |* Account ID<br><br>* All users |* Bucket read permission<br><br>* Read Permission and include object enumeration/multi\-paragraph enumeration<br><br>* Bucket write permission<br><br>* ACL read permission<br><br>* ACL write permission |No |Authorize users of another account or all users to read or write all objects in a bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only an account can authorize users of another account.</div><br> |
|Object ACL |* Account ID<br><br>* All users |* Private<br><br>* Public Read<br><br>* Public Read and Write |No |Grant all users the private, public\-read, or public\-read\-write permission on an object. |


<span id="6d9684e1"></span>
## Comparison of authorization methods

The following table compares different authorization methods. You can select appropriate methods based on your business requirements.


|**Parameter** |**Type** |**Bucket Policy** |**IAM Policy** |**ACL** |
|---|---|---|---|---|
|Principal (authorized user) |IAM users of the same account |✔️ |✔️ |❌ |
||Other accounts |✔️ |❌ |✔️ |
||IAM users of another account |✔️ |❌ |❌ |
||All users |✔️ |❌ |✔️ |
|Effect (authorization action) |Allow |✔️ |✔️ |✔️ |
||Deny |✔️ |✔️ |❌ |
|Resource (authorized resource) |All TOS resources |❌ |✔️ |❌ |
||A TOS bucket |✔️ |✔️ |✔️ |
||A group of specified TOS objects |✔️ |✔️ |❌ |
||An object in a TOS bucket |✔️ |✔️ |✔️ |
|Action (authorized operation) |Service\-level permissions (creating buckets or listing all buckets) |❌ |✔️ |❌ |
||Detailed permissions on buckets or objects |✔️ |✔️ |❌ |
||Read/write permission on buckets or objects |✔️ |✔️ |✔️ |
|Condition |Conditions supported by TOS |✔️ |❌ |❌ |


<span id="32f3547f"></span>
### Documents


* [Bucket policies](https://docs.byteplus.com/en/tos/docs/overview_5?version=1.0.0)

* [IAM policies](https://docs.byteplus.com/tos/docs/overview_6?version=1.0.0)

* [ACLs](https://docs.byteplus.com/en/tos/docs/overview_4?version=1.0.0)

* [Overview of common configuration scenarios](https://docs.byteplus.com/en/docs/tos/docs-overview_3)
