---
title: "Tag configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/ecs-tag_configuration"
---

Tags are identifiers for clusters. Adding tags to clusters makes it easier to identify and manage your cluster resources. You can bind tags when creating a cluster, or bind tags on the cluster's Basic Information page after the cluster is created. You can bind up to ten tags to a cluster.

<span id="集群创建添加标签"></span>
## Add tags when creating a cluster

Create new tags or bind existing tags to the cluster during cluster creation.


1. Log in to the EMR console and click **Create cluster**.

2. Add tags in Step 3 Other Settings \- Advanced Settings.


Note:


* Tag key: Required. Length is 1–128 characters. Letters, numbers, spaces, and the symbols _ . : / = + \- @ are allowed; cannot start with `volc:` (case\-insensitive).

* Tag value: Optional. Length is 0–256 characters. Letters, numbers, spaces, and the symbols _ . : / = + \- @

* **Each tag key must be unique** to avoid ambiguity in certain scenarios. Tag keys cannot be duplicated.


<span id="管理集群标签"></span>
## Manage cluster tags

Create, bind, and unbind tags for clusters.


1. Log in to the [E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?). Click the target cluster to enter the cluster overview.

2. In the cluster information section, find Tags and click the edit icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5402440c240e40188f30c970798c6565~tplv-goo7wpa0wc-image.image) </span>

3. In the **Edit Tags** dialog box, manage the tags for the target cluster.

   1. Create a new tag

      1. Enter the tag key and tag value

      2. Click Add

      3. Click OK

   2. Unbind an existing tag

      Click the x icon after each tag in the tag bar to unbind that tag.


<span id="使用标签搜索集群"></span>
## Search clusters using tags

On the cluster list page, search for the target cluster by tag key and tag value.


1. Log in to the EMR console and go to the **cluster list**.

2. Select the tag key and tag value in the filter conditions at the top. The list below will display clusters that meet the search criteria.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If no specific tag key is selected, all clusters bound to that tag key are displayed by default.   </div>
