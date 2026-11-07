---
title: "Overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Apache-Go-overview"
---

Byteplus Engine message queue Kafka version is fully compatible with the open source Kafka protocol and supports multi\-language SDK. The client side can access the message queue Kafka version through VPC network and public network access, and send and receive messages. This document describes the main process of using the Go client side to access the Byteplus Engine message queue Kafka version to send and receive messages.

<span id="34e87be5"></span>
## Access method

Message queue Kafka Edition provides a variety of access points in different network environments for the client side to access and send and receive messages. For detailed instructions on access points, please refer to [Viewing endpoints](https://docs.byteplus.com/en/docs/kafka/viewing-endpoints).


|**Network type** |**Access Point Type** |**agreement** |**Related Documentation** |
|---|---|---|---|
|Private network VPC |Default access point |PLAINTEXT |[Sending and receiving messages via the default endpoint](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-default) |
||SASL_SSL access point |SASL_SSL |* [Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_SSL-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_SSL endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_SSL-SCRAMuser) |
||SASL_PLAINTEXT access point |SASL_PLAINTEXT |* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_PLAINTEXT-SCRAMuser)<br><br>* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_PLAINTEXT-PLAINuser) |
|Public network |SASL_SSL access point |SASL_SSL |* [Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_SSL-PLAINuser)<br><br>* [Sending and receiving messages via a SASL_SSL endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_SSL-SCRAMuser) |
||SASL_PLAINTEXT access point |SASL_PLAINTEXT |* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the SCRAM mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_PLAINTEXT-SCRAMuser)<br><br>* [Sending and receiving messages via a SASL_PLAINTEXT endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Go-Sending-receiving-messages-SASL_PLAINTEXT-PLAINuser) |


<span id="ff0d2d52"></span>
## Example project

Byteplus Engine Message Queue Kafka Edition provides you with a Demo for quick access and experience.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1991e4e206947f88b23669ce4d91b2d~tplv-goo7wpa0wc-image.image" name="bp-kafka-go-demo.tar.gz">bp-kafka-go-demo.tar.gz</Attachment>
