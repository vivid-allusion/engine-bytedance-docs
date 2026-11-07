---
title: "Tag management"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Managing-tags"
---

Tags are used to identify resources. They help you mark and categorize resources with common characteristics from different dimensions (such as purpose, type, owner, or environment), making it easier to search, aggregate, and manage your cloud resources.

<span id=".5qCH562-6K-05piO"></span>
## Tag description

For instructions on tag usage and types, see [Tag overview](https://docs.byteplus.com/en/docs/resourcemanagement/Tag_Overview).

<span id=".6K6-6K6h5Y6f5YiZ5Y-K56S65L6L"></span>
## Design principles and examples

For design principles and examples of tags, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

<span id=".57yW6L6R5qCH562-"></span>
## Edit a tag

<span id=".5re75Yqg5qCH562-"></span>
### Add a tag


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center". Then, navigate to the migration source or migration task list page.

3. In the top menu bar, select the project to which the target resource belongs.

4. Hover the mouse over the number in the "Tag" column of the target resource and click the edit button.

5. On the "Edit tag" page, click the "Add tags" button.

6. Enter the tag key (Key) and tag value (Value) that you want to add.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_37e44ff399b8491901308e5aa3600a46.png) </span>

7. Click the "Confirm" button to complete the operation.


<span id=".5L-u5pS55qCH562-"></span>
### Modify a tag


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance)

2. In the left directory tree under any region, select "Server Migration Center". Then, navigate to the migration source or migration task list page.

3. In the top menu bar, select the project to which the target resource belongs.

4. Hover the mouse over the number in the "Tag" column of the target resource and click the edit button.

5. On the "Edit tag" page, modify the tag key (Key) and tag value (Value) based on your needs.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4e2d59dd595d5802ee16780549331671.png) </span>

6. Click the "OK" button to complete the operation.


<span id=".5Yig6Zmk5qCH562-"></span>
### Delete a tag


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance)

2. In the left directory tree under any region, select "Server Migration Center". Then, navigate to the migration source or migration task list page.

3. In the top menu bar, select the project to which the target resource belongs.

4. Hover the mouse over the number in the "Tag" column of the target resource and click the edit button.

5. On the "Edit tag" page, click the delete button to the right of the tag key (Key) and tag value (Value) that you want to delete.

6. Click the "Confirm" button to complete the operation.


<span id=".5L2_55So5qCH562-562b6YCJ6L-B56e76LWE5rqQ"></span>
## Filter migration resources by tag

<span id=".57qm5p2f6ZmQ5Yi2"></span>
### Limits

Limits on entered tags for filtering are as follows:


* You can enter a maximum of 10 tag keys at one time.

   * The relationship between multiple tag keys (Keys) is logical AND.

   * For one key, you can enter 3 tag values at one time, and the relationship between these tag values is logical OR.

* Tag value can be left blank or empty:

   * Left blank: Any value can be used.

   * Left empty: Filters tags with an empty value, which refers to tags added without an entered value.


<span id=".5pON5L2c5q2l6aqk"></span>
### Procedure


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center". Then, navigate to the migration source or migration task list page.

3. In the top menu bar, select the project to which the target resource belongs.

4. Add filter conditions in the search bar by specifying "Tag" or "Tag key" and then entering the tag key (Key) and tag value (Value).

5. Press the Enter key to filter migration resources that meet the conditions.


<span id=".562b6YCJ56S65L6L"></span>
### Filter examples

Filter conditions:


* Tag key 1: key1; Tag value: value1, value2.

* Tag key 2: key2, tag value: left blank.


Filtered cloud resources:


* Tags with both key1 and key2.

* The tag value of the tag key named key1 is value1 or value2.

* The tag value of key2 can be any value.
