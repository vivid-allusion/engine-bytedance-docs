---
title: "Tag management"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/Managing-tags"
---

Tags are used to identify resources. They help you mark and categorize resources with common characteristics from different dimensions (e.g., purpose, type, owner, or environment), making it easier to search, aggregate, and manage your cloud resources efficiently.

<span id=".5rOo5oSP5LqL6aG55Y-K57G75Z6L"></span>
## Precautions and types

For precautions and types of tags, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview).

<span id="XXLq9HxY"></span>
## Design principles and examples

For design principles and examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

<span id=".57yW6L6R5qCH562-"></span>
## Edit tag


<Tabs>
<Tab zoneid="iRSsq4zHeF" title="Add tag">
<TabTitle>Add tag</TabTitle>

1. Log in to the [NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the NAT Gateway list, hover over the number in the **Tags** column of the target NAT Gateway. In the pop\-up tooltip, click Edit tag.

4. Click **Add tag** and type in Key and Value.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="zNdDWmK1cJ" title="Modify tag">
<TabTitle>Modify tag</TabTitle>

1. Log in to the [NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the NAT Gateway list, hover over the number in the **Tags** column of the target NAT Gateway. In the pop\-up tooltip, click the edit tag button to bring up the edit tag window.

4. Modify Key and Value as needed.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="O6AVFmAyNK" title="Delete tag">
<TabTitle>Delete tag</TabTitle>

1. Log in to the [NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. In the NAT Gateway list, hover over the number in the **Tags** column of the target NAT Gateway. In the pop\-up tooltip, click Edit tag.

4. Click the delete icon to the right of your target tag.

5. Click **Save** to complete the action.


</Tab>
</Tabs>


&nbsp;

<span id=".5L2_55So5qCH562-562b6YCJ5a6e5L6L"></span>
## Filter instances by tags

**Limits**

Limits on entered tags when filtering are as follows:


* Type in up to 10 tag keys per request.

   * The relationship between multiple tag keys (Keys) is logical AND.

   * The same Key can contain 3 tag values (Values) simultaneously. The relationship between multiple Values is logical OR.

* Value can be left blank or empty:

   * Left blank: the Value can be any value.

   * Empty: Filter tags with empty value. That is, tags added without entering a value.


**Procedure**


1. Log in to the [NAT Gateway console](https://console.byteplus.com/nat/nats).

2. In the top menu bar, select a target region and project.

3. On the NAT Gateway list, click the filter icon next to **Tags** in the table header. Then, specify tag keys and tag values.

4. Click **Apply**. Then, the NAT Gateway list displays the NAT Gateways that meet your filter conditions.


**Filter examples**

Type in filters:


* Tag key 1: key1, Tag values: value1, value2.

* Key 2: key2. Values: Left blank.


Filtered cloud resources:


* Tags with both key1 and key2.

* Value of key1 is value1 or value2.

* Value of key2 can be any value.


<span id=".5qCH562-5YiG6LSm"></span>
## Cost allocation with tags

For tag accounting, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".55u45YWzQVBJ"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, see <a href="https://docs.byteplus.com/en/docs/natgateway/Identity-and-Access-Management-FAQ#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>



* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources): Add tags to specified cloud resource instances.

* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources): Delete tags from specified cloud resource instances.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources): Query related cloud resource instances by tags.
