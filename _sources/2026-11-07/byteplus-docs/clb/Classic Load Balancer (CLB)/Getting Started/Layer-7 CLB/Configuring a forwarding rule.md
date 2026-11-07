---
title: "Configuring a forwarding rule"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Layer-7-CLB-05"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

By configuring forwarding rules, access requests for different services can be forwarded to different backend server groups under the same domain name but with different URL forwarding rules.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. On the listener list page, click Configure forwarding rule to the right of the target layer\-7 listener.

2. Click Add forwarding rule and see the table below to configure the forwarding rule.

   
   |Parameter |Explanation |Value 1 |Value 2 |
   |---|---|---|---|
   |Domain name |Enter the request domain to forward, supporting wildcard domains. The `*` must appear at the beginning and end of the domain name. |www.test.com |www.test.com |
   |URL |Enter the URL to forward, supporting only absolute paths. You can add multiple URLs for the same domain name. |/ECS01 |/ECS02 |
   |Server group |The backend server group that receives/processes the request after matching the domain name and URL. |group01 |group02 |
   

3. Click **Add** to complete the action.
