---
title: "Backend Server Group FAQs"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Server-group-faq"
---


|Problem Type |Issue |
|---|---|
|Feature description<br><br> |* [Which types/operating systems of backend servers does the CLB instance support?](https://docs.byteplus.com/en/docs/42/11791#.Q0xC5a6e5L6L5pSv5oyB5ZOq5Lqb57G75Z6LL-aTjeS9nOezu-e7n-eahOWQjuerr-acjeWKoeWZqO-8nw==)<br><br>* [Does the CLB instance support adjusting backend servers at any time during operation?](https://docs.byteplus.com/en/docs/42/11791#.Q0xC5a6e5L6L6L-Q6KGM5pe25piv5ZCm5pSv5oyB6ZqP5pe26LCD5pW05ZCO56uv5pyN5Yqh5Zmo77yf)<br><br>* [Can the CLB instance associate backend servers across regions?](https://docs.byteplus.com/en/docs/42/11791#.Q0xC5a6e5L6L5Y-v5Lul6Leo5Zyw5Z-f5YWz6IGU5ZCO56uv5pyN5Yqh5Zmo5ZCX77yf)<br><br>* [Does it support multiple CLB instances forwarding requests to the same backend server?](https://docs.byteplus.com/en/docs/42/11791#.5pSv5oyB5aSa5LiqQ0xC5a6e5L6L5ZCR5ZCM5LiA5Y-w5ZCO56uv5pyN5Yqh5Zmo6L2s5Y-R6K-35rGC5ZCX77yf)<br><br>* [Does adding a backend server support selecting cloud servers under another VPC?](https://docs.byteplus.com/en/docs/42/11791#.5re75Yqg5ZCO56uv5pyN5Yqh5Zmo5pe25piv5ZCm5pSv5oyB6YCJ5oup5YW25LuWVlBD5LiL55qE5LqR5pyN5Yqh5Zmo77yf) |
|Use |* [How long does it take for the CLB instance to disconnect existing connections after deleting a backend server?](https://docs.byteplus.com/en/docs/42/11791#.5Yig6Zmk5ZCO56uv5pyN5Yqh5Zmo5ZCO5aSa5LmFQ0xC5a6e5L6L5Lya5bCG5bey5pyJ55qE6L-e5o6l5pat5byA77yf)<br><br>* [Why can clients still access the backend server after configuring the allowlist/denylist?](https://docs.byteplus.com/en/docs/42/11791#.5Li65LuA5LmI6YWN572u5LqG6buRL-eZveWQjeWNleWQju-8jOWuouaIt-err-S7jeeEtuWPr-S7peiuv-mXruWQjuerr-acjeWKoeWZqO-8nw==)<br><br>* [How is a backend server considered healthy?](https://docs.byteplus.com/en/docs/42/11791#.5ZCO56uv5pyN5Yqh5Zmo5aaC5L2V6KKr6K6k5Li65piv5YGl5bq355qE77yf)<br><br>* [Why do IPs starting with 100 frequently access the backend server?](https://docs.byteplus.com/en/docs/42/11791#.5Li65LuA5LmIMTAw5byA5aS055qESVDlnKjpopHnuYHnmoTorr_pl67lkI7nq6_mnI3liqHlmajvvJ8=)<br><br>* [How long does it take for backend server weight changes to take effect?](https://docs.byteplus.com/en/docs/42/11791#.5ZCO56uv5pyN5Yqh5Zmo5p2D6YeN5L-u5pS55ZCO5aSa5LmF55Sf5pWI77yf)<br><br>* [How should the security group of the CLB backend server be configured?](https://docs.byteplus.com/en/docs/42/11791#.6LSf6L295Z2H6KGh5ZCO56uv5pyN5Yqh5Zmo55qE5a6J5YWo57uE5bqU6K-l5aaC5L2V6YWN572u77yf)<br><br>* [Can the backend server obtain the protocol version of clients accessing the Layer 7 listener?](https://docs.byteplus.com/en/docs/42/11791#.5ZCO56uv5pyN5Yqh5Zmo6IO95ZCm6I635Y-W5a6i5oi356uv6K6_6Zeu5LiD5bGC55uR5ZCs5Zmo55qE5Y2P6K6u54mI5pys77yf)<br><br>* [What is the difference between setting the backend server weight to 0 and removing the backend server?](https://docs.byteplus.com/en/docs/42/11791#.5ZCO56uv5pyN5Yqh5Zmo5p2D6YeN6K6-572u5Li6MOS4juenu-mZpOivpeWQjuerr-acjeWKoeWZqOacieS7gOS5iOWMuuWIq--8nw==)<br><br>* [How to view which CLBs are associated with the backend server?](https://docs.byteplus.com/en/docs/clb/Server-group-faq?TagIDs=2,218,211#TJIYd86j) |
|Network related |* [After being added to the CLB instance, can the backend server access the public network?](https://docs.byteplus.com/en/docs/42/11791#.5re75Yqg5YiwQ0xC5a6e5L6L5ZCO77yM5ZCO56uv5pyN5Yqh5Zmo6IO95ZCm6K6_6Zeu5YWs572R77yf)<br><br>* [Do public CLB instance backend servers require an associated EIP?](https://docs.byteplus.com/en/docs/42/11791#.5YWs572RQ0xC5a6e5L6L55qE5ZCO56uv5pyN5Yqh5Zmo6ZyA6KaB57uR5a6a5YWs572RSVDlkJfvvJ8=)<br><br>* [How to check if the backend server network configuration is correct?](https://docs.byteplus.com/en/docs/42/11791#.5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo572R57uc6YWN572u5piv5ZCm5q2j56Gu77yf)<br><br>* [If a request reaches the backend server via CLB and the client disconnects from the CLB before receiving a reply from the backend server, does CLB also disconnect from the backend server?](https://docs.byteplus.com/en/docs/42/11791#.6K-35rGC6YCa6L-H6LSf6L295Z2H6KGh5Yiw6L6-5ZCO56uv5pyN5Yqh5Zmo77yM5aaC5p6c5a6i5oi356uv5Zyo5pyq5pS25Yiw5ZCO56uv5pyN5Yqh5Zmo55qE5Zue5aSN5YmN5Li75Yqo5pat5byA5ZKM6LSf6L295Z2H6KGh55qE6L-e5o6l77yM6LSf6L295Z2H6KGh5Lya5ZCM5pe25pat5byA5ZKM5ZCO56uv5pyN5Yqh5Zmo55qE6L-e5o6l5ZCX77yf)<br><br>* [How to check the backend server's network status?](https://docs.byteplus.com/en/docs/42/11791#.5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo55qE572R57uc54q25oCB77yf)<br><br>* [How to check the backend server's service status?](https://docs.byteplus.com/en/docs/42/11791#.5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo55qE5pyN5Yqh54q25oCB77yf) |


<span id=".5Yqf6IO95LuL57uN"></span>
## Feature description

<span id=".Q0xC5a6e5L6L5pSv5oyB5ZOq5Lqb57G75Z6LL-aTjeS9nOezu-e7n-eahOWQjuerr-acjeWKoeWZqO-8nw=="></span>
### Which types and operating systems of backend servers does the CLB instance support?

The CLB instance supports adding Elastic Compute Service (ECS), GPU cloud servers, bare metal servers, and Elastic Network Interfaces (ENIs) within the same VPC as backend servers. It also supports adding IP addresses across VPCs as backend servers without restricting the operating system type of the backend servers.

However, we recommend choosing backend servers with the same operating system for easier management and maintenance.

<span id=".Q0xC5a6e5L6L6L-Q6KGM5pe25piv5ZCm5pSv5oyB6ZqP5pe26LCD5pW05ZCO56uv5pyN5Yqh5Zmo77yf"></span>
### Does the CLB instance support adjusting backend servers at any time during operation?

It supports adding or removing backend servers at any time, modifying the port and weight of backend servers, and swapping backend servers between different CLB instances.

This is a hot configuration operation. You do not need to suspend the existing service; the new configuration takes effect immediately, new traffic is forwarded according to the new configuration, and existing connections remain unaffected.

To ensure the stability of your external services, ensure the listener’s health check function is enabled during this operation and that at least one backend server is running properly.

<span id=".Q0xC5a6e5L6L5Y-v5Lul6Leo5Zyw5Z-f5YWz6IGU5ZCO56uv5pyN5Yqh5Zmo5ZCX77yf"></span>
### Can a CLB instance associate backend servers across different regions?

Not supported.

<span id=".5pSv5oyB5aSa5LiqQ0xC5a6e5L6L5ZCR5ZCM5LiA5Y-w5ZCO56uv5pyN5Yqh5Zmo6L2s5Y-R6K-35rGC5ZCX77yf"></span>
### Does it support multiple CLB instances forwarding requests to the same backend server?

Yes, supported. The same backend server can be added to multiple backend server groups as long as the CLB instance and the backend server reside in the same VPC.

<span id=".5re75Yqg5ZCO56uv5pyN5Yqh5Zmo5pe25piv5ZCm5pSv5oyB6YCJ5oup5YW25LuWVlBD5LiL55qE5LqR5pyN5Yqh5Zmo77yf"></span>
### Does adding a backend server support selecting cloud servers from other VPCs?


* Backend server groups of the server type do not support this; only cloud servers within the VPC of the CLB instance can be selected as backend servers.

* Backend server groups of the IP type support backend servers across VPCs. For details, see [server group type](https://docs.byteplus.com/en/docs/clb/Server-group-overview).


<span id=".5pON5L2c5L2_55So"></span>
## Operations

<span id=".5Yig6Zmk5ZCO56uv5pyN5Yqh5Zmo5ZCO5aSa5LmFQ0xC5a6e5L6L5Lya5bCG5bey5pyJ55qE6L-e5o6l5pat5byA77yf"></span>
### How long after deleting a backend server will the CLB instance disconnect existing connections?


* For layer 4 listeners (TCP, UDP) without connection drain enabled, connections established with backend servers will be disconnected by the CLB instance if no requests are received after the listener timeout period.

* For layer 4 listeners (TCP, UDP) with connection drain enabled, established connections with backend servers will be maintained during the connection draining timeout period and disconnected afterward.

* For layer 7 listeners (HTTP, HTTPS), established connections with backend servers that exceed the default listener timeout of 60 seconds with no requests will be disconnected by the CLB instance.


<span id=".5Li65LuA5LmI6YWN572u5LqG6buRL-eZveWQjeWNleWQju-8jOWuouaIt-err-S7jeeEtuWPr-S7peiuv-mXruWQjuerr-acjeWKoeWZqO-8nw=="></span>
### Why can clients still access backend servers after configuring black/white lists?

Black/white lists control access only through the CLB instance. If the client bypasses the CLB instance and accesses the backend servers directly, these restrictions do not apply.

If you need to control access to the backend server itself, configure security groups. More information is available in [security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

<span id=".5ZCO56uv5pyN5Yqh5Zmo5aaC5L2V6KKr6K6k5Li65piv5YGl5bq355qE77yf"></span>
### How is the backend server considered healthy?

A newly added backend server is marked "normal" and immediately receives traffic if it responds correctly within the specified timeout. Later, the health threshold is applied. A backend server is considered to have passed health checks if it returns "normal" results for the specified number of consecutive health checks.

<span id=".5Li65LuA5LmIMTAw5byA5aS055qESVDlnKjpopHnuYHnmoTorr_pl67lkI7nq6_mnI3liqHlmajvvJ8="></span>
### Why do IPs starting with 100 frequently access the backend server?

IPs starting with 100 are the internal IPs used for communication between the CLB instance and backend servers. The subnet is 100.64.0.0/10 and it's used for health check services and Layer 7 listener forwarding. The CLB instance uses this subnet IP as the source address to probe backend servers for health checks.

Therefore, to ensure your configured CLB instance provides normal service, make sure your backend server's security policy allows the 100.64.0.0/10 subnet. For details, see [configure backend server security groups](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

<span id=".5ZCO56uv5pyN5Yqh5Zmo5p2D6YeN5L-u5pS55ZCO5aSa5LmF55Sf5pWI77yf"></span>
### How soon does the backend server weight change take effect?

The backend server weight change takes effect immediately. New access requests are forwarded based on the new weights without affecting existing connections.

<span id=".6LSf6L295Z2H6KGh5ZCO56uv5pyN5Yqh5Zmo55qE5a6J5YWo57uE5bqU6K-l5aaC5L2V6YWN572u77yf"></span>
### How should the security groups for CLB backend servers be configured?

The security group configuration rules for backend servers vary depending on the protocol type of the CLB listener.


* For layer\-4 listeners, the public and private network access requests and health check request subnets differ when sent to the backend server group. Therefore, you must allow the protocols, ports, and addresses used to receive public and private network access requests and health check requests separately in the inbound direction of the backend server's security group.

* Requests from layer\-7 listeners to the backend server group all originate from the private network segment 100.64.0.0/10. Thus, for layer\-7 listeners, you only need to allow inbound access from the 100.64.0.0/10 segment in the backend server's security group.


Refer to [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group) for detailed backend server security group configuration steps.

<span id=".5ZCO56uv5pyN5Yqh5Zmo6IO95ZCm6I635Y-W5a6i5oi356uv6K6_6Zeu5LiD5bGC55uR5ZCs5Zmo55qE5Y2P6K6u54mI5pys77yf"></span>
### Can the backend server obtain the protocol version of the client's request to the layer\-7 listener?

Yes.

<span id=".5ZCO56uv5pyN5Yqh5Zmo5p2D6YeN6K6-572u5Li6MOS4juenu-mZpOivpeWQjuerr-acjeWKoeWZqOacieS7gOS5iOWMuuWIq--8nw=="></span>
### What is the difference between setting the backend server weight to 0 and removing the backend server?


* After setting the backend server weight to 0, long connections still reuse TCP connections within the timeout period, so traffic can still reach the backend server.

* After removing the backend server, existing connections remain unaffected, but the CLB no longer forwards new requests to that backend server.


<span id="TJIYd86j"></span>
### How to view which CLBs are associated with a backend server?


1. Log in to the CLB console.

2. Use the search bar in the upper left corner to select **Backend server ID** or **Backend server private IP** from the dropdown.

3. Enter the backend server's ID or private IP address to filter and view the CLB instances associated with that backend server.


<span id=".572R57uc55u45YWz"></span>
## Network\-related

<span id=".5re75Yqg5YiwQ0xC5a6e5L6L5ZCO77yM5ZCO56uv5pyN5Yqh5Zmo6IO95ZCm6K6_6Zeu5YWs572R77yf"></span>
### After adding a backend server to a CLB instance, can the backend server access the public network?

Whether the backend server can access the public network is independent of the CLB instance. If the backend server can access the public network, it still can after using the CLB instance. If it cannot, it still cannot after using the CLB instance.

The public IP of a CLB instance only receives requests from the public network and forwards them to the backend servers through the private network.

<span id=".5YWs572RQ0xC5a6e5L6L55qE5ZCO56uv5pyN5Yqh5Zmo6ZyA6KaB57uR5a6a5YWs572RSVDlkJfvvJ8="></span>
### Do backend servers behind a public CLB instance need to bind a public IP?

After the CLB instance receives requests from the public network, it forwards the access requests through the private network, so backend servers do not need to associate an EIP.

<span id=".5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo572R57uc6YWN572u5piv5ZCm5q2j56Gu77yf"></span>
### How to check if the backend server’s network configuration is correct?


1. Confirm whether the security group configuration for the network interface used by the backend server is correct: see [Configuring a backend server security group](https://docs.byteplus.com/en/docs/clb/Configuring-a-server-security-group).

2. If selecting a secondary network interface as the backend server, confirm the route configuration is correct: see [Configuring route entries for the secondary network interface](https://docs.byteplus.com/en/docs/clb/Configuring-route-entries-for-a-secondary-network-interface).


<span id=".6K-35rGC6YCa6L-H6LSf6L295Z2H6KGh5Yiw6L6-5ZCO56uv5pyN5Yqh5Zmo77yM5aaC5p6c5a6i5oi356uv5Zyo5pyq5pS25Yiw5ZCO56uv5pyN5Yqh5Zmo55qE5Zue5aSN5YmN5Li75Yqo5pat5byA5ZKM6LSf6L295Z2H6KGh55qE6L-e5o6l77yM6LSf6L295Z2H6KGh5Lya5ZCM5pe25pat5byA5ZKM5ZCO56uv5pyN5Yqh5Zmo55qE6L-e5o6l5ZCX77yf"></span>
### If a request reaches the backend server through the CLB, and the client disconnects from the CLB before receiving a reply from the backend server, will the CLB also disconnect from the backend server?

After the client disconnects actively, the connection between the CLB and the backend server will also be disconnected.

<span id=".5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo55qE572R57uc54q25oCB77yf"></span>
### How to check the network status of the backend server?


1. Log in to the backend server; see the procedure at [Logging in to an instance](https://docs.byteplus.com/en/docs/ecs/Overview-1).

2. Run the corresponding command according to the operating system to ensure the primary network interface has been assigned the correct IP address.

   * Linux operating system: execute the `ifconfig` command.

      <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_832245b4bcd9ddb96ebc7741b12821e2.png) </span>

   * Windows operating system: run the `ipconfig` command.

3. ping the gateway IP in the subnet CIDR block of the backend server to check if the communication is normal.

   If data is returned, it indicates communication is normal.

   For example, if the backend server’s subnet segment is 192.168.1.0/24, run the command `ping 192.168.1.1`.


<span id=".5aaC5L2V5qOA5p-l5ZCO56uv5pyN5Yqh5Zmo55qE5pyN5Yqh54q25oCB77yf"></span>
### How to check the service status of the backend server?


1. Log in to the backend server. See [login instance](https://docs.byteplus.com/en/docs/ecs/Overview-1) for the procedure.

2. Run the corresponding command according to the operating system type to check if the service on the corresponding port is enabled.

   * Linux operating system: run the `netstat -antup` command.

      For example, the image below shows the TCP service on port 80 is enabled.

      <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_9d3d959bf339653a1b49723d789cc1bc.png) </span>

   * Windows operating system: run the `netstat -ano` command.

3. Run the following command to test if service communication is ACTIVE.

   `curl 127.0.0.1:80 -v`

   if the returned status code is 200, communication is ACTIVE.
