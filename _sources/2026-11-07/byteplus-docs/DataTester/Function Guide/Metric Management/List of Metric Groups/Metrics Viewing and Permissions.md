---
title: "Metrics Viewing and Permissions"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Metrics-Viewing-and-Permissions"
---

<span id="一、查看和修改指标"></span>
# 1. View and modify metrics

Entrance: Click on the metric group name on the list page to jump to the metric group details page to view.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df111fd0db9948b7b2b985f389eac6f3~tplv-goo7wpa0wc-image.image) </span>

<span id="查看："></span>
## Check:


* Basic information: Saved metric group information is echoed here.

   * Metric group name

   * Metric group description

   * Metric Group Category: Event/Retention/Funnel

   * Metric group leader (owner)

* Metric settings:

   * Check the calculation caliber: Click the drop\-down icon before the metric name to view the specific calculation caliber of the metric.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00c5d5ae14ce485ea46af8cc2de06ffb~tplv-goo7wpa0wc-image.image) </span>

   * View Correlation Experiments: The Correlation Experiments column will display the number of experiments that have been followed for this metric. Click on the number to view the specific experiments related to this metric.

      * By default, ongoing experiments are displayed, which can be viewed by filtering the experimental status in the experimental status column.

      * Support searching experiments by experiment name/experiment ID/experiment owner.

      * Clicking on the experiment name will jump to the experiment details page.

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8529d07c6e64d579afe378f9b300243~tplv-goo7wpa0wc-image.image) </span>

   * Sort by metric: drag and drop the sorting icon at the top of the list to move the order of metrics within the group (only metric owners & administrators can operate).


<span id="操作："></span>
## Operation:


* Copy the metric group: Click "Copy" in the upper right corner to copy all the configuration information and metric information of the metric group. The name of the new metric group will be named by "Original metric Group Name \- Copy" by default, and modification is supported.

* Edit metric group: Click Edit to enter the metric group editing state.

   * You can modify the name, description, and person in charge of the basic information of the metric group. The **metric group type does not support modification.** 

   * The name description and caliber setting of the index can be modified (refer to the above index modification for details).

* View operation history: Click on the operation history icon in the upper right corner to view the historical change information of the current metric group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f67ccbacedc34fdeae1467478ca16105~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8ce19fe43284f30bcb29f871b84e204~tplv-goo7wpa0wc-image.image) </span>

<span id="二、指标组权限管理"></span>
# 2. Metric group authority management


|Metric group permission type |Screenshot |Paraphrase |Remarks |
|---|---|---|---|
|Common metrics Group |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb25576983034639a13f4526650caab1~tplv-goo7wpa0wc-image.image) </span> |The metric group defaults to the "public metric group".<br><br>Users who have the viewing permission of the metric management module under the current application have by default \*\* "View metric group details permission" and "View metric statistical value permission" \*\*. In addition to the above two permissions, the administrator and metric owner of the current group's current application can also edit/up and down metric groups, user empowerment, etc.<br><br><br>> * View metric group details Permissions: View metric group details (metric caliber, operation history, etc.) |The group can access the application and has the permission to view/use the metric management module: as follows<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2921502b6163474882beffbc434051b7~tplv-goo7wpa0wc-image.image) </span> |
|Private metric group |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17ba42d8999e475c834b86f73caf77cb~tplv-goo7wpa0wc-image.image) </span> |Private metric group, the administrator of the current application and the owner of the metric group can give ordinary users "permission to view the details of the metric group". Users without any authorization cannot see the information of the current metric group in the metric group list (metrics in this metric group are not optional when starting an experiment, and the metric group is not displayed in the optional metric list).<br><br>Support for selecting roles and users as empowerment objects. If the user already belongs to a role and the role is also an authorized object of the current metric group, it will be determined by the maximum authority the user has. | |
