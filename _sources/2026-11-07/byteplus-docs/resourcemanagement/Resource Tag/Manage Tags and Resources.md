---
title: "Manage Tags and Resources"
product: "Byteplus Resource Management"
product_code: "resourcemanagement"
source: "https://docs.byteplus.com/en/docs/resourcemanagement/Manage_Tags_and_Resources"
---

You can view tags, filter resources by tag, and manage tags on resources using the methods described in this topic.

<span id="using-the-tag-management-feature-of-the-resource-management-console"></span>
## **Using the tag management feature of the resource management console**

By using the tag management feature of the resource management console, you can batch manage tags for resources under multiple services in multiple regions.

<span id="creating-custom-tags"></span>
### Creating custom tags


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Click Create tag, enter one or more key\-value pairs, and press the Enter key.

3. Click Add tag to specify additional key\-value pairs. Up to 10 pairs are supported.

4. Click OK to complete the tag creation.


<span id="viewing-all-tags"></span>
### Viewing all tags


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Tags are divided into custom tags and system tags. You can switch between the categories to view the details.

3. You can search for the required tags by tag key.


<span id="viewing-all-resources-attached-to-tag"></span>
### Viewing all resources attached to tag


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Select a tag and click the displayed number of attached resources.

3. View the information about the resources attached to the tag.

4. You can filter resources by region, resource type, and resource ID.

> If you need to attach resources to or detach resources from tags, refer to "Attaching resource to tag" and "Detaching resource from tag".


<span id="deleting-custom-tag"></span>
### Deleting custom tag


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Select the tag you want to delete and click Delete in the Actions column.

3. Click OK to delete the tag.

4. You can also select multiple tags for batch deletion.

> Note that system tags and custom tags attached to resources cannot be deleted directly.


<span id="attaching-resource-to-tag"></span>
### Attaching resource to tag


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Select a custom tag and click Attach resource.

3. Select a region or a resource type to query the resources that can be attached.

4. Select the required resource.

5. Click Next to confirm the setting.

6. Click Next to view the result.


<span id="detaching-resource-from-tag"></span>
### Detaching resource from tag


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Select a custom tag and click Detach resource.

3. Select a region or a resource type to query the resources that can be detached.

4. Select the required resource.

5. Click Next to confirm the setting.

6. Click Next to view the result.


<span id="querying-resource-by-tag"></span>
### Querying resource by tag


1. Log in to [Tag management > Resource](https://console.byteplus.com/resourcemanager/tag/resource_tag).

2. Filter resources by region and resource type.

3. Further filter resources by tag, resource ID, and resource name.

4. Complete the query.


<span id="attaching-tag-to-resource"></span>
### Attaching tag to resource


1. Log in to [Tag management > Resource](https://console.byteplus.com/resourcemanager/tag/resource_tag).

2. Select the required resource and click Attach tag.

3. Enter one or more unique key\-value pairs. Up to 10 pairs are supported.

4. Click Next to confirm the setting.

5. Click Next to view the result.


<span id="detaching-tag-from-resource"></span>
### Detaching tag from resource


1. Log in to [Tag management > Resource](https://console.byteplus.com/resourcemanager/tag/resource_tag).

2. Select the required resource and click Detach tag.

3. Select one or more tags to be detached. You can check the scope of resources to be affected by the detachment operation.

4. Click Next to confirm the setting.

5. Click Next to view the result.


<span id="downloading-tag-list"></span>
### Downloading tag list


1. Log in to [Tag management > Tags](https://console.byteplus.com/resourcemanager/tag/list).

2. Click the Download icon to download the tag list.


&nbsp;

<span id="using-cloud-service-console"></span>
## **Using cloud service console**

In a cloud service console, you can perform tag management on resources under the specified service. This section takes Elastic IP Address (EIP) as an example. The procedures are similar across the consoles of different cloud services. For more information, refer to the corresponding documentation. If you encounter any problems, submit a work order.

<span id="attaching-tag-when-creating-resource"></span>
### Attaching tag when creating resource


1. Log in to a cloud service console, such as the [EIP console](https://console.byteplus.com/eip).

2. On the top navigation bar, select a region where you want to create the resource.

3. Click Create to go to the resource creation page, enter the tag information, and complete the resource creation.


<span id="editing-tag-for-created-resource"></span>
### Editing **tag** for created resource


1. Log in to a cloud service console, such as the [EIP console](https://console.byteplus.com/eip).

2. On the top navigation bar, select the region of the target resource.

3. In the cloud resource list, hover over the number in the Tag column of the resource and click Edit tag in the box that appears.

4. Create, edit, or delete tags.

5. Click OK.


<span id="querying-resource-by-tag"></span>
### Querying resource by tag


1. Log in to a cloud service console, such as the [EIP console](https://console.byteplus.com/eip).

2. On the top navigation bar, select the region of the target resource.

3. Set tag\-based filter conditions.

4. Click OK.
