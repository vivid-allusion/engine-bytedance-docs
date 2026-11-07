---
title: "VPN management FAQ"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-vpn-management-faq"
---

While using the SealSuite VPN management module, if you encounter any issues or have questions, refer to the following frequently asked questions and its provided solution for assistance.

<span id="56a8bb23"></span>
## Does the client use DNS configured by the VPN gateway for resolution when accessing domain name type resources configured in VPN?

Currently, there are two types of SealSuite control modes: Full Tunnel mode and split tunnel mode:


* Full Tunnel mode: Resolved by the DNS server set up on the VPN gateway.

* Split tunnel mode:

   * Domain names are in split tunnel mode domain name list: When accessing domain names, SealSuite client will start a DNS 127.0.0.1 proxy in the terminal, and send the DNS request to the VPN gateway for processing, which is resolved by the DNS server configured on the VPN gateway.

   * Domain names are not in split tunnel mode domain name list: The domain names are resolved by the DNS configured on the mobile terminal.


<span id="976ca47d"></span>
## When the account system is used to access VPN, is there a risk of directly accessing the office network through VPN when the account system is leaked?

To prevent this risk, you are advised to enable the two\-factor authentication function in **Identity** \> **Account Settings** \> **Authentication** of the Admin Portal.

<span id="968d17d9"></span>
## What's the difference between SealSuite's split tunnel mode and Full Tunnel mode?

SealSuite products support two VPN modes: Full Tunnel mode and split tunnel mode, with the following differences:


* In Full Tunnel mode, all network traffic will be forwarded through VPN encrypted tunnels.

* In split tunnel mode, only IP or domain names configured within high\-speed resources will be forwarded through VPN encrypted tunnels.


<span id="c032bb01"></span>
## Why can't I access the internal domain name after configuring the split tunnel mode resources?

If you intend to access internal domain names, both domain name resources and IP resources need to be configured simultaneously.

<span id="87580945"></span>
## Does the domain name list in VPN resource configuration support pan domain names?

SealSuite supports pan domain names, and the configuration path is as follows:


1. Log in to the Admin Portal.

2. In the left navigation bar, click **VPN Management** ＞ **Advanced Settings**.

3. In the **Split Tunnel Mode** area, click **Add New Resource**.

4. Configure pan domain name resources, with a specific format of`*example.com`, and corresponding IP fields need to be configured.


<span id="465e77e1"></span>
## Can specific personnel be restricted from seeing specific VPN gateways?

Yes. Set the visible objects of VPN gateways in the **VPN Management** \> **VPN Gateway** in the Admin Portal.

<span id="238ff277"></span>
## What is the logic for switching between UDP and TCP protocols?

If the Admin Portal enables dual protocols, it will first attempt to connect via UDP protocol, and if the connection fails, it will then attempt to connect via TCP protocol.

<span id="fa199938"></span>
## How to uninstall a VPN gateway after installing it on a virtual machine?

Solution: Access the operating system and execute the following command.

```Bash
sudo /opt/feilian/vpn/uninstall.sh
```


<span id="bcda1c7a"></span>
## How to handle VPN error messages when connecting to a VPN gateway after it goes online?

Solution:


1. Please first check if the VPN gateway status displayed on the client is normal.

2. Please check if the control port and data port corresponding to accessing VPN gateways from the public network are normal.

3. Please check if the virtual machine where the VPN gateway is installed has firewalld service enabled. If so, please close it and check the iptables rule again.


<span id="a31e21e4"></span>
## How to handle the situation where the routing of Full Tunnel resources in split tunnel mode is not distributed to the client, resulting in the inability of split tunnel mode to access resources?

The resources in split tunnel mode are divided into Full Tunnel resources and single gateway resources.


* Full Tunnel resources refer to the split tunnel mode Full Tunnel resources that you have added in the **VPN Management** \> **Advanced Settings** section of the Admin Portal.

* Single gateway resources refer to the split tunnel mode single gateway resources that you add to the network mode tab within the designated VPN gateway in the **VPN Management** \> **VPN Gateway** section of the Admin Portal.


If you have configured resources in split tunnel mode in both of the two above functions, single gateway resources will take priority, resulting in Full Tunnel resources in split tunnel mode not taking effect.

<span id="19c15335"></span>
## When configuring VPN access resources, if only domain name resources are configured and HTTP+HTTPS is selected, will it be impossible to use programs such as ping and traceroute to track routes?

Programs such as ping cannot be used because they use ICMP. If you need to use it, you need to add corresponding IP resources for the domain name and add the ICMP protocol.

<span id="aa2abbaf"></span>
## How to select the transmission protocol in SealSuite VPN configuration?

The transmission protocol refers to the type of packet sent by the SealSuite client. It is recommended to select **automatic selection of TCP and UDP**, as some networks may discard UDP packets.

<span id="a7598060"></span>
## Can the default open mode of VPN be configured for a specific VPN gateway?

The default open mode is for the entire VPN function module and cannot be configured for a specific gateway.
