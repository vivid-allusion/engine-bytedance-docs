---
title: "Traffic forwarding with the same domain name but different URL paths"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Traffic-forwarding-along-different-URL-paths-with-the-same-domain-name"
---

This topic introduces how to forward traffic with the same domain but different URL paths to different backend server groups to achieve load balancing for access traffic.

## Scenarios

Layer\-7 Classic Load Balancer (CLB) forwards requests to different backend server groups by configuring forwarding rules for traffic with the same domain but different URLs. For detailed explanation of forwarding rules, see [Forwarding Rule Description](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01).

This topic describes how to configure forwarding rules for a load balancing instance to forward traffic with the same domain but different URLs. Traffic to `www.test.com/test1` is forwarded to backend server group group\-1, while traffic to `www.test.com/test2` is forwarded to backend server group group\-2.

## Prerequisites

* The CLB instance clb\-test has been created. For details, see [Creating a CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-01).

* Two backend server groups, group\-1 and group\-2, have been configured, and backend servers have been added to these groups.

   > **tip**

   * > The security groups attached to the servers in the backend server groups have allowed the protocols and ports needed to provide services. For details, see [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

   * > The backend servers have completed the deployment and configuration of backend services. For details, see [Building an HTTP static page](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-static-page) or [Building an HTTPS static page](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-static-page).

   * > If you select the secondary network interface as the backend server, you also need to [configure secondary network interface routing](https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface) so that the network interface can respond to requests from clients or the load balancer instance.

* A Layer 7 protocol listener, listener\-test, has been added to the CLB instance. For detailed steps, see [Creating an HTTP protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTP-listener) or [Creating an HTTPS protocol listener](https://docs.byteplus.com/en/docs/clb/Creating-an-HTTPS-listener).

## Procedures

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Click Configure Listener to the right of the target CLB instance.

4. Click Configure Forwarding Rules to the right of the target Layer 7 listener.

5. Click Add forwarding rules and configure parameters by referring to the table below.

   > **tip**

   > You cannot configure two forwarding rules with identical domain names and URLs in the same listener.

   |Parameter |Value (forwarding rule one) |Value (Forwarding Rule Two) |
   |---|---|---|
   |**Trigger condition** |||
   |Domain name |www.test.com |www.test.com |
   |URL |/test1 |/test2 |
   |**Forwarding action** |||
   |forwarding action |Forward to |Forward to |
   |server group |group\-1 |group\-2 |

6. Click **Add** to complete the action.

## Result verification

The following steps use the HTTP protocol as an example.

1. Launch a browser, and visit http://www.test.com/test1. If the following page is displayed (taking Nginx 1.14.1 as an example), the access request has been forwarded by the CLB instance to the backend server group group\-1, and group\-1 has processed the request properly and returned the requested page.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c4c3420676d2d648c49548efc2c5b07d.png)

2. In the browser, visit http://www.test.com/test2. If the following page is displayed (taking Nginx 1.14.1 as an example), the access request has been forwarded by the CLB instance to the backend server group group\-2, and group\-2 has processed the request properly and returned the requested page.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_89652e99c731e0eecd624c6448090279.png)
