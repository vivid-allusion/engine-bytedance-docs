---
title: "Overview of best practices"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Best-practice-overview"
---

This topic provides an overview of the best practices for using TOS to more effectively address business demands.

<span id="3994cf3a"></span>
## Accessing TOS with third\-party tools


|Best practices |Description |
|---|---|
|[Accessing TOS with Rclone](https://docs.byteplus.com/docs/tos/docs-accessing-tos-with-rclone) |Rclone is a powerful open source command\-line tool that supports interconnection with diverse cloud storage systems (including S3\-compatible object storage systems) for data upload, download, synchronization, management, and more. This article introduces the steps to install and configure the Rclone tool and common commands for accessing TOS using Rclone. |
|[Managing TOS resources with S3 Browser](https://docs.byteplus.com/docs/tos/docs-managing-tos-resources-with-s3-browser) |S3 Browser is a free [Amazon S3](https://docs.byteplus.com/docs/tos/Best-practice-overview) Windows client tool. Since BytePlus TOS is compatible with the S3 protocol, you can use S3 Browser to manage your TOS resources. This article explains the steps to install and configure the S3 Browser tool, as well as common commands for accessing TOS using S3 Browser. |
|[Access TOS with Flutter SDK](https://docs.byteplus.com/docs/tos/Access-tos-with-flutter-sdk) |The community supports TOS with the Flutter SDK, which is published on the pub.dev repository. You can use the Flutter SDK to access TOS for uploading and downloading resources.  |


<span id="c2820e60"></span>
## Granting temporary access


|Best Practices |Description |
|---|---|
|[Using pre-signed URLs for secure data downloads](https://docs.byteplus.com/docs/tos/Use-temporary-authorization-url-to-enable-secure-data-download) |In scenarios such as video surveillance, apps, and web applications, many images, files, and videos need to be uploaded to the server or downloaded for local use. In this scenario, TOS offers a solution using temporary authorization URLs for secure data downloads, explaining how to generate temporary URLs for objects and how clients send requests. |
|[Accessing TOS with temporary credentials of Security Token Service](https://docs.byteplus.com/docs/tos/Accessing-tos-with-temporary-credentials-of-security-token-service) |In scenarios where files are uploaded directly to object storage from mobile apps or PC clients, for security reasons, do not embed permanent AK/SK in the client code. Instead, the application server obtains temporary AK/SK via the STS mechanism and then distributes these temporary credentials to the client. This article describes the process and steps for using temporary AK/SK and Token via STS to access BytePlus TOS. |


<span id="66d120fb"></span>
## Data migration


|Best practices |Description |
|---|---|
|[Online migration based on non-disruptive business](https://docs.byteplus.com/docs/tos/Online-migration-based-on-non-disruptive-business) |If your business already runs on other third\-party services, ensure business stability when migrating to TOS to avoid damage caused by data migration. This article explains the solution and steps for online migration of data from third\-party services to TOS without business interruption. |


<span id="776cc3eb"></span>
## Checking data integrity


|Best practices |Note |
|---|---|
|[Verifying the integrity of uploaded objects](https://docs.byteplus.com/docs/tos/Verify-consistency-of-the-uploaded-object) |During data upload with TOS, data inconsistency may occur due to external network hijacking or data caching outside TOS during public network transmission. TOS offers multiple features related to data consistency. You can ensure upload consistency using Content\-MD5, Content\-SHA256, or CRC64. This article introduces the verification flowchart and sample code for checking uploaded object consistency. |
|[Verifying the integrity of downloaded objects](https://docs.byteplus.com/docs/tos/Verify-the-consistency-of-the-downloaded-object) |When downloading data using TOS, issues like data inconsistency may occur due to external network hijacking or data caching during public network transmission outside TOS. You can use CRC64 to verify the consistency of downloaded objects. This article introduces solutions and sample code for verifying the consistency of downloaded objects. |


<span id="YfRgQW0U"></span>
## Performance optimization


|Best practices |Description |
|---|---|
|[Best practices for optimizing performance](https://docs.byteplus.com/docs/tos/Performance-optimization-plan) |If you use sequential prefixes (such as chronological or alphabetical order) in the object naming convention within a bucket, it may cause a large number of object access requests to concentrate on a specific partition, creating a partition access hotspot. The service capacity of a hot partition is limited by the read/write limits of the storage medium, which could lead to reduced request rates. You can refer to the methods listed in this article to optimize your application performance. This article introduces best practices, based on the internal implementation of TOS, for achieving high performance with your applications. |
|[Benchmarking TOS performance using COSBench](https://docs.byteplus.com/docs/tos/COSBench-user-guide) |COSBench (Cloud Object Storage Benchmark) is a benchmarking tool developed by the Intel team in Java to measure object storage service performance. You can use the COSBench tool to test read and write performance for TOS, helping you evaluate the performance of object storage TOS and ensure business stability. |


<span id="Orq1ptNu"></span>
## Others


|Best Practices |Note |
|---|---|
|[Compatibility with the Amazon S3 protocol](https://docs.byteplus.com/docs/tos/docs-compatibility-with-amazon-s3) |Object storage TOS supports AWS S3 protocol compatibility, allowing applications that previously accessed any S3\-compatible storage to switch almost seamlessly to TOS after migrating data. This topic describes how to switch the access destination and provides TOS\-compatible S3 APIs. |
|[Uploading data from WeChat Mini Programs to TOS](https://docs.byteplus.com/docs/tos/Upload-data-directly-to-TOS-from-wechat-mini-program) |WeChat mini programs, as applications that do not require downloading, attract more and more developers and users. How to upload files from WeChat Mini Programs to TOS is a key concern for developers. This article explains the steps to directly upload files to TOS within the WeChat Mini Program environment. |
|[Uploading data from web browsers to TOS](https://docs.byteplus.com/docs/tos/Web-direct-upload-practice) |You can use the PostObject interface to directly upload files in HTML form format from the web client to TOS. The signature required for the upload can be obtained from the server side. |
|[Accessing and storing TOS data in PyTorch jobs](https://docs.byteplus.com/docs/tos/Accessing-and-storing-tos-data-in-Pytorch-tasks) |Accessing and storing TOS data in PyTorch tasks. |
|[Accessing TOS through an ECS reverse proxy](https://docs.byteplus.com/docs/tos/Use-ecs-instance-to-reverse-proxy-tos) |You can configure an Nginx reverse proxy server on an ECS instance to access files in a TOS bucket by connecting to port 80 of the ECS instance's public IP address, thereby enabling access to resources within the TOS object storage using a fixed IP address. |
