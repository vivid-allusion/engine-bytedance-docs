---
title: "Common trace storage issues"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Trace_Storage_FAQ"
---

<span id="c3c62574"></span>
## How do I delete log topics related to Trace storage?

After you create a Trace instance, TLS will automatically generate related log topics named `tls_${trace instance name}-trace` and `tls_${trace instance name}-dependency` in the log topic you selected. `tls_${trace instance name}-trace` and` tls_${trace instance name}-dependency` are dedicated log topics for Trace storage and cannot be deleted directly. If you no longer use the Trace instance, you can delete the Trace instance to remove the related log topics. For the steps to delete a Trace instance, refer to [Delete Trace instance](https://docs.byteplus.com/en/docs/tls/manage_trace_instances).
