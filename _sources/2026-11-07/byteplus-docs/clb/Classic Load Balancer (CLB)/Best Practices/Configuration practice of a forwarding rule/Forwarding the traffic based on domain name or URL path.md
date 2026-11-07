---
title: "Forwarding the traffic based on domain name or URL path"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Traffic-forwarding-based-on-the-domain-name-or-URL-path"
---

This topic introduces how to forward traffic for specified domain names or URL paths to designated backend server groups to achieve load balancing.

<span id=".5Zy65pmv5LuL57uN"></span>
## Scenarios

Layer\-7 Classic Load Balancer (CLB) forwards requests with different domain names or URLs to different backend server groups by configuring forwarding rules. For detailed information about forwarding rules, see [Forwarding rule description](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01).

This article uses domain\-based traffic forwarding as an example, explaining how to forward traffic accessing the domain ` www.test.com` to the backend server group group\-1, and forward traffic accessing other domains to the backend server group group\-2. The principle of URL path–based traffic forwarding is similar and will not be repeated here.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The CLB instance clb\-test has been created. For more information, see Creating a CLB instance.

* Two backend server groups, group\-1 and group\-2, have been configured, and backend servers have been added to these groups.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The security groups associated with the servers in the backend server group have opened the protocols and ports needed to provide services. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group">Configure backend server security groups</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backend servers have completed deployment and configuration of backend services. For details, see <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page">Set up HTTP static page</a> or <a href="https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-static-page">Set up HTTPS static page</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you select the secondary network interface as the backend server, you also need to <a href="https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface">Configure secondary network interface routing</a> to enable the interface to respond to requests from the client or load balancer instance.   </div>
   

* The Layer 7 CLB listener listener\-test has been added for the CLB instance. For more information, see Creating an HTTP listener or Creating an HTTPS listener.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Configure Listener to the right of the target CLB instance.

4. Click Configure Forwarding Rules to the right of the target Layer 7 listener.

5. Click Add forwarding rules and configure parameters by referring to the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You cannot configure two forwarding rules with exactly the same domain name and URL in the same listener.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The backend server group for the default forwarding rule of this listener is set to group\-2.   </div>
   

   
   |Parameter |Value |
   |---|---|
   |**Trigger condition** ||
   |Domain name |www.test.com |
   |URL |/ |
   |**Forwarding action** ||
   |Forwarding action |Forward to |
   |Server group |group\-1 |
   

6. Click **Add** to complete the action.


<span id=".57uT5p6c6aqM6K-B"></span>
## Result verification

The following steps use the HTTP protocol as an example.


1. Access http://www.test.com using a browser. The page displayed as shown below (taking Nginx 1.14.1 as an example) indicates that the access request was forwarded by the Cloud Load Balancer instance to backend Server Group group\-1, and the backend server successfully processed the request and returned the requested page.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c51113ccf5b686b1a956dc1a397a0a32.png) </span>

2. Access other domain names using a browser, For example: http://www.abc.com. The page displayed as shown below (taking Nginx 1.14.1 as an example) indicates that the domain name of the frontend access request did not match any forwarding rules and was forwarded by the CLB instance to the default backend Elastic Compute Service (ECS) group group\-2. The backend server successfully processed the request and returned the requested page.

    <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9fe7dd83f88ecd21a6726e29c99ed47.png) </span>


&nbsp;

&nbsp;
