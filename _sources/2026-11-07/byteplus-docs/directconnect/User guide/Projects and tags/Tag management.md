---
title: "Tag management"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Tag-management"
---

<span id=".5qaC6L-w"></span>
## Overview

As your business scale expands, the variety and quantity of cloud resource instances you use also gradually increase. When you have a large number of cloud resource instances, you can mark and categorize them by adding different tags for various types and purposes. This facilitates quick retrieval of cloud resource instances with specific characteristics in the future.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios


* **Group management**

   You can associate different tags to different environments (such as the production and test environments), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with certain key\-value pair (such as Test:Server\-Windows) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost allocation with tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. To use tags for cost allocation, enable bill tags under [Cost organization - Bill tags](https://console.byteplus.com/finance/bill/tag/) in the Billing center console, and apply the corresponding tags to bill details. For procedure, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).


<span id=".5qCH562-57G75Z6L"></span>
## Tag types


* **System Tag**: Tags automatically added to resources by the system upon creation. They typically start with `volc:` or `sys:` and are viewable but not editable.

* **Custom Tag**: Tags that you manually add to resources. You cannot create custom tags that start with `volc:` or `sys:` regardless of case. For details, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Tag usage instructions


* A single operation allows you to add up to 20 tags, and an individual instance can have a maximum of 50 tags.

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.


<span id=".57yW6L6R5qCH562-"></span>
## Edit a tag


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select your target region.

3. Access the tag editing page using any of the following methods.

   * In the DC Gateway list, hover the mouse over the number in the **Tags** column of the target DC Gateway. In the pop\-up tooltip, click **Edit tag**. In the **Edit tag** dialog box, add new tag keys and values.

   * In the DC Gateway list, click the target gateway name to enter the detail page. Click the <span>![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_761d50efa63019e6e502a1316fa70e78.png) </span>icon next to **Tags** in the **Basic information** section.

4. Edit the tag.

   * **Add tag**: In the pop\-up **Edit tag** dialog box, add new tag key and tag value.

   * **Modify tag**: In the pop\-up **Edit tag** dialog box, directly modify the tag key and tag value of the target tag.

   * **Delete tag**: In the pop\-up **Edit tag** dialog box, click the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_073056c998e7206c17a27e2f18cf6bea.png) </span>icon next to the target tag.

5. Click **Save** to complete the edit actions.


<span id=".6YCa6L-H5qCH562-5pCc57Si5a6e5L6L"></span>
## Search instances by tags

<span id=".5pON5L2c6K-05piO"></span>
#### Instructions


* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If a search condition contains multiple tags, the relationship between the Keys of these tags is a logical AND. If the same Key contains multiple Values, the relationship between these Values is a logical OR.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty values.

* During search, up to 3 tag values can be added simultaneously for the same tag key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.   </div>
   

<span id=".5pON5L2c56S65L6L"></span>
#### Example

Search for cloud resource instances based on tags. Assume that the search conditions are as follows:

Tag 1: Tag key: key1; Tag values: value1, value2.

Tag 2: Tag key: key2, with no tag value set.

The found cloud resource instances must meet all of the following conditions:


* They must possess both tag keys, key1 and key2.

* For the tag with key1, its value can be either value1 or value2.

* For the tag with key2, its value can be any value.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Log in to the [Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. In the top menu bar, select your target region.

3. In the DC Gateway list, click the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_e3c4d6e0b9bd10b403f760485254706e.png) </span>icon next to **Tags** in the table header. Then set the tag key and tag value for the search condition.

4. Click **Apply**. The DC Gateways that meet the current filter conditions are displayed in the list.

5. Click the <span>![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_80fb1da6c52eaec9b157930246bbaa93.png) </span>icon again to view the current filter conditions.

   * To modify the filter condition, click **Apply**. Then, DC Gateways that meet the new condition are displayed.

   * Click **Reset** to clear the filter condition. Then, all DC Gateways are displayed.


<span id=".6YCa6L-H5qCH562-6L-b6KGM5YiG6LSm"></span>
## **Allocate costs by tags**

You can use tags to label cloud resources and define tag keys and values as needed based on your internal cost management and analysis dimensions to classify cloud resources or allocate costs. For more information, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".5ZCv55So6LS555So5qCH562-"></span>
#### Enable bill tags


1. Log in to [the Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. On the upper\-right corner of the top menu bar, choose **Billing \> Cost organization**.

3. In the left\-side navigation pane, choose **Bill tags** under **Cost organization**.

4. In the tag list, click the toggle switch under the **Actions** column to enable the target tag.

5. Click **OK** in the pop\-up dialog box to enable a normal tag as a bill tag.


<span id=".6K6-572u6LS555So5qCH562-5YiX"></span>
#### Set the Tags column


1. Log in to [the Direct Connect console](https://console.byteplus.com/dc/PhysicalConnection).

2. On the upper\-right corner of the top menu bar, choose **Billing \> Bill management** to go to the **Bill details** page.

3. On the **Bill management** page, click the **Bill details** tab and then click **Customize column** on the right side.

4. In the pop\-up **Customize column** dialog box, check the box for the **Tags** column.

5. Click **OK**. After configuration is complete, the **Bill details** will display the **Tags** column.


<span id=".5ZCO57ut5pON5L2c"></span>
#### What to do next

You can convert bill detail data for further statistical analysis. When selecting **Billing items** or **Instance** for statistical dimension, you can view **Tags** column arguments. If the tags are not completely consistent during aggregation, the tag column will be displayed as empty. It is recommended to select the statistical period as **Detail**. For more bill\-related information, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, see <a href="https://docs.byteplus.com/en/docs/directconnect/IAM_FAQs#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>



* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources): Remove tags from specified cloud resource instances.

* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources): Add tags to specified cloud resource instances.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources): Query related cloud resource instances by tags.
