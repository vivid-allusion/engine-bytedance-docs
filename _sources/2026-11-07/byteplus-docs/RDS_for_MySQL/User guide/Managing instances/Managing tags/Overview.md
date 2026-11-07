---
title: "Overview"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_2"
---

Tags are used for identifying and categorizing cloud resources. RDS for MySQL supports adding tags to instances for classification, retrieval, and aggregation. This topic introduces the functional concepts, application scenarios, and precautions of tags.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Function overview

As the number of cloud resources continues to grow, management complexity increases. BytePlus provides tag management features for custom identification and categorized management of cloud service resources from various dimensions. For example, you can categorize cloud resources by different business types, uses, or users through tags. After binding tags to resources, you can quickly query and filter cloud resources of a specified category by tags.

RDS for MySQL supports adding tags at the instance level, which means it supports tag management on an instance dimension. A tag is a key\-value pair, consisting of a tag key and a tag value. You can add multiple tags of different categories to each MySQL instance, such as `module:http` and `city:guangzhou`. Each tag can also be bound to multiple cloud resources, such as setting the same tag `owner:zhangsan` for two MySQL instances.

<span id=".5qCH562-5YiG57G7"></span>
### Tag categories

Tags can be divided into two categories: system tags and custom tags.

<span id=".57O757uf5qCH562-"></span>
#### System tag

System tags are preset by the system for cloud resources. They generally start with `volc:` to help you manage resources more easily. Current system tags can only be viewed and cannot be used. The system tag for RDS for MySQL is `volc:rds_mysql:linkedresource`.

<span id=".6Ieq5a6a5LmJ5qCH562-"></span>
#### Custom tags

Custom tags are tags that users add to resources. You can perform operations such as associating and removing them. You cannot add custom tags that start with `volc:` in any letter case.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

Tag management is recommended for the following scenarios:


* **Classifying cloud resources**

   Managing resources only by instance name is difficult when the number of cloud resources is large. You can classify MySQL instances based on business scenarios and assign the same tags to instances in the same business scenario. After setting the tags, you can quickly filter instances by specifying the tag keys and tag values.

* **Access control for cloud resources**

   IAM access control supports tag\-based authorization. By assigning permissions to different tags, you can grant different IAM users access and operation privileges for different types of cloud resources.

* **Billing and cost allocation**

   If you need to allocate costs by organization or department, you can use tags to manage your cloud resources. Assign the same tags to resources from the same organization or department. This allows you to allocate costs to the corresponding group during regular settlement and manage cost allocation.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can add multiple tags from different categories to each MySQL instance, but each tag for an instance can only have one value. For example, when you add the module tag to MySQL instance A, if you have already added the tag `module:http`, adding the `module:tcp` tag later will overwrite the `module:http` tag.

* Tag information is not shared between different regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region.

* The total number of tags is unlimited, but you can bind up to 50 tags to each MySQL instance. For detailed tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ).


<span id=".56S65L6L"></span>
## Example

For example, a company purchased 5 RDS for MySQL instances on Volcengine, used for payment, shopping cart, and points business modules, serving Users in Beijing, Guangzhou, and Shanghai, maintained by Zhang San, Li Ming, and Han Meimei. To facilitate instance management, you can classify instances by binding tags.

In this scenario, the following tags can be designed.


|Tag key |Tag value |
|---|---|
|system |pay、shoppingcart、integral |
|city |beijing, guangzhou, shanghai |
|owner |zhangsan、liming、hanmeimei |


In this scenario, you can set corresponding tags for each instance.


|Instance name |Instance tag |
|---|---|
|MySQL instance A |* system：pay<br><br>* city: beijing<br><br>* owner：zhangsan |
|MySQL instance B |* system：pay<br><br>* city: guangzhou<br><br>* owner：liming |
|MySQL instance C |* system：shoppingcart<br><br>* city: beijing<br><br>* owner：liming |
|MySQL instance D |* system：shoppingcart<br><br>* city: shanghai<br><br>* owner：hanmeimei |
|MySQL instance E |* system：integral<br><br>* city: beijing<br><br>* owner：hanmeimei |


<span id=".55u45YWz5paH5qGj"></span>
## Relevant documents


* [Adding a tag](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_a_tag)

* [Editing tag](https://docs.byteplus.com/en/docs/RDS_for_MySQL/editing_a_tag)

* [Disassociating a tag](https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_a_tag)

* [Filtering instances by tags](https://docs.byteplus.com/en/docs/RDS_for_MySQL/filtering_instances_by_tags)

* [Tag-based bill splitting for instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/tag-based_bill_splitting_for_instances)
