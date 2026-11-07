---
title: "Application scenarios"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Use-scenarios"
---

<span id=".6auY6K6_6Zeu6YeP5Lia5Yqh55qE5rWB6YeP5YiG5Y-R"></span>
## Traffic distribution for high\-traffic businesses

<span id=".5bqU55So5Zy65pmv"></span>
### Application scenarios


* Games: version updates, new season launches, event promotions.

* E\-commerce: shopping festivals, large merchant promotional events.

* Audio and video: audio and video content updates.

* Online education: online course launches, training and learning.


<span id=".5bqU55So5o-P6L-w"></span>
### Description

For high\-traffic businesses, a single BytePlus ALB instance can handle millions of QPS concurrent requests. Based on your configured load balancing algorithm, ALB distributes traffic to different backend servers. This avoids response delays caused by overload on a single backend server and improves overall service performance.

<span id=".5bi46KeB5Lia5Yqh55qE56iz5a6a5oCn5L-d6Zqc"></span>
## Stability assurance for common business operations

<span id=".5bqU55So5Zy65pmv"></span>
### Application scenarios

Businesses with high stability requirements, such as public service institutions, corporate websites, and police systems.

<span id=".5bqU55So5o-P6L-w"></span>
### Application description

Service stability, security, and reliability are basic business requirements. BytePlus ALB allows you to add multiple backend servers, which back up each other within the same server group. ALB provides a Health Check feature to continuously monitor the health status of backend servers. If a server fails, ALB quickly isolates it and forwards requests to servers that are running normally, ensuring business stability. ALB also offers comprehensive security protection to resist complex network attacks and maintain business stability.

<span id=".5Lia5Yqh5pu05paw55qE54Gw5bqm5Y-R5biD"></span>
## Business update gray release

<span id=".5bqU55So5Zy65pmv"></span>
### Application scenarios

Financial digital currency systems, banking systems.

<span id=".5bqU55So5o-P6L-w"></span>
### Description

For frequently updated businesses, you can use BytePlus ALB to deploy multiple versions of content on different backend servers. When releasing a new version, you can adjust the weight distribution among backend servers to perform a gray release of the new business version.
