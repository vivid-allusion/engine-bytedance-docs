---
title: "Product specifications"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Product_specifications"
---

The message queue for RabbitMQ is compatible with open source RabbitMQ. It offers both stand alone and cluster versions. Each version is available in several computing specifications to choose from.

<span id=".5a6e5L6L57G75Z6L"></span>
## Instance types

The message queue for RabbitMQ offers two types of instances: stand alone version and cluster version.


* Stand alone version: deploy a single RabbitMQ broker.

* Cluster version: deploy multiple RabbitMQ brokers for high\-reliability messaging services.


<span id=".6K6h566X6KeE5qC8"></span>
## Computing specifications

Computing specifications determine the business processing performance of RabbitMQ instances. The performance of RabbitMQ instances primarily depends on factors such as the queue count, connection count, and message accumulation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">TPS peak refers to the number of messages processed per second by RabbitMQ instances, including sending messages TPS and consuming messages TPS.</div>


* <div data-tips="true" data-tips-type="tip">When TPS peaks, queue counts, connection numbers, and other metrics approach specification limits, we recommend that you determine the need for urgent scaling based on business requirements. For example, if disk usage consistently exceeds 85% of the specification limit, scaling is recommended. You can monitor various specification metrics in real time through cloud monitoring alarms. For recommended alarm rules, refer to <a href="https://docs.byteplus.com/en/docs/rabbitmq/Recommended_alarm_rules">Recommended configuration alarm rules</a>.</div>


* <div data-tips="true" data-tips-type="tip">If the production link is below 200, there will be a higher upper limit of TPS performance. Please test according to your business scenario and reserve peak resources.</div>



<span id="WFcx9org"></span>
### Normal queue


|Instance types |Specification name |Recommended TPS peak |Recommended number of queues |Maximum number of connections |Maximum number of Channels |Storage space range |
|---|---|---|---|---|---|---|
|Stand alone version |rabbitmq.n1.x2.medium |3,000 |200 |2,000 |6,000 |100~4000 GiB |
|Cluster version |rabbitmq.n3.x2.small |4,500 |300 |2,400 |7,200 |300~12000 GiB |
||rabbitmq.n3.x2.medium |9,000 |600 |6,000 |18,000 |300~12000 GiB |
||rabbitmq.n5.x2.medium |15,000 |1,000 |10,000 |30,000 |500~20000 GiB |
||rabbitmq.n7.x2.medium |21,000 |1,400 |14,000 |42,000 |700~28000 GiB |
||rabbitmq.n7.x2.large |42,000 |2,800 |28,000 |84,000 |700~28000 GiB |
||rabbitmq.n9.x2.large |54,000 |3,600 |36,000 |108,000 |900~36000 GiB |


<span id=".5a2Y5YKo6KeE5qC8"></span>
### High queue


|Instance types |Specification name |Recommended TPS peak |Recommended number of queues |Maximum number of connections |Maximum number of Channels |Storage space range |
|---|---|---|---|---|---|---|
|Stand alone version |rabbitmq.n1.x4.small |1500 |200 |1000 |3000 |100~4000 GiB |
||rabbitmq.n1.x4.medium |3000 |400 |2000 |6000 |100~4000 GiB |
||rabbitmq.n1.x4.large |6000 |800 |4000 |12000 |100~4000 GiB |
|Cluster version |rabbitmq.n3.x4.small |4500 |600 |3000 |9000 |300~12000 GiB |
||rabbitmq.n3.x4.medium |9000 |1200 |6000 |18000 |300~12000 GiB |
||rabbitmq.n3.x4.large |18000 |2400 |12000 |36000 |300~12000 GiB |
||rabbitmq.n5.x4.small |7500 |1000 |5000 |15000 |500~20000 GiB |
||rabbitmq.n5.x4.medium |15000 |2000 |10000 |30000 |500~20000 GiB |
||rabbitmq.n5.x4.large |30000 |4000 |20000 |60000 |500~20000 GiB |


<span id=".5a2Y5YKo6KeE5qC8"></span>
## Storage specifications

Storage space is mainly used to store messages. Persistent messages are saved on disk. When memory usage is high, some data will also be offloaded to disk. When selecting storage space capacity, choose appropriate storage based on business message length and replica count. For stand alone RabbitMQ instances, you can estimate the required storage space by summing the business message length and reserved disk size. For clusters with mirrored queues enabled, consider additional disk space used by redundant messages.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Because some of the storage will be used for logs and metadata storage, the actual available storage will be less than the selected value.</div>


* <div data-tips="true" data-tips-type="tip">When the remaining disk space is less than 5 GiB, RabbitMQ blocks the producer to reduce the possibility of a service crash due to disk exhaustion.</div>
