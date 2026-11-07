---
title: "Custom Domain overview"
product: "BytePlus ArkClaw Enterprise"
product_code: "ArkClaw"
source: "https://docs.byteplus.com/en/docs/ArkClaw/custom-domain-overview"
---

ArkClaw Enterprise supports configuring a custom domain or a custom domain prefix for the public access entry. On the basis of retaining the original employee login link, you can add an enterprise\-specific access address to achieve a branded login portal and enhance the employee access experience.

<span id="r5lQzS1i"></span>
## Configuration methods

ArkClaw provides two configuration methods for custom access addresses. You can choose flexibly based on your actual needs:


|Configuration method |Description |
|---|---|
|[Custom enterprise domain (new version)](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-new-version) |Bind your own registered and ICP\-filed domain to hide platform information, creating a completely enterprise\-branded dedicated login portal. |
|[Enterprise custom domain (old version)](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-enterprise-domain-old-version) ||
|[Custom domain prefix (new version)](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-new-version) |Add a custom prefix before the platform's fixed domain suffix to obtain a concise, memorable enterprise\-specific access address. No your own domain required. |
|[Custom domain prefix (old version)](https://docs.byteplus.com/en/docs/ArkClaw/configuring-a-custom-domain-prefix-old-version) ||


<span id="5eeNiHHL"></span>
## Features and limits


|**Feature type** |**Custom enterprise domain** |**Custom domain prefix** |
|---|---|---|
|Scenarios |Requires bringing your own domain (ICP\-filled) to meet brand customization and third\-party platform compliance.<br><br>Suitable for enterprise\-level scenarios. Recommended as the primary choice. |No your own domain required. Only a concise, memorable enterprise\-specific prefix is needed.<br><br>Suitable for lightweight needs. Quick and simple to configure. |
|Configuration |Complete domain (including prefix and suffix, e.g., `login.example.com`). |Domain prefix only. The suffix is uniformly provided by the platform in the format `arkclaw-enterprise-<region>.volceapi.com`. |
|Domain requirements |Must have a completed MIIT ICP filing; and the domain registrant must be consistent with the enterprise entity. |No filing required. The prefix must be globally unique across the entire platform. |
|Certificate requirements |A valid HTTPS certificate is mandatory (supports certificates from VolcanoEngine Certificate Center or third\-party). |No additional configuration needed. HTTPS is automatically provisioned by the platform. |
|Permission requirements |Configuration can be done only by the enterprise space administrator. ||


<span id="m1QNUSlg"></span>
## Access addresses

ArkClaw supports multiple access addresses being active simultaneously, without interfering with each other:


* Default login address​ (system\-assigned)

* Custom enterprise domain

* Address with custom domain prefix


You can use all three access methods concurrently. Configuring or modifying any one of them does not affect the other access addresses. If none are configured, the system\-assigned public access address is used by default.
