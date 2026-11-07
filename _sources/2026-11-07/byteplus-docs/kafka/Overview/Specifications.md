---
title: "Specifications"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/specifications"
---

Message Queue for Kafka is compatible with Apache Kafka and supports multi\-replica data storage. The computing capability and storage space of a Kafka instance depend on the instance type and storage specification you select.

<span id="计算规格"></span>
## Computing specifications

The following tables list the computing specifications that Message Queue for Kafka provides for your choice.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Certain computing specifications may be sold out in some Regions. The availability of computing specifications is subject to the information displayed on the instance creation page in the Message Queue for Kafka console.</div>


* <div data-tips="true" data-tips-type="tip">Take note of the following items when you select the maximum read traffic and maximum write traffic:</div>


   * <div data-tips="true" data-tips-type="tip">Select the traffic specifications based on the maximum read traffic and maximum write traffic of the network interface, whichever is higher.</div>


   * <div data-tips="true" data-tips-type="tip">We recommend that you estimate the maximum traffic based on your actual traffic plus 30%, and then select a suitable instance specification by considering other parameters.</div>


* <div data-tips="true" data-tips-type="tip">Each instance type offers a certain number of free partitions. The partitions beyond the free quota are charged as per the unit price.</div>


* <div data-tips="true" data-tips-type="tip">We recommend that you determine whether to scale up an instance based on your business requirements when the maximum traffic, disk capacity, and other metrics approach upper limits. For example, consider increasing the storage capacity when the disk utilization exceeds 85% of the specified limit. You can use the alarm feature of Vitality Cloud Monitor to monitor various metrics in real time. For information about recommended alarm rules, please see <a href="https://docs.byteplus.com/en/docs/kafka/recommended-alarm-rules">Recommended alarm rules</a>.</div>



<span id="e7a0bc7a"></span>
### High\-writing version (read/write 1:1)


|**Computing specification** |**Maximum Read Traffic (MB/s)**  |**Maximum Write Traffic (MB/s)**  |**Number of Free Partitions** |**Maximum Number of Partitions Allowable** |**Disk Capacity (GiB)**  |
|---|---|---|---|---|---|
|kafka.20xrate.hw |20 |20 |350 |350–1,000 |300–96,000 |
|kafka.30xrate.hw |30 |30 |350 |350–1,000 |300–96,000 |
|kafka.60xrate.hw |60 |60 |400 |400–1,000 |300–96,000 |
|kafka.100xrate.hw |100 |100 |600 |600–3,000 |600–96,000 |
|kafka.150xrate.hw |150 |150 |700 |700–3,000 |900–96,000 |
|kafka.200xrate.hw |200 |200 |750 |750–3,000 |1,200–96,000 |
|kafka.250xrate.hw |250 |250 |800 |800–3,000 |1,500–96,000 |
|kafka.300xrate.hw |300 |300 |900 |900–3,000 |1,800–192,000 |
|kafka.600xrate.hw |600 |600 |1,800 |1,800–5,000 |2,400–192,000 |
|kafka.800xrate.hw |800 |800 |2400 |2,400–6,000 |4,000–288,000 |
|kafka.1000xrate.hw |1,000 |1,000 |3,000 |3,000–7,000 |5,500–384,000 |
|kafka.1200xrate.hw |1,200 |1,200 |3,600 |3,600–8,000 |6,500–480,000 |
|kafka.1500xrate.hw |1,500 |1,500 |3,600 |3,600–8,000 |8,000–576,000 |
|kafka.2000xrate.hw |2000 |2000 |4000 |4000~8000 |12000~768000 |
|kafka.4000xrate.hw |4000 |4000 |6000 |6000~10000 |26000~1536000 |


<span id="4cdd840a"></span>
### High\-reading version (read/write 3:1)


|**Computing specification** |**Maximum Read Traffic (MB/s)**  |**Maximum Write Traffic (MB/s)**  |**Number of Free Partitions** |**Maximum Number of Partitions Allowable** |**Disk Capacity (GiB)**  |
|---|---|---|---|---|---|
|kafka.800xrate.hr |1200 |400 |2400 |2400~6000 |4000~288000 |
|kafka.1200xrate.hr |1800 |600 |3600 |3600~8000 |6500~576000 |
|kafka.1500xrate.hr |2250 |750 |3600 |3600~8000 |8000~672000 |
|kafka.2000xrate.hr |3000 |1000 |4000 |4000~8000 |12000~768000 |
|kafka.3000xrate.hr |4500 |1500 |5000 |5000~10000 |15000~1152000 |


<span id="存储规格"></span>
## Storage specifications

Storage space is mainly used for storing messages. Persistent messages that have been sent are stored on disks. Some data is also stored on disks if the memory utilization is excessively high. In addition, the multi\-replica mechanism of Message Queue for Kafka also impacts the storage space. The storage space of a Kafka instance is the sum of storage space for all replicas. Therefore, when creating a Kafka instance, we recommend that you select a suitable storage space based on your business message volume and the number of replicas.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Some storage space is used for storing logs and metadata. Redundant messages also occupy additional space. For these reasons, the actual available storage space is less than the storage specification you set. We recommend that you reserve a storage space of around 25%.</div>


* <div data-tips="true" data-tips-type="tip">The disk utilization of different nodes varies greatly if data is imbalanced. This causes low disk utilization in some nodes and compromises the efficiency of resource utilization. You can view the <strong>DiskSkewness</strong> metric in the Vitality Cloud Monitor page and adjust your business logic if any data imbalance is detected. This helps you balance the data write traffic among disks and avoid data skews.</div>



The storage specification of a Kafka instance is calculated as follows:

Actually occupied storage space = Business message volume × Number of replicas ÷ 75%

For example, if the message volume is 1,000 GiB and the number of replicas is 3 for all topics, the storage space required is 1,000 GiB × 3 ÷ 0.75 = 4,000 GiB.
