---
title: "Searching instances"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/searching_for_instances_in_batches"
---

This article introduces the steps and precautions for using the search function in the instance list.

<span id="background-information"></span>
## Background Information

RDS for MySQL provides a search function in the instance list, and supports searching for instances based on instance ID, instance name, and private network address as filter conditions. When no filtering conditions are specified, fuzzy matching is performed based on keywords, and search results based on keywords are provided under three conditions: instance ID, instance name, and private network address. The search function supports entering multiple keywords at the same time to search. Use English commas (,) to separate the keywords.

When there are multiple filtering conditions, the final result is the intersection of the search results under different filtering conditions; when there are multiple keywords under the same filtering condition, the final result is the union of the search results based on multiple keywords.

<span id="usage-restrictions"></span>
## Usage restrictions


* Supports up to 50 keywords.

* The maximum length of a single keyword is 128 characters.

* Keywords cannot contain (%), (\*) or (').

* Supports searching for instances through any private network address of multiple connected terminals to the instance, but only the private network address of the default terminal is displayed in the instance list.

* When entering the instance list, the browser will cache the instance list information. If you modify the instance information after entering the instance list, you need to refresh the instance list page to update the cache and obtain accurate search prompts when searching.

* When the search keyword matches the instance name of an instance with the same name, only one prompt option will be displayed.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>All resources</strong> at this step.</div>



3. Click the search box on the right side of the instance list. The three search scopes of instance ID, instance name, and private network address will be displayed below the search box.

   * You can directly enter keywords in the search box to search. At this time, search matching will be performed in three scopes at the same time.

   * You can first select a range and then enter keywords to search. At this time, the search will be matched only in the selected range according to the keywords.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During the process of entering keywords, the search function will continue to perform fuzzy matching on the entered content and display the matching results below the search box. At this time, up to ten matching results will be displayed under each search scope. After the keyword input is completed (press Enter), the keywords and filtering conditions will be displayed below the search box (when there is matching content for the entered keywords, the first filtering condition will be identified according to the association) Search), and display all instances that match the keyword matching results in the instance list.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keywords can be entered continuously, and multiple keywords are separated by (,).   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Use the arrow keys (↑ and ↓) to select among the matching results and press Enter to confirm.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Entered keywords can be cleared by pressing the ESC key.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to clear the filter conditions, click the <strong>Clear</strong> button under the clear search box.   </div>
