---
title: "Tag management"
product: "Cloud Enterprise Network"
product_code: "cen"
source: "https://docs.byteplus.com/en/docs/cen/Projects-and-tags-02"
---

## Overview

Tags are used to identify resources. They help you categorize and manage resources with common characteristics from different dimensions (such as purpose, type, owner, or environment). This allows you to quickly locate Cloud Enterprise Network (CEN) resources with specific tags, filter related bills based on tags, and implement cost allocation management.

## Application scenarios

* **Group management**

   You can associate different tags to different environments (such as the production environment and test environment), different operating systems (such as Windows and Linux), or different client platforms (such as iOS and Android). For example, you can associate a tag with certain key\-value pair (such as Test:Server\-Windows) to all instances involved in a test environment. During routine maintenance, you can filter a group of tagged instances from all instances and then perform actions.

* **Cost Allocation with Tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management.

## Tag types

* System tag: Tags that are automatically added to resources when they are created are system tags. System tags usually start with `volc:` or `sys:`, can only be viewed and cannot be edited.

* Custom tag: Any tags manually added to resources are considered custom tags. Note that custom tags cannot start with `volc:` or `sys:` in any case variation.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).

## Tag usage instructions

* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* The resources supported by CEN tag management function include CEN instances and bandwidth packages.

* A single operation can add up to 20 tags. A single CEN resource can have a maximum of 50 tags.

## Tag management operations

### Associate tags

#### Associate tags when creating a resource

[Create CEN instance](https://docs.byteplus.com/en/docs/cen/CEN-instances-01) or [Create BWP](https://docs.byteplus.com/en/docs/cen/CEN-bandwidth-packages-01): Click **Advanced option** on the creation page, click the add icon, input the Tag key and Tag value, and press Enter to associate tags to the CEN Instance or Bandwidth Package.

#### Bind tags after resource creation

1. Log in to the CEN resource console based on the type of resource to be tagged.

   * CEN instances: Log in to the CEN console.

   * Bandwidth package: Log in to the Bandwidth Package console.

2. In the top navigation bar, select the target project.

3. Access the tag editing page using either of these methods:

   * Find the target resource, then move the pointer over the number in the **Tag** column. In the prompt box, click **Edit tag**.

   * Click the name of the target resource. On the resource details page, click the icon behind Tag.

4. Click the add icon to bind new tags to the target resource.

5. Select or enter the tag key and tag value for the new tag.

6. Click **Migrate** to complete the action.

### Edit tags

1. Log in to the CEN resource console based on the type of resource whose tags need editing.

   * CEN instances: Log in to the CEN console.

   * Bandwidth package: Log in to the Bandwidth Package console.

2. In the top navigation bar, select the target project.

3. Access the tag editing page using either of these methods:

   * Find the target resource, then move the pointer over the number in the **Tag** column. In the prompt box, click **Edit tag**.

   * Click the resource name to enter its details page, then click the edit icon next to the Tags section.

4. Edit tag.

   * **Add tag**: In the pop\-up Edit tag dialog box, add new Tag Key and Tag Value.

   * **Modify tag**: In the pop\-up Edit tag dialog box, directly modify the Tag Key and Tag Value of the tag to be modified.

   * **Delete tag**: Click the delete icon next to the target tag.

5. Click Save to complete the action.

### Search Resources by Tags

#### Action description

* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If a search condition contains multiple tags, the relationship between the Keys of these tags is logical AND. If the same Key contains multiple Values, the relationship between these Values is logical OR.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.

   > **tip**

   > Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.

#### Operation example

Search for cloud resource instances based on **Tags**. Assume that the search conditions are as follows:

Tag 1: Keys: key1; Values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:

* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.

#### Procedures

1. Navigate to the corresponding resource management console.

   * CEN instances: Log in to the CEN console.

   * Bandwidth package: Log in to the Bandwidth Package console.

2. In the top navigation bar, select the target project.

3. In the resource list, click the filter icon in the **Tag** column.

4. Select or type Keys and Values of tags.

   > **tip**

   * > You can add up to 10 Keys and configure up to three Values for each Key in a search.

   * > The relationship between multiple specific Keys is logical AND, and the relationship between multiple Values of the same Key is logical OR.

5. Click **Apply** to search for target resources.

## Authorize IAM users to use the tag feature

1. Log in to the [IAM console](https://console.byteplus.com/iam/identitymanage/user) with the root user to which the IAM user belongs.

2. In the left\-side navigation pane, click **Policy management**.

3. In the policy list, click the **Custom policy** tab, then click **Create policy**. Create a custom policy based on the following content to grant global permissions to perform the TagResources, UntagResources, and ListTagsForResource actions.

   ```JSON
   {        
       "Statement":[        
           {        
               "Effect":"Allow",        
               "Action":[        
                    "cen:TagResources",
                    "cen:UntagResources",
                    "cen:ListTagsForResources"
               ],        
                "Resource":[        
                     "*"
               ]
           }
       ]
   }
   ```

4. In the left\-side navigation pane, select **User management \> User** to access the User page.

5. In the user list, click the username of the IAM user to be authorized.

6. On the **Policy** tab, under **Directly Add Policy**, in the **Global** page, click **Add permission** to add the newly created custom policy permission to the IAM user.

## Related documents

> **tip**

> IAM users do not have permission to use the tag feature by default. To grant tag functionality to IAM users, see [Authorizing IAM users to use the tag feature](https://docs.byteplus.com/en/docs/cen/Projects-and-tags-02#.5o6I5p2D5a2Q55So5oi35L2_55So5qCH562-5Yqf6IO9).

* [TagResources](https://docs.byteplus.com/en/docs/cen/TagResources)

* [UntagResources](https://docs.byteplus.com/en/docs/cen/UntagResources)

* [ListTagsForResources](https://docs.byteplus.com/en/docs/cen/ListTagsForResources)
