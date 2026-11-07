---
title: "Create an A Record and an AAAA Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/docs-adding-dns-records-to-your-domain"
---

You create two DNS records in BytePlus DNS, one is an A record and the other is an AAAA record.

The A record specifies the IPv4 address associated with the domain name, while the AAAA record specifies the IPv6 address associated with the domain name. BytePlus DNS can route user requests to the IPv4 and IPv6 addresses of the website server for the domain `www.example.com` based on these two DNS records.

<span id="steps"></span>
## Steps

Follow the steps below to create an A record and an AAAA record.

<span id="create-an-a-record"></span>
### Create an A record


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, click your domain in the **Domain** column of the domain list.

3. On the **Records management** tab, click **Create record set**.

4. On the **Create record set** page, set the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Record type** |Set to **A**. |
   |**Domain name** |Set to the domain prefix. For example, if your domain name is `www.example.com`, the domain prefix is `www`. |
   |**Record value** |Click **Create record value** to create a record value. Set the record value to the IPv4 address of your website server, for example, `203.0.113.1`. |
   

5. After setting the parameters, click **Submit**.


<span id="19184cf7"></span>
### Create an AAAA record


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, click your domain in the **Domain** column of the domain list.

3. On the **Records management** tab, click **Create record set**.

4. On the **Create record set** page, set the following parameters:



|**Parameter** |**Description** |
|---|---|
|**Record type** |Set to **AAAA**. |
|**Domain name** |Set to the domain prefix. For example, if your domain name is `www.example.com`, the domain prefix is `www`. |
|**Record value** |Click **Create record value** to create a record value. Set the record value to the IPv6 address of your website server, for example, `2001:db8::`. |



5. After setting the parameters, click **Submit**.


<span id="next-steps"></span>
## Next steps

[Verify Whether the DNS Records Are Active](https://docs.byteplus.com/docs/byteplus-dns-suite/docs-validating-your-dns-records)
