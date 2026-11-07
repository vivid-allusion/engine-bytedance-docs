---
title: "SDK configuration"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Go-SDK-configuration"
---

Byteplus Engine message queue Kafka Edition provides you with sample project demos for quick access and experience. This article describes the configuration file `config.json` Common parameter configuration.

<span id="3a2412f4"></span>
## Configuration file template

After downloading the demo and unzipping it locally, at the path `{DemoPath}/config/config_templete.json` View the configuration file template in.

```json
{
  "bootstrap.servers": "127.0.0.1:8092",
  "security.protocol": "PLAINTEXT",
  "debug": false,
  "topic": "my-topic",
  "producer": {
    "acks": "1",
    "batch.size": "16384"
  },
  "consumer": {
    "group.id": "test",
    "auto.offset.reset": "earliest",
    "enable.auto.commit": true
  },
  "sasl": {
    "enabled": false,
    "mechanism": "PLAIN",
    "username": "test-user",
    "password": "test-password"
  }
}
```


<span id="61255e25"></span>
## Parameter description


|**parameter name** |**Is it required?**  |**default value** |**describe** |
|---|---|---|---|
|bootstrap.servers |Required |kafka\-ap\-1z69ajxxx.kafka.ibytepluses.com:xxxx |The access point for the Kafka instance.<br><br>On the console instance details page**access point**View access point information in the area. |
|security.protocol |Optional |PLAINTEXT |Channel authentication mechanism for Kafka instance access points.<br><br><br>* PLAINTEXT: Use default access point.<br><br>* SASL_PLAINTEXT: Use SASL_PLAINTEXT access point.<br><br>* SASL_SSL: Use SASL_SSL access point. |
|debug |optional |False |Enabling DEBUG mode will output the running log of Kafka. |
|topic |Required |TopicTest |Topic names for messages sent and received.<br><br>Please specify the instance**Topic Management**Tab to view Topic information. |
|producer.acks |Optional |1 |Production reliability configuration.<br><br><br>* 0: The Kafka service side does not return write results and cannot guarantee message writing.<br><br>* 1: The service side returns the write success after the message is written to a copy.<br><br>* \-1: The service side returns write success after the message is written to all synchronous replicas.<br><br>   According to the configuration order of [0, 1, \-1], the performance decreases in turn, and the reliability increases in turn. |
|producer.batch.size |optional |16384 |Size of bulk messages. Consider increasing this value when client side messages are larger or client side messages are faster. |
|consumer.group.id |Required |GroupTest |When consuming messages, specify the name of the consumer group. It is recommended to take a business\-related name for easy distinction. Consumer groups can be used to achieve broadcast and unicast capabilities. Normally, a message will only be consumed once by one consumer group, but can be consumed multiple times by multiple consumer groups. |
|consumer.auto offset.reset |Optional |Earliest |When the consumption group does not have a valid consumption record, use this configuration to reset the consumption progress. For example: the consumption record of the consumption group is not found on the service side or the recorded consumption progress has expired.<br><br><br>* Earliest: Reset consumption progress to the earliest message.<br><br>* Latest: Reset consumption progress to the latest message. Can be used for new consumption groups to skip historical data. |
|consumer.enable.auto commit |Optional |True |Whether to turn on automatic submission of consumption progress. After turning it on, you can save the consumption progress to the service side without calling the submission method of consumption progress.<br><br>It is recommended that the production environment use turn off automatic submission, and choose the appropriate time to manually submit the consumption progress after confirming that the processing is successful to avoid the message that the automatic submission processing fails. |
|sasl.enabled |Optional |False |Whether to enable SASL authentication.<br><br><br>* True: Enable SASL authentication. Suitable for scenarios where SASL access points are accessed.<br><br>* False: Turn off SASL authentication. Applicable to scenarios with default access point access. |
|sasl.mechanism |Optional |PLAIN |SASL authentication algorithm type, required when using a SASL access point.<br><br><br>* PLAIN: PLAIN mechanism.<br><br>* SCRAM\-SHA\-256: SCRAM mechanism. |
|sasl.username |Optional |*  |SASL certified account name, required when using SASL access point.<br><br>Please fill in the username and password of the corresponding type of user for SASL authentication according to the client side authentication mechanism. For example, use the username and password of the PLAIN user under the PLAIN mechanism. |
|sasl.password |Optional |*  |The SASL\-certified account password is required when using the SASL access point.<br><br>According to the client side authentication mechanism, fill in the user name and password of the corresponding type of user for SASL authentication, for example, use the user name and password of the PLAIN user under the PLAIN mechanism. |
