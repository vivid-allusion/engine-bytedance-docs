---
title: "What is Network Load Balancer"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/What-is-Network-Load-Balancer"
---

Network Load Balancer (NLB) is a next\-generation Layer 4 load balancing service provided by BytePlus. Compared to CLB, NLB supports higher\-performance elastic forwarding capabilities for Layer 4 load balancing, helping you easily handle high\-concurrency tasks (a single instance supports up to billions of concurrent connections and 100Gbps bandwidth).

## Product architecture

Once the NLB instance becomes optional, its listener intercepts access requests on the specified protocol and port, NLB forwards access requests to healthy backend servers in the server group associated with the listener, using the load balancing algorithm configured for the server group. The product architecture is as follows:

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_600e1ba4c6bf014e4322c2b8318995c6.png)

|Composition |Explanation |
|---|---|
|Internet |Users must use their own domain names and resolve them via [resolve it via CNAME](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-set-up-cname) to the NLB domain name.<br><br>> Note that:<br><br><br>> BytePlus does not allow users to directly use the default domain name provided by the NLB service for access to Internet. If you need to provide services to the internet through an NLB instance, please use your own domain name and resolve it via CNAME to the NLB domain name. If you do not have your own domain name, refer to [Domain name services](https://docs.byteplus.com/en/docs/domain-names/introduction_en).<br> |
|NLB instance |The NLB instance is used to receive user access requests and forwards them to backend servers based on the configuration settings of the listener and server group. Divided into the following sections:<br><br><br>* NLB domain name: After an NLB instance is created, the system will automatically assign an NLB domain name. The NLB domain name format is: `<NLB instance ID>.nlb.<Region ID>.volces.com`.<br><br>   * When the access request is via IPv4 internet, the NLB instance resolves the NLB domain name to its Elastic IP (EIP).<br><br>   * When the access request is via IPv4 private network, IPv6 internet, or IPv6 private network, the NLB instance resolves the NLB domain name to its service IP.<br><br>* Network interface: After the NLB instance is created, a service network interface is automatically provisioned in each availability zone, with the following IP addresses assigned:<br><br>   * Service IP: The IP address used to provide services.<br><br>      * IPv4: One IPv4 address, which can be transformed to associate the IPv4 address with an Elastic IP (EIP).<br><br>      * IPv6 (only available in dual\-stack NLB): One IPv6 address, which can be transformed to activate IPv6 Internet bandwidth for the IPv6 address.<br><br>   * Local IP: Dedicated for communication between the NLB and backend servers.<br><br>      * IPv4: Two IPv4 addresses.<br><br>      * IPv6 (only available in dual\-stack NLB): Two IPv6 addresses.<br><br><br>> **tip**<br><br><br>> Dual\-stack NLB is currently in Beta and only supports trial applications from Accounts that have completed enterprise certification. If you need a trial, please contact the account manager.<br> |
|Listener |The listener is responsible for monitoring user access requests received by the NLB instance based on specified protocols and ports.<br><br><br>* Protocol: TCP, UDP, TLS.<br><br>* Port: 1–65535<br><br><br>A listener only supports associating one server group.<br><br>[Prerequisite](https://docs.byteplus.com/en/docs/clb/NLB-Listener-overview) |
|Server Group |A server group is a collection of backend servers.<br><br><br>* Add backend servers, supported formats are as follows:<br><br>   * Elastic Compute Service (ECS): ECS in the same Virtual Private Cloud (VPC) as the NLB instance or secondary network interface attached to ECSs.<br><br>   * IP address: Only IPv4 addresses are supported. Network reachability is the sole requirement.<br><br>* You also need to configure a scheduling algorithm and health checks for the server group.<br><br>   * **Scheduling algorithm**: Distributes access requests reasonably among backend servers to prevent any single server from being overloaded while others remain idle.<br><br>   * **Health check**: Determines whether backend servers are functioning normally, preventing requests from being forwarded to abnormal servers and ensuring service availability.<br><br><br>Server group is decoupled from the NLB instance; A single server group can be associated with listeners across multiple NLB instances.<br><br>[Prerequisite](https://docs.byteplus.com/en/docs/clb/Server-Group-Overview) |

## Classification

For your convenience, we have classified NLB as below:

|Classification |Explanation |Application scenario |
|---|---|---|
|Internet NLB |Each service IP of NLB is either associated with an Elastic IP (EIP) or has enabled IPv6 Internet bandwidth. |Provide services to the Internet through the Internet NLB. |
|Private NLB |The service IP of the NLB is neither associated with an Elastic IP (EIP) nor enabled with IPv6 Internet bandwidth. |Provides services to the private network through the Private NLB. |
|Entrusted NLB |NLB instances created by managed cloud services. The NLB console only supports viewing and does not support modification. |NLB is used by other cloud\-managed services, such as Vital Kubernetes Engine. |

## Related products

|Service name |Feature Description |
|---|---|
|[Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service) |ECS instances serve as the backend servers of an NLB instance and receive traffic. |
|[VPC](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) |Provides a private network deployment environment for the NLB instance. |
|[Elastic IP Address](https://docs.byteplus.com/en/docs/eip/What-is-EIP) |Enable NLB instances to connect to IPv4 internet. |
|[IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway) |Enable NLB instances to connect to the IPv6 Internet. |
