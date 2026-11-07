---
title: "Disassociating a tag"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/disassociating_a_tag"
---

After associating a tag with a specified instance, you can disassociate the instance tag at any time according to business needs. This topic describes how to disassociate tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can disassociate 20 tags at the maximum from instances at a time.</div>


<span id="disassociating-a-tag-for-one-instance"></span>
## Disassociating a tag for one instance


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. In the left navigation bar, choose **MySQL** \> **Instance list**.

4. Find the target MySQL instance on the **Instance list** page, and click **Edit** in the corresponding **Tag** column. Alternatively, click on the name of the target instance and click on the edit icon in the **Basic information** \> **Tag** row.

5. In the pop\-up **Edit tag** window, find the specified tag key, and click **Delete**.

6. Click **OK**.


<span id="disassociating-tags-in-batches"></span>
## Disassociating tags in batches


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. Select the region for the instance in the top menu bar.

3. In the left navigation bar, choose **MySQL** \> **Instance list**.

4. In the **Instance list**, select all instances that need tag setting, and then click  **...** \>**Remove tag** in the lower\-left of the page.

5. Select the tag key to be deleted from the drop\-down list in the pop\-up **Remove tag** window, or enter the tag key to filter.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page can display the number of selected instances corresponding to the specified tag, that is, how many instances in the list of selected instances are associated with the tag key. When you disassociate tags, all tags corresponding to the specified tag keys in the selected instance list are disassociated, and the tags of instances not in the selected list don't need to be adjusted.   </div>
   

6. Click **OK**.
