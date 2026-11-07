---
title: "Create TXT Records and MX Records"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/ipvFf6"
---

You create two TXT records and three MX records for the domain name `example.com` in BytePlus DNS.

<span id="steps"></span>
## Steps

Follow these steps to create two TXT records and three MX records.

<span id="create-two-txt-records"></span>
### Create two TXT records


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, in the domain list, click your domain name in the **Domain** column.

3. On the **Record management** tab, click **Create record set**.

4. On the **Create record set** page, set the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Domain** |Set this to the domain prefix of your domain name. In this tutorial, you need to set this parameter to `@`. |
   |**Record type** |Set this to **TXT**. |
   |**TTL** |Set this to **10 minutes**. |
   |**Record Value** |1. Click **Create record value** to create a record value, and set the record value to the TXT record value for domain ownership verification, which is `verification-code-site-App_abcde_1234`.<br><br>2. Click **Create record value** to create another record value, and set it to the TXT record value for the SPF record, which is `v=spf1 a mx ~all`. |
   

5. After setting the parameters, click **Submit**.


<span id="create-three-mx-records"></span>
### Create three MX records


1. Open the [BytePlus DNS console](https://console.byteplus.com/dns-suite/dns).

2. On the **Domain management** page, in the domain list, click your domain name in the **Domain** column.

3. On the **Record management** tab, click **Create record**.

4. On the **Create record set** page, set the following parameters:

   
   |**Parameter** |**Description** |
   |---|---|
   |**Domain** |Set this to the domain prefix of your domain name. In this tutorial, you need to set this parameter to `@`. |
   |**Record type** |Set this to **MX**. |
   |**TTL** |Set this to **10 minutes**. |
   |**Record value** |1. Click **Create record value** to add a record value. Set the record value to the MX record value with priority 1, which is `1 mx1.mail.com`.<br><br>2. Click **Create record value** to add a record value, and set it to the MX record value with priority 2, which is `2 mx2.mail.com`.<br><br>3. Click **Create record value** to add a record value, and set it to the MX record value with priority 3, which is `3 mx3.mail.com`. |
   

5. After setting the parameters, click **Submit**.


<span id="next-steps"></span>
## Next steps

[Verify Whether the DNS Records Are Active](https://docs.byteplus.com/docs/byteplus-dns-suite/duY-0a).
