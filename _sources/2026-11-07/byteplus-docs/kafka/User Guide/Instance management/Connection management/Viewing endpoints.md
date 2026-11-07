---
title: "Viewing endpoints"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/viewing-endpoints"
---

Message Queue for Kafka instances supports two access methods: internal access and internet\-facing access. Endpoints vary depending on network environments. When accessing Message Queue for Kafka to send and receive messages, select a suitable endpoint according to the network environment and authentication mechanism. This topic describes the differences among endpoints and the procedure for viewing the endpoints.

<span id="支持的网络类型"></span>
## Supported network types

Message Queue for Kafka instances support two access methods: internal access and internet\-facing access.


|Network Type |Description |
|---|---|
|VPC |A virtual private cloud (VPC) offers Kafka instances an isolated, self\-configured, and self\-managed virtual network environment, allowing messages to be transmitted over the PLAINTEXT protocol in a secure network channel without encryption. To access instances over the VPC, you must set up a development environment on an Elastic Compute Service (ECS) instance in the same Region, deploy clients, or use Cloud Enterprise Network (CEN) to connect ECS instances across different Regions for network connection.<br><br>In the VPC, Message Queue for Kafka offers default endpoints, SASL_SSL endpoints, and SASL_PLAINTEXT endpoints.<br><br><br>* The default endpoint requires no identity authentication, enabling quick access upon configuration.<br><br>* For enhanced security policies, you can authenticate identities through Simple Authentication and Security Layer (SASL) users and encrypt data links using SSL certificates. |
|Internet |Kafka instances support internet\-facing access, enabling any internet\-connected client to access the instance. In this scenario, ECS is not required. You can configure the endpoint in your data center or other development environments to connect to the instance.<br><br>Message Queue for Kafka offers SASL_SSL and SASL_PLAINTEXT endpoints for access over the internet, requiring client authentication through SASL users. Select a suitable endpoint based on whether an SSL certificate is required for encryption. |


<span id="3f0c3a82"></span>
## Supported security mechanisms

Message Queue for Kafka offers multiple security mechanisms to safeguard data security in both VPC and internet environments.

<span id="SASL身份验证"></span>
### SASL authentication

SASL is an authentication mechanism for exchanging identity credentials. Messages are transmitted over a secure channel after SASL authentication. In Message Queue for Kafka, SASL endpoints are available for both internet and VPC environments.

Kafka instances support two SASL mechanisms. Select an authentication method as needed.


* PLAIN mechanism: It is a simple username and password authentication method with low security. Passwords are stored in the JAAS configuration file of Kafka instances. Usernames or passwords cannot be modified.

* SCRAM mechanism: It is a complex username and password authentication method, providing higher security than the PLAIN mechanism. When the client uses the SCRAM mechanism for authentication, passwords are transmitted to the server after being hashed using SHA\-256. Users can be dynamically added or reduced, without restarting instances.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Message Queue for Kafka supports permission management based on access control lists (ACLs). When using the SASL mechanism, ensure the SASL user used for authentication is granted the required permissions. For user authorization methods, see <a href="https://docs.byteplus.com/en/docs/kafka/creating-an-ACL">Creating an access control list</a>.</div>


<span id="SSL 加密"></span>
### SSL encryption

SSL is a protocol for encrypting network connections between the transport and application layers. Message Queue for Kafka offers SSL encryption. Connecting to the instance with SASL_SSL endpoint requires SSL authentication for message transmission. After SSL encryption, messages or data is securely transmitted over the network, offering higher security than standard internet\-facing access methods and ensuring data security.

In the internet environment, the SASL mechanism is commonly paired with SSL authentication to secure the data transmission link beyond identity verification and authorization. Compared to data transmission through the standard internet\-facing access methods, it reduces the risk of data and messages being listened to or intercepted.

<span id="Kafka 实例接入点"></span>
## Endpoints for Kafka instances

For different network types, Kafka instances offer the following endpoints. Select an access method that best meets the security performance needs of your business.


|**Network Type** |**Endpoint Type** |**Protocol** |**Description** |
|---|---|---|---|
|VPC |DEFAULT_ENDPOINT |PLAINTEXT |The default endpoint requires no encryption or identity authentication during the transmission process, facilitating convenient access. The default endpoint is suitable for instance access over the VPC without requiring additional security policies.<br><br>The issue is manifested as follows:<br><br><br>* The VPC guarantees the security of the transmission process, eliminating the need for encryption.<br><br>* Sending and receiving messages does not require SASL user authentication, simplifying the configuration process. |
||SASL_SSL_ENDPOINT |SASL_SSL |This endpoint is suitable for scenarios that require SSL encryption and SASL authentication in VPCs.<br><br>In high data security requirement scenarios like finance and healthcare, this endpoint allows for instance access from VPC, with message data encrypted through SASL_SSL for transmission. |
||SASL_PLAINTEXT endpoint |SASL_PLAINTEXT |This endpoint is suitable for scenarios that require SASL authentication in VPCs.<br><br>This endpoint has the following security features:<br><br><br>* Messages are transmitted in a VPC, eliminating the need for encryption.<br><br>* Message sending and receiving requires SASL user authentication. Message Queue for Kafka supports the following two mechanisms for identity authentication:<br><br>   * SASL/PLAIN: PLAIN mechanism<br><br>   * SASL/SCRAM: SCRAM\-SHA\-256 |
|Internet |SASL_SSL_ENDPOINT |SASL_SSL |This endpoint is suitable for scenarios where Kafka instances are accessed over the internet. In addition, SSL encryption is required for the data link, and SASL authentication is required for message sending and receiving.<br><br>This endpoint has the following security features:<br><br><br>* Messages are encrypted with SSL certificates during transmission, ensuring the security of transmission over the internet.<br><br>* Message sending and receiving requires SASL user authentication. Message Queue for Kafka supports the following two mechanisms for identity authentication:<br><br>   * SASL/PLAIN: PLAIN mechanism<br><br>   * SASL/SCRAM: SCRAM\-SHA\-256 |
||SASL_PLAINTEXT endpoint |SASL_PLAINTEXT |This endpoint is suitable for scenarios where Kafka instances are accessed over the internet. In addition, only SASL user authentication and authorization are required for message sending and receiving, without the need for additional security policies such as SSL. |


<span id="查看接入点"></span>
## Viewing endpoints


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. On the **Instances** page, click the name of the instance.

4. Navigate to **Instance Details \> Service access**, then view the internet\-facing access status and endpoints of the instance.

   * Public endpoints are displayed only when internet\-facing access is enabled for the instance.

   * An instance endpoint is displayed in the format of `domain name:port number`. When you connect to an instance, specify the complete endpoint information, including the domain name and port number.
