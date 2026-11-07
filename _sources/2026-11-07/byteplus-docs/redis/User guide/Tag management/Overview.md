---
title: "Overview"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/tag-overview"
---

Cache for Redis supports tag management. Tags can be used to identify cloud resources, helping you label and classify similar instances based on different criteria (such as usage, type, owner and environment), making it easier to filter and manage the tags.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

As the number of resources on the cloud continues to increase, tag management becomes more difficult. BytePlus offers tag management features for custom labeling and categorization\-based management of cloud service resources employing different criteria. For example, tags can be used to classify and manage cloud resources by business category, usage or object. After associating tags with resources, users can use tags to quickly query and filter cloud resources of a specified category.

Cache for Redis supports adding tags for instances, which enables tag management at the instance level. A tag is a key\-value pair, consisting of a tag key and a tag value. You can add multiple tags of different categories to each Redis instance, such as `department:game`, `region:beijing` and so on. Each tag can also be associated with multiple instances, for example, by setting the same tag `owner:Alice` for multiple Redis instances at once.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

We recommend using the tag management feature in the following scenarios.


* **Classifying cloud resources**

   When there is a large number of cloud resources, managing and identifying them solely by instance name can be difficult. You can classify Redis instances based on service scenarios and set the same tags for instances belonging to the same business scenario. After setting the tags, you can quickly filter instances by specifying the tag keys and tag values.

* **Billing and cost allocation**

   If you need to allocate costs by organization or department, you can use tags to manage your cloud resources. Assign the same tags to resources from the same organization or department. This allows you to allocate costs to the corresponding group during regular settlement and manage cost allocation.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can add multiple tags of different categories for each Redis instance. Each tag key must be unique for instance, and can have only one tag value.

   For example, when adding tags to Redis instance A, if the tag `Owner:Alice` has already been added, you must first delete `Owner:Alice` before adding `Owner:Bob`.

* Tag information is not shared between different regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region.

* The total number of tags is unlimited, but each Redis instance can associate up to 50 tags. For detailed tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/redis/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).

* The tag feature of Cache for Redis has been integrated into the BytePlus cloud resource management system, supporting direct tag management on the resource management console.


<span id=".5L2_55So56S65L6L"></span>
## Usage example

For example, a company purchases 5 Redis instances for Cache for Redis from BytePlus, and the instances are used respectively by the gaming, e\-commerce and IoT business departments to serve users in Johor, Guangzhou and Shanghai. Three people Alice, Bob, and Carol are responsible for maintaining these instances. For easier management, instances can be categorized using tags. In this scenario, the following tag key\-values can be designed.


|Tag key |Tag value |
|---|---|
|department |game, e\-commerce, iot |
|region |beijing, guangzhou, shanghai |
|owner |Alice, Bob, Carol |


In this scenario, you can set corresponding tags for each instance as follows.


|Instance name |Instance tag |
|---|---|
|Redis instance A |* `department: game`<br><br>* `city: beijing`<br><br>* `owner: Alice` |
|Redis instance B |* `department: game`<br><br>* `city: guangzhou`<br><br>* `owner: Bob` |
|Redis instance C |* `department: e-commerce`<br><br>* `city: beijing`<br><br>* `owner: Bob` |
|Redis instance D |* `department: e-commerce`<br><br>* `city: shanghai`<br><br>* `owner: Carol` |
|Redis instance E |* `department: iot`<br><br>* `city: beijing`<br><br>* `owner: Carol` |


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documentations


* [Associating or adding tag](https://docs.byteplus.com/en/docs/redis/associate-tag)

* [Filtering instances by tag](https://docs.byteplus.com/en/docs/redis/filter-by-tag)

* [Disassociating or deleting tag](https://docs.byteplus.com/en/docs/redis/disassociate-tag)
