---
title: "Tag overview"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Tag_overview"
---

Tags are used for identifying and categorizing cloud resources. AI Native Database Platform supports adding tags to workspaces for classifying, searching, and aggregating. This topic introduces the functional concepts, application scenarios, and precautions of tags.

<span id="iS6rjk4i"></span>
## Function overview

As the number of cloud resources continues to grow, management complexity increases. BytePlus provides tag management features for custom identification and categorized management of cloud service resources from various dimensions. For example, you can categorize cloud resources by different business types, uses, or users through tags. After binding tags to resources, you can quickly query and filter cloud resources of a specified category by tags.

AI Native Database Platform supports adding tags to workspaces, enabling tag management at the workspace level. A tag is a key\-value pair consisting of one tag key and one tag value. You can add multiple tags of different categories to each workspace, such as module:http and city:guangzhou. Each tag can also be bound to multiple cloud resources, such as setting the same tag owner:zhangsan for two workspaces.

<span id="Ioc2vM29"></span>
### Tag categories

Tags can be divided into two categories: system tags and custom tags.

<span id="cHtxBXZ8"></span>
#### System tag

System tags are preset by the system for cloud resources. They generally start with volc: to help you manage resources more easily. Current system tags can only be viewed and cannot be used.

<span id="RHTJVgcl"></span>
#### Custom tags

Custom tags are tags that users add to resources. You can perform operations such as associating and removing them. You cannot add custom tags that start with `volc:` in any letter case.

<span id="m2y3HCKh"></span>
## Application scenarios

Tag management is recommended for the following scenarios:


* **Cloud resource classification**


Managing resources only by workspace name becomes difficult when the number of cloud resources is large. You can classify workspaces based on business scenarios and assign the same tags to workspaces with the same business scenario. After setting, you can quickly filter workspaces by specified tag keys and values.


* **Cloud resource access control**


IAM access control supports tag\-based authorization. By assigning permissions to different tags, you can grant different IAM users access and operation privileges for different types of cloud resources.


* **Billing and cost allocation**


If you need to allocate costs by organization or department, you can use tags to manage your cloud resources. Assign the same tags to resources from the same organization or department. This allows you to allocate costs to the corresponding group during regular settlement and manage cost allocation.

<span id="3xNzuuzg"></span>
## Precautions


* You can add multiple tags of different categories to each workspace, but a workspace can have only one tag value per tag. For example, when adding a tag module to workspace A, if the tag module:http already exists, adding the module:tcp tag will overwrite the module:http tag.

* Tag information is not shared across different regions. For example, tags created in China (Beijing) are not visible in China (Shanghai).

* The total tag quantity is unlimited, but each workspace can add up to 50 tags. For detailed tag setting rules, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Adding_a_tag#75qtosde).


<span id="6WNZmNQp"></span>
## Example

For example, a company purchased five AI Native Database Platform workspaces from Volcengine, used respectively for payment, shopping cart, and points business modules, serving users in Beijing, Guangzhou, and Shanghai, maintained by Zhang San, Li Ming, and Han Meimei. To facilitate managing workspaces, tagging can be used to classify workspaces.

In this scenario, the following tags can be designed.


|Tag key |Tag value |
|---|---|
|system |pay, shoppingcart, integral |
|city |beijing, guangzhou, shanghai |
|owner |zhangsan, liming, hanmeimei |


Tags can be configured for each workspace in this scenario.


|Name |Workspace tag |
|---|---|
|Workspace A |* system: pay<br><br>* city: beijing<br><br>* owner: zhangsan |
|Workspace B |* system: pay<br><br>* city: guangzhou<br><br>* owner: liming |
|Workspace C |* system: shoppingcart<br><br>* city: beijing<br><br>* owner: liming |
|Workspace D |* system: shoppingcart<br><br>* city: shanghai<br><br>* owner: hanmeimei |
|Workspace E |* system: integral<br><br>* city: beijing<br><br>* owner: hanmeimei |
