---
title: "What is hierarchical namespace"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/What-is-hierarchical-namespace"
---

A hierarchical namespace (HNS) bucket is a new type of bucket introduced by TOS. It uses a hierarchical structure to organize metadata. Besides its hierarchical namespace features, an HNS bucket can scale as much as a flat namespace (FNS) bucket. It also delivers seamless interoperability between object and file semantics. This allows **data to be accessed through multiple protocols**, so you can process data more efficiently.

HNS buckets can do everything FNS buckets can do, plus more. They support directory\-level mv and rename operations. They also improve common read operations, like List and Head for directories, to make data processing more efficient and faster. This makes them well\-suited for use cases in big data, data lakes, and AI.

<span id="a9f27159"></span>
## Supported regions

The following regions currently support hierarchical namespace:


* Asia Pacific (Johor)

* Asia Pacific (Jakarta)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you require usage in other regions, please <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001170">submit a ticket</a> or contact your account manager.</div>


<span id="e034b0d1"></span>
## Supported features

Currently, HNS buckets can be accessed via the TOS console, APIs, and SDKs. For details on the features supported by each method of access, see the following documents:


* [Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets)

* [API list (HNS buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket)

* [SDK overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Sdk-overview-hierarchical-bucket)

* [Tool overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Tool-overview-hierarchical-bucket)


<span id="eda289fc"></span>
## Benefits

Hierarchical namespace provides the following benefits:


* **Rapid integration**: Use TOS HNS buckets with your existing big data analytics applications, such as Hadoop and Spark, without making any modifications. With the proper configuration, TOS operates similarly to native HDFS, allowing you to leverage its extensive storage capacity, elastic scalability, security, reliability, and availability.

* **Protocol interoperability**: Data written to an HNS bucket via object semantics, such as the S3 API, can be read directly through HDFS\-compatible methods. Likewise, data written in HDFS can be read using object semantics. Besides its hierarchical namespace features, an HNS bucket can scale as much as an FNS bucket. It also delivers seamless interoperability between object and file semantics. This allows data to be accessed through multiple protocols, so you can process data more efficiently.

* **Performance optimization**: HNS buckets offer high\-performance, atomic directory and file operations. They significantly improve directory rename performance, completing the task in milliseconds for both large directories and files. Compared to FNS buckets, latency is reduced by over 99%.

* **Ecosystem compatibility**: HNS buckets easily integrate with various open\-source tools within the BytePlus ecosystem. This allows users to create flexible big data and AI pipelines based on TOS. They are compatible with the BytePlus big data platform and its components, including E\-MapReduce (EMR), Lake AI Service (LAS), Cloud File System (CloudFS), and Machine Learning Platform (AML), as well as open\-source tools such as Hadoop and Spark. They also support integration with leading cache solutions, such as JuiceFS and Alluxio.


<span id="67529d16"></span>
## Use cases

Below are some common scenarios in which you should consider using hierarchical namespace:


* Cloud\-native data lakehouse

* Offline/batch data analysis

* Real\-time data warehouse

* Data migration


<span id="299ae8dd"></span>
## Reference


* [Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets)

* [Usage notes](https://docs.byteplus.com/docs/tos/Usage-instructions)

* [Creating a bucket with hierarchical namespace enabled](https://docs.byteplus.com/docs/tos/Create-a-hierarchical-namespaces)

* [API list (HNS buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket)

* [Compatibility with the Amazon S3 protocol](https://docs.byteplus.com/docs/tos/docs-compatibility-with-amazon-s3)

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">TOS is compatible with the AWS S3 protocol. Once data is migrated from any S3\-compatible storage solution to TOS, applications that previously accessed that storage solution can seamlessly switch to TOS with minimal adjustments.   </div>
