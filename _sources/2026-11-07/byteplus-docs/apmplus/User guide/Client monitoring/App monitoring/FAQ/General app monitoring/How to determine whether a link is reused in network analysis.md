---
title: "How to determine whether a link is reused in network analysis"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_determine_whether_a_link_is_reused_in_network_analysis"
---

In network analysis, you can view the link reuse rate. How can you determine whether a link is reused, and how can you calculate the link reuse rate?

The methods for judgment differ between Android and iOS.


* iOS: Determine whether the link is reused via the system interface

* Android: Determine whether connections are reused by checking if the DNS phase is present in the Okhttp Listener callback. After determining this, calculate the connection reuse rate using the following formula: connection reuse rate = number of reused connections / total number of connections.
