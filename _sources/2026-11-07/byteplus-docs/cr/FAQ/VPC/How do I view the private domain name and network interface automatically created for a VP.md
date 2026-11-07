---
title: "How do I view the private domain name and network interface automatically created for a VPC?"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/How_to_view_the_private_domain_name_and_the_network_interface_when_creating_a_private_network_VPC"
---

To establish the connectivity between a CR instance and a VPC, the private domain name of the instance needs to be resolved to an IP address within that VPC. Therefore, for each VPC you associate with an instance, one **private domain name (PrivateZone) record** and one **elastic network interface (ENI)**  are automatically created for resolution. You can view them as follows.

1. When you add a VPC to the instance, the resolved private IP address is automatically generated. Obtain it from the **Intranet resolution IP** field.

2. View the private domain name and elastic network interface in the corresponding consoles.

   * **Private DNS record**

      On the [Domain management](https://console.byteplus.com/TrafficRoute/dns/privatezone/zones) page, click the target domain name. Then, on the **DNS records** page, view the record whose **Record value** is the **Intranet resolution IP** of the VPC.

   * **Elastic network interface**

      In the [VPC console](https://console.byteplus.com/vpc), go to the "Network Interface" page and find the interface whose **Private IP Address** matches the **Intranet resolution IP** of the VPC.
