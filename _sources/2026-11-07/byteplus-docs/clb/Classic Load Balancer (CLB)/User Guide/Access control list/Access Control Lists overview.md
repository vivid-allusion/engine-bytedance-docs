---
title: "Access Control Lists overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Access-control-list-01"
---

<span id=".5qaC6L-w"></span>
## File transfer overview

Classic Load Balancer (CLB) supports the listener\-level Access Control Lists (ACLs). To allow or deny requests of some IP addresses to access a CLB instance through the listening port, you can configure an ACL for this listener.

You can configure ACLs when creating a listener, or modify or reconfigure ACLs after the listener is created.

<span id=".6K6_6Zeu5o6n5Yi26K-05piO"></span>
## About the ACL

Before enabling the ACL feature for the listener, you must create at least one ACL. An ACL is a collection of multiple IP entries used for centralized management of IPs, and allows you to conveniently associate IP entries with the listener.

The ACL itself does not restrict the access control mode and access control is implemented by the listener. You can select blocklist or allowlist for access control of the IPs in the policy group:


* **Blocklist**: Prohibit the CLB instance from forwarding access requests of the IPs in the policy group to the backend server.

* **Allowlist**: Only allow the CLB instance to forward access requests of the IPs in the policy group to the backend server.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Connections established before the listener ACL enabled are not subject to access control restrictions and require the client or backend server to disconnect.</div>


* <div data-tips="true" data-tips-type="tip">When CLB serves as the endpoint service resource for PrivateLink, you need to allow the CLB to forward requests from the PrivateLink service CIDR block 100.64.0.0/10. If the listener has enabled the ACL allowlist, please add 100.64.0.0/10; if the listener has enabled the ACL blocklist, please do not add 100.64.0.0/10.</div>



When configuring an ACL for the listener, note that:


* Each ACL\-enabled listener must be associated with at least one ACL.

* The ACL name must be unique.

* Both IPv4 and IPv6 addresses or IP address segments can be added to an ACL.

* The IP address or IP address segment of each IP entry in the same ACL must be unique.

* For relevant constraints, refer to [Constraints](https://docs.byteplus.com/en/docs/clb/Product-Overview-07).
