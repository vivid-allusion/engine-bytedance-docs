---
title: "How to make a security group plan"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups"
---

This topic describes commonly used planning principles for security groups.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

A security group controls the inbound and outbound traffic of each network interface of an ECS instance. Security groups offer status detection and packet filtering capabilities that you can use to segment security domains in the cloud. BytePlus provides security groups as an important network isolation method​ to ensure security.

Proper security group planning simplifies business traffic management and enhances security. Inadequate security group planning not only complicates ongoing maintenance but also exposes your business to security risks. Therefore, we recommend that you plan security groups appropriately from the outset, differentiate security groups based on business requirements, and specify corresponding security group rules.


* For example, if the network interfaces of all ECS instances are associated with the same security group, some ECS instances inevitably allow access from unnecessary IP addresses and ports, which introduces security risks.

* For example, if a separate security group is associated with the network interface of each ECS instance, you need to maintain a large number of security groups. This not only results in heavy repetitive work, but also raises the risk of omissions when you modify security group rules, which significantly increases maintenance complexity.


<span id=".6KeE5YiS5Y6f5YiZ"></span>
## Planning principles

<span id=".5pyA5bCP5o6I5p2D"></span>
### Least privilege

To mitigate security risks arising from exposing ECS instances to unnecessary IP addresses and ports, you should strictly follow the principle of least privilege. Open only the specific IP addresses and ports required, and exercise caution when you permit traffic to safeguard ECS instances.

**Example:**  When O&M users use a cloud\-based jump server to perform O&M operations on cloud resources, the access method of the jump server is exposed to the Internet to enable remote login by O&M users. The jump server has high\-level access permissions on cloud resources. Therefore, the security group rules for the jump server should only allow access to the SSH port of the jump server from the public IP addresses of O&M users, and deny access requests from other IP addresses.

Additionally, port 22, the default port for the SSH service, is considered a high\-risk port. To further enhance security, we recommend that you [change the SSH service port of your cloud-based jump server](https://docs.byteplus.com/en/docs/ecs/How-to-modify-the-default-remote-port-of-an-ECS-instance).

<span id=".5oyJ6ZyA5YiS5YiG"></span>
### Planning based on business requirements

You can associate ECS instances with security groups based on specific network communication requirements. For ECS instances with the same requirements, you can associate their network interfaces with the same security group. For ECS instances with different requirements, their network interfaces should be associated with separate security groups.


* **Example 1: Plan security groups by application**

   For ECS instances deployed with the same application, you can associate their network interfaces with the same security group. For ECS instances deployed with different applications, their network interfaces should be associated with separate security groups.

   * For example, when the same application is deployed on multiple backend servers of Cloud Load Balancer, these servers have identical communication requirements. Their network interfaces can be associated with the same security group.

   * For example, servers hosting web services and servers hosting database services have distinct network communication requirements. Their network interfaces should therefore be associated with separate security groups.

* **Example 2: Plan security groups by environment**

   In real\-world development and production workflows, a common practice to achieve system isolation is to deploy an online production environment alongside multiple test environments. As the test environment is frequently modified, the network interfaces of ECS instances across different environments should be associated with separate security groups with corresponding rules configured to prevent unintended impacts on the online production environment. This allows you to separately restrict access to production and test environments from ports and IP addresses, ensuring that modifications in the test environment do not affect production stability, and that multiple test environments remain isolated from one another.

&nbsp;

* **Example 3: Plan security groups by network service type**

   ECS instances that require Internet access and ECS instances that require only private network access should have their network interfaces associated with different security groups.

   * For ECS instances that require Internet access, the security group associated with their network interfaces must allow outbound and inbound traffic to/from EIPs to ensure communication with the Internet.

   * For ECS instances that require only private network access, the security group associated with their network interfaces should allow outbound and inbound traffic to/from private IP addresses and must explicitly block outbound and inbound traffic to/from EIPs. This effectively mitigates unnecessary Internet\-access risks and safeguards the security and stability of the private network environment.

* **Example 4: For ECS instances that require inter\-instance communication, associate their network interfaces with the same security group​** 

   By default, network interfaces associated with the same security group can communicate with each other. If multiple ECS instances require inter\-instance communication, you can associate their network interfaces with the same security group. In scenarios where multiple security groups exist and the security group rules are complex, you can create a new security group. Then, associate the network interfaces of the ECS instances that require inter\-instance communication with this new security group. This enables communication between the instances.


<span id=".5riF5pmw566A5rSB"></span>
### Clarity and conciseness


* The names and descriptions of security groups should be clear and easy to understand. This way, their purposes can be quickly identified. For example, a description could be: "Enable SSH login to servers via a jump server".

* Security group rules are sorted by priority in the console. You should assign priorities appropriately. For example, when you add security group rules to allow access from 192.168.1.66 over port 66 and port 88, you should assign the same priority to the rules.

* Keep security group rules simple to facilitate maintenance. For example, to allow access from the same IP address over multiple consecutive ports, you can specify a single security group rule instead of configuring a separate security group rule for each port.


<span id=".5Y-g5Yqg5L2_55So"></span>
### Combined use of security groups

For an ECS instance with one requirement, one security group is sufficient to meet the requirement. For an ECS instance with multiple requirements, the network interface can be associated with multiple security groups simultaneously. A network interface of an ECS instance can be associated with up to five security groups. Rules from multiple security groups are cumulative, equivalent to adding multiple rules to a single security group. When an ECS instance is associated with multiple security groups and the same IP address block and port are specified in multiple rules, whether the rules take effect varies based on the following conditions:


* If the rules are exactly the same, any one rule can take effect.

* If rule priorities are different, the rule with higher priority takes effect.

* If the rules have the same priority but different policies, the rule with the deny policy takes effect, while the rules with the allow policy do not take effect.


**Example:**  If an ECS instance requires both Internet access and private network access, and also needs to support remote login by using a jump server, its network interface can be associated with three security groups. These three security groups serve specific purposes: one for Internet access, one for private network access, and one for remote login.

<span id=".5ouS57ud562W55Wl"></span>
### Deny policy

When an ECS instance requires access from a large CIDR block, you can configure a deny policy to block traffic from specific IP addresses within that block. This meets access requirements while enhancing security and controllability. You should filter the IP address range to be denied based on your business requirements to ensure that security risks can still be effectively mitigated when you specify a large publicly accessible CIDR block.

**Example**: An ECS instance that provides services to all internet users can block malicious access from specific IP addresses by using a security group with a deny policy, after allowing access from the entire CIDR block (0.0.0.0/0).

<span id=".5Y-K5pe25riF6Zmk"></span>
### Prompt removal

<span id=".5Y-K5pe25riF6Zmk5YaX5L2Z5a6J5YWo57uE6KeE5YiZ"></span>
#### Promptly remove redundant security group rules

If security group rule A is covered by security group rule B and has a lower priority than rule B, rule A will not be matched, as specified in the [security group matching rules](https://docs.byteplus.com/en/docs/ecs/Security-group-overview#.5Yy56YWN6K-05piO). In this case, rule A is considered redundant. You should promptly clear redundant security group rules to keep security group rules clear and concise, thereby simplifying management.

<span id=".5Y-K5pe25riF6Zmk5LiN5YaN5L2_55So55qE5a6J5YWo57uE"></span>
#### Promptly remove security groups that are no longer in use

Each rule in a security group acts as either an allowlist or a blocklist, controlling traffic to and from the network interfaces of ECS instances associated with that security group. When a security group is no longer in use, remove the security group promptly to prevent potential issues caused by mistakenly associating the security group with the network interface of an ECS instance.
