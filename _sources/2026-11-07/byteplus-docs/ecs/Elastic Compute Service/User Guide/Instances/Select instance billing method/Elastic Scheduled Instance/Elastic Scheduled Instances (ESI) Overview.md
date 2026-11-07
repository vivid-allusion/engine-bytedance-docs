---
title: "Elastic Scheduled Instances (ESI) Overview"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview"
---

Elastic Scheduled Instances (ESI) are pay\-as\-you\-go instances that support advance reservation, are designed for elastic scenarios, and ensure stable resource supply. After you make a reservation purchase, a Pay\-as\-you\-go instance can be automatically created for you within the resource delivery time window.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Elastic Scheduled Instances are currently only available for sale in the China (Beijing), China (Shanghai), and China (Guangzhou) regions. Moreover, the instance types offered in different regions and availability zones vary slightly. Please refer to the actual display in the console for details.</div>


<span id=".6K6h6LS56KeE5YiZ"></span>
## Billing rule

Elastic Scheduled Instances (ESI) are subject to a minimum one\-hour charge. Regardless of whether the instance is released within the first hour after creation, a bill will be issued and a fee for one hour of usage will be charged. If usage exceeds one hour, charges will be based on actual usage. For detailed billing rules for Elastic Scheduled Instances, refer to [Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances).

<span id=".5rWB56iL6K-05piO"></span>
## Process description


1. Create an ESI order

   When making a reservation, you need to complete the instance configuration (including compute specifications, image, storage, network, number of instances, and so on), and specify the resource delivery time window. After a reservation is successful, the system will automatically generate an ESI order. [Learn more](https://docs.byteplus.com/en/docs/ecs/Creating_ESIs).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After a reservation order is successfully created, it is not recommended to modify the relevant configuration of a <strong>pending delivery</strong> reservation order. Otherwise, instance delivery may fail. For details, refer to <a href="https://docs.byteplus.com/en/docs/ecs/Elastic_Scheduled_Instances_Overview#.5rOo5oSP5LqL6aG5">Precautions</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can <a href="https://docs.byteplus.com/en/docs/ecs/Cancel_appointment">cancel the appointment</a> within 30 minutes after the appointment order is created.   </div>
   

2. Automatic delivery of Elastic Scheduled Instances (ESI) by the system

   After the resource delivery time window specified in the reservation order is reached, the system automatically creates a Pay\-as\-you\-go instance based on the reservation order information. At this time, the instance status is **Creating**.

   Instance delivery results are as follows:

   * Delivered: All instances in the reservation order have been created, and the instance status has changed to **Running**.

   * Partial delivery: There is a delivery risk, and some instances failed to be created. You can view details through event notifications sent by the platform via channels such as internal message, SMS, email, and so on.

   * Delivery failed: There is a delivery risk; all instances failed to be created. You can view details through event notifications sent by the platform via channels such as internal message, SMS, or email.

3. Release an instance

   After Elastic Scheduled Instances (ESI) are successfully delivered, they will not be released automatically (except when resources are released due to an overdue payment). You can manually [delete the instance](https://docs.byteplus.com/en/docs/ecs/Delete_Elastic_Scheduled_Instances) after your business is complete.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Limitations |Description |
|---|---|
|Instance type |Instance families that support scheduled purchase:<br><br><br>* General<br><br>* Compute\-optimized<br><br>* Memory\-optimized<br><br>* HFG2 general\-purpose instance with high processor base frequency<br><br>* Local\-SSD i3s and i2<br><br>* Some heterogeneous compute\-optimized instance families |
|vCPU quota |A single account can use up to 300 vCPUs in a single availability zone. If you need to increase your vCPU quota, please go to the [Quota Center](https://console.byteplus.com/quota/ProductList/inParameterList?ProviderCode=ecs) to apply. [Learn more](https://docs.byteplus.com/en/docs/ecs/ECS-resource-quota-management). |
|Number of instances |You can purchase up to 500 instances at a time. |
|Deduction on the bill |Using Reserved Instances (RI) to deduct the compute resource (vCPU and memory) portion of the Elastic Scheduled Instances (ESI) bill is not supported; however, Reserved Storage Capacity can be used to deduct the storage portion of the bill. |
|Modify instance type |Not supported. |
|Convert billing methods |Not supported. |
|Pay\-as\-you\-go Economical Mode |Not supported. |
|Deployment Set |Not supported. |


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Due to the potential for delayed delivery with Elastic Scheduled Instances (ESI), **it is not recommended to perform any actions that modify resources associated with the reservation order from the time the order is created until resource delivery is complete, as this may result in delivery failure**, including but not limited to the following actions:


|Time periods |Resource |Risk actions |
|---|---|---|
|From the start of reservation order creation to the completion of resource delivery |Network Interface |When creating a reservation order, a network interface is pre\-created (at this point, the network interface is not yet mounted to the instance). The following actions are not allowed on this network interface; otherwise, resource delivery will fail.<br><br><br>* Mounting to other instances or deleting the network interface is not allowed.<br><br>* Changing the security group associated with the network interface, or associating or disassociating an EIP, is not permitted.<br><br>* You are not allowed to delete resources attached to the network interface, such as VPCs, subnets, security groups, and other resources.<br><br>* If an IPv6 address has already been assigned to the network interface, you are not allowed to enable IPv6 Internet bandwidth for it. |
||Bandwidth Package |* Pay\-as\-you\-go Shared Bandwidth Packages: cannot be deleted.<br><br>* Subscription Shared Bandwidth Packages must not be in Expired, Suspended, or Unsubscribed status. |
||Safety package |If an enhanced protection type EIP that supports DDoS Native Protection is associated, the security protection package must be in normal status. For more information about security protection, refer to the EIP part of [Network configuration](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances#.572R57uc6YWN572u). |
||Images |* For ESI orders created using a Custom Image, deleting the Custom Image is not allowed.<br><br>* For ESI orders created using a Shared Image, canceling the Shared Image is not allowed. |
||Key Pair |You are not allowed to delete key pairs associated with the instance before delivery. |
||Project |Deleting projects associated with the reservation order is not allowed before instance delivery. |
||Other risks:<br><br><br>* The account is overdue. Instance delivery failed. You can refer to [bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details) to view overdue details and top up promptly.<br><br>* Other actions that may modify the resources relied upon by Elastic Scheduled Instances (ESI), as well as instance delivery failures caused by storage or network issues, such as insufficient Volume inventory, insufficient EIP inventory, and so on. ||


<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

**A foreseeable peak in one\-off resource demand**

In business scenarios where a large volume of access is expected within a short period, it is necessary to reserve resources for critical business during specific time windows and maintain high\-performance access. For example: major e\-commerce promotions, video live streaming, peak ticketing periods during holidays, and so on.

**Regular periodic business peaks**

For predictable computing workloads that are scheduled to occur at fixed daily, weekly, or monthly intervals, where application load peaks are concentrated within these periods, Elastic Scheduled Instances (ESI) can be used to ensure stable resource supply and an optimal user experience during peak times. For example, daily business peak periods for online gaming, online education, big data analytics, and rendering services, as well as monthly reconciliation peak periods for financial services and so on.

**Elastic requirements for offline businesses that can tolerate some delay**

Business peak periods are irregular and difficult to predict. However, for offline workloads that can tolerate some waiting time, you can schedule Elastic Scheduled Instances (ESI) once a business peak begins and run your workloads after the instances are delivered. This approach provides lower costs and greater resource certainty compared to Pay\-as\-you\-go billing. For example: irregular business peaks in scientific computing, offline rendering, and so on.

<span id=".55Sf5ZG95ZGo5pyf"></span>
## Lifecycle

**ESI order status**

After the reservation is successful, the system generates an ESI order and, within the resource delivery time window, delivers instance resources according to the order.


|Status name |Status attribute |Status description |
|---|---|---|
|Creating |Intermediate status |The status after you create an ESI order and before it enters **Pending delivery**. |
|Pending |Stable status |The normal status of an ESI order after it is created and before resource delivery. |
|Delivering |Intermediate status |After the resource delivery time period is reached, resource delivery begins. |
|Delivered |Stable status |All resources have been delivered. |
|Failed |Stable status |All resources failed to be delivered. |
|Partially failed |Stable status |Not all resources have been delivered. |
|Invalid |Stable status |The ESI order record will be permanently deleted 15 days after all resources have been released and the ESI order has become invalid. |
|Canceled |Stable status |Cancel the reservation. |


**Elastic Scheduled Instance statuses**

After the successful delivery of Elastic Scheduled Instances (ESI), their lifecycle is the same as that of regular ECS instances. For details, refer to [instance lifecycle](https://docs.byteplus.com/en/docs/ecs/Instance-lifecycle).

<span id=".5L2_55So5oyH5a-8"></span>
## Usage guide


|Actions |Document |
|---|---|
|Create an ESI order |[Create Elastic Scheduled Instances](https://docs.byteplus.com/en/docs/ecs/Creating_ESIs) |
|View Elastic Scheduled event |[View ESI order event](https://docs.byteplus.com/en/docs/ecs/View_ESI_order_event) |
|Purchase reservation orders with the same configuration |[Purchase reservation orders with the same configuration](https://docs.byteplus.com/en/docs/ecs/Purchase_reservation_orders_of_the_same_configuration) |
|Purchase Elastic Scheduled Instances (ESI) with the same configuration |[Purchase instances with the same configuration](https://docs.byteplus.com/en/docs/ecs/Buying-ECS-instances-that-use-the-same-configuration) |
|Cancel appointment |[Cancel appointment](https://docs.byteplus.com/en/docs/ecs/Cancel_appointment) |
|Stop Elastic Scheduled Instances (ESI) |[Stop instances](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) |
|Delete Elastic Scheduled Instances (ESI) |[Delete Elastic Scheduled Instances (ESI)](https://docs.byteplus.com/en/docs/ecs/Delete_Elastic_Scheduled_Instances) |


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

[Elastic Scheduled Instances (ESI) FAQ](https://docs.byteplus.com/en/docs/ecs/ESI_FAQs).
