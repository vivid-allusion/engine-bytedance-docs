---
title: "Overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Overview1"
---

FileNAS supports tag management function. Tags can be used to identify cloud resources and help you tag and categorize instances with the same characteristics from different dimensions, such as usage, type, owner, environment, etc., facilitating filtering and management.

<span id=".5Yqf6IO95LuL57uN"></span>
## Function Introduction

With the continuous growth of cloud resources, the difficulty of management also increases. Byteplus provides a tag management feature for custom identification and classification management of cloud service resources from various dimensions. For example, different business categories, purposes, or user\-specific cloud resources can be classified and managed through tags. After binding tags to resources, you can quickly query and filter cloud resources of specific categories through tags. FileNAS supports adding tags to instances, which means it supports tag management at the instance level. A tag consists of a key\-value pair, including a tag key and a tag value. You can add multiple tags of different categories to each FileNAS instance, such as`StoreType:100`, `region:ap-southeast-1`, etc. Each tag can also be associated with multiple instances, for example, setting the same tag `owner:Alice`for a batch of FileNAS instances.

<span id=".5bqU55So5Zy65pmv"></span>
## Application Scenarios

Recommended to use the tag management function in the following scenarios.


* **Classification management of cloud resources**:When the number of cloud resources is large, it is difficult to manage and identify resources solely based on instance names. You can classify FileNAS instances according to business scenarios and set the same tags for instances in the same business scenario. After setting is completed, you can quickly filter instances by specifying the tag key and tag value.

* **Bill and Cost Allocation**:If there is a need for cost allocation based on different organizations or departments in the business scenario, cloud resources can be classified and managed through tags. By setting the same tags for cloud resources within the same organization or department, the cost of cloud resources can be allocated to the corresponding organization or department during regular settlement, achieving cost allocation management.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note


* You can add multiple tags of different categories for each FileNAS instance, but the tag keys of multiple tags under the same instance cannot be duplicated, and each tag key can only have one tag value. For example, when adding a tag to FileNAS instance A, if the tag `filesystemtype:extreme` has already been added, if you want to add the tag `filesystemtype:extreme` later, you need to delete the tag `filesystemtype:extreme` first.

* The tag information between different regions is not interoperable.

* There is no limit to the total number of tags, but each FileNAS instance can be associated with a maximum of 50 tags. For more information, please refer to [Tag Setting Rules](https://docs.byteplus.com/docs/nas/Binding-or-adding-tags#%E6%A0%87%E7%AD%BE%E8%AE%BE%E7%BD%AE%E8%A7%84%E5%88%99).


<span id="97cd3c4a"></span>
## Example Usage

For example, a company purchased 5 FileNAS instances on the Byteplus, which are used for the game, artificial intelligence, and Internet of Things business departments, and are maintained by Alice, Ben, and Carl. For easy management, instances can be categorized using tags. In this scenario, the following tag key\-value pairs can be designed.


|**Tag Key** |**Tag Value** |
|---|---|
|department |game, ai, iot |
|owner |Alice, Ben, Carl |


In this scenario, it is possible to set corresponding tags for each instance.


|**Instance Name** |**Instance Tag** |
|---|---|
|FileNAS Instance A |* `department:game`<br><br>* `owner:Alice` |
|FileNAS Instance B |* `bdepartment:game`<br><br>* `owner:Ben` |
|FileNAS Instance C |* `department:ai`<br><br>* `owner:Ben` |
|FileNAS Instance D |* `department:ai`<br><br>* `owner:Carl` |
|FileNAS Instance E |* `department:iot`<br><br>* `owner:Carl` |


&nbsp;

<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [Binding or adding tags](https://docs.byteplus.com/docs/nas/Binding-or-adding-tags)

* [Filtering file systems by tags](https://docs.byteplus.com/docs/nas/Filtering-file-systems-by-tags)

* [Unbinding or deleting tags](https://docs.byteplus.com/docs/nas/Unbinding-or-deleting-tags)
