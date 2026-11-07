---
title: "Best practices for instance delivery"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance-delivery-best-practice"
---

The platform offers multiple methods for delivering ECS instances. You can purchase instances on demand at any time, purchase instances on different underlying hardware, purchase instances on dedicated underlying physical resources, or purchase instances by using the automatic scaling rules specified based on your business requirements. These methods meet instance creation requirements in various scenarios.

<span id=".5oyJ6ZyA6LSt5Lmw"></span>
## Purchase instances on demand

In any scenario, you can purchase an instance at any time. Batch purchase of instances with the same configuration is also supported.


|Purchase method |Applicable scenario |
|---|---|
|[Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances) |Purchase an instance with custom configurations. This method allows you to select the billing method, image, instance type, storage capacity, network, and security group based on your needs in different scenarios. |
|[Purchase an ECS instance with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration) |If you need a new instance with the same configuration as the current instance, you can use this method to quickly create a new instance. |
|[Purchasing an instance based on an instance launch template](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-a-launch-template-or-version) |You can create an instance launch template and purchase an instance based on it with one click. This method simplifies the configuration process and shortens the configuration duration. |
|[Purchasing an instance based on a custom image](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-with-custom-images) |If you have preferred operating system, applications, or other configurations, you can create a custom image. When you create an instance, you can use this custom image to improve configuration efficiency. |


<span id=".6auY5Y-v55So5YiG5pWj6LSt5Lmw"></span>
## Purchase instances on different underlying hardware for high availability

If your business requires high disaster recovery capabilities and high availability at the infrastructure level, you can purchase instances within a deployment set. This ensures instances across the specified regions are distributed and started according to your defined deployment policy.

A deployment set enables you to manage the distribution of instances across underlying hardware while ensuring physical isolation. By creating a deployment set, you can forcibly distribute instances across different underlying hosts, switches, or racks.

For more information, see [Deployment set overview](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview).

<span id=".6Ieq5Yqo5by55oCn6LSt5Lmw"></span>
## Purchase instances by using Auto Scaling

If your business requires continuous, stable operation or needs to handle scenarios such as short\-term traffic spikes or scheduled promotions, we recommend that you use Auto Scaling (AS) to purchase instances.

AS provides an on\-demand scalable resource pool of ECS instances. You can configure desired instance counts, scheduled quantitative scaling, or monitoring\-driven intelligent scaling, or perform manual scaling. Then, AS identifies real\-time workload changes and automatically adjusts the number of instances or their instance types in a scaling group promptly. This balances business demands with resource capacity while reducing the costs of manual operations and human maintenance.

For more information, see [Auto Scaling overview](https://docs.byteplus.com/en/docs/as/What-is-Auto-Scaling).
