---
title: "Instance overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/type_of_instance"
---

To use ALB service, you need to create an ALB instance first. An ALB instance is a specific load balancer that you can configure and manage. The ALB instance receives requests from clients and distributes them to backend servers based on your forwarding rules and load balancing policies.

<span id="629339d3"></span>
## Instance Network Type

ALB instances are divided into two types: Internet\-facing instances and private instances. You can create an Internet\-facing instance or a private instance based on your usage scenario.

<span id="cda8fb2f"></span>
### Internet\-facing instance

After you create an Internet\-facing instance, it obtains both a [public IP address](https://docs.byteplus.com/en/docs/eip/What-is-EIP) and a [private IP address](https://docs.byteplus.com/en/docs/vpc/What-is-VPC). The public IP address enables the instance to handle requests from clients on the internet. Private IP addresses enable instances to handle requests from clients within the private network.

<span id="4b7ded5e"></span>
### Private instance

After you create a private instance, it receives only one [private IP address](https://docs.byteplus.com/en/docs/vpc/What-is-VPC) and can only handle requests from clients within the private network.

<span id="1ebc9688"></span>
## Instance IP type

The IP types for ALB instances include IPv4 and IPv4/IPv6 dual\-stack.


|**IP type** |**Public network ALB instance** |**Private network ALB instance** |**Explanation** |
|---|---|---|---|
|IPv4 |Each availability zone where the public network ALB instance resides provides one public IPv4 address and one private IPv4 address. |Each availability zone where the private network ALB instance resides provides one private IPv4 address. |When the ALB instance’s IP type is IPv4, clients can only access the ALB instance using the IPv4 address.<br><br>The ALB instance forwards client requests to backend servers that support IPv4. |
|IPv4/IPv6 dual\-stack |Each availability zone where the public network ALB instance is located provides one public IPv4 address, one private IPv4 address, and one IPv6 address. The IPv6 address serves as both the public and private IP address. |Each availability zone where the private network ALB instance resides provides one private IPv4 address and one private IPv6 address. |When the ALB instance’s IP type is IPv4/IPv6 dual\-stack, clients can access the ALB instance using either the IPv4 address or the IPv6 address.<br><br>The ALB instance forwards client requests to backend servers that support IPv4. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the IP type of an ALB instance is IPv4/IPv6 dual\-stack, please note the following conditions:</div>



* <div data-tips="true" data-tips-type="tip">The network type of an ALB instance cannot be changed.</div>


* <div data-tips="true" data-tips-type="tip">If you need to use a dual\-stack ALB instance, contact customer service support or <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000645">submit a ticket</a> to apply.</div>



<span id="1d33eca0"></span>
## Instance domain name

After you create an ALB instance, the system assigns not only an IP address but also a unique domain name to the instance. The format of the instance domain name is: *instanceId*.*regionId*.volcenginealb.com。 e.g., alb\-abc123def456.cn\-beijing.volcenginealb.com.

Instance domain names can only be used as target domains in CNAME records and cannot be accessed directly. You can use a more memorable custom domain name like www.example.com, then use a CNAME record to associate it with the instance domain name. When clients initiate requests using the custom domain name, the DNS server resolves the custom domain name to the instance domain name. For instructions on adding a CNAME record, see [Add a CNAME record pointing to the instance domain name](https://docs.byteplus.com/docs/clb/Configuring-domain-name-resolution).

<span id="05692b72"></span>
## Availability zones and instance nodes

When creating an ALB instance, you need to select its region and availability zones. If multiple availability zones exist within your chosen region, it is recommended to select at least two availability zones to deploy ALB instances to further improve overall system availability. Thus, when an availability zone fails or has no available backend servers, ALB forwards requests to backend servers in other availability zones to ensure business continuity. For more information about regions and availability zones, see [Regions and Availability Zones](https://docs.byteplus.com/docs/clb/Regions-and-Availability-Zones).

When you deploy an ALB instance to an availability zone, ALB creates an instance node in each availability zone where the instance is located. Under normal circumstances, client traffic is evenly distributed to each instance node.

<span id="10f8813b"></span>
## Cross\-availability zone load balancing

The ALB instance\-level <i\>cross\-availability zone load balancing</i\> feature is enabled by default and cannot be disabled. By default, an instance node in one availability zone distributes received requests to backend servers across all availability zones where the ALB instance is located.

You can disable the <i\>cross\-availability zone load balancing</i\> feature at the server group level. After disabling this feature, the instance node only distributes received requests to backend servers within the same availability zone.

For more information about the <i\>cross\-availability zone load balancing</i\> feature, see [cross-availability zone load balancing](https://docs.byteplus.com/docs/clb/Cross-zone-load-balancing).
