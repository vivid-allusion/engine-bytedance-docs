---
title: "Tag management"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Managing-tags"
---

Tags are used to identify resources. They help you mark and categorize resources with the same characteristics from different dimensions (e.g., purpose, type, owner, and environment) for easy searching and aggregation, simplifying cloud resource management.

<span id=".5rOo5oSP5LqL6aG55Y-K57G75Z6L"></span>
## Precautions and types

For precautions and types of tags, see [Tag management](https://docs.byteplus.com/en/docs/ecs/Tag-overview).

<span id=".6K6-6K6h5Y6f5YiZ5Y-K56S65L6L"></span>
## Design principles and examples

For design principles and examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

<span id=".57yW6L6R5qCH562-"></span>
## Edit a tag


<Tabs>
<Tab zoneid="l671G25aA8" title="Add tag">
<TabTitle>Add tag</TabTitle>

1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package list, hover your cursor over the digit in the "Tag" column of the target Bandwidth Package. Click the **Edit** icon that appears to pop up the Edit tag window.

4. Click **Add tag** and type in Key and Value.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="YDoLpjZpUQ" title="Modify tag">
<TabTitle>Modify tag</TabTitle>

1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package list, hover your cursor over the digit in the **Tag** column of the target Bandwidth Package. Click the **Edit** icon that appears to pop up the Edit tag window.

4. Modify Key and Value as needed.

5. Click **Save** to complete the action.


</Tab>
<Tab zoneid="vooRJhdBOo" title="Delete tag">
<TabTitle>Delete tag</TabTitle>

1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Bandwidth Package list, hover your cursor over the digit in the **Tag** column of the target Bandwidth Package. Click the **Edit** icon that appears to pop up the Edit tag window.

4. Click the delete icon to the right of your target tag.

5. Click **Save** to complete the action.


</Tab>
</Tabs>


<span id=".5L2_55So5qCH562-562b6YCJ5a6e5L6L"></span>
## Filter instances by tags

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits

Limits on entered tags when filtering are as follows:


* Type in up to 10 tag keys per request.

   * The relationship between multiple tag keys (Keys) is logical AND.

   * The same Key can contain 3 tag values (Values) simultaneously. The relationship between multiple Values is logical OR.

* Value can be left blank or empty:

   * Left blank: the Value can be any value.

   * Empty: Filter tags with empty value. That is, tags added without entering a value.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. In the Shared Bandwidth Package list, click after the Tag in the header.<span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e3c4d6e0b9bd10b403f760485254706e.png) </span>to enter the tag key (Key) and tag value (Value).

4. Click **Apply**. Bandwidth Package instances that meet the filter are listed.


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
## Cost allocation with tags

For tag\-based bill splitting, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".55u45YWzQVBJ"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, see <a href="https://docs.byteplus.com/en/docs/bandwidthpackage/FAQs#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>



* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources): Add tags to specified cloud resource instances.

* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources): Delete tags from specified cloud resource instances.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources): Query related cloud resource instances by tags.
