---
title: "Benefits"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Benefits"
---

<span id=".6Ieq5Yqo5YyW5Ly457yp6LWE5rqQ"></span>
## Automated scaling of resources

The Auto Scaling service can identify business changes in real time and promptly adjust the number and type of instances within the scaling group. This ensures a balance between business requirements and resource capacity.


* Intelligent scaling of instances is achieved without manual operation or tracking.

* When business requirements increase, ECS instances are automatically scaled up, or the instance type is automatically upgraded.

* When business demand declines, ECS instances are automatically scaled in​, or the instance type is automatically downgraded.


<span id=".54G15rS76auY5pWI"></span>
## Flexibility and efficiency


* Multiple scaling methods

   AS provides multiple methods for scaling instances. For example, you can configure desired instance counts, scheduled quantitative scaling, or monitoring\-driven intelligent scaling, or perform manual scaling. This helps meet your diverse business planning and scenario\-specific requirements.

   At the same time, the lifecycle hook feature is supported. When instances are added to or removed from the scaling group, they are suspended to allow you to perform custom operations, such as installing required software or backing up important data. This provides flexible management capabilities during automatic scaling operations.

* Multiple scaling policies

   * Multi\-availability zone policy: For instances to be automatically added, you can choose to deploy them in the availability zone with higher priority or implement balanced deployment across multiple availability zones.

   * Custom billing type: For instances to be automatically added, you can choose the number or proportion of pay\-as\-you\-go instances in the scaling group, or select spot instances to reduce costs.

   * Instance removal policy: For instances to be automatically removed, you can prioritize removing the earliest or latest created instances in the scaling group, or prioritize removing instances corresponding to the earliest associated scaling configuration.

   * Instance reclaim policy: For instances to be automatically removed, you can also choose to release or retain certain instance resources based on your needs.

   * Lifecycle hook: When instances are added to or removed from the scaling group, they are suspended to allow you to perform custom operations, such as installing required software or backing up important data. This provides flexible management capabilities during automatic scaling operations.

* Multiple scaling configuration sources

   You can use scaling configurations or instance launch templates as scaling configuration sources, both of which allow you to select multiple instance types. This prevents expansion failure caused by insufficient stock of a particular type, increases fault tolerance during scaling up, and improves availability.

* Multiple instance types

   You can select multiple instance types at the same time. We recommend choosing instance types that are similar in configuration, pricing, performance, and other aspects. If an instance type cannot be created due to stockouts or other reasons, the scaling group automatically creates instances of other types, reducing the risk of expansion failure and improving fault tolerance.


<span id=".5L2O5oiQ5pys"></span>
## Lower cost

With AS automation capabilities, you do not need to devote excessive human effort to monitoring business developments. There is no need to prepare redundant resources in advance to accommodate business growth, and you do not need to worry about delayed resource release, thereby optimizing cost efficiency. This feature offers timely adjustments to help you maximize cost savings while ensuring stable business operations.

<span id=".6auY5Y-v55So"></span>
## High availability

With the CLB product enabled, incoming traffic is automatically distributed across all instances in the scaling group. When instances in the scaling group are added or released, they are automatically synchronized to the CLB backend server group. This enables new instances to be accessible to clients and released instances to be promptly removed from the group. This enhances business smoothness and provides continuous, stable enterprise\-level reliability.

<span id=".6auY5a656ZSZ5oCn"></span>
## High fault tolerance


* AS offers health check capabilities to periodically monitor the running status of instances. After an instance is detected as abnormal, a new instance is automatically created to replace the faulty one. This effectively prevents issues caused by delayed exception detection.

* For instances with special workloads, you can mark them as protected instances. Protected instances are excluded from health status checks and are not affected by scaling actions performed by the scaling group.


<span id=".5a6e5pe257uG57KS5bqm55uR5o6n"></span>
## Fine\-grained monitoring in real time

When a scaling action is triggered by an alert task, monitoring metrics data is collected every minute. This helps you stay informed about the real\-time running status of resources.
