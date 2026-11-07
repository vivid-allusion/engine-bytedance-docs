---
title: "Create an IP-based Line"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-creating-an-ip-based-line"
---

Before configuring an IP\-based line for your DNS records, you need to create an IP\-based line.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">BytePlus DNS prioritizes using the partial client IP address included in the <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-basicconcepts#ecs-protocol-edns-client-subnet-protocol">EDNS Client Subnet (ECS) protocol</a> information in the DNS query to match the line. If the user's Local DNS server does not support the ECS protocol, BytePlus DNS will use the client IP address in the UDP packet to match the line. Most of these client IP addresses are the egress IP addresses of the Local DNS server. You can refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-how-it-works">How It Works</a> for more information.</div>


<div data-tips="true" data-tips-type="tip">Therefore, if the user's Local DNS server does not support the ECS protocol, you need to determine the IP address range in the IP\-based line based on the egress IP address of the Local DNS server when creating an IP\-based line. For detailed steps, please refer to <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/docs-getting-the-egress-ip-of-user-s-local-dns">Get the Egress IP of User's Local DNS</a>.</div>


<span id="steps"></span>
## Steps

You can add an IP\-based line by following these steps.


1. Open the [IP-based Lines](https://console.byteplus.com/dns-suite/dns/lines) page in the BytePlus DNS console.

2. Click on **Create IP\-based line**.

3. On the **Create IP\-based line** page, configure the following parameters:



|**Parameter** |**Description** |
|---|---|
|**Name** |The name of the IP\-based line. It should be in UTF\-8 format and can have a maximum length of 32 UTF\-8 characters. |
|**Comments** |Additional comments for the IP\-based line. It should be in UTF\-8 format and can have a maximum length of 64 UTF\-8 characters. |
|**CIDR block** |The CIDR block of the IP\-based line, represented in [CIDR format](https://datatracker.ietf.org/doc/html/rfc1519). You can enter a CIDR address block for IPv4 or IPv6 addresses. For example, `192.168.1.0/24` or `2001:db8::/103`. You can also enter multiple CIDR blocks. You can add up to 1000 CIDR address blocks. Each CIDR block should be on a new line. For example:<br><br>```Plain```<br>```192.168.1.0/24```<br>```10.24.0.0/21```<br> |



4. Click **OK**. The IP\-based line you created will be displayed in the list.


<span id="next-steps"></span>
## Next steps


* [Configure DNS Records to Use IP-based lines](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-configure-dns-records-to-use-ip-based-lines)

* [Update an IP-based Line](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-updating-an-ip-based-line)

* [Delete an IP-based Line](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-deleting-an-ip-based-line)
