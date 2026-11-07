---
title: "Introduction to the C++ SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/C-sdk-introduction"
---

This document presents the usage methods, interface definitions, and parameter descriptions of the Volcengine Object Storage Service (TOS) C++ SDK across various scenarios.

The SDK provides sample code for bucket and object operations to facilitate your reference and use.

<span id=".c2RrLeamguiniA=="></span>
## SDK Overview


|Project ||Reference Document |
|---|---|---|
|Preparation for Use ||* [Installing the SDK](https://docs.byteplus.com/docs/tos/Install-c-sdk)<br><br>* [Initialize Client](https://docs.byteplus.com/docs/tos/Initialize-client-side-c-sdk)<br><br>* [Quick Start Guide](https://docs.byteplus.com/docs/tos/Quick-start-c-sdk) |
|Storage Bucket Interface |Bucket Basic Interface |* [Create Bucket](https://docs.byteplus.com/docs/tos/Create-bucket-c-sdk)<br><br>* [Enumerating Buckets](https://docs.byteplus.com/docs/tos/List-buckets-c-sdk)<br><br>* [Retrieve Bucket Metadata](https://docs.byteplus.com/docs/tos/Get-bucket-metadata-c-sdk)<br><br>* [Delete Bucket](https://docs.byteplus.com/docs/tos/delete-bucket-c-sdk)<br><br>* [Retrieve Bucket Region](https://docs.byteplus.com/docs/tos/Get-the-bucket-region-c-sdk) |
||Managing Bucket Configuration |* [Managing Bucket ACLs](https://docs.byteplus.com/docs/tos/Manage-bucket-acl-c-sdk)<br><br>* [Bucket Management Policy](https://docs.byteplus.com/docs/tos/Manage-bucket-policy-c-sdk)<br><br>* [Managing Bucket Storage Classes](https://docs.byteplus.com/docs/tos/Manage-bucket-storage-c-sdk)<br><br>* [Managing Bucket Lifecycle](https://docs.byteplus.com/docs/tos/Manage-the-bucket-lifecycle-c-sdk)<br><br>* [Managing Mirror Origin Fetch](https://docs.byteplus.com/docs/tos/Manage-image-return-to-source-c-sdk)<br><br>* [Managing Cross-Origin Resource Sharing](https://docs.byteplus.com/docs/tos/Manage-cross-origin-resource-sharing-c-sdk)<br><br>* [Managing Cross-Region Replication](https://docs.byteplus.com/docs/tos/Manage-cross-region-replication-c-sdk)<br><br>* [Managing Website Configuration](https://docs.byteplus.com/docs/tos/Manage-site-configuration-c-sdk)<br><br>* [Management Event Notification](https://docs.byteplus.com/docs/tos/Manage-event-notifications-c-sdk)<br><br>* [Managing Custom Domain Names](https://docs.byteplus.com/docs/tos/Manage-custom-domain-names-c-sdk)<br><br>* [Managing Real-Time Logs](https://docs.byteplus.com/docs/tos/Manage-real-time-logs-c-sdk) |
|Object Interface |Upload Object |* [Standard Upload](https://docs.byteplus.com/docs/tos/Normal-upload-c-sdk)<br><br>* [Additional Upload](https://docs.byteplus.com/docs/tos/Append-upload-c-sdk)<br><br>* [Multipart Upload](https://docs.byteplus.com/docs/tos/Shard-upload-c-sdk)<br><br>* [Breakpoint Resume](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-c-sdk) |
||Download Object |* [Standard Download](https://docs.byteplus.com/docs/tos/Normal-download-c-sdk)<br><br>* [Conditional Download](https://docs.byteplus.com/docs/tos/Limited-download-c-sdk)<br><br>* [Range Download](https://docs.byteplus.com/docs/tos/Scope-download-c-sdk)<br><br>* [Resumable Download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-c-sdk) |
||Copy Object |* [Standard Copy](https://docs.byteplus.com/docs/tos/Normal-copy-c-sdk)<br><br>* [Shard Copy](https://docs.byteplus.com/docs/tos/Shard-copy-c-sdk)<br><br>* [Breakpoint Resume Copy](https://docs.byteplus.com/docs/tos/Breakpoint-resume-copy-c-sdk) |
||Enumerated Objects |* [Enumeration Object V2](https://docs.byteplus.com/docs/tos/List-objects-v2-c-sdk)<br><br>* [Enumeration of Objects](https://docs.byteplus.com/docs/tos/List-objects-c-sdk)<br><br>* [Listing Objects with Multiple Versions](https://docs.byteplus.com/docs/tos/List-multiversion-objects-c-sdk)<br><br>* [List Multipart Upload Tasks](https://docs.byteplus.com/docs/tos/List-shard-upload-tasks-c-sdk) |
||Management Object |* [Managed Object Metadata](https://docs.byteplus.com/docs/tos/Manage-object-meta-information-c-sdk)<br><br>* [Managed Object Read/Write Permissions](https://docs.byteplus.com/docs/tos/Manage-object-read-and-write-permissions-c-sdk)<br><br>* [Delete Object](https://docs.byteplus.com/docs/tos/Delete-object-c-sdk)<br><br>* [Managed Object Tags](https://docs.byteplus.com/docs/tos/Manage-object-labels-c-sdk)<br><br>* [Recovery Object](https://docs.byteplus.com/docs/tos/Restore-objects-c-sdk) |
|Other |Pre\-Signed Mechanism |* [Standard Pre-Signature](https://docs.byteplus.com/docs/tos/Normal-pre-signature-c-sdk)<br><br>* [Presigned POST Form](https://docs.byteplus.com/docs/tos/Post-form-Presignature-c-sdk) |
||Log Configuration |[Log Configuration](https://docs.byteplus.com/docs/tos/log-configuration-c-sdk) |
||Data Security |[Data Security](https://docs.byteplus.com/docs/tos/Data-security-c-sdk) |
|Introduction to Typical Scenarios ||* [Large Object Scenario](https://docs.byteplus.com/docs/tos/Large-object-scenes-c-sdk)<br><br>* [Table of Contents Scenario](https://docs.byteplus.com/docs/tos/Catalog-scenes-c-sdk)<br><br>* [Multi-Version Scenario](https://docs.byteplus.com/docs/tos/Multi-version-scenes-c-sdk)<br><br>* [Delete Scenario](https://docs.byteplus.com/docs/tos/Delete-scenes-c-sdk)<br><br>* [Move and Rename Scenario](https://docs.byteplus.com/docs/tos/Move-and-rename-scenes-c-sdk) |
|Fault Handling ||[Exception Handling](https://docs.byteplus.com/docs/tos/Exception-handling-c-sdk) |
