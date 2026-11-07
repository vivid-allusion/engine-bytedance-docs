---
title: "Product advantages"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Product_advantages"
---

Elastic File Storage (EFS) combines the deeply optimized file storage architecture with enterprise\-grade features designed for AI. It can meet current business needs and adapt to future technology trends.

<span id="9GCtogZS"></span>
## Elastic scaling

EFS adopts a cloud\-native architecture and supports elastic storage scaling. A single file system instance supports configuring capacity from zero to a maximum of 10 PiB. You can scale storage as needed at any time.

<span id="TtM8hK29"></span>
## Configurable performance

For common file storage, performance and capacity are often bound with each other. This means, to get higher performance or capacity, you need to purchase larger capacity or performance as well. This may lead to either wasted storage resources or performance. However, EFS breaks this binding. Through provisioned bandwidth mode and burst bandwidth feature, EFS enables independent performance and capacity allocation.

<span id="UDUFhooX"></span>
## High\-performance client

In high\-concurrency and large\-scale data transfer scenarios, traditional NFS clients are limited by protocol and cannot fully realize its potential of storage system capabilities. The FSX client, which was designed by BytePlus, is built on the FUSE (Filesystem in Userspace) architecture. It provides more efficient access to EFS.

<span id="U9b4Mo3M"></span>
## Hundreds of billions of files

The dataset that AI training relies on is often made up of massive numbers of small files (such as image samples from autonomous driving, NLP text fragments, and multimodal audio and video clips). The file counts can easily reach tens of billions. In AI scenarios, the file volume is large, files are fragmented and are in dynamic growth. Therefore, the one billion file limit of traditional storage is conflicting with file characteristics in AI scenarios. This limitation not only impedes data storage and business workflows, but also makes users adopt compromises like splitting data across multiple volumes or deleting files. This leads to performance degradation, increased costs, and greater management complexity. EFS breaks through this file storage limit. EFS supports hundreds of billions of files and effectively solves these problems, providing a scalable storage foundation for AI applications.

<span id="Ln3KxdpH"></span>
## Data security and reliability

EFS is a cloud\-native file storage solution with a fully in\-house developed architecture. Thanks to its multi\-level reliability architecture, it achieves data reliability of 99.999999999% (eleven nines) and service availability of 99.95%. It integrates the operation log audit service provided by Torch Log Service based on permission groups and access point IAM authentication. This ensures comprehensive data security.
