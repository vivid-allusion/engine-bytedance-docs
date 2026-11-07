---
title: "[Product update] \"XID exception\" check item added to the check and self-healing feature"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Product-update_XID-exception-check-item-added-to-the-check-an-self-healing-feature"
---

To better meet the requirements of GPU failure self‑healing scenarios, the node check and self‑healing feature of VKE has added the "XID exception" check item. This is used to identify and handle GPU failures caused by XID exceptions. For details, see [Check and self-healing overview](https://docs.byteplus.com/en/docs/vke/Check_and_self-healing_overview).

For the existing check items, including GPU card dropout, recoverable memory failure on GPU, unrecoverable memory failure on GPU, GPU link failure, and GPU driver failure, the XID exception check capabilities they provide will no longer take effect from August 30, 2026. The XID exceptions involved include 48, 63, 64, 74, 79, 94, 95, 119, 120, and 140. Among the preceding existing check items, GPU failures that are not caused by XID exceptions will continue to be checked and are not affected by this adjustment.

If you want to continue detecting and self‑healing GPU failures caused by XID exceptions, we recommend configuring the "XID exception" check item as soon as possible. If you already use the node check and self\-healing feature, we recommend promptly reviewing your existing rule configurations and making necessary adjustments based on your business requirements. For more details, see [Configuring node check and self-healing](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The XID exception check item is not available in the Asia Pacific (Johor), Asia Pacific (Jakarta), and China (Hong Kong) regions.</div>
