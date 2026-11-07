---
title: "Viewing instance list"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_instance_list"
---

The instance list displays the basic information of all instances under the primary account. By viewing the instance list, you can have a preliminary understanding of the information of all instances. This article describes the steps to view the instance list.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The instance list displays information about the HBase instance, including the instance name/ID, running status, availability zone, private network, number of RS nodes, used space, billing type, storage type, service type/version, tags, creation time, project, and supported operations.

The **Actions** column of the instance list provides shortcuts to the following operations:


* [Restarting instances](https://docs.byteplus.com/en/docs/HBase/Restarting_instances)

* [Adding or removing nodes](https://docs.byteplus.com/en/docs/HBase/Adding_or_removing_nodes)

* [Deleting or unsubscribing an instance](https://docs.byteplus.com/en/docs/HBase/Deleting_or_unsubscribing_an_instance)

* [Switching to yearly or monthly subscription](https://docs.byteplus.com/en/docs/HBase/Switching_to_yearly_or_monthly_subscription)

* [Renewal management](https://docs.byteplus.com/en/docs/HBase/Renewal_management)


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Instances** on the left navigation bar to view the instance list.

4. (Optional) Customize the display column of the instance list. Click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ad31d166c8d6a2f8b75e8a2fbdcd2298.jpg)<sub> </sub></span> icon in the upper right corner of the instance list to customize the display of the columns in the instance list. Except for the **Instance name/ID** and **Actions** columns, the remaining columns can be customized to display.


<span id=".5pCc57Si5a6e5L6L"></span>
## Searching instances

Table Storage for HBase provides a search function in the instance list, supporting instance ID and instance name as filter conditions for searching for instances. If no filter conditions are specified, fuzzy matching is performed based on the entered keyword, and all search results containing the keyword are displayed by instance ID and instance name. When searching using these two filter conditions at the same time, the final search results are the **intersection** of the keywords under the two filter conditions. The specific usage is as follows:


* During the process of entering keywords, the search function will continue to perform fuzzy matching on the entered content and display the matching results below the search box.

* After selecting the instance ID or instance name filter, enter a keyword to search. This will search and match only within the selected scope based on the keyword.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">During keyword input, the search function will continue to perform fuzzy matching on the input content and display the matching results below the search box. At this time, a maximum of 10 matching results will be displayed under each search scope.</div>


* <div data-tips="true" data-tips-type="tip">Enter a keyword and press Enter. The filter conditions and corresponding keywords will be displayed below the search box, and all instances that match the keyword will be displayed in the instance list. When there are multiple matching contents for the input keyword, the search will be performed according to the first filter condition of the identification association; if there is no matching content, the search will be performed according to the instance name.</div>


* <div data-tips="true" data-tips-type="tip">Use the arrow keys (↑ and ↓) to select among the matching results and press Enter to confirm.</div>


* <div data-tips="true" data-tips-type="tip">Entered keywords can be cleared by pressing the ESC key.</div>


* <div data-tips="true" data-tips-type="tip">If you need to clear the filter conditions, click the <strong>Clear</strong> button under the clear search box.</div>



<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeDBInstances](https://docs.byteplus.com/en/docs/HBase/DescribeDBInstances) |Call the DescribeDBInstances interface to query the HBase instance list. |
