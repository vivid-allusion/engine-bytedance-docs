---
title: "Use DNAT to configure Logstash access from the public network"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Use_DNAT_to_configure_Logstash_access_from_the_public_network"
---

The Logstash instance for Cloud Search is deployed in a Virtual Private Cloud (VPC). To push data to Logstash from the public network, you need to connect the private network and the public network through a NAT gateway, ensuring that Logstash inside the VPC can communicate normally with the public network. This topic describes how to use DNAT to configure public network access to Logstash.

<span id="AniHVNcW"></span>
## Feature introduction

The public NAT Gateway is an enterprise\-level public network gateway that provides public address translation services for cloud servers within a private network. The public NAT Gateway supports SNAT rules that translate source addresses. When a cloud server actively accesses the public network, the NAT Gateway replaces the source IP and port in the request with a public IP and port before forwarding. For details, see [What is a NAT Gateway](https://docs.byteplus.com/en/docs/natgateway/What-is-NAT-Gateway).

<span id="1OdkQv2y"></span>
## Prerequisites

Created Logstash instance. For detailed operations, see [Create a Logstash instance](https://docs.byteplus.com/en/docs/cloudsearch/Create_a_Logstash_instance).

<span id="1OdkQv2y"></span>
## Precautions

If a NAT gateway is already configured in the virtual private cloud, you need to configure routing for it to take effect. For detailed operations, see [Deploy multiple public NAT gateways in a single virtual private cloud](https://docs.byteplus.com/en/docs/natgateway/Configuring-multiple-Internet-NAT-Gateways-in-a-VPC).

<span id="1OdkQv2y"></span>
## Procedure


1. Refer to [Create a public NAT gateway](https://docs.byteplus.com/en/docs/natgateway/Creating-an-Internet-NAT-gateway) to create a public NAT gateway, and select the **VPC** and **Subnet** to which the target Logstash instance belongs.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To view the virtual private cloud and subnet of the Logstash instance, see <a href="https://docs.byteplus.com/en/docs/cloudsearch/View_Logstash_instance_information">View Logstash instance information</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">It is recommended to choose <strong>Manual configuration</strong> for <strong>EIP and access rule setup</strong> to restrict access by virtual private cloud and subnet. If you want all containers in the virtual private cloud to access the public network, select <strong>Automatic configuration</strong> and then choose the public IP to associate. Selecting <strong>Automatic configuration</strong> allows you to skip the following steps.   </div>
   

2. See [Associate/Disassociate an EIP](https://docs.byteplus.com/en/docs/natgateway/Associating-or-disassociating-an-EIP) to associate the EIP with the created public NAT gateway.

3. See [manage DNAT rules](https://docs.byteplus.com/en/docs/natgateway/Managing-DNAT-rules?lang=en) to create DNAT rules.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The agreement depends on the input plugin type; if in doubt, please <a href="https://console.byteplus.com/workorder/create?step=1&SubProductID=P00000255">submit a ticket</a> for consultation.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The private network port can only be 9600 or within the range [10000, 11000].   </div>
