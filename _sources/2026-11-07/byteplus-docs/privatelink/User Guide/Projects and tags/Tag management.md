---
title: "Tag management"
product: "PrivateLink"
product_code: "privatelink"
source: "https://docs.byteplus.com/en/docs/privatelink/Managing-tags"
---

## Overview

Tags are used to identify resources. They help you categorize and manage resources with common characteristics from different dimensions (such as purpose, type, owner, or environment). This allows you to quickly locate PrivateLink resources with specific tags, filter related bills based on tags, and implement cost allocation management.

## Application scenarios

* **Group management**

   You can associate different tags to different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with certain key\-value pair (such as Test:Server\-Windows) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost Allocation with Tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. To use tags for cost allocation, enable the cost allocation feature in the Billing center console under **Bill management** ** \> ** **Bill tags**, and then apply the corresponding tags to your bill details.

* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom tag: Tags that you manually add to resources are considered custom tags. You cannot create custom tags that start with `volc:` or `sys:` (in any case variation).

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

## Tag usage instructions

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* PrivateLink supports the tag management feature for the following resources: Endpoint Services and Endpoints.

* You can add up to 20 tags in a single operation. A maximum of 50 tags can be added to an individual endpoint service or endpoint.

## Procedures

### Associate tags

#### Associate tags when creating a resource

To [Create endpoint service](https://docs.byteplus.com/en/docs/privatelink/Creating-endpoint-services) or [Create endpoint](https://docs.byteplus.com/en/docs/privatelink/Endpoint-02), expand the **Advanced options** section on the creation page. Click **Add tag**, enter the tag key and value, then press Enter to confirm and bind the tag to your PrivateLink resource.​​

#### Associate tags for a created resource

1. Log in to the Private Link resource console based on the type of resource you want to tag.

2. In the top menu bar, select the target project and region.

3. Click the **Edit** icon in the **Tag** column on the same row as the target resource to edit the tag.

4. Click **Add tag** to Associate new tags with the PrivateLink resource.

5. Click **Apply** to complete the action.

### Edit tags

1. Log in to the PrivateLink resource console based on the type of resource you want to tag.

2. In the top menu bar, select the target project and region.

3. Click the **Edit** icon in the **Tag** column of the row where the target resource is located to edit the tags.

   * **Add tag**: Click **Add tag** to add new tag keys and tag values.

   * **Modify tag**: directly modify the Tag Key and Tag Value of the tag to be modified.

   * **Delete tag**: Click the icon on the right side of the target tag![图片](https://lf6-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_a090885f76ea0a5462180d85adef8c09.png) monitor icon.

4. Click **Apply** to complete the action.

### Search for instances by tags

#### Action description

* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical **AND**. If the same key has multiple values, the relationship between these values is a logical **OR**.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.

   > **tip**

   > Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.

#### Operation example

Search for cloud resource instances based on Tags. Assume that the search conditions are as follows:

Tag 1: Keys: key1; Values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:

* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.

#### Procedures

1. Log in to the Private Link resource console based on the type of resource you want to tag.

2. In the top menu bar, select the project and region of your target resource.

3. Select **tag** in the search box above the resource list or click the **tag** column icon in the list.![图片](https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_f1d025bfe95132f059e4d7e13f9adf4a.png) monitor icon.

4. Select or type Keys and Values of tags.

> **tip**

* > You can add up to 10 Keys and configure up to three Values for each Key in a search.

* > The relationship among the specified keys is logical **AND**, and the relationship among multiple values of the same key is logical **OR**.

5. Click **Apply** to search for target resources.

## Related documents

> **tip**

> IAM users do not have permission to use the tagging feature by default. For IAM users who need to use this feature, refer to [Authorizing the use of PrivateLink tags](https://docs.byteplus.com/en/docs/privatelink/Permission-management-02#.56S65L6L5Zub77ya5o6I5p2D5L2_55So56eB572R6L-e5o6l5qCH562-5Yqf6IO9) to add a custom policy and grant them the necessary permissions.

* [TagResources](https://docs.byteplus.com/en/docs/privatelink/TagResources)

* [UntagResources](https://docs.byteplus.com/en/docs/privatelink/UntagResources)

* [ListTagsForResources](https://docs.byteplus.com/en/docs/privatelink/ListTagsForResources)
