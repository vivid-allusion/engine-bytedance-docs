---
title: "Tag management"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Managing-tags"
---

Tags identify resources. They help you mark and classify resources with the same characteristics across different dimensions (such as purpose, type, owner, or environment), facilitating search and aggregation to manage cloud resources easily.

<span id=".5rOo5oSP5LqL6aG55Y-K57G75Z6L"></span>
## Precautions and types

For precautions and types of tags, see [Tag overview](https://docs.byteplus.com/en/docs/ecs/Tag-overview).

<span id=".6K6-6K6h5Y6f5YiZ5Y-K56S65L6L"></span>
## Design principles and examples

For design principles and examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

<span id=".57yW6L6R5qCH562-"></span>
## Edit a tag


<Tabs>
<Tab zoneid="ifoyi045Cz" title="Add tag">
<TabTitle>Add tag</TabTitle>

1. Log in [to the EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, hover over the number in the target EIP's **Tag** column. In the tooltip that appears, click the **Edit** icon to open the edit tag window.

4. Click **Add tag**, then enter the tag key and tag value.

5. Click **Save ** to complete the operation.


</Tab>
<Tab zoneid="bORFU2MrjA" title="Modify tag">
<TabTitle>Modify tag</TabTitle>

1. Log in to the EIP console.

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, hover over the number in the target EIP's **Tag** column, then click the **Edit ** icon in the tooltip to open the edit tag window.

4. Modify Key and Value as needed.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="Xbd71LchBY" title="Delete tag">
<TabTitle>Delete tag</TabTitle>

1. Log in to the EIP console.

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, hover over the number in the target EIP's **Tag** column, then click the **Edit** icon in the tooltip to open the edit tag window.

4. Click the delete icon to the right of your target tag.

5. Click **Save** to complete the deletion.


</Tab>
</Tabs>


<span id=".5L2_55So5qCH562-562b6YCJ5a6e5L6L"></span>
## Filter instances by tags

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits

Limits on entered tags when filtering are as follows:


* Type up to 10 tag keys per request.

   * The relationship between multiple tag keys (Keys) is logical AND.

   * The same tag key can have 3 tag values entered at the same time, and the relationship between multiple tag values is logical OR.

* Value can be left blank or empty:

   * Left blank: The tag value (Value) can be any value.

   * Empty: Filter tags with an empty value, meaning tags added without entering a value.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [EIP console](https://console.byteplus.com/eip/eips).

2. In the top menu bar, select the region and project of your target EIP.

3. In the EIP list, click the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e3c4d6e0b9bd10b403f760485254706e.png) </span>icon next to the **Tag** header and enter the tag key and tag value.

4. Click **Apply**, and the EIP list will display EIPs matching the current filters.


<span id=".562b6YCJ56S65L6L"></span>
### Filter examples

Type in filters:


* Key 1: key1. Values: value1, value2.

* Key 2: key2. Values: Left blank.


Filtered cloud resources:


* Tags with both key1 and key2.

* Value of key1 is value1 or value2.

* Value of key2 can be any value.


<span id=".5qCH562-5YiG5biQ"></span>
## Tag accounting

For tag accounting, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".55u45YWzQVBJ"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM users do not have permission to use the tag feature by default. For IAM users who need to use the tag feature, see <a href="https://docs.byteplus.com/en/docs/eip/EIP-FAQs#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>



* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources): Add tags to specified cloud resource instances.

* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources): Delete tags from specified cloud resource instances.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources): Query related cloud resource instances by tags.
