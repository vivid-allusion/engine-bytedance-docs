---
title: "Queue reserved resource policy"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Queue_reserved_resource_policy"
---

To ensure stable queue operation, each node reserves a portion of resources for system components, such as process management, monitoring, and basic services. These resources are not included in business scheduling, so the actual allocatable resources per node are lower than the node specification. This document provides a clear overview of how to estimate reserved resources based on node specifications from three perspectives: **reservation policy, calculation examples, and key explanations**.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Estimated results may differ slightly from actual values. Refer to the console display for actual values.</div>


<span id="45f6b14b"></span>
## Reservation policy

Reserved resources are divided into two categories: **CPU reservation** and **memory reservation**. Both are calculated in segments based on node specifications, following the rules below:

<span id="f8aed5ee"></span>
### CPU reservation policy

The reserved CPU amount is calculated using segmented accumulation based on the total number of CPU cores per node. The specific segmentation rules are shown in the table below.


|**Total CPU** |**Reserved resources** |
|---|---|
|Total CPU ≤ 4 cores |1.38 Core |
|4 cores < total CPU ≤ 64 cores |1.38 cores + (total CPU–4) cores × 2.5% |
|64 cores < total CPU ≤ 128 cores |1.38 cores + (64\-4) cores × 2.5% + (total CPU–64) cores × 1.25% |
|Total CPU \> 128 cores |1.38 cores + (64\-4) cores × 2.5% + (128\-64) cores × 1.25% + (total CPU–128) cores × 0.5% |


<span id="8e392803"></span>
#### Example: 32\-core CPU node (CPU standard type 1:4)

Total CPU = 32 cores, which falls within the segment "4 cores < total CPU ≤ 64 cores":

Reserved CPU = 1.38 + (32\-4) × 2.5% = 1.38 + 28 × 0.025 = 1.38 + 0.7 = **2.08 cores**

<span id="dc1cb59e"></span>
### **Memory reservation policy**

The reserved memory amount is also calculated using segmented accumulation based on the total memory capacity per node, with additional "basic fixed reservation" and "memory ratio reservation" applied. The specific rules are shown in the table below.


|**Total memory** |**Reserved resources** |
|---|---|
|Total memory ≤ 4 GiB |2 GiB + total memory × 5.4% + total memory × 25% |
|4 GiB < total memory ≤ 8 GiB |2 GiB + total memory × 3.5% + 4 GiB × 25% + (total memory \- 4) GiB × 20% |
|8 GiB < total memory ≤ 16 GiB |2 GiB + total memory × 3.5% + 4 GiB × 25% + (8\-4) GiB × 20% + (total memory \- 8) GiB × 10% |
|16 GiB < total memory ≤ 128 GiB |2 GiB + total memory × 3.5% + 4 GiB × 25% + (8\-4) GiB × 20% + (16\-8) GiB × 10% + (total memory \- 16) GiB × 6% |
|Total memory \> 128 GiB |2 GiB + total memory × 3.5% + 4 GiB × 25% + (8\-4) GiB × 20% + (16\-8) GiB × 10% + (128\-16) GiB × 6% + (total memory \- 128) GiB × 2% |


<span id="9d0e46ae"></span>
#### Example: 128 GiB memory node (CPU standard type 1:4, 32 cores correspond to 128 GiB memory)

Total memory = 128 GiB, which falls within the segment "16 GiB < total memory ≤ 128 GiB":

Reserved memory = 2 + 128 × 3.5% + 4 × 25% + (8\-4) × 20% + (16\-8) × 10% + (128\-16) × 6% = **15.8 GiB**

<span id="8fdfd21f"></span>
## Reserved CU calculation

CU is a comprehensive calculation unit for "CPU + memory". The reserved CU must be the minimum of "4 CU" and 15% of "the number of CUs converted from memory and CPU", ensuring that the system's requirements for both CPU and memory are met.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">CU (Compute Unit) is a comprehensive resource calculation unit. For standard CPU resources, 1 CU = 4 GB memory + 1 CPU core.</div>


<span id="5201a188"></span>
### Calculation formula

Reserved CU = Min(4 CU, 15% CU)

<span id="31ff6198"></span>
#### Example: 32\-core + 128 GiB node (CPU standard type 1:4)

Calculation process:


* Number of CUs converted from memory and CPU = 32

* Reserved CU = Min(4 CU, 15% × CU) = Min(4 CU, 15% × 32) = Min(4 CU, 4.8 CU) = 4 CU
