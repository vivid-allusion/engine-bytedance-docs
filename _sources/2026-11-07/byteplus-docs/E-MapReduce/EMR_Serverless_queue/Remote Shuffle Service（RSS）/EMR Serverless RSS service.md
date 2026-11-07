---
title: "EMR Serverless RSS service"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_Serverless_RSS_service"
---

Serverless RSS (Serverless Remote Shuffle Service) is a product developed by the Volcano Engine EMR team that provides remote shuffle management and enhances performance and stability for big data and AI scenarios such as Spark, Flink, Hadoop, and MapReduce. This document introduces how to create and manage the EMR Serverless RSS service.

<span id="1de9b793"></span>
# Context

To meet your daily basic business requirements, EMR Serverless provides a "public RSS service," offering a certain amount of free capacity and preset elastic capacity. You can also create a "dedicated RSS service" as needed.


|RSS service types |Service Note |
|---|---|
|Public RSS service |EMR Serverless provides a shared public RSS service for all users:<br><br><br>* The public RSS service offers a certain amount of free capacity.<br><br>   * **Basic free quota**: Tenant level **50 TiB**.<br><br>   * **High\-spec bonus policy**: For users who purchase dedicated queue resources greater than 1024 CU, for every additional 32 CU, the tenant level receives an extra **3 TiB** of free fixed capacity.<br><br>* Additionally, **900 TiB** of elastic capacity is set by default.<br><br>   * The public RSS service will be officially commercialized on October 12, 2026. After commercialization, when your Remote Shuffle instantaneous peak **exceeds** the free fixed capacity but is below the elastic capacity limit, the excess portion (within the elastic capacity range) will be billed based on **actual usage × duration**. For billing rules, see [Shuffle capacity billing details](https://docs.byteplus.com/docs/undefined/6a1432e76f5e8205336a4013).<br><br>   * You can set the elastic capacity limit independently in the console via  **"Change Elastic Configuration"** , or set it to 0 TiB to disable elastic expansion.<br><br>      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div><br>      <br><br>      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Please configure the elastic limit carefully. If the actual Shuffle capacity demand exceeds the sum of "free fixed capacity + elastic capacity limit," your job will fail.      </div><br>       |
|Dedicated RSS service |You can create dedicated RSS services as needed. Dedicated RSS service resources are independently applicable to scenarios with high capacity demands and ensure stable RSS resources.<br><br><br>* Dedicated RSS services support combined configuration of "fixed Shuffle capacity" (Subscription) and "elastic Shuffle capacity" (billed by usage). For billing rules, see [Shuffle capacity billing details](https://docs.byteplus.com/docs/undefined/6a1432e76f5e8205336a4013). |


<span id="680dfe99"></span>
# Important notes


* The current Serverless dedicated RSS service features an allowlist function. To enable this feature, [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D) for activation.

* Only administrators have permission to create and manage Serverless dedicated RSS services.


<span id="6c82d0b8"></span>
# Create a Serverless dedicated RSS service

<span id="21969a92"></span>
## Entry point for creation


1. Log in to [EMR Serverless console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/serverless/queue_manage?StatusesInclude=0&projectName=default).

2. In the top menu bar, select the region and project space from the dropdown according to your actual scenario:

   1. Region: The created queue and corresponding resources will be deployed in the selected region and cannot be changed after creation.

   2. Project: The default project is displayed.

3. Go to the create queue page.

   1. Method 1: On the overview page, click Create resource \> Serverless RSS Service.

   2. Method 2: In the left navigation bar, select Resources \> Serverless, and click the Create resource \> Serverless RSS button in the upper left corner of the page.


<span id="6840e309"></span>
## Configure service parameters

<span id="412b1902"></span>
### Configure resource information


|**Configuration item** |**Note** |
|---|---|
|Region |Select the geographic region where the resource is located. Resources in different regions cannot communicate with each other over the internal network. |
|Availability zone |Select the availability zone where the resource is located. You can select one or more availability zones. Additional zones can be added during configuration, but removal is not allowed. Selecting multiple availability zones means you accept cross\-zone deployment, and underlying node resources may not be evenly distributed across all zones. When resources in a single availability zone are insufficient or a failure occurs, failover and disaster recovery can be achieved, but business access latency may increase. We recommend using a multi\-availability zone solution for queues exceeding 3000 CU to obtain better resource supply. |
|access configuration |Configure whether to enable the VPC network connection switch. After enabling, EMR on ECS and EMR on VKE clusters within the same VPC can use Serverless Celeborn.<br><br>Enabling the network connection requires additional configuration of the following parameters:<br><br><br>* VPC: Select the private network under the current project.<br><br>* Subnet: Select the subnet within the current availability zone.<br><br>* Security group: Select the security group under the private network. |


<span id="b8cb2168"></span>
### Configure billing information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350cdb989ec9497699d0628c2574cd37~tplv-goo7wpa0wc-image.image) </span>


|**Configuration item** |**Note** |
|---|---|
|Payment type |Currently, only the Subscription type is supported. For billing details, see [Shuffle capacity pricing details](https://docs.byteplus.com/docs/undefined/6a1432e76f5e8205336a4013).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Currently, the overall billing type for the Serverless RSS service only supports the Subscription type. However, you can flexibly configure the fixed Shuffle capacity and elastic Shuffle capacity for the Subscription service.</div><br> |
|Billing duration &Auto\-renewal |* Billing duration: Select the purchase duration for Subscription queue resources. Default value: 1 month.<br><br>* Auto\-renewal: Set whether to enable auto\-renewal after the current Subscription queue resources expire. It is recommended to enable this option to avoid business impact due to resource expiration. After enabling:<br><br>   * The system will automatically deduct the fee from the account balance on a monthly basis before the resource expires, without requiring manual payment.<br><br>   * The auto\-renewal cycle is fixed as "monthly". That is, regardless of the Billing duration configuration duration for queue resources, each subsequent auto\-renewal will extend the duration by one month. |


<span id="aab1a3dd"></span>
### Capacity configuration


|**Configuration item** |**Note** |
|---|---|
|Service name |Customize the name of the Serverless RSS service to identify the service. The name length must be 1–64 characters and can only contain lowercase letters, numbers, and `_`. |
|Fixed Shuffle Capacity |Set the fixed Shuffle capacity. The fixed Shuffle capacity portion uses the Subscription billing type.<br><br><br>* Capacity unit: TiB.<br><br>* Step size: 3 TiB.<br><br>* The minimum fixed Shuffle capacity is 90 TiB. |
|Elastic Shuffle Capacity |Set the elastic Shuffle capacity. The elastic Shuffle capacity portion uses the pay\-as\-you\-go billing type.<br><br><br>* Capacity unit: TiB.<br><br>* Step size: 3 TiB.<br><br>* The maximum elastic Shuffle capacity that can be set is 300 TiB. |


<span id="1b8176fa"></span>
### Other configuration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d32cf67c08da4fd09e435255db43d67a~tplv-goo7wpa0wc-image.image) </span>


|**Configuration item** |**Note** |
|---|---|
|Tag |Add tags to resources for easier classification and management. You can select existing tags or create new tags. Note: Up to 20 tags can be added. |


<span id="fdc26749"></span>
## View creation results


1. After creation, you can view the list of created RSS services on the RSS service tab. When the status of the RSS service changes from "Creating" to "Running", it indicates that the RSS service has been successfully created and is running normally.

2. After creation, you can click the corresponding RSS service name to enter the RSS service details page, where you can view information such as the service address and capacity.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8d348d7e23b48a3b23a3c7aeddec1f7~tplv-goo7wpa0wc-image.image) </span>


<span id="f2a34e32"></span>
## Next step

<span id="67109d60"></span>
### Bind queue resources

After creating the Serverless RSS service, you can bind the service to Serverless queue resources. You can bind it when creating a new queue resource or when editing an existing queue resource in "Other configurations".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6408d9b2c93b4c25bf910ec1c4f7b0fd~tplv-goo7wpa0wc-image.image) </span>

You can turn on the Independent Shuffle Service switch and select an existing RSS service from the dropdown to achieve better shuffle performance and load isolation.

<span id="173c8b70"></span>
### Bind compute group resources

Already created Serverless RSS services can also be bound to Spark compute groups to achieve better shuffle performance and load isolation.


* The configuration priority of the compute group’s Independent Shuffle Service is higher than that of the queue configuration.

* Currently, only the Spark SQL compute group supports configuringIndependent Shuffle Service, and the general compute group inherits the queue's configuration.


<span id="53aa2e43"></span>
### Apply RSS service to jobs


* Jobs submitted by queues or compute groups bound to the service will use the RSS service by default, enabling remote shuffle processing.

* Spark jobs can also use the RSS service by setting parameters. The specific parameters are as follows:

   ```SQL
   set spark.celeborn.master.endpoints=您的rss内网地址，如x.x.x.x:9097
   ```
   


<span id="5c65bfd1"></span>
# Manage Serverless RSS service

<span id="e31eec28"></span>
## Modify capacity configuration


1. You can click Change capacity configuration in the Actions column on the RSS service list page to adjust the capacity of the RSS service.

2. You can adjust the capacity of Fixed Shuffle Capacity and Elastic Shuffle Capacity to easily perform scaling operations.

   * After **Elegant shrinkage** is enabled and submitted during scale\-down, Shuffle resources will be scaled down after the task ends or after a 12\-hour timeout.

   * When scaling down, if **Elegant shrinkage** is disabled and submitted, Shuffle resources will be forcibly scaled down immediately, which may cause running jobs to fail. Please choose carefully.


<span id="27eebcd3"></span>
## Modify availability zone


1. You can click Availability Zones and Access Configuration in the Actions column on the RSS service list page to adjust the availability zone configuration of the RSS service.

2. Add new availability zones in the pop\-up sidebar.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/454500957b4145d5be4273b07da26844~tplv-goo7wpa0wc-image.image) </span>


<span id="7246ac2b"></span>
## Permission control & service monitoring

Click the monitoring and authorization buttons in the Actions column on the RSS service list page to view monitoring metrics for the RSS service and manage permissions for the RSS service.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87fd0958d98e430ab04427da0f9e0e78~tplv-goo7wpa0wc-image.image) </span>


* Service monitoring: Metrics such as the number of active Shuffle tasks and Shuffle partitions are currently preset for the RSS service.

* Permission control: Currently, only Admin users can operate and use the RSS service. To grant other users access to the RSS service, you must assign Admin permissions to the corresponding user or role.


<span id="d077e404"></span>
## Service renewal & cancellation

Click the renewal and cancellation buttons in the Actions column on the RSS service list page to perform renewal or cancellation operations.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d196e7c174b94390a9c7f42d0f67551e~tplv-goo7wpa0wc-image.image) </span>

The cancellation of the RSS service is irreversible and will directly affect associated business operations. It is strongly recommended to remove the above associations in the compute queue and ensure that no business tasks are running before cancellation.
