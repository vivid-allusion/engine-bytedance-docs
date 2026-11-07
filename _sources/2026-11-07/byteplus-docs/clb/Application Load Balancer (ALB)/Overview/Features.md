---
title: "Features"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/How-it-works"
---

## ALB components

The Application Load Balancer (ALB) includes three components: instances, listeners, and server groups, as shown below.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1edd5b5885203fe4e5c2e6a9a581232c.png)

The description of components and related concepts is as follows:

### Instance

* An instance is the smallest unit for ALB service and billing. ALB instances receive client traffic and forward requests to backend servers to balance the load.

* There are two types of ALB instances: internet\-facing instances and private instances. A single ALB instance can handle millions of QPS requests.

### Listener

* Listeners are configured on ALB instances. Listeners process requests on specific ports using specified protocols according to your configuration instructions.

* Each instance must have at least one listener to forward data; a single instance can have up to 50 listeners.

### Forwarding rules

* Forwarding rules are configured on listeners. Based on your configured forwarding rules, the ALB instance forwards requests for different domain names and URLs to the specified server groups.

* Each ALB instance has one default forwarding rule that can be modified but not deleted. You can also add custom forwarding rules.

* If a client request does not match any custom forwarding rules, ALB forwards the request according to the default forwarding rules.

* Under a single custom forwarding rule, you can add multiple server groups.

### Server Group

* A server group is a collection of backend servers. One server group can include multiple backend servers, and one backend server can be added to different server groups.

* Server groups and instances operate independently. A server group can associate with any instance within the same [VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC).

* ALB offers two types of server groups: server type and IP type.

## Related products

When BytePlus ALB provides services, it involves other BytePlus services. The relationship between ALB and these services is as follows:

|**Related products** |**Relationship with ALB** |Related links |
|---|---|---|
|Elastic Compute Service (ECS) |Elastic Compute Service (ECS) can serve as backend servers that actually handle your business traffic. ECS can be added to server groups, allowing you to manage ECS by server group. |If you want to learn more about the concept and features of Elastic Compute Service, click [here](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service). |
|Elastic IP Address (EIP) |EIP enables Cloud Load Balancer public instances to communicate with the public network. After you create a public instance, it automatically receives an EIP. |If you want to learn more about the concept and features of EIP, please click [here](https://docs.byteplus.com/en/docs/eip/What-is-EIP). |
|Virtual Private Cloud (VPC) |The ALB instance can only communicate with backend servers within the same VPC. Therefore, whether you create an Internet\-facing instance or a private instance, you need to plan and complete the creation of the VPC in advance. |If you want to learn more about Virtual Private Cloud and VIP, click [here](https://docs.byteplus.com/en/docs/vpc/What-is-VPC). |

## working principle

The working principle of BytePlus ALB is as follows:

1. The client sends a request to your application. The request is first sent to the ALB.

2. The ALB receives the request and forwards it to the associated server group according to the forwarding rules you set.

3. Based on the routing algorithm you configure, the ALB distributes traffic to different healthy backend servers within the server group.

4. The backend server receives and processes the request, then returns the response to the client through the ALB.
