---
title: "Tag management"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/NLB-Tag-Management"
---

## Overview

Tags are used to identify resources. They help you categorize and manage resources with common characteristics from different dimensions (such as purpose, type, owner, or environment). This allows you to quickly locate Load Balancer resources with specific tags, filter related bills based on tags, and implement cost allocation management.

## Application scenarios

* **Group management**

   You can associate different tags to different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with certain key\-value pair (such as `Test:Server-Windows`) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost Allocation with Tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. When using tags for bill allocation, you need to enable bill tags in the [Billing Management > Bill tags](https://console.byteplus.com/finance/bill/tag/) section of the Billing center console and apply the corresponding tags to bill details. For detailed steps, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

## Tag types

* System Tags: Tags automatically added to resources by the system upon creation are called system tags. They typically start with volc: or sys: and are viewable but not editable.

* Custom tag: Any tags manually added to resources are considered custom tags. Note that custom tags cannot start with `volc:` or `sys:` in any case variation.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

## Tag usage instructions

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* NLB supports tag management for resources including: NLB instances, listeners, and server groups.

* Tags added when creating an Internet NLB instance apply only to the NLB instance. Associated Elastic IP (EIP) addresses do not inherit these tags.

* You can add up to 20 tags at a time and add up to 50 tags to each Cloud Load Balancer (CLB) resource.

## Procedures

### Associate tags

* **Associate tags when creating a resource**

   When [creating an NLB instance](https://docs.byteplus.com/en/docs/clb/Creating-an-NLB-instance), [adding a listener](https://docs.byteplus.com/en/docs/clb/NLB-Adding-a-listener), or [creating a server group](https://docs.byteplus.com/en/docs/clb/NLB-Creating-a-server-group), click **Add tag**, enter the tag key and tag value, then press Enter to associate the tag with the NLB resource.

* **Associate tags for a created resource**

   Refer to Editing tags in the section below for adding tags.

### Edit tags

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Instance Management or Server Group.

   > **tip**

   > When associating tags with a listener, go to the NLB instance details page and select the Listener tab.

4. Hover over the number in the Tag column of the target resource and click the edit icon.

   * Add tags: Add new tag keys and tag values.

   * Edit tags: Directly modify the original tag key and tag value.

   * **Delete tag**: Click the delete icon on the right of the target tag.

5. Click **Migrate** to complete the action.

### Search for instances by tags

#### Action description

* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical `AND`. If the same key has multiple values, the relationship between these values is a logical `OR`.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.

   > **tip**

   > Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.

#### Operation example

Search for cloud resource instances based on Tags. Assume that the search conditions are as follows:

Tag 1: Tag key: key1; Tag values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:

* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.

#### Procedures

1. Log in to the [NLB console](https://console.byteplus.com/nlb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select Instance Management or Server Group.

   > **tip**

   > When searching for listeners by tags, select the Listener tab on the NLB instance details page.

4. In the Tag column, click the filter icon.

5. Select or type Keys and Values of tags.

   > **tip**

   * > A maximum of 10 tag keys can be set simultaneously for search, with each tag key supporting up to 3 tag values at the same time.

   * > The relationship among the specified keys is logical `AND`, and the relationship among multiple values of the same key is logical `OR`.

6. Click **Apply** to search for target resources.

### Accounting by tags

For specific actions, see [Bill tags](https://docs.byteplus.com/en/docs/byteplus-platform/bill_tags).

## Related documents

> **tip**

> By default, IAM users do not have permissions to use tags. If you want to use tags as an IAM user, refer to Granting permissions to use NLB tags to add a custom policy and grant permissions to IAM users.

* [TagNLBResources](https://docs.byteplus.com/en/docs/clb/TagResources)

* [UntagNLBResources](https://docs.byteplus.com/en/docs/clb/UntagResources)

* [ListTagsForNLBResources](https://docs.byteplus.com/en/docs/clb/ListTagsForResources)
