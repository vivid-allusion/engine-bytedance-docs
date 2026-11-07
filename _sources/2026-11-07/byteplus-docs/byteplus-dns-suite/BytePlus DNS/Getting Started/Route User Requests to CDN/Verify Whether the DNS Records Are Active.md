---
title: "Verify Whether the DNS Records Are Active"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/V3qfZ8"
---

You can use the `nslookup` command or the `dig` command to check if your created DNS record has taken effect.

<span id="steps"></span>
## Steps

Taking `nslookup` as an example, you can run the following command to verify if the DNS record has taken effect. This tutorial assumes your domain name is `www.example.com`. You need to replace this domain name with the one you're actually using.

```bash
# Check if the CNAME record has taken effect
nslookup -type=cname www.example.com
```


If the result returns a CNAME record, it indicates that the CNAME record you added has taken effect.

Now, you have routed the user requests to your domain to CDN through the CNAME record.
