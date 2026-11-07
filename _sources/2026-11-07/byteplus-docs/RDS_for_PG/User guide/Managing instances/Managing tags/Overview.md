---
title: "Overview"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/overview"
---

Tags are used for identifying and categorizing cloud resources. RDS for PostgreSQL supports adding tags to instances for instance classification, retrieval, and aggregation. This topic introduces the functional concepts, application scenarios, and precautions of tags.

<span id=".5Yqf6IO95qaC6L-w"></span>
## **Function overview**

As the number of cloud resources continues to grow, management complexity increases. BytePlus provides tag management features for custom identification and categorized management of cloud service resources from various dimensions. For example, you can categorize cloud resources by different business types, uses, or users through tags. After binding tags to resources, you can quickly query and filter cloud resources of a specified category by tags. RDS for PostgreSQL supports adding tags to instances, enabling instance\-level tag management. A tag is a key\-value pair consisting of one tag key and one tag value. You can add multiple tags of different categories to each PostgreSQL instance, for example, `module:http`, `city:guangzhou`, and so on. Each tag can also be bound to multiple cloud resources, such as setting the same tag `owner:zhangsan` for two PostgreSQL instances.

<span id=".5bqU55So5Zy65pmv"></span>
## **Application scenarios**

Tag management is recommended for the following scenarios:


* **Cloud resource classification** Managing resources only by instance name is difficult when the number of cloud resources is large. You can classify instances based on business scenarios and assign the same tag to instances within the same business scenario. Once set, you can quickly filter instances by specifying tag keys and tag values.

* **Cloud resource access control** IAM access control service supports authorization and authentication at the tag level. By authorizing different tags, you can grant different IAM users access and operation permissions for different categories of cloud resources.

* **Billing and cost allocation** If your business requires cost allocation by organization or department, you can classify cloud resources using tags. Assign the same tag to resources under the same organization or department, and allocate cloud resource costs to the corresponding entity during periodic billing to achieve cost sharing management.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* You can add multiple tags of different categories to each instance, but an instance can only have one tag value per tag key. For example, when adding a tag module to instance A, if the tag `module:http` already exists, adding the `module:tcp` tag will overwrite the `module:http` tag.

* Tag information is not shared across different regions. For example, tags created in Huabei 2 (Beijing) are not visible in Huadong 2 (Shanghai).

* The total number of tags is unlimited, but each instance can bind up to 50 tags. For detailed tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag#.5qCH562-6K6-572u6KeE5YiZ).


<span id=".56S65L6L"></span>
## **Example**

For example, a company purchased 5 RDS for PostgreSQL instances on Volcengine, used for payment, shopping cart, and points business modules, serving Users in Beijing, Guangzhou, and Shanghai, maintained by Zhang San, Li Ming, and Han Meimei. To facilitate instance management, you can classify instances by binding tags. In this scenario, the following tags can be designed.


|Tag key |Tag value |
|---|---|
|system |pay、shoppingcart、integral |
|city |beijing、guangzhou、shanghai |
|owner |zhangsan、liming、hanmeimei |


In this scenario, you can set corresponding tags for each instance.


|Instance name |Instance tag |
|---|---|
|PostgreSQL instance A |system：pay<br><br>city：beijing<br><br>owner：zhangsan |
|PostgreSQL instance B |system：pay<br><br>city：guangzhou<br><br>owner：liming |
|PostgreSQL instance C |system：shopping<br><br>cartcity：beijing<br><br>owner：liming |
|PostgreSQL instance D |system：shoppingcart<br><br>city：shanghai<br><br>owner：hanmeimei |
|PostgreSQL instance E |system：integral<br><br>city：beijing<br><br>owner：hanmeimei |


<span id=".55u45YWz5paH5qGj"></span>
## **Related documents**


* [Adding a tag](https://docs.byteplus.com/en/docs/RDS_for_PG/associating_a_tag)

* [Editing a tag](https://docs.byteplus.com/en/docs/RDS_for_PG/editing_a_tag)

* [Disassociating a tag](https://docs.byteplus.com/en/docs/RDS_for_PG/disassociating_a_tag)

* [Filtering instances by tags](https://docs.byteplus.com/en/docs/RDS_for_PG/filtering_instances_by_tags)

* [Tag-based bill splitting for instances](https://docs.byteplus.com/en/docs/RDS_for_PG/tag-based_bill_splitting_for_instances)
