---
title: "Tag management"
product: "IPv6 Gateway"
product_code: "IPv6"
source: "https://docs.byteplus.com/en/docs/IPv6/Managing_tags"
---

<span id=".5qaC6L-w"></span>
## Overview

Tags are used to identify resources and can help you mark and classify resources with the same characteristics from different dimensions (such as purposes, types, owners, or environments). This enables you to quickly find IPv6 gateway and Internet bandwidth resources with certain tags, and to filter related resource bills based on tags for accounting.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios


* **Group management**

   You can associate different tags with different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate all instances involved in a test environment with a tag that has a certain key\-value pair (such as Test:Server\-Windows). During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost allocation with tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. To use tags for accounting, you need to enable tags on the Billing Center console by the path of [Bill management - Bill tags](https://console.byteplus.com/finance/bill/tag/), and apply related tags to Bill details. For specific actions, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).


<span id=".5qCH562-57G75Z6L"></span>
## Tag types


* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, which can only be viewed and cannot be edited.

* Custom tag: Any tags manually added to resources are considered custom tags. Note that custom tags cannot start with `volc:` or `sys:` in any case variation.

* For details, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Use instructions


* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* IPv6 gateway resources that support tag management include IPv6 gateway instances and Identity and Access Management (IAM) policy groups.

* You can add up to 20 tags per request, and add up to 50 tags for a single IPv6 gateway resource.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


<Tabs>
<Tab zoneid="QjTplY6zoJ" title="Associate tag">
<TabTitle>Associate tag</TabTitle>

<span id="SLw801VG"></span>
### Associate tags when creating a resource

When [creating an IPv6 Gateway instance](https://docs.byteplus.com/en/docs/IPv6/Creating_an_IPv6_gateway_instance) or [creating an IPv6 Internet bandwidth](https://docs.byteplus.com/en/docs/IPv6/Enable_IPv6_internet_bandwidth), click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_810700f892fb46fdf2bc52aff782e3d4.png) </span> icon, enter the tag key and tag value, then press Enter to associate tags with the instance resource.

<span id="ZxojG390"></span>
### Associate tags with an existing resource


1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select the project and region of your target resource.

3. Hover over the number in the target resource's **Tag** column, then click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e1f625c403017fb8adc5ef68ed88660e.png) </span> icon.

4. In the pop\-up Edit tag window, type Keys and Values.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="B4jA5roBwe" title="Add tag">
<TabTitle>Add tag</TabTitle>

1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select the region and project of your target resource.

3. Hover over the count in **Tag** column to the right of target resource, and click the **Edit** icon appears to pop up the Edit tag window.

4. Modify Key and Value as needed.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="KkYhTuGiiv" title="Delete tag">
<TabTitle>Delete tag</TabTitle>

1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select the region and project of your target resource.

3. Hover over the count in **Tag** column to the right of target resource, and click the **Edit** icon appears to pop up the Edit tag window.

4. Click the delete icon to the right of your target tag.

5. Click **Save** to complete the action.


</Tab>
</Tabs>


<span id=".6YCa6L-H5qCH562-5pCc57Si5a6e5L6L"></span>
## Search for instances by tags

<span id=".5pON5L2c6K-05piO"></span>
### Action description


* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If a search condition contains multiple tags, the relationship between the Keys of these tags is logical AND. If the same Key contains multiple Values, the relationship between these Values is logical OR.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.


<span id=".5pON5L2c56S65L6L"></span>
### Operation example

Search for cloud resource instances by tags. Assume that the search conditions are as follows:

Tag 1: Keys: key1; Values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:


* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [IPv6 Gateway console](https://console.byteplus.com/eip/ipv6s).

2. In the top menu bar, select the project and region of your target resource.

3. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aed8c49aaec17d12df8debdfcc81069d.png) </span> icon in the **Tag** column of the resource list.

4. Select or type Keys and Values of tags.

   * You can add up to 10 Keys and configure up to 3 Values for each Key in a search.

   * The relationship between multiple specific Keys is logical AND, and the relationship between multiple Values of the same Key is logical OR.

5. Click **Apply** to search for target resources.


<span id=".6YCa6L-H5qCH562-6L-b6KGM5YiG6LSm"></span>
## Accounting by tags

For specific actions, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, see <a href="https://docs.byteplus.com/en/docs/IPv6/FAQs#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>
