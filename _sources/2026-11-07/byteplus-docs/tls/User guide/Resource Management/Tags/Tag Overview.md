---
title: "Tag Overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/tag_overview"
---

Tags are used to identify and classify cloud resources. Torch Log Service (TLS) allows you to attach tags to projects and topics. You can use tags to classify cloud resources, then search for or aggregate cloud resources by tag. This topic describes the concepts and limits on tags and how to use tags.

<span id="功能概述"></span>
## Feature overview

The increasing number of cloud resources increases the difficulty of resource management. The tagging feature offered by BytePlus can help you identify and classify your cloud service resources from various dimensions. For example, you can attach different tags to cloud resources that are used for different business modules, purposes, or objects for managing the resources by category. You can use tags as conditions to quickly query and filter cloud resources of the specified categories.

TLS allows you to attach tags to projects and topics. This way, you can perform tag\-based resource management. A tag is a key\-value pair consisting of a tag key and a tag value. You can add different tags to a project or topic, such as `module:http` and `city:guangzhou`. You can also attach the same tag to multiple cloud resources. For example, attach the tag `owner:zhangsan` to two projects.

<span id="应用场景"></span>
## Use scenarios

We recommend that you use tags for resource management in the following scenarios:


* Cloud resource classification

   If you have a large number of cloud resources, it is difficult to manage and identify the resources by project name. In this case, you can classify the projects by business module and attach the same tags to the projects for the same business module. Then, you can specify tags to quickly query projects.

* Bill splitting and cost allocation

   In scenarios where cloud resource costs are allocated to multiple organizations or departments, you can use tags to classify cloud resources. For example, you attach the same tags to the cloud resources of an organization or department and allocate the costs of the cloud resources to the organization or department during periodic settlement.


<span id="注意事项"></span>
## Precautions


* You can add multiple tags to a cloud resource and specify only one value for each tag. For example, if the `module:http` tag is attached to Project A, you must delete the tag before you attach the `module:tcp` tag to the project.

* Tags do not take effect across Regions.

* The total number of tags within your account is unlimited. However, you can attach up to 50 tags to one project or topic. For more information on tag setting rules, refer to [Rules for setting tags](https://docs.byteplus.com/docs/tls/Add_tags#%E6%A0%87%E7%AD%BE%E8%AE%BE%E7%BD%AE%E8%A7%84%E5%88%99).


<span id="示例"></span>
## Example

For example, your company has five projects on BytePlus, which are used for three business modules of payment, shopping cart, and credit point accumulation respectively. These projects are maintained by Zhang San, Li Ming, and Han Meimei. To facilitate resource management, you can use tags to classify the projects.

In this scenario, you can create the following tags:


|Tag Key |Tag Value |
|---|---|
|system |pay, shoppingcart, and integral |
|owner |zhangsan, liming, and hanmeimei |


Attach tags to projects as follows:


|Project name |Tags |
|---|---|
|Project A |* system:pay<br><br>* owner:zhangsan |
|Project B |* system:pay<br><br>* owner:liming |
|Project C |* system:shoppingcart<br><br>* owner:liming |
|Project D |* system:shoppingcart<br><br>* owner:hanmeimei |
|Project E |* system:integral<br><br>* owner:hanmeimei |
