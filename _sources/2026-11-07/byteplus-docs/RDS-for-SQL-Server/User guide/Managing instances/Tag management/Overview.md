---
title: "Overview"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/tag-overview"
---

Labels are used to identify and classify cloud resources. RDS for SQL Server supports adding labels to instances and classifying them through labels for easy instance search and resource aggregation. This article introduces the function concept, application scenarios and precautions of tags.

<span id="feature-overview"></span>
## Feature Overview

As the number of resources on the cloud continues to grow, so does the difficulty of managing them. The Byteplus provides tag management capabilities for custom identification and classification management of Cloud as a Service resources from various dimensions, such as classifying and managing cloud resources of different business categories, uses, or use objects through tags. After binding tags to resources, you can quickly query and filter out cloud resources of the specified category through tags.

RDS for SQL Server supports adding labels to instances, that is, label management for instance dimensions. A label is a key\-value pair, including a label key and a label value. You can add multiple labels of different categories for each instance of SQL Server, such as `module: http`, `city: guangzhou`, etc. Each tag can also bind multiple cloud resources, such as setting the same tag `owner: zhangsan` for two SQL Server instances.

<span id="application-scenario"></span>
## application scenario

It is recommended to use the label management function in the following scenarios:


* Classified management of cloud resources, when the number of cloud resources is large, it is difficult to manage and identify resources only by instance names. You can categorize SQL Server instances according to business scenarios and set the same labels for instances of the same business scenario. After the setup is complete, you can quickly filter the instance by specifying the label key with the label value.

* Access control of cloud resources The IAM access control service supports authorization and authentication in the label dimension. By authorizing different labels, you can grant different IAM users access and operation rights to different categories of cloud resources.

* Billing and cost allocation, if there is a need for cost allocation according to different organizations or departments in a business scenario, cloud resources can be classified and managed through labels, and the same labels can be set for cloud resources of the same organization or department. Cloud resource costs are allocated to corresponding organizations or departments during regular settlement to achieve cost allocation management.


<span id="precautions"></span>
## Precautions


* You can add multiple labels of different categories for each SQL Server instance, but only one label value can be set for each label of an instance. For example, when you add the tag module to SQL Server instance A, if you have already added the tag `module: http`, and then add the `module: tcp` tag, it will overwrite the `module: http` tag.

* Label information between different regions is not interoperable. For example, tags created in the North China 2 (Beijing) region are not visible in the East China 2 (Shanghai) region.

* The total number of tags is unlimited, but each SQL Server instance can bind up to 50 tags. For detailed label setting rules, please refer to the [label setting rules](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-tag).


<span id="example"></span>
## example

For example, a company purchased five cloud database SQL Server instances in Byteplus, which were used for payment, shopping cart, and points business modules, respectively. They served users in Beijing, Guangzhou, and Shanghai, and were maintained by Zhang San, Li Ming, and Han Meimei. To make it easier to manage instances, instance classification can be done by tagging.

In this scenario, the following labels can be designed:


|Label key |label value |
|---|---|
|system |pay、shoppingcart、integral |
|city |beijing、guangzhou、shanghai |
|owner |zhangsan、liming、hanmeimei |


In this scenario, a corresponding label can be set for each instance:


|instance name |instance tag |
|---|---|
|SQL Server Instance A |* system：pay<br><br>* city：beijing<br><br>* owner：zhangsan |
|SQL Server Instance B |* system：pay<br><br>* city：guangzhou<br><br>* owner：liming |
|SQL Server Instance C |* system：shoppingcart<br><br>* city：beijing<br><br>* owner：liming |
|SQL Server Instance D |* system：shoppingcart<br><br>* city：shanghai<br><br>* owner：hanmeimei |
|SQL Server Instance E |* system：integral<br><br>* city：beijing<br><br>* owner：hanmeimei |
