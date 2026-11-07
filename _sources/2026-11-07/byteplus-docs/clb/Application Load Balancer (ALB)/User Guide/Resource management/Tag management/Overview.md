---
title: "Overview"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Tag-Overview"
---

<span id="8sdSpcCi"></span>
## Overview

Tags are used to identify resources. They help you categorize and manage resources with common characteristics from different dimensions (such as purpose, type, owner, or environment). This allows you to quickly locate Load Balancer resources with specific tags, filter related bills based on tags, and implement cost allocation management.

<span id="Qk8R7Ivj"></span>
## Application scenarios


* **Group management**

   You can associate different tags to different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with certain key\-value pair (such as `Test:Server-Windows`) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Tag accounting**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. To use tags for cost allocation, enable the cost allocation feature in the Billing center console under [Bill management - Bill tags](https://console.byteplus.com/finance/bill/tag/), and then apply the corresponding tags to your bill details. 


<span id="rum6VBuG"></span>
## Tag types


* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom tag: Any tags manually added to resources are considered custom tags. Note that custom tags cannot start with `volc:` or `sys:` in any case variation.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id="eZSqgqa4"></span>
## Tag usage instructions


* Tag keys and values are case\-sensitive in English.

* Within the resources of the same ALB instance, tag keys cannot be duplicated, and each key can only correspond to one tag value;

* The tag key and tag value can only contain Chinese characters, uppercase and lowercase English letters, numbers, spaces, and the special characters _.:/=+\-@.

* The tag key restrictions: Cannot start with volc: or sys:, or any case variations of volc: and sys:.

* The tag key cannot be empty, while the tag value can be empty.

* A single operation can add up to 20 tags. A single ALB resource can have a maximum of 50 tags.


<span id="89cba1c3"></span>
##
