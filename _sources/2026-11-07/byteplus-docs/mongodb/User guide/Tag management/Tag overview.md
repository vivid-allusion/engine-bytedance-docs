---
title: "Tag overview"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/tag-overview"
---

Document Database for MongoDB supports tag management. Tags can be used to identify cloud resources, helping you label and classify similar instances based on different criteria (such as usage, type, owner and environment), making it easier to filter and manage the tags.

<span id=".5Yqf6IO95LuL57uN"></span>
## Feature introduction

As the number of resources on the cloud continues to increase, tag management becomes more difficult. BytePlus offers tag management features for custom labeling and categorization\-based management of cloud service resources employing different criteria. For example, tags can be used to classify and manage cloud resources by business category, usage or object. After associating tags with resources, users can use tags to quickly query and filter cloud resources of a specified category.

Document Database for MongoDB supports adding tags for instances, which enables tag management at the instance level. A tag is a key\-value pair, consisting of a tag key and a tag value. You can add multiple tags of different categories to each MongoDB instance, such as `instancetype:shard`, `region:beijing` and so on. Each tag can also be associated with multiple instances, for example, by setting the same tag `owner:Alice` for multiple MongoDB instances at once.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

We recommend using the tag management feature in the following scenarios.


* **Classifying cloud resources**

   When there is a large number of cloud resources, managing and identifying them solely by instance name can be difficult. You can classify MongoDB instances based on service scenarios and set the same tags for instances belonging to the same business scenario. After setting the tags, you can quickly filter instances by specifying the tag keys and tag values.

* **Billing and cost allocation**

   If you need to allocate costs by organization or department, you can use tags to manage your cloud resources. Assign the same tags to resources from the same organization or department. This allows you to allocate costs to the corresponding group during regular settlement and manage cost allocation.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can add multiple tags of different categories for each MongoDB instance. Each tag key must be unique for instance, and can have only one tag value.

   For example, when adding tag `instancetype` to MongoDB instance A, if the tag `instancetype:shard` has already been added, you must first delete `instancetype:shard` before adding `instancetype:replica`.

* Tag information is not shared between different regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region.

* The total number of tags is unlimited, but each MongoDB instance can associate up to 50 tags. For the tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/mongodb/associate-tag#.5qCH562-6K6-572u6KeE5YiZ).


<span id=".5L2_55So56S65L6L"></span>
## Usage example

For example, a company purchases 5 MongoDB instances from BytePlus, and the instances are used respectively by the gaming, e\-commerce and IoT business departments to serve users in Johor, Guangzhou and Shanghai. Three people Alice, Bob, and Carol are responsible for maintaining these instances. For easier management, instances can be categorized using tags. In this scenario, the following tag key\-values can be designed.


|Tag key |Tag value |
|---|---|
|department |game, e\-commerce, iot |
|region |beijing, guangzhou, shanghai |
|owner |Alice, Bob, Carol |


In this scenario, you can set corresponding tags for each instance.


|Instance name |Instance tag |
|---|---|
|MongoDB instance A |* `department:game`<br><br>* `region:beijing`<br><br>* `owner:Alice` |
|MongoDB instance B |* `department:game`<br><br>* `region:guangzhou`<br><br>* `owner:Bob` |
|MongoDB instance C |* `department:e-commerce`<br><br>* `region:beijing`<br><br>* `owner:Bob` |
|MongoDB instance D |* `department:e-commerce`<br><br>* `region:shanghai`<br><br>* `owner:Carol` |
|MongoDB instance E |* `department:iot`<br><br>* `region:beijing`<br><br>* `owner:Carol` |


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents


* [Associating tag](https://docs.byteplus.com/en/docs/mongodb/associate-tag)

* [Filtering instances by tag](https://docs.byteplus.com/en/docs/mongodb/filter-by-tag)

* [Disassociating or deleting tag](https://docs.byteplus.com/en/docs/mongodb/disassociate-tag)
