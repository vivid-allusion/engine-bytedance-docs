---
title: "Tag overview"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Tag_overview"
---

Tags identify and classify cloud resources. BytePlus Message Queue for RabbitMQ supports adding tags to instances. You can categorize RabbitMQ instances with tags to facilitate instance search and resource aggregation. This section introduces tag functions, usage instructions, and usage restrictions.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Function overview

As the number of cloud resources grows, management becomes more challenging. BytePlus provides tag management to customize identification and classification of cloud service resources from multiple dimensions. For example, it allows classification of cloud resources by different business types, purposes, or users. After binding resources with tags, you can quickly query and filter cloud resources by category using tags.

The message queue for RabbitMQ supports adding tags to instances, allowing instance\-level tag management. A tag is a key\-value pair. It consists of a tag key and a tag value. You can add multiple tags of different categories to each RabbitMQ instance, such as `module:http` or `city:Guangzhou`. Each tag can also be bound to multiple cloud resources. For example, assigning the same tag `owner: Zhang San` to two RabbitMQ instances.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

Recommended use of the tag management feature in the following scenarios:


* Cloud resource classification management

   When managing a large number of cloud resources, it is difficult to manage and identify resources only by instance names. You can classify RabbitMQ instances according to business scenarios and assign the same tags to instances within the same scenario. After setting tags, you can quickly filter instances by specifying tag keys and values.

* Billing and cost allocation

   If you need to allocate costs based on different organizations or departments, use tags to classify cloud resources. Assign identical tags to cloud resources of the same organization or department. Allocate costs to the corresponding entities during periodic billing and enable cost allocation management.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You can add multiple different categories of tags to each RabbitMQ instance, but each tag can have only one value per instance. For example, when adding the tag module to RabbitMQ instance A, if the tag `module:http` has already been added, you must delete the `module:http` tag before adding the `module:tcp` tag.

* Tag information is not shared across different regions. For example, tags created in the North China 2 (Beijing) region are not visible in the East China 2 (Shanghai) region.

* There is no limit to the total number of tags, but each RabbitMQ instance can bind up to 50 tags. For detailed tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/rabbitmq/Bind_tags#.5qCH562-6K6-572u6KeE5YiZ).


<span id=".56S65L6L"></span>
## Example

For example, a company purchases 5 RabbitMQ instances on BytePlus, which are used respectively for payment, shopping cart, and points business modules. The instances are used to serve users in Beijing, Guangzhou, and Shanghai and are maintained by Zhang San, Li Ming, and Han Meimei. To facilitate instance management, instances can be categorized using tags.

In this scenario, the following tags can be designed:


|Tag key |Tag value |
|---|---|
|system |pay、shoppingcart、integral |
|city |Beijing, Guangzhou, Shanghai |
|owner |Zhang San, Li Ming, Han Meimei |


In this scenario, corresponding tags can be set for each instance:


|Instance name |Instance tags |
|---|---|
|RabbitMQ instance A |* system：pay<br><br>* city: Beijing<br><br>* owner: Zhang San |
|RabbitMQ instance B |* system：pay<br><br>* city: Guangzhou<br><br>* owner: Li Ming |
|RabbitMQ instance C |* system：shoppingcart<br><br>* city: Beijing<br><br>* owner: Li Ming |
|RabbitMQ instance D |* system：shoppingcart<br><br>* city: Shanghai<br><br>* owner: Han Meimei |
|RabbitMQ instance E |* system：integral<br><br>* city: Beijing<br><br>* owner: Han Meimei |
