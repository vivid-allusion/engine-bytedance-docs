---
title: "Verify Whether the DNS Records Are Active"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/duY-0a"
---

You can use the `nslookup` command or the `dig` command to Check whether your created DNS records have taken effect.

<span id="steps"></span>
## Steps

Taking `nslookup` as an example, you can run the following commands to verify whether the DNS records have taken effect. This tutorial assumes your domain name is `example.com`. You need to replace this domain name with the one you're actually using.

```bash
# Check whether the TXT record has taken effect
nslookup -type=txt example.com
```


```bash
# Check whether the MX record has taken effect
nslookup -type=mx example.com
```


If the results return both TXT and MX records, it indicates that the TXT and MX records you added have taken effect.

Now, you have verified your domain ownership through the TXT record and associated your domain with an email server using the MX record.
