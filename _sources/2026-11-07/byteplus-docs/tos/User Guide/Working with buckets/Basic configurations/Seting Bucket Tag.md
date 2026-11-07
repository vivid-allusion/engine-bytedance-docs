---
title: "Seting Bucket Tag"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Set-bucket-tag"
---

Object storage supports tag management capabilities. Tags can be used to identify cloud resources and help you tag and classify buckets with the same characteristics from different dimensions (e.g., purpose, type, owner, environment, etc.) for easy management.

<span id="33cc82bb"></span>
## **Function introduction**

As the number of resources on the cloud continues to grow, so does the difficulty of managing them. BytePlus provides tag management capabilities for customizing and classifying Cloud as a Service resources from various dimensions, such as classifying cloud resources for different business categories, uses, or usage objects through tags. Object storage supports adding tags to buckets, i.e. tag management for bucket dimensions. A tag is a key\-value pair, including a tag key and a tag value. You can add multiple tags of different categories for each bucket, such as `region: Beijing`, `storageclass: standard`, etc. Each tag can also bind multiple buckets, for example, set the same tag `owner: Alice`for all buckets.

<span id="d625b6f3"></span>
## **Application scenario**

We recommend that you use the tag management function in the following scenarios.

**Billing and cost allocation**: ** ** If there is a need for cost allocation according to different organizations or departments in the business scenario, the classification management of cloud resources can be carried out through tags, and the same tag is set for cloud resources of the same organization or department. The cost of cloud resources is allocated to the corresponding organization or department at the time of regular settlement to achieve cost allocation management.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you delete the bucket or untie the tag from the bucket, the tag of the split bill will be empty, and you are advised to proceed with caution.</div>


<span id="44761f11"></span>
## **Tag setting rules**

Object storage tag setting rules are shown in the following table.


|**Restriction** |**Explain** |
|---|---|
|tag key |* UTF\-8 format characters, spaces, numbers, and the following special characters are supported: `_ .:/=+-@`<br><br>* The length of the tag key should be between 1 and 128 characters.<br><br>* Tag keys are case sensitive, such as `Type`and `type`are two different tag keys. |
|tag value |* UTF\-8 format characters, spaces, numbers, and the following special characters are supported: `_ .:/=+-@`<br><br>* Tag values are case sensitive, such as `Standard`and `standard`are two different tag values.<br><br>* The length of the tag key should be 0 to 256 characters, that is, the tag value can be empty. |
|other |* There is no limit to the total number of tags, but you can bind up to 50 tags per bucket.<br><br>* You can add multiple tags of different categories to each bucket, but tag keys for multiple tags under the same bucket cannot be repeated, and each tag key can have only one tag value.<br><br>* Tag information between different regions is not interoperable. For example, tags created in the North China 2 (Beijing) region are not visible in the East China 2 (Shanghai) region. |


<span id="f8419192"></span>
## Add a tag


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click the **Buckets** to enter the **Bucket tagging** page. The following two methods are supported:

   * On the bucket list page, hover over the tag icon under the target bucket **Tag** column and click the edit icon.

   * On the bucket list page, click the name of the target bucket and select **Basic Settings \> Tag Management** in the left navigation bar.

3. Click **Edit** , click **Add tag** , set tag key and tag value.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">tag key value needs to meet certain setting rules, specific rules, please refer to the <a href="https://www.volcengine.com/docs/6453/179074">tag setting rules </a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Click <strong>Add tag</strong> to add tags continuously, with up to 50 tags per bucket.   </div>
   

4. When the tag settings are complete, click **Save** .


<span id="47542e0b"></span>
## Delete a Tag


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click the **Buckets** to enter the **Bucket tagging** page. The following two methods are supported:

   * On the bucket list page, hover over the tag icon under the target bucket **Tag** column and click the edit icon.

   * On the bucket list page, click the name of the target bucket and select **Basic Settings \> Tag Management** in the left navigation bar.

3. Click **Edit** , click Target tag **Action** column **Delete** .

4. When the tag settings are complete, click **Save** .

   After removing the tag, you can untie the tag for the bucket.


<span id="e9daf0d8"></span>
## Modify tag


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click the **Buckets** to enter the **Bucket tagging** page. The following two methods are supported:

   * On the bucket list page, hover over the tag icon under the target bucket **Tag** column and click the edit icon.

   * On the bucket list page, click the name of the target bucket and select **Basic Settings \> Tag Management** in the left navigation bar.

3. Click **Edit** to modify the **Bucket tag key** and **Bucket tag value** .

4. When the tag settings are complete, click **Save** .
