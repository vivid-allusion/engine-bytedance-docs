---
title: "Step 5: Verify DNS Outbound Forwarding"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/IdrNXF"
---

This document introduces how to verify whether DNS requests are forwarded to external DNS servers according to rules.

<span id="steps"></span>
## Steps

Send a DNS query from the VPC associated with the rule. The domain name in the DNS request should be the one you set in the rule. If you receive the resolution result returned by the external DNS server, it indicates that DNS outbound forwarding is effective.
