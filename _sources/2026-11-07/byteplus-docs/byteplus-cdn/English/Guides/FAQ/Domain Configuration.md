---
title: "Domain Configuration"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/domain-config-faqs_en-us"
---

<span id="cannot-update-policy-configurations-for-a-locked-domain"></span>
## Cannot update policy configurations for a locked domain

When a domain is locked, you cannot update its configurations by modifying the policy configurations. Use the [single-domain configuration method](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en#method-1-managing-domain-configurations-based-on-domains) to update the domain configurations directly.

When you update domain configurations using the single\-domain configuration method, CDN maintains a system\-created policy specifically for that domain. The name of this policy ends with `(system-tpl)`. For more details, see [Pre-operations executed by CDN in single-domain configuration](https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en#preliminary-operations-performed-by-cdn).
