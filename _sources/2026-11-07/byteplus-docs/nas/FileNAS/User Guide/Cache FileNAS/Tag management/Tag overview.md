---
title: "Tag overview"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Tag_overview"
---

FileNAS supports tag\-based resource management. Tags help you categorize file systems by purpose, type, owner, environment or other criteria, making filtering and managing cloud resources easier.

<span id="36131b58"></span>
## Feature introduction

As cloud resources grow, management complexity increases. BytePlus offers tag\-based resource management, enabling customizable identification and classification of cloud service resources across various dimensions. You can use tags to organize cloud resources by business category, purpose, user, or other criteria. These tags allow for the quick querying and filtering of specific resource categories once applied. With tags, you can manage FileNAS resources at the file system level. A tag consists of a key\-value pair, where a tag key is associated with exactly one tag value. You can add multiple tags of different categories to each FileNAS file system, such as `filesystemtype:extreme` and `region:beijing`. Each tag can be applied to multiple file systems. For example, you can assign the same tag `owner:Alice` to certain FileNAS file systems in a batch.

<span id="ca2339db"></span>
## Application scenarios

Tags are particularly useful in the following scenarios.


* **Classified management of cloud resources**: Managing and identifying cloud resources just by their file system names is challenging when there are many resources. In this case, you can group FileNAS file systems by business scenarios and tag those with the same scenario. After setting up tags, you can easily filter file systems by tag keys and values.

* **Billing and cost allocation**: If your business scenario requires cost allocation by different organizations or departments, you can use tags to classify cloud resources. Assign identical tags to cloud resources within the same organization or department to allocate costs during periodic billing.


<span id="837635e3"></span>
## Notes


* You can add multiple tags to each FileNAS file system. However, tag keys under the same file system can't repeat. Each key can only have one value. For example, if you want to add the tag `filesystemtype:common` to FileNAS file system A, which already has the tag `filesystemtype:extreme`, you must first delete the `filesystemtype:extreme` tag.

* Tag information is not shared across regions. For example, tags created in the China (Beijing) region are not visible in the China (Shanghai) region.

* Each FileNAS file system can have up to 50 tags, but there is no global limit on total tags. Refer to the[ Tagging rules](https://docs.byteplus.com/en/docs/nas/Binding-or-adding-tags) for detailed guidelines on tag configuration.


<span id="7ab351cf"></span>
## Usage examples

For example, company A purchased five FileNAS file systems on BytePlus. These file systems were assigned to the gaming, AI, and IoT departments and serve users in Beijing, Guangzhou, and Shanghai. Alice, Ben, and Carl maintain these file systems. To make management easier, file systems can be classified by tagging. In this case, company A can create the following tag keys and values.


|Tag key |Tag value |
|---|---|
|department |game, ai, iot |
|region |beijing, guangzhou, shanghai |
|owner |Alice, Ben, Carl |


In this case, company A can assign the following tags to each file system.


|File system name |File system tag |
|---|---|
|FileNAS file system A |* department:game<br><br>* region:beijing<br><br>* owner:Alice |
|FileNAS file system B |* department:game<br><br>* region:guangzhou<br><br>* owner:Ben |
|FileNAS file system C |* department:ai<br><br>* region:beijing<br><br>* owner:Ben |
|FileNAS file system D |* department:ai<br><br>* region:shanghai<br><br>* owner:Carl |
|FileNAS file system E |* department:iot<br><br>* region:beijing<br><br>* owner:Carl |


<span id="88d2f53c"></span>
## Related documentation


* [Binding tags](https://docs.byteplus.com/en/docs/nas/Binding_tags)

* [Filtering file systems by tag](https://docs.byteplus.com/en/docs/nas/Filtering_file_systems_by_tag)

* [Editing tags](https://docs.byteplus.com/en/docs/nas/Editing_tags)

* [Unbinding tags](https://docs.byteplus.com/en/docs/nas/Unbinding_tags)
