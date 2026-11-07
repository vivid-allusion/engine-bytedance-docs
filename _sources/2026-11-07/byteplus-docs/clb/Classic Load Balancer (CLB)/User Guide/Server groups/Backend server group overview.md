---
title: "Backend server group overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Server-group-overview"
---

## Introduction​

The Server Group is a group of backend servers.

## Classification

|Topic |Explanation |Application scenario |
|---|---|---|
|Server type |Support adding the following resources as backend servers:<br><br><br>* ECS in the VPC where CLB is located<br><br>* Secondary network interface mounted to ECS in the VPC where CLB is located |* The backend server and CLB are in the same VPC<br><br>* The client IP address is transparent |
|IP type |Supports IPv4 addresses as backend servers as long as the network is reachable. e.g.<br><br><br>* IP address of the VPC where CLB is located.<br><br>* IPv4 address of other VPCs.<br><br>* IPv4 address of the server in the data center. |* Backend server and CLB are in different VPCs<br><br>* No need to pass through client IP address |

> **tip**

> The feature using an IP address as a backend server is currently in beta stage. If you need a trial, please contact your account manager.

Default backend server group

* For Layer 7 listeners, a default forwarding rule must be set and linked to the default backend server group. The rule's domain name is empty, and the URL is `/`, used to forward requests that do not match any forwarding rules.

* the default server group only supports IPv4\-type backend servers and does not support IPv6\-type backend servers yet.

## Protocol and port

* backend server protocol type

   |**Protocol of the access request** |**Protocol CLB uses to forward requests to backend servers** |
   |---|---|
   |TCP |TCP |
   |UDP |UDP |
   |HTTP |HTTP |
   |**HTTPS** |**HTTP** |

* backend server port

   the port where the backend server provides service, receiving and processing requests from the listener.

   requests from the same listening port can be forwarded to different backend servers, and different backend servers may receive requests on different ports.

## Limitations

the following limits apply when adding a backend server:

* a layer\-4 listener can be associated with only one backend server group.

* Each forwarding rule of a Layer 7 listener can only be associated with one backend server group.

* A backend server group can have up to 200 backend servers.

* Backend server port range: 1 to 65535.

## Usage process

1. [Create backend server group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group?LibVersion=3.24.0)

2. [Add backend server](https://docs.byteplus.com/en/docs/clb/Adding-a-server?LibVersion=3.24.0)

3. [Configure security group for backend server](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group?LibVersion=3.24.0)

4. [Attach listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener?LibVersion=3.24.0)
