---
title: "Listener overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview"
---

## Introduction​

The listener is responsible for monitoring user access requests received by the NLB instance based on specified protocols and ports. NLB forwards access requests to healthy backend servers within the server group according to the scheduling algorithm configured for the server group associated with the listener.

## Listening Protocol and Ports

* **Listening protocol**

   |Listening protocol |Explanation |Application scenarios |
   |---|---|---|
   |TCP |TCP is a connection\-oriented protocol that requires establishing a connection via three\-way handshake to ensure reliability before data transmission. Once data transfer is complete, the connection must be terminated. |Applicable to scenarios that prioritize reliability and data accuracy, such as file transfers, email communications, remote logins, and web applications. |
   |UDP |UDP is a connectionless protocol that does not require establishing a connection. The sender can directly transmit the datagram to the receiver, and the receiver also does not need to send an acknowledge back to the sender. |Applicable to scenarios that require real\-time performance, such as voice and video chat, online gaming, and real\-time financial updates. |
   |TLS |On the foundation of a TCP connection, TLS utilizes certificates and security policies to establish a secure connection between the client and the server, encrypting and authenticating data in transit. |Applicable for scenarios under the TCP protocol with very high security requirements, such as large\-scale TLS offloading scenarios. |

* **Listening port**

   Within the same NLB instance, TLS and TCP listeners cannot share the same port. However, both can coexist on the same port with a UDP listener. Listeners support two types of ports: single port and full port range.

   |Classification |Explanation |Supported listening protocols |Application scenario |
   |---|---|---|---|
   |Listen by single port |Listening port range is specified from 1 to 65535 |TCP, UDP, TLS |Applicable for scenarios where all backend servers use the same port to provide external services. |
   |Full port listening |Specify the port range for listening ports within the range of 1 ~ 65535 ||Suitable for scenarios where a range of consecutive ports is open for backend server applications. |

## Limitations

|Quota item |Maximum |Adjustable |
|---|---|---|
|Number of listeners that can be added to a single NLB instance |50 |Yes |
|The number of server groups that can be attached to a single listener |1 |No |
|The number of times a single server group can be attached to a listener |50 times |Yes |
