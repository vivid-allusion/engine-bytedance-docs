---
title: "Verify Whether the DNS Records Are Active"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-validating-your-dns-records"
---

You can use the `nslookup` command or the `dig` command to Check whether the DNS records you created are active.

<span id="steps"></span>
## Steps

This tutorial assumes your domain name is `example.com`. Using `nslookup` as an example, you can run the following commands to verify if the DNS records are active.

You need to replace this domain name with the one you're actually using.

```Bash
# Check whether the A record is active
nslookup www.example.com
```


```Bash
# Check whether the AAAA record is active
nslookup -type=aaaa www.example.com
```


If the results return the IPv4 address from the A record and the IPv6 address from the AAAA record, it indicates that the A record and AAAA record you created are active.

Now, you have routed user requests accessing your website domain to your website server through A and AAAA records.
