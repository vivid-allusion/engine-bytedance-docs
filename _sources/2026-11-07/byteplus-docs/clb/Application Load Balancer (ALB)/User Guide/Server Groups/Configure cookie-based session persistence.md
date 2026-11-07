---
title: "Configure cookie-based session persistence"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Cookie-based-session-persistence"
---

This article introduces how to configure cookie\-based session persistence in the console.

By default, to distribute the load, ALB forwards client requests to different backend servers based on the load balancing algorithm you set. However, in some application scenarios, session consistency is required. To meet this need, ALB offers a cookie\-based session persistence feature. After enabling this feature, ALB can forward requests from the same client to the same backend server. This feature suits business scenarios that require maintaining user session status on backend servers, such as saving user login status and shopping cart information on e\-commerce sites, recording playback progress on video platforms, and tracking transaction processes on financial service platforms.

<span id=".5Z-65LqOLWNvb2tpZS3nmoTkvJror53kv53mjIHmqKHlvI8="></span>
## Background

ALB supports two session persistence modes: cookie placement and rewrite cookies.


* Cookie placement: ALB actively generates a cookie and embeds it in the response.

   When the client sends a request to the ALB for the first time, the ALB selects a backend server based on the load balancing algorithm to handle the request and inserts a cookie in the response returned to the client. When subsequent client requests carry this cookie, the ALB forwards the requests to the corresponding backend server. When selecting this mode, you need to set the session persistence timeout. After the set duration expires, the ALB stops maintaining session persistence based on the current cookie and selects a backend server again according to the load balancing algorithm.

* Rewrite cookies: The ALB retrieves the cookie returned by the backend server and rewrites the cookie value.

   When selecting this mode, you need to specify the name of the cookie to be rewritten. When the ALB detects a cookie with the specified name in the backend server’s response, it rewrites the cookie value and returns the rewritten cookie to the client. When subsequent client requests carry the rewritten cookie, the ALB forwards the requests to the corresponding backend server.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you enable the rewrite cookies session persistence feature for the server group:

   * You need to configure the corresponding cookie on the backend server. Because the methods for setting cookies vary across different web servers, refer to the official documentation of the respective server for configuration.

   * If the cookie in the backend server's response does not match the cookie you specified, the ALB will not rewrite the cookie. The next client request will be distributed to the backend server according to your configured load balancing algorithm.

   * The session established timeout matches the cookie expiration time specified by the backend server in the response's Set\-Cookie header.

* The priority of the cookie\-based session persistence feature is higher than that of the load balancing algorithm. After you enable session persistence for the server group, the ALB forwards the client’s initial request to a backend server according to the load balancing algorithm. For subsequent requests from that client, the ALB ignores the load balancing algorithm and always forwards the requests to that backend server.

* When a client request carrying a cookie arrives at the ALB, if the ALB fails to parse the cookie successfully, it forwards the request to the backend server based on your configured load balancing algorithm.

* After enabling the session persistence feature, if the backend server responsible for handling requests shows an abnormal health check status, the ALB automatically blocks that backend server. Then, ALB forwards the request to a healthy backend server and establishes session persistence.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Before you begin


* Created a server group. For details, see [Create Server Group](https://docs.byteplus.com/docs/clb/Managing-server-groups#%E5%88%9B%E5%BB%BA%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%BB%84).

* At least one ECS instance has been created, and a web service is deployed on the ECS instance.

* The ECS instance has been added to the server group.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

When creating a server group, you can enable session persistence and select the session retention mode directly. To enable session persistence for an existing server group, follow these steps:


1. Log in to the [Application Load Balancer console](https://console.byteplus.com/alb).

2. In the left navigation pane, click **server group** to enter the **server group** page.

3. On the **server group** page, click the server group name to be configured for session persistence.

4. On the **detail** tab, click **edit**.

5. On the **edit server group** page, enable **session persistence** and set the session retention mode.

   * Cookie placement: You need to set the session established timeout. The default is 1000 seconds. The value range is 1 to 86400 seconds.

   * Rewrite cookies: You need to enter the Cookie name. The Cookie name can only include letters, numbers, underscore (_), and hyphen (\-). The length must not exceed 200 characters.

6. After confirming the configuration is correct, click **confirmed**.
