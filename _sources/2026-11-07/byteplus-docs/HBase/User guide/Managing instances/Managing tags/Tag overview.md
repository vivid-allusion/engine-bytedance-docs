---
title: "Tag overview"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Tag_overview"
---

Tags are used to identify cloud resources. They help you label and categorize Table Storage for HBase instances with similar characteristics from different dimensions, such as purpose, type, owner, and environment, which facilitates filtering and management.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Overview

As the number of cloud resources grows, managing them becomes increasingly difficult. BytePlus provides a tag management feature, which allows you to define custom identifiers and categorize cloud service resources from various dimensions. For example, you can use tags to categorize cloud resources by business category, purpose, or user. Once you bind tags to resources, you can quickly filter for specific categories of resources. Table Storage for HBase supports adding tags to instances, enabling instance\-level tag management. A tag is a key\-value pair (Key\-Value) that consists of a tag key and a tag value. You can add multiple different tags to each HBase instance, such as `department:game` and `region:beijing`. You can also add the same tag to multiple instances, such as adding the tag `owner:Alice` to multiple HBase instances in a batch.

<span id=".5bqU55So5Zy65pmv"></span>
## Use cases

Tag management is recommended for the following scenarios.


* **Categorical Management of Cloud Resources**

   When you have a large number of cloud resources, it can be difficult to manage and identify them using only instance names. You can categorize HBase instances based on your business scenarios and assign the same tags to instances within the same scenario. Once the tags are set, you can quickly filter for instances using specific tag keys and values.

* **Billing and Cost Allocation**

   If you need to allocate costs across different organizations or departments, you can categorize your cloud resources using tags. Assign the same tag to all resources belonging to the same organization or department. This enables you to allocate costs to the corresponding group during periodic billing and effectively manage cost allocation.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* You can add multiple tags to each HBase instance, but each tag key for a given instance must be unique and can only have one value. For example, if you want to add the tag `owner:Bob` to an HBase instance that already has the tag `owner:Alice`, you must first delete the `owner:Alice` tag.

* Tag information is not shared between different regions. For example, tags created in the North China 2 (Beijing) region are not visible in the East China 2 (Shanghai) region.


<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tagging Rules


|Restrictions |Description |
|---|---|
|Tag key |* Supports language characters (e.g., Chinese and English), numbers, spaces, and English symbols `_.:/=+-@`.<br><br>* `volc:` is a system\-reserved tag key. A tag key cannot begin with `volc:`, regardless of case.<br><br>* The tag key must be 1 to 128 characters long. |
|Tag value |* Supports language characters (e.g., Chinese and English), numbers, spaces, and English symbols `_.:/=+-@`.<br><br>* The tag value can be empty or up to 256 characters long. |
|Number of tags |* There is no limit on the total number of tags, but each HBase instance supports a maximum of 50 tags.<br><br>* A maximum of 20 tags can be added per operation. |


<span id=".5L2_55So56S65L6L"></span>
## Example

For example, a company has purchased five HBase instances on BytePlus for its gaming, e\-commerce, and IoT business units. These instances serve users in Beijing and Shanghai and are maintained by Alice, Bob, and Carol. To facilitate management, you can use tags to categorize the instances. In this scenario, you can design the following tag key\-value pairs.


|Tag key |Tag value |
|---|---|
|department |game、e\-commerce、iot |
|region |beijing、shanghai |
|owner |Alice、Bob、Carol |


In this scenario, you can assign the following tags to each instance:


|Instance name |Instance tag |
|---|---|
|HBase instance A |* `department：game`<br><br>* `city：beijing`<br><br>* `owner：Alice` |
|HBase instance B |* `department：game`<br><br>* `city：shanghai`<br><br>* `owner：Bob` |
|HBase Instance C |* `department：e-commerce`<br><br>* `city：beijing`<br><br>* `owner：Bob` |
|HBase instance D |* `department：e-commerce`<br><br>* `city：shanghai`<br><br>* `owner：Carol` |
|HBase instance E |* `department：iot`<br><br>* `city：beijing`<br><br>* `owner：Carol` |
