---
title: "Enhancing ECS instance security"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances"
---

The platform provides a variety of security products to enhance the security capabilities of your ECS instances. These products help prevent events such as cryptojacking on instances, file\-encrypting ransomware attacks, and intranet breaches via insecure configurations, which could threaten instance data security and disrupt your business operations.

This topic describes how to enhance the security capabilities of your ECS instances via different security products.

<span id=".5a6J5YWo5Lqn5ZOB5LuL57uN"></span>
## Security product overview


|Protection method |Security products |Operation guide |
|---|---|---|
|Internal protection for instance |* Password/key pair<br><br>* Security group<br><br>* Network Access Control List (ACL) |* [Improve password complexity](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.5o-Q6auY5a-G56CB5aSN5p2C5bqm)<br><br>* [Configure security groups](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.6YWN572u5a6J5YWo57uE)<br><br>* [Configure Network ACL](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.6YWN572u572R57ucQUNM) |
|External protection for instance |* Security enhancement |* [Enable security enhancement](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.5byA5ZCv5a6J5YWo5Yqg5Zu6) |
|Data protection |Data backup |[Back up instance data](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.5a6e5L6L5pWw5o2u5aSH5Lu9) |
|Alerts and monitoring |Resource monitoring |[Resource monitoring and alerts](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.6LWE5rqQ55uR5o6n5LiO5ZGK6K2m) |
||Resource alerts ||
|Account permission |Account security |[Configure account security settings](https://docs.byteplus.com/en/docs/ecs/How-to-enhance-the-security-of-ECS-instances#.6K6-572u6LSm5Y-35a6J5YWo) |


<span id=".5pON5L2c5oyH5Y2X"></span>
## Operation guide

<span id=".5o-Q6auY5a-G56CB5aSN5p2C5bqm"></span>
### Improve password complexity

Password is one of the security credentials for logging in to an ECS instance. For Linux instances that support logging in via [SSH key pairs](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview), we recommend prioritizing key\-based login for higher security than password login.

If you select using a password, when creating multiple ECS instances, set different passwords separately. Additionally, specify complex passwords to improve security.

Rules for setting passwords are as follows:


* The length is limited to 8 ～ 30 characters

* A password can only consist of uppercase letters, lowercase letters, numbers, and special characters, and must include at least three of these elements

* Valid special characters: `~!@#$%^&\*()_\-+=|{}[]:;'<\>,.?/

* The password cannot start with "/" or "$6$"


<span id=".6YWN572u5a6J5YWo57uE"></span>
### Configure security groups

A security group is composed of multiple security group rules. It is used to control the outbound and inbound traffic at the ECS network interface. Security groups offer status detection and packet filtering capabilities that you can use to segment security domains in the cloud. The platform provides security groups as an important network isolation method​ to ensure security.

You can use the following methods to control access of each network interface on your ECS instances:


* Create multiple security groups, and add different rules to each security group.

* Associate a network interface with one or multiple security groups. Based on associated rules, access by specified traffic is allowed for an instance, and the instance can access specified resources.

* Configure security groups to allow specified IP addresses and resources associated with specified security groups to access instances.


For how to plan and configure security groups, refer to [Best practices for planning security groups of ECS instances](https://docs.byteplus.com/en/docs/ecs/How-to-plan-security-groups) and [Best practices for configuring security groups of ECS instances](https://docs.byteplus.com/en/docs/ecs/How-to-configure-security-group-rules).

<span id=".6YWN572u572R57ucQUNM"></span>
### Configure Network ACL

Network ACL (Access Control List) consists of a series of ACL rules for controlling inbound and outbound traffic of a subnet. Within one subnet, all ECS instances and their associated network interfaces are subject to the associated Network ACL rules.

When used with security groups, Network ACLs allow you to control the inbound and outbound traffic of each ECS instance in a VPC more flexibly and precisely.

For how to learn and configure Network ACLs, refer to [Use cases of Network ACLs](https://docs.byteplus.com/en/docs/vpc/Network-ACL-use-cases).

<span id=".5byA5ZCv5a6J5YWo5Yqg5Zu6"></span>
### Enable security enhancement

ECS instances offer a security enhancement feature that provides real\-time monitoring and analysis of system activities. It generates alerts for risks detected during file and process monitoring, as well as threats like abnormal logins, helping reduce host intrusion risks and safeguard your host security.


* When you create an instance by using a Linux public image, security enhancement is enabled by default.

* When you create or reinstall a system based on a Windows public image or a custom image, security protection is disabled by default. 

* When you reinstall the system for an instance based on a Linux public image by using a Windows image or a custom image, security protection is disabled by default.  


For more information, refer to [Security enhancement](https://docs.byteplus.com/en/docs/ecs/Security-enhancement).

<span id=".5a6e5L6L5pWw5o2u5aSH5Lu9"></span>
### Back up instance data

We recommend regularly backing up data on your instances. This allows you to roll back data when an operational error occurs, and prevents data errors or loss caused by human mistakes, hacker attacks, virus infections, and other issues.

You can use [snapshots ](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot)or [Torch Object Storage](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos) for backing up data.

<span id=".6LWE5rqQ55uR5o6n5LiO5ZGK6K2m"></span>
### Resource monitoring and alerts

ECS instances support monitoring services. Based on the visualized data display of multiple monitoring metrics, such as metrics of basic monitoring, operating system monitoring, and process monitoring, you can track the running state of your resources.

You can also customize metric thresholds, alert notifications, event monitoring rules, and other capabilities. This allows you to be timely informed when the instance has an exception and therefore to run your businesses stably.

To learn more and configure monitoring and alert services, refer to[ Monitoring overview](https://docs.byteplus.com/en/docs/ecs/Monitoring-overview).

<span id=".6K6-572u6LSm5Y-35a6J5YWo"></span>
### Configure account security settings

Identity and Access Management (IAM) is a permission management system provided by the platform. It is used to control access to cloud resources by identity.

The root account has full access permissions to all cloud resources under the account. However, in complex cloud scenarios, sharing root account credentials is inconvenient and risky to account security. This feature enables you not to delegate the full permissions of your root account. Specifically, you can create identities such as users and roles, and grant different permissions to them based on scenario, achieving granular permission control.

To learn more and configure IAM, refer to [IAM overview](https://docs.byteplus.com/en/docs/ecs/Overview-3).
