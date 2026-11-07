---
title: "Resource Quota"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/quota_en"
---

To effectively manage your usage and plan for scaling, it is important to understand the resource limits within BytePlus CDN. This document provides a comprehensive list of the default quotas for key resources and operations, such as domains, certificates, and cache purge actions. These quotas apply to your primary account, and you can request an adjustment by [submitting a ticket](https://console.byteplus.com/workorder/create).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The quotas in this document apply to resources under the primary account.</div>



|**Resource/Operation** |**Default Quota** |**Reference** |
|---|---|---|
|Project |Up to 500 | |
|Domain |Up to 200 |[Domain names](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-add-domain-name_1) |
|Delivery policy |Up to 201 |[Policy overview](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-policy) |
|Encryption policy |Up to 201 ||
|Rules engine policy |Up to 201 ||
|Number of published versions per policy |Up to 50 ||
|Number of ancestors per policy |Up to 10 ||
|Number of operation records per policy |Up to 10 ||
|Number of delivery policies that can be bound to a domain |Up to 1 ||
|Number of encryption policies that can be bound to a domain |Up to 1 ||
|Number of rules engine policies that can be bound to a domain |Up to 1 ||
|Certificate |Up to 500 |[Certificate Center overview](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-certificate-center-overview) |
|Edge function |* Up to 100 functions.<br><br>* Each function can be associated with up to 100 domains.<br><br>* Each domain can be associated with up to 50 functions.<br><br>* Up to 100 scheduled tasks per function. |[Edge Functions Overview](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview-of-edge-function) |
|Cache purge |* Up to 10,000 files per day.<br><br>* Up to 100 files per request.<br><br>* Up to 50 directories per day. |[Cache purge](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-purge) |
|Origin prefetch |* Up to 1,000 files per day.<br><br>* Up to 100 files per request. |[Origin prefetch](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-prefetch) |
