---
title: "Step 4: Create Rules in the DNS Server of the On-premise IDC/Third-party Cloud Services"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/8NimQy"
---

This document describes how to create a rule in the DNS server of your on\-premise IDC/third\-party cloud service.

<span id="steps"></span>
## Steps

Create a rule in the DNS server of your on\-premise IDC/third\-party cloud service to forward DNS queries to the inbound IP address of the inbound endpoint. Refer to [Create an Inbound Endpoint](https://docs.byteplus.com/docs/byteplus-dns-suite/EddkeA) to learn how to obtain the inbound IP address of the inbound endpoint.

For example, if you want the DNS queries for `a.example.com` to be forwarded to the resolver, and the inbound IP addresses of the inbound endpoint are `10.0.0.1` and `10.0.1.128`, you create a rule in the DNS server:


|Domain |Target IP |
|---|---|
|`a.example.com` |`10.0.0.1`, `10.0.1.128` (backup) |


There should be at least 2 inbound IP addresses. Therefore, you can set one of the IP addresses as the primary address and the other IP addresses as backup addresses.

<span id="next-steps"></span>
## Next steps

Next, you can [verify DNS query responses](https://docs.byteplus.com/en/docs/6758/1171696).
