---
title: "Overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Java-SDK-overview"
---

Byteplus Engine message queue Kafka version is fully compatible with the open source Kafka protocol and supports multi\-language SDK. The client side can access the message queue Kafka version through VPC network and public network access, and send and receive messages. This document describes the main process of using the Java client side to access the Byteplus Engine message queue Kafka version to send and receive messages.

<span id="f984f054"></span>
## Access method

Message queue Kafka Edition provides a variety of access points in different network environments for the client side to access and send and receive messages. For detailed instructions on access points, please refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).


|**Network type** |**Access Point Type** |**agreement** |**Related Documentation** |
|---|---|---|---|
|Private network VPC |Default access point |PLAINTEXT |[Sending and receiving messages via the default endpoint](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-default) |
||SASL_SSL access point |SASL_SSL |* [Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_SSL endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-SCRAMuser) |
||SASL_PLAINTEXT access point |SASL_PLAINTEXT |* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_PLAINTEXT-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_PLAINTEXT-SCRAMuser) |
|Public network |SASL_SSL access point |SASL_SSL |* [Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_SSL endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-SCRAMuser) |
||SASL_PLAINTEXT access point |SASL_PLAINTEXT |* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_PLAINTEXT-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_PLAINTEXT-SCRAMuser) |


<span id="5a2747e5"></span>
## Example project

Byteplus Engine Message Queue Kafka Edition provides you with a Demo for quick access and experience.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36bbd6e3e6b34b2d8b09a843bf645c65~tplv-goo7wpa0wc-image.image" name="bp-kafka-java-demo.tar.gz">bp-kafka-java-demo.tar.gz</Attachment>
