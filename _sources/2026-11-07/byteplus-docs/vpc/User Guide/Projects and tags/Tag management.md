---
title: "Tag management"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-tags"
---

<span id=".5qaC6L-w"></span>
## Overview

Tags are used to identify resources. They help you mark and categorize resources with common characteristics from different dimensions (e.g., purpose, type, owner, or environment), making it easier to search, aggregate, and manage your cloud resources efficiently.

<span id=".5bqU55So5Zy65pmv"></span>
## Application scenarios


* **Group management**

   You can assign different tags to various environments (e.g., Production and Test), operating systems (e.g., Windows and Linux), or client platforms (e.g., iOS and Android). For example, add a key\-value pair like Test:Server\-Windows to all instances involved in a test environment. During daily maintenance, you can first filter instances with this tag before performing operations.

* **Cost allocation with tags**

   In team or project management, you can add tags based on groups, projects, or departments (e.g., CostCenter:Project) to categorize resources. Then, use these tags in the Billing Center for cost allocation management. When using tags for accounting, you need to enable Bill tags in the Billing Center console and apply the corresponding tags to bill details. 


<span id=".5qCH562-57G75Z6L"></span>
## Tag types


* System tags: Automatically added to resources by the system upon creation, they typically start with `volc:` and are viewable but not editable.

* Custom tags: Tags you add manually are custom tags. You cannot add custom tags starting with `volc:` in any letter case.

* For tag design principles, see [Tag design principles](https://docs.byteplus.com/en/docs/ecs/Tag-design-principles).


<span id=".5qCH562-5L2_55So6K-05piO"></span>
## Tag usage instructions


* A tag consists of a tag\-key (Key) and a tag\-value (Value), both of which are case\-sensitive. Value can be empty.

* Keys of multiple tags for the same instance must be unique, and each Key can have only one Value.

* A single operation can add up to 20 tags. A single VPC resource can have a maximum of 50 tags.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures

<span id=".5re75Yqg5qCH562-"></span>
### Add tag

<span id=".5Yib5bu66LWE5rqQ5pe25re75Yqg5qCH562-"></span>
#### Add tags when creating resources

During creation, select or enter a tag key and tag value to add a tag.

<span id=".5Yib5bu66LWE5rqQ5ZCO5re75Yqg5qCH562-"></span>
#### Add tags after creating resources


1. Log in to the VPC resources console.

2. In the top menu bar, select the target project and region.

3. Click the name of target resource, then click the edit icon next to the tag.

4. Click the add icon to add new tags to the resource.

5. Select or enter the tag key and tag value for the new tag.

6. Click **Add** to complete the action.


<span id=".57yW6L6R5qCH562-"></span>
### Edit tags


1. Log in to the VPC resources console.

2. In the top menu bar, select the target project and region.

3. Click the name of target resource, then click the edit icon next to the tag.

4. Edit tag.

   * **Add tag**: In the pop\-up **Edit tag** dialog box, add new Tag Key and Tag Value.

   * **Modify tag**: In the pop\-up **Edit tag** dialog box, directly modify the Tag Key and Tag Value of the tag to be modified.

   * **Delete tag**: Click the delete icon on the right of the target tag.

5. Click **Save** to complete the action.


<span id=".6YCa6L-H5qCH562-5pCc57Si6LWE5rqQ"></span>
### Search resources by tags

<span id=".5pON5L2c6K-05piO"></span>
#### Action description


* Supports searching with multiple tags simultaneously. A maximum of 10 tags can be added in a single operation.

* If there are multiple tags in the search box, the relationship between the keys of these tags is logical `AND`. If the same key has multiple values, the relationship between these values is a logical `OR`.

* During a search, you can leave Value blank or empty. Leaving blank indicates no restrictions on Values; while an empty value indicates searching tags with empty Values.

* During a search, you can add up to three Values for a single Key.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Since different cloud resource instances can share the same tag key but have different tag values, you may encounter scenarios where multiple values are added for the same tag key during searches.   </div>
   

<span id=".5pON5L2c56S65L6L"></span>
#### Operation example

Search for cloud resource instances based on tags. Assume that the search conditions are as follows:

Tag 1: Keys: key1; Values: value1, value2.

Tag 2: Key: key2; Values: no specified values.

The cloud resource instances listed in the result must meet all of the following conditions:


* It contains both key1 and key2.

* For a tag with key1, its Value can be value1 or value2.

* For a tag with key2, its Value can be any value.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedures


1. Log in to the VPC resources console.

2. In the top menu bar, select the target project and region.

3. In the resource list, click the filter icon in the **Tag** column.

4. Select or type Keys and Values of tags.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can add up to 10 Keys and configure up to three Values for each Key in a search.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The relationship among the specified keys is logical <code>AND</code>, and the relationship among multiple values of the same key is logical <code>OR</code>.   </div>
   

5. Click **Apply** to search for target resources.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">IAM users do not have permission to use the tagging feature by default. For IAM users who need to use this feature, refer to <a href="https://docs.byteplus.com/en/docs/vpc/Example-of-custom-policy#hfn4hJt1">Authorizing the Use of VPC Tags</a> to add a custom policy and grant them the necessary permissions.</div>



* [TagResources](https://docs.byteplus.com/en/docs/vpc/TagResources)

* [UntagResources](https://docs.byteplus.com/en/docs/vpc/UntagResources)

* [ListTagsForResources](https://docs.byteplus.com/en/docs/vpc/ListTagsForResources)


&nbsp;

&nbsp;
