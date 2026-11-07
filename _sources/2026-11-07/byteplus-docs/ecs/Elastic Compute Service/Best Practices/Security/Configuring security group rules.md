---
title: "Configuring security group rules"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How-to-configure-security-group-rules"
---

In addition to properly planning security groups for your cloud products, you also need to configure appropriate policies and access rules under security groups.

<span id=".5oC75L2T6KeE5YiZ"></span>
## General principles


* When you set inbound and outbound access rules, follow the principle of least permissions, which means authorizing only when necessary.

* Simplify security group rules as much as possible.

   You can associate an ECS instance with up to five security groups, and add up to 200 access rules to each security group. Therefore, in an ECS instance, hundreds of access rules are probably taking effect at the same time. If a security group consists of complex rules, you may find it hard to manage and modify it in later operations.


<span id=".5ZCI55CG5L2_55So5a6J5YWo57uE6KeE5YiZ"></span>
## Properly use security group rules

A security group rule acts as an allowlist or denylist. By configuring it, you can allow or deny access requests, thereby controlling access for ECS instances. For how to configure security groups, see [Managing security group rules](https://docs.byteplus.com/en/docs/ecs/Modifying-security-group-rules).

<span id=".6YG_5YWN6K6-572uMC4wLjAuMC8w6K6_6Zeu6KeE5YiZ"></span>
## Avoid setting 0.0.0.0/0 in access rules

When you add access rules, avoid using 0.0.0.0/0. Using 0.0.0.0/0 means allowing all inbound accesses and exposing all ports to the public network, which is extremely unsafe and risky.

Use security groups as allowlists. This means when you configure a security group rule, first deny all access requests, and then add allow policies for required ports of the ECS instance. For example, if you need to allow access to ECS instance services via HTTP and HTTPS protocols, you can configure the security group rules as follows to allow inbound traffic on ports 80 and 443.

<span id=".6ZmN5L2O6Z2e5b-F6KaB6KeE5YiZ55qE5LyY5YWI57qn"></span>
## Lower priorities of unnecessary rules

When adding a security group rule, you need to specify a priority value. The priority value ranges from 1 to 100. The smaller the value, the higher the priority. If the current security group includes a 0.0.0.0/0\-contained rule, confirm whether all ports are necessarily required to be exposed externally based on applications or services on this ECS instance.

If not necessary, you can add a security group rule with policy set to "Deny" and priority to "100". For example, when you have deployed a MySQL database service on an ECS instance, for a 0.0.0.0/0\-specified rule, avoid allowing port 3306 by adding a "Deny" policy. Detailed operations are as follows.

<span id=".5bC95Y-v6IO96YG_5YWN5Y-Y5pu05a6J5YWo57uE6KeE5YiZ"></span>
## Avoid modifying security group rules

Since modifying security group rules may affect the interconnectivity of ECS instances, your online services may be impacted. Therefore, avoid modifying security group rules as much as possible.

If you do need to change security group rules, create a new security group first and then associate secondary network interfaces of the ECS instances that need interconnectivity with the new security group. After this, you can modify the existing rules. During this process, modify rules one by one. This means after you modify one rule, check whether your online businesses are running properly. Proceed to the next rule only when no business is impacted. If you find your businesses are affected, restore the original security group rule immediately.

<span id=".6K6-572u5a6J5YWo57uE5L2c5Li66K6_6Zeu5a-56LGh"></span>
## Set a security group as the access target

[ security group rules](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups)[ security group rules](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups)[ security group rules](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups) involves a principle of associating different applications and services with different security groups. Therefore, in such scenarios, when you configure access rules of security groups, set a security group as the source address.

For distributed applications, applications of different types are associated with different security groups, which may cause network connectivity isolation between involved security groups. To enable access to the target application, you can add an allow rule in the security group of the target application by setting the source address to the security group of the application initiating access. This grants permission to access target application resources to the application initiating access. Suppose a service in a distributed application needs to access a database. In that case, you can configure the database security group (sg\-database) to allow traffic on port 3306 from the service security group (sg\-service).

<span id=".6K6-572u5Y-v5L-hSVDnvZHmrrXkvZzkuLrorr_pl67lr7nosaE="></span>
## Set trusted IP CIDR blocks as the access target

Suppose you only need to allow access from an ECS instance within a specific subnet of a VPC. In that case, you can first deny all access in the security group of the target resource, then specify the CIDR block of the subnet that needs access to allow access by the trusted IP CIDR block.
