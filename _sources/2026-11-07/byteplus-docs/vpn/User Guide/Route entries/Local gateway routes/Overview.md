---
title: "Overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Overview-1"
---

When using VPN Connect to achieve interconnection between an on\-premises data center (IDC) and a Virtual Private Cloud (VPC), you also need to configure VPN in the IDC's gateway after completing configurations on the cloud. Due to the wide variety of local firewall models, configurations may vary slightly between different models. Therefore, this topic introduces the on\-premises VPN configuration of common firewalls.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The gateway device in your on\-premises data center supports the IKE V1 or IKE V2 protocol.

* The gateway device in your data center has a static Elastic IP Address (EIP).

* The CIDR blocks of your data center must not overlap with those of the VPC where the VPN gateway to be communicated with is located.


<span id=".6YWN572u5Y-C6ICD"></span>
## Configuration examples

For your convenience, we introduce two configuration methods. You can select the one that best suits your scenario.

<span id=".5omL5Yqo6YWN572u"></span>
### Manual configuration


* [Configuring the Sangfor firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Sangfor_firewall)

* [Configuring the Cisco firewall](https://docs.byteplus.com/en/docs/vpn/Configuring-a-Cisco-firewall)

* [Configuring the H3C firewall](https://docs.byteplus.com/en/docs/vpn/Configuring-an-H3C-firewall)

* [Configuring the Hillstone firewall](https://docs.byteplus.com/en/docs/vpn/Configuring_a_Hillstone_firewall)


<span id=".5paH5Lu26YWN572u"></span>
## File configuration


* [Cisco firewall configuration file](https://docs.byteplus.com/en/docs/vpn/Cisco-firewall-configuration-file)

* [H3C firewall configuration file](https://docs.byteplus.com/en/docs/vpn/H3C-firewall-configuration-file)
