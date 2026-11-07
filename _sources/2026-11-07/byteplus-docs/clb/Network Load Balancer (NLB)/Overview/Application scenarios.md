---
title: "Application scenarios"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Application-scenario"
---

<span id=".5rW36YeP5Lia5Yqh5by55oCn6L2s5Y-R"></span>
## Elastic traffic forwarding for massive applications

Network Load Balancer (NLB) provides ultra\-high layer 4 load processing capability, suitable for high\-traffic and high\-concurrency business scenarios and can serve as an IoT service entry point for applications like the Internet of Things and Internet of Vehicles. Instance performance can be quickly scaled up based on business changes, eliminating the need for manual intervention during business fluctuations and effectively reducing O&M costs.

<span id=".5Lia5Yqh6auY5Y-v55So5oCn5L-d6Zqc"></span>
## Ensuring high availability for business operations

NLB adopts NFV architecture, supporting multi\-Availability Zone deployment, availability zone affinity between LB instances and backend servers, and mechanisms like all zones deployment, health checks, and all zones traffic forwarding to ensure overall service availability.

<span id=".5re35ZCI5LqR57uE572R5Zy65pmv"></span>
## Hybrid cloud scenarios

NLB instances support adding cross\-VPC backend servers to achieve hybrid cloud complex networking. Compared to CLB, NLB directly uses IP addresses within the VPC CIDR block to communicate with backend servers, rather than 100.64.0.0/10 CIDR block addresses. Cross\-VPC backend route configuration is simple and free from address conflict issues.
