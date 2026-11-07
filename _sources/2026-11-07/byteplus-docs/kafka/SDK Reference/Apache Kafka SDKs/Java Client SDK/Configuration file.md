---
title: "Configuration file"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Java-Configuration-file"
---

Byteplus Engine message queue Kafka Edition provides you with sample project demos for quick access and experience. This article describes the configuration file `config.properties`Common parameter configuration.

<span id="c73717d2"></span>
## Configuration file template

After downloading the demo and unzipping it locally, at the path `{DemoPath}/src/main/resources` View profile templates in `config.properties` and `ssl.config.properties`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When filling in the configuration file in the actual scenario, all comment statements should be deleted.</div>


```YAML
// AccessPoint which can be acquired through the console.
bootstrap.servers=xxxxx
// Security protocol: PLAINTEXT, SASL_PLAINTEXT
security.protocol=PLAINTEXT
topic=my-topic
consumer.group.id=test
consumer.auto.offset.reset=earliest
consumer.enable.auto.commit=false
client.dns.lookup=use_all_dns_ips
// Encryption mechanism: PLAIN, SCRAM-SHA-256.
sasl.mechanism=PLAIN
sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="xxxx" password="xxxxx";
#org.apache.kafka.common.security.scram.ScramLoginModule required username="xxxx" password="xxxxx";
```


<span id="13025ed8"></span>
## Parameter description


|**parameter name** |**Is it required?**  |**default value** |**describe** |
|---|---|---|---|
|bootstrap.servers |Required |kafka\-ap\-1z69ajxxx.kafka.ibytepluses.com:xxxx |The access point for the Kafka instance.<br><br>On the console instance details page**access point**View access point information in the area. |
|security.protocol |Optional |PLAINTEXT |Channel authentication mechanism for Kafka instance access points.<br><br><br>* PLAINTEXT: Use default access point.<br><br>* SASL_PLAINTEXT: Use the SASL access point. |
|topic |Required |TopicTest |Topic names for messages sent and received.<br><br>Please specify the instance**Topic Management**Tab to view Topic information. |
|consumer.group.id |Required |GroupTest |When consuming messages, specify the name of the consumer group. It is recommended to take a business\-related name for easy distinction. Consumer groups can be used to achieve broadcast and unicast capabilities. Normally, a message will only be consumed once by one consumer group, but can be consumed multiple times by multiple consumer groups. |
|consumer.auto offset.reset |Optional |Earliest |When the consumption group does not have a valid consumption record, use this configuration to reset the consumption progress. For example: the consumption record of the consumption group is not found on the service side or the recorded consumption progress has expired.<br><br><br>* Earliest: Reset consumption progress to the earliest message.<br><br>* Latest: Reset consumption progress to the latest message. Can be used for new consumption groups to skip historical data. |
|consumer.enable.auto commit |Optional |True |Whether to turn on automatic submission of consumption progress. After turning it on, you can save the consumption progress to the service side without calling the submission method of consumption progress.<br><br>It is recommended that the production environment use turn off automatic submission, and choose the appropriate time to manually submit the consumption progress after confirming that the processing is successful to avoid the message that the automatic submission processing fails. |
|sasl.mechanism |Optional |PLAIN |SASL authentication algorithm type, required when using a SASL access point.<br><br><br>* PLAIN: PLAIN mechanism.<br><br>* SCRAM\-SHA\-256: SCRAM mechanism. |
|sasl.jas.config |Optional |*  |SASL authentication information, including account name and account password, is required when using a SASL access point.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Please fill in the username and password of the corresponding type of user for SASL authentication according to the client side authentication mechanism. For example, use the username and password of the PLAIN user under the PLAIN mechanism.</div><br> |
|client.dns.lookup |Optional |*  |Specifies how the Kafka client side resolves domain names via DNS.<br><br><br>* use_all_dns_ips: Attempt to connect to each returned IP address until a connection is successfully established. Versions 2.7 and above default to use_all_dns_ips client side.<br><br>* Default: Only the first of multiple IP addresses will be returned using DNS. If the first IP is not available, it will not be able to connect. The client side defaults to default in versions below 2.7. |
