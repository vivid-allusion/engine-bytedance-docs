---
title: "Planning and preparation"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Planning-and-preparation"
---

Before creating a Classic Load Balancer (CLB) instance, you need to make the following planning and preparation:

<span id=".5YeG5aSH5ZCO56uv5pyN5Yqh5Zmo"></span>
## Prepare backend servers


* Prepare a VPC environment: the CLB instance should be in the same VPC as the backend servers it serves. When creating a VPC, it is recommended to choose a region as close to the client's geographical location as possible to reduce latency and improve download speed. You can see [Building an IPv4 VPC](https://docs.byteplus.com/en/docs/vpc/Building-an-IPv4-VPC) to create a new VPC.

* Build your backend server environment within the VPC: backend servers support two types: Elastic Compute Service and network interface.

   * Please see [purchasing an Elastic Compute Service](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) to create an Elastic Compute Service instance.

   * If you select a network interface as the backend server, first [create a network interface](https://docs.byteplus.com/en/docs/vpc/Creating-a-secondary-network-interface) and attach it to the Elastic Compute Service instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Ensure the security group associated with the backend server group has the service ports open. Please see <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">configuring backend server security groups</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select the secondary network interface, also configure a route entry for this secondary network interface so that the network interface can respond to the requests sent by the client or CLB instance. Please see <a href="https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface">configuring secondary network interface routes</a>.   </div>
   

* Plan the request weights according to the service capabilities of each backend server instance.


<span id=".6KeE5YiS5a6e5L6L5Zyw5Z-f5Y-K5Y-v55So5Yy6"></span>
## Plan instance regions and availability zones


* Plan the region

   * The deployment region of the CLB instance and the backend server is recommended to be as geographically close as possible to the client's source to reduce latency and improve download speed.

   * Please Confirm that the CLB instance and the backend server instance providing the service are located in the same Region.

* Plan availability zones

   It is recommended that the primary Availability Zone of the CLB instance remains consistent with the Availability Zone of the backend server.


<span id=".6KeE5YiS572R57uc57G75Z6L"></span>
## Plan network type

CLB is divided into two types: internet and private network. The IP versions of CLB include IPv4 and dual\-stack.


|Topic |IP version |Explanation |
|---|---|---|
|Internet\-facing instance |IPv4 |If you want the CLB instance to be accessible to the internet throughout its lifecycle, it is recommended to select the internet Type. |
||Dual\-stack |CLB currently does not support creating dual stack types of internet instances. |
|private instance |IPv4 |If you want the CLB instance to flexibly adjust whether it is exposed to the IPv4 internet, it is recommended to select the IPv4 private network type. After creating a CLB instance, you can bind/disassociate an Elastic IP (EIP) to/from the instance at any time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Before associating an EIP, confirm that you have purchased an EIP instance.</div><br> |
||Dual\-stack |If you want the CLB instance to be accessible from an IPv6 network, it is recommended to select the dual stack private network type. After creating a CLB instance, the instance can be accessed simultaneously via IPv4 and IPv6 private networks. You can also flexibly adjust whether the instance is exposed to the IPv4 and IPv6 internet based on the network type.<br><br><br>* IPv4 internet: bind/unbind an EIP to the instance.<br><br>* IPv6 internet: open/delete IPv6 internet bandwidth for the instance's IPv6 address. |


If you select a public instance, plan in advance the maximum EIP bandwidth and ISP, and ensure that the ISP is BGP (Multi\-ISP).

<span id=".6KeE5YiS5a6e5L6L6KeE5qC8"></span>
## Plan instance type

Based on the expected business volume, select the suitable instance type by referring to the specifications in [Product Type and Specifications](https://docs.byteplus.com/en/docs/clb/Product-Overview-02).

<span id=".6KeE5YiS5Y2P6K6u57G75Z6L"></span>
## Plan protocol type

The working mechanism of the CLB listener varies depending on the protocol. Select the listener protocol type according to your business needs.


* Working principle of layer\-4 protocol listeners:

   Listener working principle: Upon receiving a request, the listener only forwards data and modifies the packet's IP address. The actual connection is established between the client and the backend server.

* Working principle of layer\-7 protocol listeners:

   The listener establishes a connection with the client, receives and parses client packets, and based on specific fields and traffic distribution policies in the packet, establishes new connections with backend servers to forward the data.
