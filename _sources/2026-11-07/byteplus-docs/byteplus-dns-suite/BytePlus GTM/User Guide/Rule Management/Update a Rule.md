---
title: "Update a Rule"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/T849Eo"
---

This document describes how to update rules in BytePlus GTM.

Before updating a rule, you must stop the GTM instance where the rule is included.

<span id="steps"></span>
## Steps

Complete the following steps to update a rule.


1. On the [Instance management page](https://console.byteplus.com/dns-suite/gtm/instances), find your GTM instance. Click the domain name in the **Domain** column.

2. In the **Policy management** tab, click the **Configure** button of the enabled policy.

3. In the **Custom rules** tab, find the rule you need to configure. Click **Manage** in the **Actions** column to update the rule. Refer to [Create a Rule](https://docs.byteplus.com/docs/byteplus-dns-suite/snlUdP) for detailed parameter information.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to change the address type from IP address to domain name, or from domain name to IP address, you need to clear the pool of the GTM instance and then modify the address type of the GTM instance.   </div>
   

4. After the update is complete, click **OK** to save the changes. The updated rule takes effect after you restart the GTM instance that contains the rule.
