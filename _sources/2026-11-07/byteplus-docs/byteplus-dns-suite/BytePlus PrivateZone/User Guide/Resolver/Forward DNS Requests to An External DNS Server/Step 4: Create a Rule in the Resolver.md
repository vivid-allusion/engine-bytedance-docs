---
title: "Step 4: Create a Rule in the Resolver"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/Zd7JQO"
---

This document describes how to create a rule. A rule specifies the domain names for which DNS queries need to be forwarded, the corresponding outbound endpoints, and the IP addresses of external DNS servers.

<span id="steps"></span>
## Steps

Follow the steps below to create a rule.


1. Open the [Resolver](https://console.byteplus.com/dns-suite/privatezone/resolver) page. Select the **rules** tab.

2. Click **Create rule**. On the **Create rule** page, configure the following parameters:

   
   |Parameter |Description |
   |---|---|
   |**Rule name** |The name of the rule. Supports UTF\-8 characters. |
   |**Rule type** |The type of the rule. You need to set this parameter to **Forward DNS queries to an external DNS server**: forward DNS queries originating from the VPC to an external DNS server. |
   |**Outbound endpoint** |The outbound endpoint you created. See [Create an Outbound Endpoint](https://docs.byteplus.com/docs/byteplus-dns-suite/OxDblm). This parameter cannot be modified after the rule is created. |
   |**Root domain** |The root domain associated with the rule. For example, if you set this parameter to `example.com`, DNS requests for `example.com` and all its subdomains will be forwarded.<br><br>You can enter one or more domain names. After entering a single domain name, press Enter to confirm. You can also paste multiple domain names at once, separated by semicolons (;). |
   |**IP address and port of an external DNS server** |The IP address and port of the external DNS server outside the VPC. `100.96.0.2` and `100.96.0.3` are reserved addresses. You cannot set this parameter to a reserved address. You can add up to 10 IP addresses. |
   |**VPC information** |The VPC associated with the rule. You can associate one or more VPCs. The region of the VPC associated with the rule must be the same as the region of the outbound VPC. |
   

   **Resource management**

   
   |Parameter |Description |
   |---|---|
   |**Project** |The name of the project to which the rule belongs. The default is **default**. You can click the drop\-down menu to select a project. BytePlus PrivateZone displays all projects for which the current primary account or IAM account has management permissions in the drop\-down menu. You can also click **Create project** to create a new project. |
   |**Tag** |Tags for the rule. Each tag is a key\-value pair. Click **Add tag** to add a tag, then enter the tag key and tag value in the two input boxes respectively, for example, `example-key` and `example-value`. Both tag keys and tag values support UTF\-8 characters. You need to press Enter after each input to confirm the content. You can add up to 20 tags for a rule. |
   

3. Click **Ok**.


<span id="next-steps"></span>
## Next steps

Next, you can [verify DNS outbound forwarding](https://docs.byteplus.com/docs/byteplus-dns-suite/IdrNXF).
