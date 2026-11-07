---
title: "What to do when APMPlus reported events are exhausted?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/What_should_you_do_when_APMPlus_reporting_events_are_exhausted"
---

**Description**

If the event count exceeds the quota of the resource package within the validity period, or if there is remaining event quota but the resource package expires, will this affect normal business operations, and how should it be handled?

**Solutions**

If the resource quota is exceeded or the resource package expires, business operations are affected. In this case, the client will continue to report data, but the server will discard the reported data and not display it. You need to purchase a new resource package as soon as possible. For details, see [Activating and renewing services](https://docs.byteplus.com/en/docs/apmplus/Activate_client_monitoring).

After purchasing a resource package under the existing app ID, the client SDK does not need to be updated.
