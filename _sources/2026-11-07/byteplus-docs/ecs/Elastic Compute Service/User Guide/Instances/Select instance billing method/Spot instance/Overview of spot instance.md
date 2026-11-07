---
title: "Overview of spot instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Spot_instances_overview"
---

A spot instance is a type of on\-demand instance with performance same as regular pay\-as\-you\-go instances. It offers a certain discount compared to pay\-as\-you\-go instances. This helps you lower the cost of instance usage in certain scenarios.

<span id="sFaE6XxQ"></span>
## Operation process

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_28425e87c0605abeabef01d5dab9be81.png) </span>

When you purchase a spot instance, you need to set the maximum price. When inventory is sufficient and your bid price is greater than or equal to the spot market price, you can successfully purchase the instance. For detailed information, refer to [Purchaseing spot instance](https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance).

After you successfully purchase a spot instance, the instance launches automatically. Then, you can deploy businesses immediately. During this period, the system checks the instance inventory and compares the spot market price with the bid in real time. Specific situations are as follows:


* When the stock is sufficient **and** the bid price is greater than or equal to the spot market price, you can continue using the spot instance. After business completion, you can manually release the instance.

* When the inventory is insufficient ** or** the market price exceeds your bid price, a spot instance interruption event is triggered. Meanwhile, the system sends a notification about the upcoming instance release via internal messages, SMS, email, or other channels before the release. At the corresponding time after the notification is sent, the system will automatically release the spot instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For non\-GPU instances, the notification about the upcoming instance release is sent 5 minutes in advance; for GPU instances, it is sent 1 hour in advance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can <a href="https://docs.byteplus.com/en/docs/ecs/Receiving-event-notifications#.6K6i6ZiF5LqL5Lu26YCa55-l">subscribe to event notifications </a>and receive instance release notifications via internal message, SMS, email, or other channels before your spot instance is interrupted.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Normally, the system starts releasing spot instances from the lowest bid. If multiple spot instances have the same bid price, the release order of the instances is determined randomly.   </div>
   


<span id="nOI63JRM"></span>
## Limits


* You can not change instance type.

* You can not change billing method.


<span id="2npVumCT"></span>
## Scenarios

Spot instances are suitable for stateless application scenarios. Examples include stateless web site services, image rendering, big data analysis, offline analysis, and large\-scale parallel computing and testing. The greater an application's distributed nature, scalability, and fault tolerance, the more effectively it can use spot instances to reduce costs and boost throughput.

You can deploy the following businesses on spot instances:


* Real\-time analysis

* Big data analysis

* Geospatial survey and analysis

* Image and media encoding

* Scientific computation

* Elastic and scalable business sites

* Testing


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid impacts on business operations by the interrupt reclamation mechanism, do not use spot instances for long\-term workloads or stateful applications with high stability requirements, such as databases. Preserving application state is challenging when a spot instance is released.</div>


<span id="3RhDQeMo"></span>
## Note

You can check whether a spot instance is in pending termination status through [viewing spot instance interruption event](https://docs.byteplus.com/en/docs/ecs/View_spot_instance_interruption_event). You can also save limited data during the termination grace period through [Best practices for data recovery when spot instances are reclaimed](https://docs.byteplus.com/en/docs/ecs/Data_Recovery_When_Spot_Instances_Are_Reclaimed_Best_Practices). But we still recommend that you upgrade application design and back up your data in advance. This makes sure that after the spot instance is reclaimed, applications can still work normally. Methods of data backup are as follows:


* Method 1: Create a snapshot to back up valid data in the volume. For specific operations, refer to [Creating a snapshot](https://docs.byteplus.com/en/docs/ecs/Create-a-snapshot).

* Method 2: Go to the [TOS console](https://console.byteplus.com/tos/bucket) to enable TOS service. Then upload files that need to be saved to the bucket. For detailed operations, refer to [Uploading files](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file).


<span id="p3EOZeIm"></span>
## Billing rules

Spot instance prices fluctuate in real time with market supply and demand. For specific billing rules, refer to [Spot instance](https://docs.byteplus.com/en/docs/ecs/Spot_Instance).

<span id="molth40q"></span>
## Usage guide


|Actions |Documentation |
|---|---|
|Purchasing spot instances |[Purchasing spot instances](https://docs.byteplus.com/en/docs/ecs/Buying_spot_instance) |
|Viewing interruption events for spot instances |[View interruption events of spot instance](https://docs.byteplus.com/en/docs/ecs/View_spot_instance_interruption_event) |
|Spot instance reclamation mechanism |[Reclaiming spot instances](https://docs.byteplus.com/en/docs/ecs/Reclaiming_spot_instance) |
|Restore data of the spot instance to be reclaimed |[Best practices for data recovery when a spot instance is reclaimed](https://docs.byteplus.com/en/docs/ecs/Data_Recovery_When_Spot_Instances_Are_Reclaimed_Best_Practices) |
|Stop spot instance |[Instance stopped](https://docs.byteplus.com/en/docs/ecs/Stopping-instances) |
|Delete spot instance |[Instance deletion](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances) |
|Query the historical prices, average interruption rate, discount rate, and other relevant information of spot instance over the last 30 days |* [DescribeSpotPriceHistory](https://docs.byteplus.com/en/docs/ecs/DescribeSpotPriceHistory)<br><br>* [DescribeSpotAdvice](https://docs.byteplus.com/en/docs/ecs/DescribeSpotAdvice) |


<span id="SaQeB5KJ"></span>
## FAQ

[Spot instance FAQs](https://docs.byteplus.com/en/docs/ecs/Instance-FAQs#.5oqi5Y2g5byP5a6e5L6L6Zeu6aKY).
