---
title: "Tag management"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Tag-management"
---

<span id=".5qaC6L-w"></span>
## Overview

As your business scale expands, the variety and quantity of cloud resource instances you use also gradually increase. When you have a large number of cloud resource instances, you can mark and categorize them by adding different tags for various types and purposes. This facilitates quick retrieval of cloud resource instances with specific characteristics in the future.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios


* **Group management**

   You can associate different tags with different environments, operating systems, or client platforms.Examples include production and test environments, Windows and Linux, or iOS and Android. For example, you can associate a certain tag key\-value object (Test:Server\-Windows) with all instances in a test environment. During routine maintenance, you can filter tagged instances and perform relevant actions.

* **Cost allocation with tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. When using tags for bill allocation, you need to enable bill tags in the [Cost organization > Bill tags](https://console.byteplus.com/finance/bill/tag/) section of the Billing center console and apply the corresponding tags to bill details. For detailed steps, see [Bill tags](https://console.byteplus.com/finance/bill/tag/).


<span id=".5qCH562-57G75Z6L"></span>
## Tag types


* **System tags**: Tags automatically added by the system when creating resources are system tags, usually starting with `volc:` or `sys:`. System tags support view only. Editing and deleting are not allowed.

* **Custom tag**: Tags that you manually add to resources are considered custom tags. You cannot create custom tags that start with `volc:` or `sys:` (in any case variation). For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Tag instructions


* VPN attachments that support tag management include VPN gateway, customer gateway, IPsec connection, SSL server, and SSL client certificate.

* A single operation can add up to 20 tags. A single VPN resource can have a maximum of 50 tags.

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Tag keys (Key) cannot be duplicated across multiple tags on the same resource, and each tag key (Key) can only have one tag value (Value).


<span id=".57yW6L6R5qCH562-"></span>
## Edit tags


1. Log in to the VPN Connect resource console based on the resource type of the tags to be edited. For example, log in to [the VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Access the tag editing page using any of the following methods.

   * In the VPN resource list, hover the mouse over the number in the target VPN resource **tag** column, and click the **edit** icon in the pop\-up tooltip.

   * In the VPN resource list, click the target VPN resource name to enter the detail page, then click the **edit** icon after the **basic information** section's **tag**.

4. Edit tags according to actual needs.

   * **Add tag**: In the pop\-up **Edit tag** dialog box, add new Tag Key and Tag Value.

   * **Modify tag**: In the pop\-up **Edit tag** dialog box, directly modify the Tag Key and Tag Value of the tag to be modified.

   * **Delete tag**: In the pop\-up **Edit tag** dialog box, click the **delete** icon after the tag to be deleted.

5. Click **Save** to complete the edit actions.


<span id=".6YCa6L-H5qCH562-5pCc57Si5a6e5L6L"></span>
## Search for instances by tags

<span id=".5pON5L2c6K-05piO"></span>
#### Instructions


* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical AND. If the same key has multiple values, the relationship between these values is a logical OR.

* During a search, you can leave Value blank or empty. Leaving it blank indicates no restrictions on Values; whereas an empty value means searching for tags with empty values.

* During a search, you can add up to three Values for a single Key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.   </div>
   

<span id=".5pON5L2c56S65L6L"></span>
#### Action example

Search for cloud resource instances based on **tags**. Assume that the search conditions are as follows:

Tag 1: Tag key: key1; Tag values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:


* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Log in to the VPN Connect resource console according to the resource type of the tags to be edited. For example, log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. In the VPN resource list, click the **tag** filter icon next to the table header, then set the tag filter key (Key) and tag filter value (Value).

4. Click **Apply** to display VPN resources that meet the current filters in the VPN resource list.

5. Click the **filter** icon again to view the current filter condition.

   * You can directly modify the filter condition and click **OK**. The VPN resource list will show VPN resources that meet the new condition.

   * Click **Reset** to clear the filter condition. The list will display all VPN resources.


<span id=".6YCa6L-H5qCH562-6L-b6KGM5YiG6LSm"></span>
## Accounting by tags

You can use tags to label cloud resources and define tag keys and values as needed based on your internal cost management and analysis dimensions to classify cloud resources or allocate costs. For more information, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".5LiA44CB5ZCv55So6LS555So5qCH562-"></span>
#### 1. Enable bill tags


1. Log in to the VPN resource console according to the resource type of the tag to be edited.

   For example, log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. On the upper\-right corner of the top menu bar, choose **Billing \> Cost organization**.

3. In the left\-side navigation pane, choose **Bill tags** under **Cost organization**.

4. In the tag list, click the toggle under the **Actions** column to enable the target tag.

5. Click **OK** in the pop\-up dialog box to enable a normal tag as a billing tag.


<span id=".5LqM44CB6K6-572u6LS555So5qCH562-5YiX"></span>
#### 2. Set bill tag columns


1. Log in to the VPN resource console according to the resource type of the tag to be edited.

   For example, log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. On the upper\-right corner of the top menu bar, choose **Billing \> Bill management** to go to the **Bill details** page.

3. Select the **Bill details** tab and click **Custom column** on the right.

4. In the pop\-up **Custom column** dialog, check **Tag**.

5. Click **OK**. After configuration is complete, the **Bill details** will display the **Tag** column.


<span id=".5ZCO57ut5pON5L2c"></span>
#### What to do next

You can convert bill detail data for further statistical analysis. When selecting **Billing items** or **Instance** for statistical dimension, you can view **Tag** column arguments. If the tags are not completely consistent during aggregation, the tag column will be displayed as empty. It is recommended to select the statistical period as **Detail**. For more bill\-related information, see [Bill management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-bill-details).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, see <a href="https://docs.byteplus.com/en/docs/vpn/Identity-and-Access-Management-FAQs#.5a2Q55So5oi35aaC5L2V5L2_55So5qCH562-5Yqf6IO977yf">How do IAM users use tag features</a>.</div>



* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources): Add tags to specified cloud resource instances.

* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources): Remove tags from specified cloud resource instances.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources): Query related cloud resource instances by tags.
