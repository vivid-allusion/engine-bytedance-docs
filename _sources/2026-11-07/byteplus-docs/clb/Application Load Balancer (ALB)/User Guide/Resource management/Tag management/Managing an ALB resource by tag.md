---
title: "Managing an ALB resource by tag"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/Using-tags-to-manage-ALB-resources"
---

You can set tags for Application Load Balancer (ALB) resources to group and manage them. Resources with the same tag form a group. You can search resources by tags.

<span id="356e4200"></span>
## Manage tags and resources on the Tags page

<span id="712ed296"></span>
### View a tag


1. Log in to [the Tags console](https://console.byteplus.com/resourcemanager/tag/list).

2. You can search for your target tags using keywords in the tag key.

3. Click the digit in the **Number Of tag resources** column to view all resources tagged with the current tag key and value.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can type the keyword of one tag key in the search bar at the top left to find a specific tag.</div>


<span id="4c871334"></span>
### Create a tag


1. Log in to [the Tags console](https://console.byteplus.com/resourcemanager/tag/list).

2. Click **Create tag** on the **Tags** page, and type the tag key and tag value as needed.

3. Click **OK** to complete the creation.


<span id="fbefa798"></span>
### Delete a tag

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">System tags do not support manual deletion.</div>


* <div data-tips="true" data-tips-type="tip">If a tag is associated with a resource, <a href="https://docs.byteplus.com/docs/clb/Using-tags-to-manage-ALB-resources#dc4ae0cd">untag the resources</a> before deleting the tag.</div>


1. Log in to [the Tags console](https://console.byteplus.com/resourcemanager/tag/list).

2. On the **Tags** page, locate your target tag, and click **Delete** in its **Actions** column.

3. Click **OK** to complete the deletion.


<span id="390791ff"></span>
### Tag a resource

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">System tags do not support manual association.</div>



1. Log in to [the Tags console](https://console.byteplus.com/resourcemanager/tag/list).

2. On the **Tags** page, locate your target tag, and click **TagResource** in its **Actions** column.

3. On the **TagResource** page, select the region and resource type.

4. Check the target resource, then click **Next**. After confirming the information is correct, click “Next”.

5. Click **OK**.


<span id="dc4ae0cd"></span>
### Untag a resource


1. Log in to [the Tags console](https://console.byteplus.com/resourcemanager/tag/list).

2. On the **Tags** page, locate your target tag, and click **UntagResource** in its **Actions** column.

3. On the **UntagResource** page, select the resource region and resource type.

4. Check the target resource, then click **Next**.

5. After confirming the information is correct, click **Next**.

6. Click **OK**.


<span id="c458ebba"></span>
## Manage tags and resources in the ALB console

The following uses an ALB instance as an example.

<span id="e6b986d9"></span>
### Add tags to an instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Elastic IP addresses (EIPs) on public ALB instances do not inherit instance tags.</div>


* <div data-tips="true" data-tips-type="tip">You can add up to 20 tags in a single action and a maximum of 50 tags for a single instance.</div>


* <div data-tips="true" data-tips-type="tip">ALB instances do not support manual addition of system tags.</div>



You can add tags to an instance either during or after its creation.

<span id="1df73e38"></span>
#### **Add tags during instance creation**

You can add tags to an instance during [instance creation](https://docs.byteplus.com/docs/clb/Creating-an-instance). When adding tags to an instance, you can add a new tag or select an existing one.


* Add a new tag: Type a new tag (including the tag key and tag value) in the tag list.

* Add an existing tag: Select one or more tags in use from the tag list.


<span id="e9301ff5"></span>
#### **Add tags after instance creation**

If you do not add tags when creating an instance, you can also add tags to it post\-creation based on this section.


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Instance**.

3. On the **Instance management** page, locate your target instance and click the edit icon in its **Tag** column.

4. On the **Edit tab** page, click **Add tags** to associate tags with the instance as needed.

   * Add a new tag: Type a new tag (including the tag key and tag value) in the tag list.

   * Add an existing tag: Select one or more tags in use from the tag list.

5. After confirming the tag information is correct, click **Save** to complete the tag addition.


<span id="0cd47c17"></span>
### Remove tags from an instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">System tags do not support manual deletion.</div>



1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Instance**.

4. Click the **edit** icon in the **Tag** column of the target instance.

5. Click the **delete** icon to the right of your target tag.

6. Click **Save** to complete the action.


<span id="c09ed899"></span>
### Filter instances by tags

After instances are tagged, you can search for instances by tags.


1. Log in to the [ALB console](https://console.byteplus.com/alb).

2. In the top menu bar, select the target project and region.

3. In the left\-side navigation pane, select **Instance**.

4. Click the **filter** icon next to the **Tag** column header.

5. Select or type the tag key. The system supports setting up to 10 tags. The system filters instances by tags using the following logic:

   1. Multiple tag values for a single tag key are combined with "or".

   2. Multiple tag keys are combined with "and".

6. After completing the tag selection, click Save. The console will display instances that meet the filter.
