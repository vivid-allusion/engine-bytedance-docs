---
title: "Tag overview"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/tag-overview"
---

Tags are used to identify and categorize cloud resources. Message Queue for Kafka allows you to add tags to instances. You can classify Kafka instances by tag for simplified instance search and resource aggregation. This topic describes the tag feature, usage guidelines, and limits.

<span id="功能概述"></span>
## Feature overview

With the continuous increase in the number of cloud resources, managing them becomes increasingly complex. With the tag management feature offered by BytePlus, you can identify and classify cloud service resources across various dimensions. For example, use tags to classify and manage cloud resources based on different business types, uses, or user groups. After tagging resources, you can query and filter the specific category of cloud resources by tag.

Message Queue for Kafka allows you to add tags to instances, meaning that it supports tag management at the instance level. A tag consists of a key\-value pair, including a tag key and a tag value. You can add multiple tags of different categories to each Kafka instance, such as `module:http` and `city: guangzhou`. A single tag can be associated with multiple cloud resources, For example, you can add the same tag `owner: zhangsan` to two Kafka instances.

<span id="应用场景"></span>
## Use scenarios

We recommend that you use the tag management feature in the following scenarios:


* Management and classification of cloud resources. With a vast number of cloud resources, managing and identifying them solely by instance name can be challenging. You can categorize Kafka instances based on business scenarios and add the same tags to instances in the same scenario. Once added, you can filter instances by specifying a tag key and a tag value.

* Billing and cost sharing. If business scenarios require cost allocation among different organizations or departments, you can use tags to classify and manage cloud resources. Add the same tags to cloud resources in the same organization or department. This way, during regular settlements, cloud resource costs can be apportioned to the respective organization or department for cost sharing management.


<span id="注意事项"></span>
## Precautions


* You can add multiple tags of different categories to each Kafka instance, but each tag of an instance can only have one tag value. For example, when adding the tag module to Kafka instance A, if the tag `module:http` has already been added, the `module:http` tag must be deleted before you add the `module:tcp` tag.

* Tag information is isolated among different Regions. For example, tags created in the China (Beijing) Region are invisible in the China (Shanghai) Region.

* The total number of tags is unlimited, but each Kafka instance can be associated with a maximum of 50 tags. For detailed rules on setting tags, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/kafka/associating-with-tags#tag-setting-rules).


<span id="示例"></span>
## Example

For example, a company buys five Message Queue for Kafka instances for its payment, shopping cart, and loyalty points business modules. These instances serve users in Beijing, Guangzhou, and Shanghai and are maintained by Zac, Mark, and Mae. To simplify instance management, classify instances by tag.

In this scenario, set the following tags:


|**Tag Key** |**Tag Value** |
|---|---|
|system |pay, shoppingcart, integral |
|city |Beijing, Guangzhou, Shanghai |
|owner |Zac, Mark, and Mae |


In this scenario, set the following tags for each instance:


|**Instance Name** |**Instance Tag** |
|---|---|
|Kafka instance A |system: pay<br><br>city: Beijing<br><br>owner: Zac |
|Kafka instance B |system: pay<br><br>city: Guangzhou<br><br>owner: Mark |
|Kafka instance C |system: shoppingcart<br><br>city: Beijing<br><br>owner: Mark |
|Kafka instance D |system: shoppingcart<br><br>city: Shanghai<br><br>owner: Mae |
|Kafka instance E |system: integral<br><br>city: Beijing<br><br>owner: Mae |
