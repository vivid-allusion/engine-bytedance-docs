---
title: "Related cloud products"
product: "Auto Scaling"
product_code: "as"
source: "https://docs.byteplus.com/en/docs/as/Related-cloud-services"
---

When using the Auto Scaling service, you may also need to use cloud products, such as ECS instances and Load Balancer. This topic describes the capabilities of each cloud product and explains the differences in the creation and deletion processes for cloud products associated with the Auto Scaling service.

<span id=".5LqR5Lqn5ZOB6IO95Yqb"></span>
## Capabilities


|Cloud product |Capabilities |
|---|---|
|[ECS](https://docs.byteplus.com/en/docs/ecs/What-is-Elastic-Compute-Service) |Elastic Compute Server (ECS) is a collection of resources such as CPUs, memory, and volumes. The computing and storage capabilities provided by ECS instances vary by instance type and size. Therefore, you can select appropriate instances to match different business workloads based on your needs. |
|[EIP](https://docs.byteplus.com/en/docs/eip/What-is-EIP) |Elastic IP Address (EIP) and its internet egress bandwidth are IP connectivity services provided by BytePlus. These services can be purchased and held separately for cloud resources. For a cloud resource such as an ECS instance and Load Balancer, it can access the Internet after being associated with an EIP. |
|Load Balancer |* [Classic Load Balancer (CLB)](https://docs.byteplus.com/en/docs/clb/Product-Overview-01) is a service that distributes access traffic to multiple backend servers (such as ECS instances) based on a specific policy.<br><br>* [Application Load Balancer (ALB)](https://docs.byteplus.com/en/docs/clb/Introduction) is a load\-balancing technology that operates at the application layer of the OSI model based on protocols such as HTTP, HTTPS, HTTP/2, WebSocket, and QUIC.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After a scaling group is associated with Load Balancer, when the scaling group performs adjustments, the ECS instances will be automatically synchronized to the backend server group of Load Balancer. This helps expand the external service capabilities of the system, eliminates single points of failure, and improves the overall availability of the system.</div><br> |


<span id=".5LqR5Lqn5ZOB55qE5Yib5bu6L-WIoOmZpOaWueW8jw=="></span>
## Methods for creating/deleting cloud products

In the Auto Scaling console, only operations, such as creating, removing, and deleting associated cloud products within a scaling group, are supported. For other standard operations, such as modifying cloud product features, associating volumes/EIPs, and deleting specific cloud products, there is no difference in the console\-based operation process. You can directly manage and operate the cloud products in their respective consoles.

When you create, remove, or delete cloud products within a scaling group, the operation methods vary slightly by product, as detailed below:

<span id=".5LqR5pyN5Yqh5Zmo"></span>
### ECS

In the Auto Scaling service, ECS instances are categorized into two types, with corresponding differences in billing methods and management operations listed below:


|Type |Billing method |Description |
|---|---|---|
|ECS instances automatically created for scale\-out |Currently, only pay\-as\-you\-go instances can be created. |Instance lifecycle is managed by the scaling group. An instance is automatically removed and deleted when the scaling group scales in, or when the health check feature detects it as abnormal. After the instance is deleted, its billing stops. |
|ECS instances manually added to the scaling group |Instances with billing methods of pay\-as\-you\-go and subscription can be added. |* The lifecycle of subscription instances does not support being managed by the scaling group. Specifically, a subscription instance will be automatically removed when the scaling group scales in or when the health check feature detects it as abnormal. After being removed, the instance is retained and continues to be billed. You can manually release it by deleting the instance in the ECS console.<br><br>* For pay\-as\-you\-go instances, you can choose whether to have the lifecycle managed by the scaling group. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If an instance has scale\-in protection enabled, it can avoid impacts caused by adjustments and health checks. Regardless of whether it is managed, it will not be automatically deleted or removed.</div>


<span id=".6LSf6L295Z2H6KGh"></span>
### Load Balancer

The Auto Scaling service only supports configuring whether to associate with Load Balancer products, but does not perform automatic creation or deletion.

<span id=".UkRT5pWw5o2u5bqT"></span>
### RDS database

The Auto Scaling service only supports configuring whether to associate with RDS database products, but does not perform automatic creation or deletion.

<span id=".5YWs572RSVDor7TmmI4="></span>
### EIP

If you check the EIP allocation option for scaling configuration, instances automatically created or manually added to the scaling group will have EIPs automatically purchased and associated. Additionally, when an instance is deleted or removed, the EIP can be automatically released.
