---
title: "Supported tools (HNS buckets)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Tool-overview-hierarchical-bucket"
---

This article mainly introduces tool support for hierarchical namespace.

<span id="563435f7"></span>
## Background

This article only explains tools supporting HNS buckets. For details on other access method features, please refer to the following documents:


* [Supported console features (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets)

* [Supported APIs (HNS buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket)

* [Supported SDKs (HNS buckets)](https://docs.byteplus.com/docs/tos/Sdk-overview-hierarchical-bucket)


<span id="6060d2f2"></span>
## Notes

The symbols in the table are explained as follows:


* ✅ : indicates support for this feature.

* ✔️: indicates partial support; see remarks for details.

* ❌: indicates the feature is not supported.


<span id="70badc9a"></span>
## Supported tools


|Tool |Note |Support or not |Remarks |
|---|---|---|---|
|[tosutil](https://docs.byteplus.com/docs/tos/overview) |tosutil is a command\-line tool for accessing and managing TOS. Using this command\-line tool, you can batch process data between local storage and TOS to handle common scenarios such as migrating small to medium data to the cloud, downloading data from the cloud locally, and integrating automated script tasks. |✔️ |Version 4.0.0 and above of the tosutil tool supports HNS bucket features. For detailed tosutil functions, see [tosutil Overview](https://docs.byteplus.com/docs/tos/overview). |
|[TOS Browser](https://docs.byteplus.com/docs/tos/Overview3) |TOS Browser is a graphical management tool provided by TOS. Use this tool to manage buckets and objects. |✔️ |Creating HNS buckets using TOS Browser is currently unsupported. |
|[tos-import](https://docs.byteplus.com/docs/tos/Overview4) |TOS Import is a command\-line tool for data migration. You can deploy this tool on a local or cloud server, then use it to migrate local files, URL list files, or S3\-compatible object storage files to TOS. |❌ | |
|S3 Tool |An AWS S3\-compatible tool that allows you to manage resources in TOS buckets using S3 tools. |❌ |* **Support Information**:<br><br>   * Upload and download object interfaces compatible with the S3 protocol.<br><br>   * Support multipart interfaces.<br><br>   * Support ACL permission management for directories and objects.<br><br>   * Support lifecycle management.<br><br>   * List objects in the bucket: support both flat and hierarchical listing; hierarchical listing only supports using`/`as the delimiter.<br><br>* **Unsupported description**:<br><br>   * The delete interface does not support deleting non\-empty directories.<br><br>   * The batch delete interface currently does not support including directories.<br><br>   * HNS buckets strictly manage metadata in a "hierarchical" manner, distinguishing directory and file entities; standard S3 manages metadata in a "flat" manner with only one entity type: objects. These two management methods cause some differences: simply using object keys to simulate directory hierarchy differs from having an actual directory hierarchy system, such as deleting directories and listing subdirectories and files, which behave differently in the two types of buckets. Consult technical support before using third\-party S3\-compatible tools for business needs. |
|[DMS](https://docs.byteplus.com/docs/dms/What-is-data-migration-service) |DMS is an online storage migration service that helps transfer data from other cloud providers' object storage services to TOS online. It can also assist with data migration between TOS buckets. |✔️ |Currently, only migration from FNS buckets to HNS buckets is supported; migration from HNS buckets to FNS buckets is not supported. |
