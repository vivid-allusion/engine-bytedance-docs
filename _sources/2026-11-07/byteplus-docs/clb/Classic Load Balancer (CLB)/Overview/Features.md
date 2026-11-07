---
title: "Features"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Feature-list"
---

## Product features

|Feature |Explanation |Related documents |
|---|---|---|
|High connectivity |A CLB instance can forward traffic to backend servers in different availability zones within the same region; some regions support disaster recovery between primary and secondary availability zones. |[CLB disaster recovery configuration for Region main and standby Availability Zones](https://docs.byteplus.com/en/docs/clb/Best-practices-12) |
|Scheduling algorithm |The listener offers three routing algorithms: Weighted Round Robin (WRR), Weighted Least Connections (WLC), and Source IP Hash (SH). |[Routing algorithm principles](https://docs.byteplus.com/en/docs/clb/Listeners-01#.6LCD5bqm566X5rOV5Y6f55CG) |
|Health check |The listener's health check feature monitors the status of backend servers. If a backend server is detected to be in poor health, traffic will stop being forwarded to it and will be redirected to other normally functioning backend servers. |[Health check overview](https://docs.byteplus.com/en/docs/clb/Health-check-01) |
|Access control |CLB instances support denylist and allowlist mechanisms to flexibly control access from clients. |[Identity and Access Management overview](https://docs.byteplus.com/en/docs/clb/Access-control-list-01) |
|Domain name URL forwarding |The CLB instance’s layer 7 listener supports configuring domain names and URL forwarding rules, allowing requests to different domains and URLs to be forwarded to different backend servers. |[Forwarding rule description](https://docs.byteplus.com/en/docs/clb/Configuring-a-forwarding-rule-01) |
|Certificate |Provides unified certificate management service for the HTTPS protocol. Certificates do not need to be uploaded to the backend server and support decryption processing on the CLB instance, reducing CPU overhead on backend servers. |[Certificate overview](https://docs.byteplus.com/en/docs/clb/Certificate-management-01) |
|Access Log |You can use this feature to obtain detailed access log records of Layer\-7 CLB (HTTP and HTTPS listeners), including the client IP address and server response. The log helps you analyze client user behaviors, learn the geographical distribution of client users, and troubleshoot problems. |[Access log overview](https://docs.byteplus.com/en/docs/clb/Access-log-overview) |
|Alerts and monitoring |After integrating CLB with the cloud monitor service, various business metrics can be monitored in real time Through customizable metric thresholds and alert notifications, anomalies are detected promptly to ensure stable business operations. |* [Viewing monitoring data](https://docs.byteplus.com/en/docs/clb/Viewing-monitoring-data)<br><br>* [Configuring an alarm strategy](https://docs.byteplus.com/en/docs/clb/Configuring-an-alert-policy) |
|Health check log |After the CLB integrates with Torch Log Service (TLS), you can view health check logs, which helps analyze and identify the reasons for health check exceptions. |[Health check log overview](https://docs.byteplus.com/en/docs/clb/Health-check-log-01) |
|Session Persistence |Session persistence allows the server to remember the same user’s session state for a certain period to identify the user and maintain session information in subsequent requests. CLB supports session persistence for both layer\-4 and layer\-7 listeners.<br><br><br>* Layer\-4 listeners (TCP/UDP) support source IP\-based sticky sessions.<br><br>* Layer\-7 listeners (HTTP/HTTPS) support cookie\-based sticky sessions. |[Creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener) |
|Cross\-VPC backend |The Cloud Load Balancer (CLB) supports adding Elastic Compute Service (ECS) instances, network interfaces, or servers within IDC as backend servers via IP addresses across VPCs.<br><br>> **tip**<br><br><br>> The IP\-type backend server feature is in beta testing. To request a trial, contact customer service support.<br> |[Cross-VPC backend server overview](https://docs.byteplus.com/en/docs/clb/Cross-VPC-server-overview) |
|Redirection |The Layer 7 listener supports redirect functionality, allowing requests matching a certain domain name or URL to be redirected to other protocols, domain names, ports, or paths. It also supports specifying redirect status codes. |[Adding the redirect forwarding rules](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule#.5re75Yqg44CM6YeN5a6a5ZCR6L2s5Y-R6KeE5YiZ44CN) |

## Related products

|Service name |Feature Description |
|---|---|
|Elastic Compute Service |Serves as the backend server for the CLB instance, handling traffic. |
|VPC |Provide a private network deployment environment for CLB instances. |
|Elastic IP Address |Enables a CLB instance to connect to the IPv4 internet. |
|IPv6 Gateway |Provides the capability for a CLB instance to connect to the IPv6 internet.<br><br>> **tip**<br><br><br>> The IPv6 Gateway is currently in Beta. If you need a trial, contact your customer service support.<br> |
|PrivateLink (PL) |Allows sharing CLB resources within a VPC to other VPCs. |
