---
title: "Create a CNAME Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/9h8CZf"
---

You add a CNAME record for the domain name `www.example.com` in BytePlus DNS.

<span id="steps"></span>
## Steps

Follow these steps to add a CNAME record.

<span id="create-a-cname-record"></span>
### Create a CNAME record


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, in the domain list, click your domain name in the **Domain** column.

3. On the **Record management** tab, click **Create record set**.

4. On the **Create record set** page, set the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Domain** |Set this to the domain prefix of your domain name. In this tutorial, you need to set this parameter to `www`. |
   |**Record type** |Set this to **CNAME**. |
   |**TTL** |Set this to **10 minutes**. |
   |**Record value** |Click **Create record value** to add a record value. Set the record value to the CNAME record value, which is `www.example.com.byteplusgslb.com`. |
   

5. After setting the parameters, click **Submit**.


<span id="what-to-do-next"></span>
## What to do next

[Verify Whether the DNS Records Are Active](https://docs.byteplus.com/docs/byteplus-dns-suite/V3qfZ8?type=preview)
