---
title: "ACL FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Access-control-list-faq"
---

<span id=".6LSf6L295Z2H6KGh5pyN5Yqh55qE6K6_6Zeu5o6n5Yi25LiO5a6J5YWo57uE5pyJ5LuA5LmI5Yy65Yir77yf"></span>
## What is the difference between access control lists (ACLs) and security groups in the CLB?

**ACLs** are used to control the inbound and outbound traffic of CLB instances.

**Security groups** are used to control the inbound and outbound traffic of backend servers.

You can use ACLs and security groups jointly to add two layers of filtering between internal/external users and backend server groups, which ensures secure access to the servers. For more introduction and configuration methods, refer to [CLB-based security](https://docs.byteplus.com/en/docs/clb/CLB-security-defense).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_167a5bd9ac55cfaa5c7cb3fdd1f885b6.png) </span>

<span id=".5Y-Y5pu06K6_6Zeu5o6n5Yi2562W55Wl57uE5LitSVDmnaHnm67ml7bvvIzmmK_lkKblr7nljp_mnInmtYHph4_lrp7ml7bnlJ_mlYjvvJ8="></span>
## When an IP entry in an ACL is changed, does the change take effect in real time on the original traffic?

ACLs are stateful.

ACLs use connection tracking to track traffic entering the listener. When an IP entry in an ACL is changed, connection tracking in the associated listener of this ACL is automatically disabled. Then, traffic entering the listener is treated as a new connection and needs to be re\-matched with the IP entry in the ACL to ensure that the change takes effect immediately. This ensures the security of traffic entering the listener.

<span id=".5aaC5L2V5Li66K6_6Zeu5o6n5Yi2562W55Wl57uE5YWz6IGU55uR5ZCs5Zmo77yf"></span>
## How can I associate a listener with an ACL?

After creating an ACL, you must associate this ACL with a listener to achieve the expected effect of this ACL. You can associate the ACL with a listener when creating the ACL or after creating the listener. For detailed steps, refer to [Configuring ACLs for a listener](https://docs.byteplus.com/en/docs/clb/Configuring-access-control-for-a-listener).
