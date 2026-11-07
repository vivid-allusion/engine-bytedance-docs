---
title: "Create a DNS Record"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/8Ek2VY"
---

After adding a domain name, you can create an DNS record for the domain in BytePlus PrivateZone. In the DNS record, you point `ecs.example.com` to the private IP address `10.0.1.128` of an ECS instance.

<span id="steps"></span>
## Steps

Follow these steps to add a DNS record:


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, find the domain name for which you want to create a DNS record. Click **Manage** in the **Action** column.

3. On the **Record management** page, select the **DNS records** tab. Then click **Create record set** to create a DNS record for the domain name.

4. On the **Create record set** page, configure the basic information of the DNS record:

   * **Domain name**: Set the domain name prefix to `ecs`. This way, the domain name becomes `ecs.example.com`.

   * **Record type**: Set this parameter to **A**.

   * **Record value**: Set this parameter to the private IP address of the ECS instance, which is `10.0.1.128`.

5. After the configuration is complete, click **Submit**. You can see the created DNS record on the **Record management** page.


You have now successfully added a DNS record. Next, you need to [verify the DNS record](https://docs.byteplus.com/en/docs/byteplus-dns-suite/IjW1Ax).
