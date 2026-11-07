---
title: "Add a Domain"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/YBQ0UN"
---

After activating the service, you need to add the domain `example.com` in BytePlus PrivateZone and associate the domain name with a VPC named `vpc01` with ID `vpc-xxxxx`.

<span id="steps"></span>
## Steps

Follow these steps to add a domain:


1. Open the [BytePlus PrivateZone console](https://console.byteplus.com/dns-suite/dns/privatezone/zones).

2. On the **Domain management** page, click **Create domain**.

3. In the **Create domain** dialog box, configure the basic information of the domain and the Virtual Private Cloud (VPC) information.

   * **Domain name**: Set this parameter to `example.com`.

   * **VPC information**: Associate the domain with a VPC named `vpc01` with ID `vpc-xxxxx`.

4. Click **OK**. You can see the added domain on the **Domain management** page.


You have successfully added a domain.

Next, you need to create a DNS record for the domain. See [Create a DNS record](https://docs.byteplus.com/docs/byteplus-dns-suite/8Ek2VY).
