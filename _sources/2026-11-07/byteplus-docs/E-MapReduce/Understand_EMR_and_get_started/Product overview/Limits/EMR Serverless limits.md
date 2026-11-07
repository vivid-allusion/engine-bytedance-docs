---
title: "EMR Serverless limits"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_limits"
---

<span id="1f829ff8"></span>
# Serverless queues

<span id="eb79d907"></span>
### **Resource quotas**


* The elastic portion of a dedicated queue must not exceed **MAX (100% of fixed CU count, 256 CU)** .

* The default upper limit for public queues is **1000 CU**. To request a higher quota, contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).

* To use GPU resources, contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).

* When specifying task resource specifications, a single Pod specification must not exceed 32 cores and 128 GB. The ratio of cores to memory must be kept within 1:8.


<span id="d90a2a91"></span>
### **Query performance**


* A single tenant supports up to **200 concurrent tasks** by default. To request more concurrency, contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).


<span id="5c2f7c15"></span>
### **Elastic scaling**


* For public queues and dedicated queues with elastic resources, resource allocation cannot be guaranteed in scenarios with high concurrency or limited resources, which may cause tasks to run slowly while waiting for resources.

* For scenarios requiring strong resource guarantees, it is recommended to use fixed resources in dedicated queues.


<span id="fc9592a4"></span>
### **Shuffle jobs**


* Queues use a shared Shuffle resource pool by default. The maximum Shuffle data volume per job is **100 TB**.

* Insufficient capacity during peak periods may cause job delays or failures. For heavy Shuffle scenarios, it is recommended to use an independent Shuffle cluster. To use this, contact Volcano Engine technical support by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).


<span id="1bfd9109"></span>
### **Small file merging and cleanup**


* EMR Serverless only provides computing capabilities and does not automatically merge small files or clean up expired files.

* Users must actively merge and clean up data. If not handled, fragmentation and redundancy may occur, increasing metadata and I/O overhead, which can lead to query latency and higher costs.


<span id="ffd6b509"></span>
### **Region and availability zone limits**

The service coverage is limited and is only available in the following specified availability zones.


* North China 2 (Beijing)

* East China 2 (Shanghai)

* Asia Pacific Southeast (Johor)


<span id="3bb114d6"></span>
# Serverless instances

<span id="c2d150eb"></span>
### Product services

**Region and availability zone restrictions**: Service coverage is limited and is only available in the following designated availability zones.


* North China 2 (Beijing)

* East China 2 (Shanghai)

* Asia Pacific Southeast (Johor)


<span id="00a93458"></span>
# Data recovery and accidental deletion prevention note

When using TOS object storage in an EMR environment, to avoid irreversible risks caused by unintended deletions, you must enable the corresponding security protection features based on the bucket type.


* Flat Bucket: You must enable versioning. After enabling, delete operations will only generate a "Delete Marker," and historical version data will remain, ensuring version rollback is possible after accidental deletion.

* Hierarchical Bucket: You must enable Recycle Bin. After enabling, files or directories deleted using the FileSystem delete method or hadoop rm commands will be moved to the Recycle Bin and provide an "undo window" within the configured retention period. If not enabled, data will be physically deleted directly.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to configure according to the above instructions. If protection is not enabled, any delete operation will result in permanent data loss.</div>
