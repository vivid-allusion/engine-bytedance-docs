---
title: "Tag overview"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Tag_overview"
---

Tags can be used to identify cloud resources, helping you label and classify similar instances based on different criteria (such as usage, type, owner and environment), making it easier to filter and manage the tags.

<span id=".5Yqf6IO95qaC6L-w"></span>
## Overview of features

As the number of resources on the cloud continues to increase, tag management becomes more difficult. BytePlus offers tag management features for custom labeling and categorization\-based management of cloud service resources employing different criteria. For example, tags can be used to classify and manage cloud resources by business category, usage or object. After associating tags with resources, users can use tags to quickly query and filter cloud resources of a specified category.

NDB for MySQL supports adding tags for instances, which enables tag management at the instance level. A tag is a key\-value pair, consisting of a tag key and a tag value. You can add multiple different categories of tags, such as `department:game` and `region:beijing`, to each instance. Each tag can also be associated with multiple instances, for example, by setting the same tag `owner:Alice` for multiple instances at once.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios

We recommend using the tag management feature in the following scenarios.


* **Classification\-based management of cloud resources**

   When there are a substantial amount of cloud resources, it is difficult to manage and identify the resources solely through instance names. You can classify instances based on service scenarios and set the same tags for instances belonging to the same business scenario. After setting the tags, you can quickly filter instances by specifying the tag keys and tag values.

* **Billing and cost allocation**

   If you need to allocate costs according to different organizations or departments in a business scenario, cloud resources can be classified and managed through tags. For cloud resources belonging to the same organization or department, set the same tags for them, and allocate the cloud resource costs to the corresponding organization or department upon regular settlement.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* You can add multiple tags of different categories for each instance. Each tag key must be unique for an instance, and can have only one tag value. For example, when adding tags to instance A, if the tag `Owner:Alice` has already been added, the tag `Owner:Bob` can be added only after `Owner:Alice` is deleted.

* Tag information between different regions is not interoperable. For example, tags created in the Asia Pacific (Johor) region are not visible in the China (Shanghai) region.


<span id=".5qCH562-6K6-572u6KeE5YiZ"></span>
## Tag setting rules


|Limit item |Description |
|---|---|
|Tag key |* Letters of any alphabetic language (such as English) or characters (such as Chinese), digits, spaces and the following special characters are supported: `_.:/=+-@`<br><br>* `volc:` Is a tag key reserved for the system. When adding a tag, you cannot start a tag key with `volc:` in any case.<br><br>* The length of a tag key should be 1 to 128 characters. |
|Tag value |* Letters of any alphabetic language (such as English) or characters (such as Chinese), digits, spaces and the following special characters are supported: `_.:/=+-@`<br><br>* The length of a tag value should be 0 to 256 characters, meaning that tag values can be empty. |
|Count |* There is no limit on the total number of tags, but up to 50 tags can be associated per instance.<br><br>* You can add up to 20 tags per at a time. |


<span id=".5L2_55So56S65L6L"></span>
## Examples

For example, a company purchases 5 instances from BytePlus, and the instances are used respectively by the gaming, e\-commerce and IoT business departments to serve users in Johor, Guangzhou and Shanghai. Three people Alice, Bob, and Carol are responsible for maintaining these instances. The instances can be classified by tag for easy management, in which case the tag key values can be designed as follows.


|Tag key |Tag value |
|---|---|
|department |game、e\-commerce、iot |
|region |beijing、shanghai |
|owner |Alice、Bob、Carol |


In this scenario, you can set corresponding tags for each instance:


|Instance name |Instance tag |
|---|---|
|Instance A |* `department：game`<br><br>* `city：beijing`<br><br>* `owner：Alice` |
|Instance B |* `department：game`<br><br>* `city：shanghai`<br><br>* `owner：Bob` |
|Instance C |* `department：e-commerce`<br><br>* `city：beijing`<br><br>* `owner：Bob` |
|Instance D |* `department：e-commerce`<br><br>* `city：shanghai`<br><br>* `owner：Carol` |
|Instance E |* `department：iot`<br><br>* `city：beijing`<br><br>* `owner：Carol` |
