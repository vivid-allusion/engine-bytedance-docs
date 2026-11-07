---
title: "Tag management"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Tag-management"
---

## Overview

Tags are used to identify resources. They help you categorize and manage resources with common characteristics from different dimensions (such as purpose, type, owner, or environment). This allows you to quickly locate CLB resources with specific tags, filter related bills by tags, and implement cost allocation management.

## Application scenarios

* **Group management**

   You can associate different tags to various environments (e.g., Production and Test), operating systems (e.g., Windows and Linux), or client platforms (e.g., iOS and Android). For example, you can associate a tag with certain key\-value pair (such as Test:Server\-Windows) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost Allocation with Tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. When using tags for bill allocation, you need to enable bill tags in the Billing Management \> Bill tags section of the Billing center console and apply the corresponding tags to bill details. For detailed steps, see Bill tags.

## Tag types

* System Tags: Tags automatically added to resources by the system upon creation are called system tags. They typically start with volc: or sys: and are viewable but not editable.

* Custom tag: Tags you manually add to resources are custom tags. You cannot add custom tags that start with `volc:` or `sys:` in any letter case.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

## Tag usage instructions

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* A single operation can add up to 20 tags. A single CLB resource can have a maximum of 50 tags.

* Resources supporting tag management in CLB include CLB instances, listeners, server groups, access control policy groups, certificates, and forwarding rules.

## Procedures

### Associate tags

#### Associate tags when creating a resource

When [creating a CLB instance](https://docs.byteplus.com/en/docs/clb/CLB-instances-01), [creating a listener](https://docs.byteplus.com/en/docs/clb/Creating-a-Listener), [creating a server group](https://docs.byteplus.com/en/docs/clb/Creating-a-server-group), [creating an access control policy group](https://docs.byteplus.com/en/docs/clb/Managing-access-control-policy-groups#.5Yib5bu6562W55Wl57uE), [uploading a certificate](https://docs.byteplus.com/en/docs/clb/Uploading-a-certificate), or [adding forwarding rules](https://docs.byteplus.com/en/docs/clb/Adding-a-forwarding-rule), click the add icon in the tag section, enter the tag key and tag value, then press Enter to associate tags with the CLB resource.

#### Associate tags for a created resource

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Select the CLB resource in the navigation tree on the left to open the resource list page.

   > **tip**

   > When associating tags with listeners and server groups, switch to the corresponding tab on the CLB instance details page to enter the resource list page.

4. Select the appropriate method to enter the tag editing page:

   * Click ··· \> Edit tags to the right of the target resource.

   * Find the target resource, then move the pointer over the number in the **Tag** column. In the prompt box, click **Edit tag**.

   * Click the name of the target resource to enter the details page, and click the edit icon next to the Basic information pane.

5. Click the add icon to attach a new tag to the CLB resource.

6. Click **Migrate** to complete the action.

### Edit tags

1. Log in to the [CLB console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. Select CLB resources in the left navigation tree to enter the resource list page.

   > **tip**

   > When editing tags for listeners and server groups, switch to the corresponding tab on the CLB instance details page to enter the resource list page.

4. Select the appropriate method to enter the tag editing page:

   * Click ··· \> Edit tags to the right of the target resource.

   * Find the target resource, then move the pointer over the number in the **Tag** column. In the prompt box, click **Edit tag**.

   * Click the name of the target resource to enter the details page, and click the edit icon next to the Basic information pane.

5. Edit tag.

   * **Add tag**: In the pop\-up **Edit tag** dialog box, add new Tag Key and Tag Value.

   * **Modify tag**: In the pop\-up **Edit tag** dialog box, directly modify the Tag Key and Tag Value of the tag to be modified.

   * **Delete tag**: Click the delete icon on the right of the target tag.

6. Click **Migrate** to complete the action.

### Search for instances by tags

#### Action description

* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical **AND**. If the same key has multiple values, the relationship between these values is a logical **OR**.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.

   > **tip**

   > Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.

#### Operation example

Search for cloud resource instances based on **Tags**. Assume that the search conditions are as follows:

Tag 1: Tag key: key1; Tag values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:

* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.

#### Procedures

1. Log in to the [CLB Console](https://console.byteplus.com/clb/LoadBalancer).

2. In the top menu bar, select the target project and region.

3. In the left navigation pane, select CLB resources to access the resource list page.

   > **tip**

   > When searching listeners and server groups by tags, switch to the corresponding tab on the CLB instance details page to access the resource list page.

4. Select the Tag in the search box above the resource list or click the filter icon in the Tag column.

5. Select or type Keys and Values of tags.

   > **tip**

   * > A maximum of 10 tag keys can be set simultaneously for search, with each tag key supporting up to 3 tag values at the same time.

   * > The relationship among the specified keys is logical **`AND`**, and the relationship among multiple values of the same key is logical **`OR`**.

6. Click **Apply** to search for target resources.

For detailed operations, see Bill tagsBill tags.

## Related documents

> **tip**

> IAM users do not have permission to use the tag feature by default. For IAM users who need this feature, refer to [Authorize to use the CLB tag feature](https://docs.byteplus.com/en/docs/clb/Example-of-custom-policy) to add custom policies and grant permissions to IAM users.

* [TagResources](https://docs.byteplus.com/en/docs/clb/TagResources)

* [UntagResources](https://docs.byteplus.com/en/docs/clb/UntagResources)

* [ListTagsForResources](https://docs.byteplus.com/en/docs/clb/ListTagsForResources)
