---
title: "Internet border firewall"
product: "Cloud Firewall"
product_code: "cloud_firewall"
source: "https://docs.byteplus.com/en/docs/cloud_firewall/Internet_border_firewall"
---

<span id="590a3bc3"></span>
### What asset types does the internet border firewall currently support? Which asset types support automatic protection activation? The internet border firewall can provide protection for the following cloud assets:


* Cloud server (ECS)

* High\-availability virtual IP (HAVIP)

* Traditional load balancer (CLB)

* Application load balancer (ALB)

* NAT gateway

* VPN gateway

* Elastic Network Interface (ENI)

* WAF Elastic Public IP (CNAME Access Method)


<span id="d100c80b"></span>
### What impact will turning the asset protection switch on or off in the Internet boundary firewall have on the business? 

The Internet boundary firewall supports switching public EIP asset protection in seconds. Whether protection is turned on or off, it will not affect your business.

<span id="eb7f83c9"></span>
### Does the Internet boundary firewall support protecting IPv6 assets? 

Currently, the Internet boundary firewall only supports IPv4 asset protection and does not support IPv6 asset protection.

<span id="52a102e5"></span>
### Just activated the cloud firewall, and the Internet boundary switch page shows no public EIP assets? 

This is a normal phenomenon. After the cloud firewall is activated for the first time, the system needs to synchronize the EIP asset information under your account, and this process usually takes 2\-3 minutes. After synchronization is complete, you will be able to see all public EIP assets on the internet boundary switch page. We recommend that you wait a moment and refresh to check.
