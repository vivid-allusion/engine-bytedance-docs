---
title: "Pushing images from CR Standard Edition instance in on-premises environment"
product: "Container Registry"
product_code: "cr"
source: "https://docs.byteplus.com/en/docs/cr/pull-a-container-registry-in-the-local-environment"
---

Some customers use hybrid cloud environments. They connect on\-premises IDC networks or office networks to the cloud through a VPN. This topic describes how to push and pull images between on\-premises environments and the cloud by using CR Standard Edition instances.

## Considerations

Public service CIDR blocks, such as `100.64.0.0/10`, may conflict with those of other cloud vendors. If you connect dedicated lines to multiple cloud vendors, IP address conflicts may occur. If this happens, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000208).

## VPN configuration options

You need a VPN to use CR in an on\-premises environment without public network access. The VPN configuration options are as follows.

> **tip**

* > You can obtain the TOS backend domain name by capturing network packets.

* > Editing the hosts file is lightweight, but the TOS resolved IP address may change. If your business requirements are high, we recommend that you configure DNS instead.

> If you need the above technical support, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000208).

### On\-premises environment without a self\-managed DNS

|Option |Procedure |Advantage |Disadvantage |
|---|---|---|---|
|Configure the hosts file |1. Establish routes between on\-premises and cloud CIDR blocks.<br><br>2. On the nodes that use CR, edit `/etc/hosts`.<br><br>   1. Resolve the CR instance domain name to the correct IP address.<br><br>   2. Resolve the CR instance's backend TOS domain name to the correct IP address. |Easy to configure. |* Only nodes configured with fixed IP resolution can use CR over the private network.<br><br>* TOS DNS resolution may change and may not be fixed. |

### On\-premises environment with a self\-managed DNS

|Option |Procedure |Advantage |Disadvantage |
|---|---|---|---|
|Configure DNS |1. Establish routes between on\-premises and cloud CIDR blocks.<br><br>2. Configure DNS settings. Set the upstream DNS servers of `*.cr.volces.com` and `*.ivolces.com` to `100.96.0.2` and `100.96.0.3`. |All on\-premises nodes can use CR over the private network. You do not need to configure TOS domain name resolution. TOS domain name changes do not affect usage. |More complex to configure. |
|Configure the hosts file |1. Establish routes between on\-premises and cloud CIDR blocks.<br><br>2. On the nodes that use CR, edit `/etc/hosts`.<br><br>   1. Resolve the CR instance domain name to the correct IP address.<br><br>   2. Resolve the CR instance's backend TOS domain name to the correct IP address. |Easy to configure. |* Only nodes configured with fixed IP resolution can use CR over the private network.<br><br>* TOS DNS resolution may change and may not be fixed. |

> **warning**

> Public service CIDR blocks, such as 100.64.0.0/10, may conflict with those of other cloud vendors. If you connect dedicated lines to multiple cloud vendors, IP address conflicts may occur. If this happens, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000208).

## Procedure

> **warning**

> TOS domain names and IP addresses in VPN settings require backend confirmation by CR engineers. If you need VPN or dedicated line configuration, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000208).

This topic uses the hosts file configuration option to describe how to pull images from a CR Standard Edition instance to an on\-premises data center.

1. Configure a VPN.

   Ensure the on\-premises data center and the CR Standard Edition instance can ping each other through private IP addresses. For details, see [Establishing network connectivity between VPC and self-managed cloud server](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-an-Alibaba-Cloud-server).

2. Configure the hosts file in the on\-premises data center.

   * Resolve the CR Standard Edition instance domain name `cr-demo-cn-beijing.cr.volces.com` to the VPC private IP address of the instance.

   * Resolve the TOS domain name `cr-cd99c276-3640-4cda-8fd6-****.tos-s3-cn-beijing.ivolces.com` to the VPC private IP address of the TOS storage corresponding to the CR Standard Edition instance.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_caad373d74fbbeed8640b55ebb34ddc0.png)

      > **tip**

      * > You can obtain the TOS backend domain name `cr-cd99c276-3640-4cda-8fd6-****.tos-s3-cn-beijing.ivolces.com` by capturing network packets.

      * > Editing the hosts file is lightweight, but the TOS resolved IP address may change. If your business requirements are high, we recommend that you configure DNS instead.

      > If you need the above technical support, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000208).

## Verification

* You can successfully log in to the CR instance in the on\-premises data center.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d465b3384273b0609344b43f24d5e378.png)

* You can successfully push images to the CR Standard Edition instance from the on\-premises data center.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9180bb7f0bfe8d357b8a4d8cb6af7d58.png)
