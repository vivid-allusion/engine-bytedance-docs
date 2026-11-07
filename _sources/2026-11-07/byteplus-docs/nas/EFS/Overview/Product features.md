---
title: "Product features"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Product_features"
---

This topic introduces the features of Elastic File Storage (EFS).

<span id="XuDooHVX"></span>
## Bandwidth modes

EFS offers two bandwidth modes: baseline bandwidth mode and provisioned bandwidth mode.


|Mode |**Use cases** |**Performance** |**Billing** |Features |
|---|---|---|---|---|
|Baseline Bandwidth mode |Suitable for workloads with basic performance requirements that need bandwidth to scale with storage capacity. |Supports up to 30 GB/s of bandwidth and 900,000 IOPS. |Billed based on storage capacity usage. |Billed based on storage capacity usage. |
|Provisioned Bandwidth mode |Suitable for workloads with predictable performance requirements. |Supports up to 2 TB/s read bandwidth and 30 million read IOPS. |Custom provisioned bandwidth is billed only for the portion exceeding the baseline. |* **Decoupled capacity and performance**: Baseline bandwidth scales linearly with capacity, while provisioned bandwidth can be configured independently of capacity.<br><br>* **Flexible on\-demand configuration**: Supports online enabling, upgrading, downgrading, and disabling of bandwidth to adjust values dynamically, addressing both sudden and long\-term performance changes.<br><br>* **Transparent, predictable costs**: Only bandwidth exceeding the baseline is billed, helping reduce storage expenses. |


<span id="L2LkxLxB"></span>
### Example scenarios


* Scenario 1: Inference scenario. Model weight files typically occupy tens of GiB to multiple TiBs of storage capacity (e.g., a 1 TiB model weight file to be loaded onto 100 GPU servers) but require fast loading to compute nodes when starting inference services.

   * With EFS Premium Tier in Baseline Bandwidth Mode, only 125 MB/s read bandwidth is available, resulting in a loading time of nearly 10 days or more.

   * With EFS Premium Tier in Provisioned Bandwidth Mode (provisioning 200 GB/s of bandwidth), loading completes in just 8.5 minutes.

* Scenario 2: Data preprocessing scenario. Files occupy 1 PiB of storage capacity and require 40 GB/s of read bandwidth.

   * With EFS Premium Tier in Baseline Bandwidth Mode, only 30 GB/s read bandwidth is available, which fails to meet the business requirement.

   * With EFS Premium Tier in Provisioned Bandwidth Mode (configured with 40 GB/s of provisioned bandwidth), 1 PiB of storage provides 30 GB/s of baseline bandwidth. You only pay for the additional 10 GB/s of provisioned bandwidth that exceeds the baseline.


<span id="qhy6TFsN"></span>
## Burst bandwidth

The burst bandwidth feature is an elastic capability designed to handle temporary high\-bandwidth demands. When baseline or provisioned bandwidth is insufficient, you can temporarily obtain extra bandwidth. Once enabled, the feature dynamically leverages idle cluster bandwidth resources, and performance automatically adjusts to workload pressure.


|**Use cases** |**Performance** |**Billing** |Features |
|---|---|---|---|
|Designed for bursty workloads with short\-duration high peaks and unpredictable traffic patterns. |Supports up to 60 GB/s burst read bandwidth. |Billed only for bandwidth exceeding both baseline and provisioned bandwidth, enabling flexible cost control. |* Optimized for burst high\-performance scenarios: If performance peaks of your workload are unpredictable or average throughput is 5% of the peak throughput or even less, we recommend that you enable burst bandwidth.<br><br>* On\-demand dynamic activation: Burst bandwidth can be enabled or disabled at any time to meet peak demand whenever needed. |


<span id="lw66gthh"></span>
### Example scenarios

In inference scenarios, initial batch loading of model weight files involves tens to hundreds of compute nodes. Additionally, temporary node expansions during runtime require new nodes to also load model weight files.


* With EFS Premium Tier in provisioned bandwidth mode (provisioned to 200 GB/s), loading a 1 TiB model weight file to 100 GPU servers takes just 8.5 minutes.

* Since the timing of new node additions is unpredictable, maintaining 200 GB/s of provisioned bandwidth continuously is unnecessary. Instead, you can lower the provisioned bandwidth to a reasonable level (e.g., 30 GB/s) and enable Burst Bandwidth (with a 60 GB/s upper limit) to handle unexpected temporary high\-bandwidth needs.


<span id="yIQJqbGA"></span>
## Access point

An access point is a file system directory\-level entry provided by EFS. You can access it via FSX. You can create multiple access points for each directory and configure different IAM policies and permission groups for these access points based on your business needs. This enables fine\-grained permission management for different clients and users on the same dataset.

The advantages of accessing the file system through access points are as follows:


* **Tenant isolation at the directory level**: Each access point corresponds to a root directory (a subdirectory of the file system). When you access the file system via the access point, you can only access data within the corresponding root directory.

* **Precise control over permissions**: Supports permission management based on IAM. You can configure IAM policies for access points and grant permissions to different IAM users or different IAM roles.

* **Simplified permission management**: Supports binding POSIX user information for role assumption. When accessing the file system through the access point, a unified POSIX user identity is used for reading and writing data.


<span id="G463R7TZ"></span>
## Mount target

The mount target is the file system\-level access entry provided by EFS. You can access it via NFS. You can create multiple mount targets for an EFS file system and configure different permission groups for these mount targets based on your business needs. This allows precise permission management for different clients on the same file system. Currently, EFS supports NFSv4.1 and NFSv3 protocol versions.

The main advantage of accessing the file system through mount target is **strong compatibility**. NFS is the most widely used access protocol in file storage. With its high compatibility, NFS can be deployed on almost any Linux operating system.

<span id="G463R7TZ"></span>
## Directory quota

The directory quota feature counts and limits the number of files and storage usage within a specified EFS directory.


* **Statistical quota**: Supports statistical feature. Provides file count and storage usage statistics for a specified directory in the file system.

* **Restricted quota**: Provides statistics and also restricted features. Limits the number of files and storage usage in a specified directory of the file system.


<span id="B9PpEgSK"></span>
## Monitoring alarm

EFS offers comprehensive monitoring, including file system\-level capacity and file count metrics, directory\-level capacity and file count metrics, file system\-level performance monitoring for bandwidth, IOPS, latency, and QPS, as well as access point\-level performance metrics. You can know comprehensively about the running state of file system.

<span id="M10aMfnP"></span>
## Permission group

A permission group is a mechanism provided by EFS that allows for precise management of permissions over clients via IP addresses or CIDR blocks. Permission groups must be associated with access points or mount targets.


* Default permission group: Grants full access (including read/write and unrestricted Linux system user access rights) to any IP address within the VPC that can access the mount targets or access points.

* Custom permission group: Enables you to create permission groups. You can grant different access levels (read\-only or read/write) to specific client IPs or subnets based on different business requirements.


<span id="PfzBD6QO"></span>
## DataFlow

The DataFlow feature allows you to synchronize data bidirectionally between EFS and Torch Object Storage (TOS). You can easily export cold data from EFS to TOS and import data from TOS back to EFS. To meet various data transfer and management needs, DataFlow offers two configuration options: **DataFlow policies** and **DataFlow tasks**.


* **DataFlow policy**: After a policy is created, the system loads metadata of all files within the TOS bucket or bucket prefix associated with the policy into EFS at once. When a user or application accesses files through EFS and the data already exists, the system returns the data directly. If the data is absent in EFS, the system automatically loads the data from TOS to EFS. You can access the data in real time, without having to wait for the load to finish. These policies support bidirectional data transfer and run automatically based on configured import, export, or eviction rules. In the event of a file name conflict, the most recently added file is retained by default.

* **DataFlow task**: This method executes a one\-time, unidirectional data transfer between EFS and TOS, depending on the selected task type and its corresponding rules. It supports import, export, and eviction tasks. For import tasks, both the metadata and the data must be imported together. If there are file name conflicts, you can choose to skip the conflicting file, keep the most recent version, or overwrite the existing file.
