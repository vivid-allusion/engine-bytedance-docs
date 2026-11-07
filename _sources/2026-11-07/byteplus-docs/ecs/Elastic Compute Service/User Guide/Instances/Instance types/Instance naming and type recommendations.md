---
title: "Instance naming and type recommendations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-type-selection-best-practice"
---

The platform offers a variety of instance types to meet your requirements in different scenarios. This topic describes how to select and purchase ECS instances based on your business requirements, allowing you to make full use of the elastic scaling capabilities of your ECS instance.

## Notes

* This topic only describes instances of x86 Compute and EBM architectures. For specific instance types, refer to the [instance types introduction](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types); however, this topic does not cover burstable performance instances and shared instances which are of an x86 Compute architecture. For related information, refer to [Burstable instances](https://docs.byteplus.com/en/docs/ecs/Burstable-performance-instances) and [Shared instances](https://docs.byteplus.com/en/docs/ecs/Shared).

* For recommendations on selecting heterogeneous compute\-optimized GPU instances, refer to [Best practices for GPU instance type selection](https://docs.byteplus.com/en/docs/gpu/Best_practices_for_instance_selection).

## Instance name

### Instance type family name

**Format: <Instance type family series\><Instance type family generation\><Processor type\><Suffix\>**

|Instance type family series |**Instance type family generation** |**Processor type** |**Suffix** |
|---|---|---|---|
|Lowercase letters, representing an instance type family type, are usually abbreviations of certain words that represent the performance domain of the instance type family.<br><br><br>* g: General\-purpose<br><br>* c: Compute\-optimized<br><br>* r: RAM, Memory\-optimized.<br><br>* re: Memory Enhanced<br><br>* i: Local SSD<br><br>* d: Big Data<br><br>* hfg/c/r: High Frequency<br><br>* t: Burstable<br><br>* s/e: Shared Standard/Economic<br><br>* ebm prefix: the EBM type<br><br>* \-flex suffix: FLEX |Arabic numerals that indicate the generation of the instance type family. A larger number indicates a later generation. |A lowercase English letter representing the CPU vendor.<br><br><br>* i: Intel<br><br>* a: AMD |Lowercase English letters, indicating other attributes of the instance type family.<br><br><br>* e: The enhanced balance attribute<br><br>* t: The enhanced security attribute<br><br>* s: The storage attribute<br><br>* ne: The enhanced network attribute<br><br><br>For more instance attributes, please refer to [instance types](https://docs.byteplus.com/en/docs/49/12774#65Hn0bTI). |

### Instance type name

**Format: ecs.<Instance type family\>.<Size\>**

|ecs |Instance type family name |Size |
|---|---|---|
|Represents the product name Elastic Compute Service (ECS) and cannot be changed. |For details, refer to [Instance type family name](https://docs.byteplus.com/en/docs/49/12774#wKT0xHxq). |The number of vCPUs for an instance type, typically represented as `large` or `<nx>large`. `large` represents 2 vCPUs, `xlarge` represents 4 vCPUs, `2xlarge` represents 2 \* 4 = 8 vCPUs, and `3xlarge` represents 3 \* 4 = 12 vCPUs. So, a larger n value represents more vCPUs and a larger specification. |

## Instance type

ECS offers multiple instance types with different computing and storage capabilities to suit different scenarios.

Due to the large number of instance type families, some families do not strictly follow the above naming rules. See the following details:

|Instance type family type |Instance type family name |Explanation |
|---|---|---|
|General\-purpose |* g4i<br><br>* g3i<br><br>* g3a<br><br>* g3il<br><br>* g3al |* g: General\-purpose. This instance type family does not offer local volumes. vCPU:memory=1:4.<br><br>* i: Intel processor<br><br>* a: AMD processor |
|Compute\-optimized |* c4i<br><br>* c3i<br><br>* c3a<br><br>* c3il<br><br>* c3al |* c: Compute\-optimized. This instance type family does not offer local volumes. vCPU:memory=1:2.<br><br>* i: Intel processor<br><br>* a: AMD processor |
|Memory\-optimized |* r4i<br><br>* r3i<br><br>* r3a<br><br>* r3il<br><br>* r3al |* r: Memory\-optimized. This instance type family does not offer local volumes. vCPU:memory=1:8.<br><br>* i: Intel processor<br><br>* a: AMD processor |
|Local SSD |* i4<br><br>* i4ag<br><br>* i3s<br><br>* i2 |* i: Local SSD. Local volumes of SSD type are offered.<br><br>* a: AMD processor<br><br>* s: The storage attribute. This instance family offers local volumes with large capacity.<br><br>* g: General\-purpose |
|Big Data |* d4c<br><br>* d4s<br><br>* d2c<br><br>* d2 |* d: Big Data. Local volumes of HDD type are offered.<br><br>* c：Compute\-optimized |
|Burstable |t2 |t: Burstable. This instance type family does not offer local volumes. Multiple processor\-to\-memory ratios (1:1, 1:2, and 1:4) are available. |
|Shared |e |e: Shared Economic. This instance type family does not offer local volumes. Multiple processor\-to\-memory ratios (1:1, 1:2, and 1:4) are available. |
|General\-purpose EBM |* ebmg3id<br><br>* ebmg3ad |* ebm: The EBM server<br><br>* g: General\-purpose. vCPU:memory=1:4<br><br>* i: Intel processor<br><br>* a: AMD processor<br><br>* d: Local volumes of SSD type are offered. |
|Compute\-optimized EBM |ebmc3id |* ebm: The EBM server<br><br>* c: Compute\-optimized. vCPU:memory=1:2.7<br><br>* i: Intel processor<br><br>* d: It includes a local volume of SSD type. |

##

## Recommended instance type families for common business scenarios

|Business scenario |Commonly used software |Recommended instance type families |
|---|---|---|
|Web service |Apache, Nginx |General\-purpose, Compute\-optimized, General\-purpose EBM, Compute\-optimized EBM |
|Middleware |RocketMQ, RabbitMQ, Kafka |General\-purpose, General\-purpose EBM |
|Database |MySQL, NoSQL |Memory\-optimized, local SSD |
|Cache |Redis, Memcache |Memory\-optimized |
|Big data |HDFS, MapReduce |Local SSD, Big Data |
