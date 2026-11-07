---
title: "Validate the DNS Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/IjW1Ax"
---

Finally, you need to verify whether the DNS record you created is active. Follow these steps to verify the DNS record.

<span id="verify-whether-the-dns-record-is-active"></span>
## Verify whether the DNS record is active

You can remotely connect to an ECS instance in the VPC associated with the domain name. Use the `nslookup` command to verify whether the domain `ecs.example.com` is successfully resolved.

```shell
$ nslookup ecs.example.com

Server:         100.96.0.2
Address:        100.96.0.2#53

Name:   ecs.example.com
Address: 10.0.1.128
```


If the DNS response contains the DNS record you added, it indicates that the DNS record is active.
