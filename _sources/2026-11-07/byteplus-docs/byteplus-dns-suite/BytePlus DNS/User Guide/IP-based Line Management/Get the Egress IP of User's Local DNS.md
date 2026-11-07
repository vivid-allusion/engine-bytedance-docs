---
title: "Get the Egress IP of User's Local DNS"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-getting-the-egress-ip-of-user-s-local-dns"
---

This document describes how to obtain the egress IP of a user's Local DNS server.

If the user's Local DNS server does not support the ECS protocol, BytePlus DNS will use the client IP in the UDP packet to match the IP\-based line. You need to configure the IP\-based line based on the egress IP of the Local DNS server.

<span id="steps"></span>
## Steps

You can use the `dig` command to obtain the egress IP of the user's Local DNS. Assuming the IP address of the Local DNS server is `2xx.2xx.1xx.2xx` and the user's IP address range is `1.1.1.1/20`, you need to use the following command to obtain the egress IP of the user's Local DNS.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Because the Local DNS server may have multiple egress IPs, the egress IP returned by the following command may not include all egress IPs.</div>


```Shell
dig @2xx.2xx.1xx.2xx whoami.byte008.com +subnet=1.1.1.1/20
```


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28950f1d7b5c8f17538bc9978d9129cc.png) </span>

After obtaining the egress IP of the user's Local DNS server, you need to [create an IP-based line](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-creating-an-ip-based-line) based on that IP.
