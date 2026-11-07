---
title: "Tag management"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Tags"
---

<span id=".5qaC6L-w"></span>
## Overview

Tags identify resources and help you mark and categorize resources with similar characteristics from different dimensions (such as purpose, type, owner, or environment). This makes it easy to quickly find Transit Router (TR) resources with specific tags, filter related resource bills by tags, and implement cost allocation management.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios


* **Group management**

   You can associate different tags with different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with a certain key\-value pair (such as Test:Server\-Windows) with all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost allocation with tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. When using tags for cost allocation, you need to enable cost tags under **Cost organization** ** \- Bill tags** in the Billing Center console to apply the corresponding tags to bill details. For detailed instructions, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).


<span id=".5qCH562-57G75Z6L"></span>
## Tag types


* System tag: Tags that are automatically added to resources when they are created. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom tag: Tags that are manually added to resources. Note that custom tags cannot start with `volc:` or `sys:` in any case variation.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Tag usage instructions


* A tag consists of a tag key and a tag value, both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each key can have only one value.

* Resources that support tag management, including TR instances, network instance attachments, TR route tables, inter\-region attachments, CEN bandwidth packages, and multicast domains.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In cross\-account scenarios, the recipient account can add tags to a shared TR instance after accepting it, independently of the tags added by the sharer account that owns the resource.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In cross\-regions scenarios, you can add tags separately for the same inter\-region attachment in different regions without affecting each other.   </div>
   

* You can add up to 20 custom tags per operation and up to 50 custom tags per TR resource.


<span id=".5qCH562-5pON5L2c"></span>
## Tag actions

<span id=".57yW6L6R5qCH562-"></span>
### Edit a tag


1. Log in to the Transit Router console according to the resource type of the tag to be edited.

   For example, log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. In the top menu bar, select the project and region to which the target TR instance belongs.

3. Hover over the number in the **tag** column of the target TR instance, then click the **edit** icon.

4. Edit the tag.

   * **Add a tag**: Enter new tag keys and values as needed.

   * **Modify a tag**: Modify the key and value of an existing tag.

   * **Delete a tag**: Click the **delete** icon to the right of the target tag.

5. Click **Save** to complete the action.


<span id=".6YCa6L-H5qCH562-5pCc57Si5a6e5L6L"></span>
### Search instances by tags

<span id=".5pON5L2c6K-05piO"></span>
#### Instructions


* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical AND. If the same key has multiple values, the relationship between these values is a logical OR.

* During a search, you can leave value blank or empty. Leaving it blank indicates no restrictions on values; while an empty value indicates searching for tags with empty values.

* During a search, you can add up to three values for a single key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.   </div>
   

<span id=".5pON5L2c56S65L6L"></span>
#### Example

Search for cloud resource instances based on tags. Assume that the search conditions are as follows:

Tag 1: Keys: key1; Values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:


* It contains both key1 and key2.

* For a tag with key1, its value can be value1 or value2.

* For a tag with key2, its value can be any value.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Log in to the Transit Router console according to the resource type of the tags to be searched.

   For example, log in to the [Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Select the project and region of the target TR instance in the top navigation bar.

3. In the **Tag** column, click the **filter** icon.

4. Select or type keys and values of tags.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add up to 10 keys and configure up to three values for each key in a search.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The relationship among the specified keys is logical AND, and the relationship among multiple values of the same key is logical OR.   </div>
   

5. Click **Apply** to search for target resources.


<span id=".6YCa6L-H5qCH562-6L-b6KGM5YiG6LSm"></span>
### Accounting by tags

For details, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM users do not have permission to use the tagging feature by default. For IAM users who need to use the tagging feature, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Permission-management-02#.56S65L6L5Zub77ya5o6I5p2D5L2_55So5Lit6L2s6Lev55Sx5Zmo5qCH562-5Yqf6IO9">authorizing the use of TR tag feature</a> to add a custom policy and grant permissions to IAM users.</div>



* [TagResources](https://docs.byteplus.com/en/docs/transitrouter/TagResources): Add custom tags to TR resources.

* [UntagResources](https://docs.byteplus.com/en/docs/transitrouter/UntagResources): Remove custom tags from TR resources.

* [ListTagsForResources](https://docs.byteplus.com/en/docs/transitrouter/ListTagsForResources): Query tags of TR resources that meet specified conditions.
