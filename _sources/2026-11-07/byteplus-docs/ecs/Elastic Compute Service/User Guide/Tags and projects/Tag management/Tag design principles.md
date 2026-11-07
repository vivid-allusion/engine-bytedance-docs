---
title: "Tag design principles"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Tag-design-principles"
---

Tags are essential grouping tools for personnel, finance, and resource management. This topic mainly describes the design principles of tags and provides common examples. This helps you quickly and accurately use the tagging feature to achieve horizontal resource management.

<span id=".5qCH562-6K6-6K6h5Y6f5YiZ"></span>
## Tag design principles

When associating tags with resources, refer to the following guidelines to create tags.

**Comprehensive plan**

This principle means that when planning resources, you need to plan tags comprehensively (with priority given to the design of tag keys). Then, associate the planned tag keys and their corresponding tag values with resources. This helps you group and retrieve resources by tag dimensions later.

**Mutual exclusion**

This principle means that using two or more tag keys for the same attribute should be avoided. For example, if you use `key=owner` to mark a resource owner, do not use other tag keys with the same meaning (such as own, belonger).

**Simplified design**

This principle means the simplified use of tag keys. When you plan tags, use tag keys with fixed dimensions. This reduces errors during operations due to an excessive number of tag keys.

**Limited value**

This principle mainly applies to the design of tag values. Remove redundant tag values from resources and retain only core ones. This helps to simplify processes, such as resource management, access control, and automatic O&M.

**Consider future changes**

Changing tags may cause changes in tag\-based processes, such as resource management, access control, and automatic O&M. When you plan tags, consider the impact of adding or removing tag values on existing processes in future work to change tags more flexibly.

<span id=".5qCH562-6K6-6K6h56S65L6L"></span>
## Tag design examples

The table below lists common tag naming examples by business dimension for your reference.


|Business dimension |Tag key |Tag value |
|---|---|---|
|Organizational architecture |* company<br><br>* department<br><br>* organization<br><br>* team<br><br>* group |Related names |
|Business architecture |* product<br><br>* business<br><br>* module<br><br>* service |Related names |
|Project\-related |* project<br><br>* schedule<br><br>* risk<br><br>* subtask |Project\-related values |
|Usage\-related |* purpose<br><br>* use |Usage\-related values |
|Role architecture |* role<br><br>* user |* System administrator<br><br>* Network administrator<br><br>* O&M administrator<br><br>* R&D personnel<br><br>* Test personnel |
|Personnel type |* sponsor<br><br>* creator<br><br>* owner<br><br>* member |Personnel type values |
|Business department (for cost allocation and business tracking) |* costcenter<br><br>* businessunit<br><br>* biz<br><br>* financecontact |Department\-related values |
|Finance owner​ |owner |Names, email addresses, and more |
|Financial order |order |Order category ID |
