---
title: "What is Elastic File Storage (EFS)"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/What_is_Elastic_File_Storage"
---

BytePlus Elastic File Storage (EFS) is a fully managed cloud\-native elastic file storage service designed for both AI and traditional NAS workloads. It is designed for both AI and traditional NAS workloads.

<span id="05cRNhU8"></span>
## Product overview

EFS, based on standard POSIX semantics, provides a high\-performance file storage client FSX for AI business scenarios, and mainstream protocols NFSv4.1 and NFSv3 for traditional NAS scenarios. It seamlessly integrates with various AI training and inference frameworks, Linux operating systems, and applications, providing a user experience consistent with local file systems.

<span id="YXN95BYL"></span>
## Product advantages

EFS not only inherits the advantages of traditional elastic file storage, but also adopts a new design language. This greatly enhances the capabilities of public cloud file storage.


* **Elastic capacity scaling**: Zero base capacity; 4KiB scaling increments; 10PiB of maximum capacity for a single instance; pay\-as\-you\-go billing.

* **Mainstream access protocols**: Standard NFSv4.1 and NFSv3 protocols, seamlessly integrating with cloud servers and container services.

* **Performance configuration on demand**: EFS provides a new file storage performance delivery mode; supports on\-demand performance configuration and decouples performance from capacity; meets the requirements for high\-throughput sequential reads on small capacity for AI inference, and high\-throughput reads and writes for model training, with a single file system instance supporting up to TB/s throughput.

* **High\-performance client**: FSX client cache performance reaches up to 45GB/s; supports high\-throughput data processing capabilities; enables significant acceleration for large\-scale AI model training.

* **Hundreds of billions of files capacity**: A single file system instance supports up to one billion files by default; the advanced version can handle hundreds of billions of files.

* **Computing ecosystem integration**: EFS deeply integrates with cloud servers, container services, and machine learning platforms; delivers end\-to\-end solutions for AI training and inference scenarios to accelerate business deployment.
