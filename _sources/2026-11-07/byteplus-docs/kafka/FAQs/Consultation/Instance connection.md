---
title: "Instance connection"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Instance-connection-faq"
---

This topic provides answers to frequently asked questions (FAQs) related to instance connections in Message Queue for Kafka.

<span id="504ab14e"></span>
## Can I modify the VPC and subnet of a Kafka instance?

After a Kafka instance is created, you cannot modify the virtual private cloud (VPC) but can modify the subnet. For more information, refer to [Switching subnets](https://docs.byteplus.com/en/docs/kafka/switching-subnets).

<span id="7a017d66"></span>
## Can I modify the connection address and port number for a Kafka instance?


* You can modify the domain name prefix of an instance endpoint, but cannot modify the port number.

* After a Kafka instance is created, you can modify the domain name prefix of a public or private endpoint to change it from the instance ID to any character string that is more recognizable. For more information, refer to [Modifying the domain name prefix of an endpoint](https://docs.byteplus.com/en/docs/kafka/modifying-domainname-prefix).

* You cannot directly modify the private or public IP address of an instance. To change the public IP address, disable internet\-facing access, enable it again, and then associate another elastic IP address (EIP) with the instance.

* The port number of any instance endpoint cannot be modified.


<span id="d67dc3af"></span>
## How long is the validity period of an SSL certificate?

Downloading and manual configurations of an SSL certificate are not required when a Kafka instance is accessed from a Kafka client. You do not need to manually replace old certificates with new ones when they expire. This frees you from worrying about the risk of certificate expiration. For information on the message sending and receiving process using the SASL_SSL method, refer to [Sending and receiving messages via a SASL_SSL endpoint using the PLAIN mechanism](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-SASL_SSL-PLAINuser) illustrated in the demo of the SDK for Java.

In addition, Message Queue for Kafka instances maintain and regularly update SSL certificates to ensure long\-term certificate availability.

<span id="873f32c6"></span>
## Can I access a Kafka instance without a password?

Yes, you can access the instance via the default endpoint over a VPC without a password. During the transmission process, encryption and identity verification are not required. This eliminates the need to provide a password or identity credentials. For more information, refer to [Sending and receiving messages via the default endpoint](https://docs.byteplus.com/en/docs/kafka/Apache-Java-Sending-receiving-messages-default).

<span id="9fde7941"></span>
## Can I access a Kafka instance across VPCs or subnets?

Yes.


* You can access a Kafka instance across VPCs by using Cloud Enterprise Network (CEN). You can use CEN to interconnect VPC\-connected instances under the same BytePlus account in the same Region or across Regions. For more information, refer to [Getting started](https://docs.byteplus.com/en/docs/kafka/started-overview).

* Subnets in the same VPC can communicate with each other by default. If the Elastic Compute Service (ECS) instance on which a Kafka client is installed and a Kafka instance are in the same VPC, the Kafka instance can be accessed from a different subnet CIDR block by default.


<span id="58c8643a"></span>
## Can I access a Kafka instance across Regions or Availability Zones?

Yes.


* You can access a Kafka instance across Regions over the internet or by setting up a leased line.

* If a Kafka instance and the ECS instance on which a Kafka client is installed are in different Availability Zones of the same Region, you can connect the client to the Kafka instance by using VPC or CEN. The relevant limits are as follows:

   * The IP address of the ECS instance must be included in the allowlist associated with the Kafka instance. For information on how to configure an allowlist, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/kafka/creating-allowlist).

   * If the ECS instance and the Kafka instance are in different VPCs, enable communication by using other methods such as using CEN. For more information, refer to [Getting started](https://docs.byteplus.com/en/docs/kafka/started-overview).


<span id="f98c212f"></span>
## Can I access a Kafka instance by using a proxy?

No, you cannot access a Kafka instance by using a proxy.

<span id="5abb0cbe"></span>
## How do I test the connectivity to a Kafka instance?

You can test the connectivity to a Kafka instance via its endpoints. We recommend that you run the `ping` or `telnet` command on an ECS instance in the same Region as the Kafka instance to connect to its default endpoint.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Before testing, confirm that the IP address of the ECS instance is included in the allowlist associated with the Kafka instance.</div>


* <div data-tips="true" data-tips-type="tip">If you connect to the public endpoint of a Kafka instance over the internet, make sure that the client can access the internet.</div>
