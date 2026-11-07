---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/overview"
---

tosutil is a command\-line tool for accessing and managing TOS. This tool allows batch data processing between local storage and TOS to support common scenarios such as migrating small and medium local data to the cloud, downloading cloud data locally, and integrating automated script tasks.

<span id=".5LiL6L295LiO5a6J6KOF"></span>
## Download and Installation

For the download link and installation instructions of tosutil, see [Download and Installation](https://docs.byteplus.com/docs/tos/Download-and-install).

<span id=".5Yqf6IO95qaC6L-w"></span>
## Function Overview

The common commands of the tosutil tool are as follows.


|Type |command |Description |
|---|---|---|
|Common commands |[ls](https://docs.byteplus.com/docs/tos/List-the-resources-under-the-account-ls#3558fadd) |List buckets, objects within buckets, or multipart upload tasks within buckets. |
||[mkdir](https://docs.byteplus.com/docs/tos/Create-folder-mkdir#c35ac863) |Create folder. |
||[du](https://docs.byteplus.com/docs/tos/Calculate-object-and-sharding-size-and-quantity-du#8ba54f37) |Calculate the size and number of objects and shards in the bucket. |
||[mb](https://docs.byteplus.com/docs/tos/Create-bucket) |Create a new bucket with the specified name and parameters. |
||[cp](https://docs.byteplus.com/docs/tos/Overview2) |Upload, download, or copy objects. |
||[setmeta](https://docs.byteplus.com/docs/tos/Set-object-metadata-setmeta) |Set object metadata. |
||[stat](https://docs.byteplus.com/docs/tos/Query-properties-stat) |Query bucket or object properties. |
||[rm](https://docs.byteplus.com/docs/tos/Delete-a-bucket-object-or-shard-upload-task-rm) |Delete buckets, objects, or multipart upload tasks. |
||[share](https://docs.byteplus.com/docs/tos/Create-authorization-code-share-crt) |Create an authorization code for the object to be shared, and use the authorization code to list or download the object. |
||[set-acl](https://docs.byteplus.com/docs/tos/Set-a-predefined-access-policy-for-a-bucket-or-object-set-acl#9b092155) |Set predefined access policies for buckets or objects. |
||[mount](https://docs.byteplus.com/docs/tos/The-mount-bucket-is-a-local-file-system-directory-mount#cd767bb5) |Mount the bucket as a local file system directory. |
|Auxiliary commands |[config](https://docs.byteplus.com/docs/tos/View-or-update-the-configuration-file-config) |View configuration file path and update key configuration information in the configuration file. |
||[help](https://docs.byteplus.com/docs/tos/View-support-commands-or-help-documentation) |view command help. |
||[probe](https://docs.byteplus.com/docs/tos/Test-network-speed-probe) |Test upload and download speeds. |
||[netdig](https://docs.byteplus.com/docs/tos/One-click-network-diagnostics-netdig#c7603de5) |supports one\-click network diagnostics.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This command supports only Linux and macOS.</div><br> |
||[hash](https://docs.byteplus.com/docs/tos/Calculate-the-file-hash) |Calculate the file hash value. |
||[fcp](https://docs.byteplus.com/docs/tos/Copy-local-files-fcp#1394b87b) |copy local files or folders. |
||[clear](https://docs.byteplus.com/docs/tos/Delete-breakpoint-log-file-clear) |Delete breakpoint record files in the specified folder and attempt to perform cloud\-side cleanup. |
||[version](https://docs.byteplus.com/docs/tos/Check-the-tool-version) |Check the version number. |
||[ping](https://docs.byteplus.com/docs/tos/Measuring-network-latency-ping#5f7eca0d) |Measure network latency. |
||[connect](https://docs.byteplus.com/docs/tos/Calculate-network-connection-time-connect#b110e678) |calculate network connection latency. |
||[traceroute](https://docs.byteplus.com/docs/tos/Scraping-the-network-traceroute#3ad9a74c) |Fetch network path. |
||[curl](https://docs.byteplus.com/docs/tos/Send-http-request-curl#b048c772) |send HTTP request. |


<span id=".5bi46KeB56S65L6L"></span>
## Common Examples

TOS provides example commands for common scenarios. Refer to the following documents to choose suitable commands:


* [Object Upload Example](https://docs.byteplus.com/docs/tos/Upload-object-example)

* [download object example](https://docs.byteplus.com/docs/tos/Download-object-example)

* [delete object example](https://docs.byteplus.com/docs/tos/Delete-object-example)


<span id="5a1686eb"></span>
## frequently asked questions

TOS provides FAQs and error code explanations for the tosutil tool. You can refer to the following documents for troubleshooting:


* [tosutil tool FAQs](https://docs.byteplus.com/docs/tos/Tosutil-tool-faq)

* [tosutil tool error code explanations](https://docs.byteplus.com/docs/tos/Tosutil-tool-error-code-description)
