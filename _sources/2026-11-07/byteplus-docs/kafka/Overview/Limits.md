---
title: "Limits"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/limits"
---

This topic describes the limits of Message Queue for Kafka on some metrics and performance. To avoid exceptions, do not exceed these limits when you use Message Queue for Kafka.


|**Item** |**Limit** |**Description** |
|---|---|---|
|Number of instances |8 |The number of Kafka instances in a single Region.<br><br>You can also apply in the Quota Center to increase the maximum number of instances (InstanceNum) in each Region. The maximum supported number is 16. |
|Total storage capacity |90 TiB |The total storage capacity of all Kafka instances in a single Region.<br><br>You can also apply in the Quota Center to increase the total storage capacity (StorageSum) of all instances in each Region. The maximum supported value is 150 TiB. |
|Sum of the maximum read traffic and maximum write traffic |3,000 MB/s |The sum of the maximum read traffic and the maximum write traffic of all Kafka instances in a single Region.<br><br>You can also apply in the Quota Center to increase the sum of the maximum read traffic and the maximum write traffic (BandwidthSum) of all instances in each Region. The maximum supported value is 6,000 MB/s. |
|Decrease in the number of partitions of a topic |Not supported |Subject to the design limits of Apache Kafka. |
|Exposing ZooKeeper |Not supported |No need for clients to access ZooKeeper and no need for you to understand how ZooKeeper works. For security concerns, Message Queue for Kafka does not expose ZooKeeper. |
|Logon to hosts where Message Queue for Apache Kafka is deployed |Not supported |None. |
|Changing the Region of an instance |Not supported |None. |
|Apache Kafka version |* 2.2.2<br><br>* 2.8.2 |Currently, only Apache Kafka versions 2.2.2 and 2.8.2 are supported. |
|Number of connections |20,000 |The upper limit on the number of concurrent connections established to each Kafka instance. |
|Number of connections per IP |1,000 |The maximum number of connections per client IP. |
