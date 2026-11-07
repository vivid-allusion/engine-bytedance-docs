---
title: "Introduction to Python SDK"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Python-sdk-introduction"
---

This article introduces the usage methods, interface definitions, and parameter explanations of the BytePlus Torch Object Storage Python SDK in various scenarios.

Explanation.

<span id="e13ada5d"></span>
## Precautions

In multi\-process scenarios, create multiple TosClients instead of sharing one TosClient to avoid concurrency issues that may cause data to be corrupted during read and write requests.

<span id=".56S65L6L5Luj56CB"></span>
## Example code

The SDK provides example code for bucket and object operations for your reference.


|Category ||Reference |
|---|---|---|
|Preparation for use ||* [Install SDK](https://docs.byteplus.com/docs/tos/Install-the-python-sdk)<br><br>* [Initialize client](https://docs.byteplus.com/docs/tos/Initializing-the-client-side-python-sdk)<br><br>* [Get started quickly](https://docs.byteplus.com/docs/tos/Quick-start-python-sdk) |
|Bucket interface |Basic bucket interface |* [Create bucket](https://docs.byteplus.com/docs/tos/Create-a-bucket-python-sdk)<br><br>* [List buckets](https://docs.byteplus.com/docs/tos/List-buckets-python-sdk)<br><br>* [Get bucket metadata](https://docs.byteplus.com/docs/tos/Get-bucket-metadata-python-sdk)<br><br>* [Delete bucket](https://docs.byteplus.com/docs/tos/Delete-bucket-python-sdk)<br><br>* [Get bucket region](https://docs.byteplus.com/docs/tos/Get-the-bucket-region-python-sdk) |
||Manage bucket configuration |* [Manage bucket ACL](https://docs.byteplus.com/docs/tos/Manage-bucket-acl-python-sdk)<br><br>* [Manage bucket policy](https://docs.byteplus.com/docs/tos/Manage-bucket-strategy-python-sdk)<br><br>* [Manage bucket storage type](https://docs.byteplus.com/docs/tos/Manage-bucket-storage-types-python-sdk)<br><br>* [Manage bucket lifecycle](https://docs.byteplus.com/docs/tos/Manage-the-bucket-lifecycle-python-sdk)<br><br>* [Manage image origin retrieval](https://docs.byteplus.com/docs/tos/Manage-image-return-to-source-python-sdk)<br><br>* [Manage cross-origin resource sharing](https://docs.byteplus.com/docs/tos/Manage-cross-origin-resource-sharing-python-sdk)<br><br>* [Manage cross-region replication](https://docs.byteplus.com/docs/tos/Manage-cross-region-replication-python-sdk)<br><br>* [Manage website configuration](https://docs.byteplus.com/docs/tos/Manage-website-configuration-python-sdk)<br><br>* [Manage event notifications](https://docs.byteplus.com/docs/tos/Managing-event-notifications-python-sdk)<br><br>* [Manage custom domains](https://docs.byteplus.com/docs/tos/Manage-custom-domains-python-sdk)<br><br>* [Manage real-time logs](https://docs.byteplus.com/docs/tos/Manage-real-time-logs-python-sdk) |
|Object interface |Upload object |* [Standard upload](https://docs.byteplus.com/docs/tos/Normal-upload-python-sdk)<br><br>* [Append upload](https://docs.byteplus.com/docs/tos/Append-upload-python-sdk)<br><br>* [Multipart upload](https://docs.byteplus.com/docs/tos/Shard-upload-python-sdk)<br><br>* [Resumable upload](https://docs.byteplus.com/docs/tos/Breakpoint-resumption-python-sdk) |
||Download object |* [Normal download](https://docs.byteplus.com/docs/tos/Normal-download-python-sdk)<br><br>* [Conditional download](https://docs.byteplus.com/docs/tos/Limited-download-python-sdk)<br><br>* [Range download](https://docs.byteplus.com/docs/tos/Scope-download-python-sdk)<br><br>* [Resumable download](https://docs.byteplus.com/docs/tos/Breakpoint-resume-download-python-sdk) |
||Copy object |* [Standard copy](https://docs.byteplus.com/docs/tos/Normal-copy-python-sdk)<br><br>* [Multipart copy](https://docs.byteplus.com/docs/tos/Shard-copy-python-sdk)<br><br>* [Resumable copy](https://docs.byteplus.com/docs/tos/Breakpoint-continuation-copy-python-sdk) |
||List objects |* [List objects V2](https://docs.byteplus.com/docs/tos/List-objects-v2-python-sdk)<br><br>* [List objects](https://docs.byteplus.com/docs/tos/List-objects-python-sdk)<br><br>* [List multi-version objects](https://docs.byteplus.com/docs/tos/List-multi-version-objects-python-sdk)<br><br>* [List unmerged objects (list multipart upload tasks)](https://docs.byteplus.com/docs/tos/List-unmerged-objects-python-sdk) |
||Manage object |* [Manage object metadata](https://docs.byteplus.com/docs/tos/Manage-object-metadata-python-sdk)<br><br>* [Manage object access permissions](https://docs.byteplus.com/docs/tos/Manage-access-to-objects-python-sdk)<br><br>* [Delete object](https://docs.byteplus.com/docs/tos/Delete-objects-python-sdk)<br><br>* [Manage object tags](https://docs.byteplus.com/docs/tos/Manage-object-tags-python-sdk)<br><br>* [Restore object](https://docs.byteplus.com/docs/tos/Manage-object-tags-python-sdk) |
|Data processing |Image processing |* [Basic image processing](https://docs.byteplus.com/docs/tos/Basic-image-processing-python-sdk)<br><br>* [Retrieve image information](https://docs.byteplus.com/docs/tos/Get-image-information-python-sdk)<br><br>* [Abnormal image detection](https://docs.byteplus.com/docs/tos/Abnormal-image-detection-python-sdk)<br><br>* [Image storage](https://docs.byteplus.com/docs/tos/Image-processing-persistence-python-sdk) |
||Video processing |* [Video frame capture](https://docs.byteplus.com/docs/tos/Video-framing-python-sdk)<br><br>* [Video information acquisition](https://docs.byteplus.com/docs/tos/Get-video-information-python-sdk)<br><br>* [Video frame image persistence](https://docs.byteplus.com/docs/tos/Video-capture-image-persistence-python-sdk) |
|Others |Pre\-signing mechanism |* [Standard pre-signature](https://docs.byteplus.com/docs/tos/Restore-objects-python-sdk)<br><br>* [Post form pre-signature](https://docs.byteplus.com/docs/tos/Post-form-pre-signature-python-sdk) |
||Log configuration |[Log configuration](https://docs.byteplus.com/docs/tos/Logging-configuration-python-sdk) |
||Data security |[Data security](https://docs.byteplus.com/docs/tos/Data-security-python-sdk) |
|Typical scenario introduction ||* [Large object scenario](https://docs.byteplus.com/docs/tos/Large-object-scenes-python-sdk)<br><br>* [Directory scenario](https://docs.byteplus.com/docs/tos/Directory-scenes-python-sdk)<br><br>* [Multiple versions scenario](https://docs.byteplus.com/docs/tos/Multi-version-python-sdk)<br><br>* [Deletion scenario](https://docs.byteplus.com/docs/tos/Delete-the-scenes-python-sdk)<br><br>* [Move and rename scenario](https://docs.byteplus.com/docs/tos/Move-and-rename-scenes-python-sdk) |
|Troubleshooting ||[Exception handling](https://docs.byteplus.com/docs/tos/Exception-handling-python-sdk) |
