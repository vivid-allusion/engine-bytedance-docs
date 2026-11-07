---
title: "What are the differences between session persistence in LoadBalancer Services and session persistence in CLB Listeners?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Difference-between-session-persistence-in-a-LB-Service-and-session-persistence-in-a-CLB-listener"
---

The differences between the two types of session persistence are as follows:


* Session persistence for Services is a native Kubernetes feature. It distinguishes traffic accessing Services by client IP address and, within the timeout period, forwards traffic from the same client IP address to the same backend.

* Session persistence for TCP/UDP protocols of CLB instances. It distinguishes traffic accessing CLB instances by client IP address and, within the timeout period, forwards traffic from the same client IP address to the same backend.


A Load Balancer\-type Service involves two IP addresses: ClusterIP and the external endpoint (the IP address of the CLB instance). Traffic to the ClusterIP uses the session persistence timeout of the Service. Traffic to the IP address of the CLB instance uses the session persistence timeout of the CLB instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">We recommend that the session persistence timeout configured for a Load Balancer\-type Service be consistent with that configured for the corresponding CLB listener. Since both correspond to the same back\-end server, they should have the same session persistence timeout from a business perspective.</div>
