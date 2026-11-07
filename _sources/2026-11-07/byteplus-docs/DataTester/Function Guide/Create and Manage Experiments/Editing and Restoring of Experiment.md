---
title: "Editing and Restoring of Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Editing-and-Restoring-of-Experiment"
---

DataTester provides you with management operations such as experimental editing, modification, and startup and shutdown. It has introduced the relevant operation instructions for debugging and startup and shutdown of the experiment in each created experimental document. This article introduces the relevant operation points of experimental editing and restore for you.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The privatized 4.9.2 version starts to support modifying the experimental parameters of the MAB experiment in debugging/in progress/in suspension, and supports custom cold start flow and number of rounds in the custom configuration. The operation entrance is also the experimental edit button.</div>


<span id="5e744566"></span>
# Experimental editing (reduction)

After the experiment is successfully created, you can click the Edit button in the upper right corner of the experiment details page to edit and modify the experiment.


* For experimental traffic: You can reduce the experimental traffic (i.e. shrinkage) or increase the experimental traffic according to the actual business situation. The following are the key points for you to focus on the operation of shrinkage.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Running and pausing the shrinkage to a high\-risk operation will cause the user to leave the group, and affect the scientificity of the report, resulting in the unavailability of the experimental report data. Please operate with caution.   </div>
   

* The modification configuration of other parameters is consistent with the main points when creating the experiment.

1. Once logged in to the experiment details page, click the Edit button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b16510b6ef7149ff9760496ef1769a7e~tplv-goo7wpa0wc-image.image) </span>

2. On the experimental editing page, you can adjust the parameters for each experiment. If you modify the experimental traffic:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6373cbe37a24e7785af8dc26f3e3f11~tplv-goo7wpa0wc-image.image) </span>

   * If you modify the experimental traffic: the original experimental traffic will be increased or decreased, and after the increase or decrease, the experimental traffic ratio of the experimental version and the control version will be consistent with the results of the experimental configuration.

   * If you reduce the experimental traffic: You need to evaluate whether the experimental shrinkage will affect the accuracy of the experimental report according to the interface prompts, and then proceed to follow\-up operations after confirmation.

   * After modifying the experimental traffic, the modified data can be viewed on the same day as the number of people entering the group and the real\-time indicator data; the changed result data can only be seen on the next day for offline indicator data.


<span id="f30ad4fc"></span>
# Experiment restore

<span id="12b23b34"></span>
### Precautions


* After the experiment is stopped, the experiment can be restored **within 24 hours**.

* The person in charge of the experiment or the administrator can restore the experiment.


<span id="e168627c"></span>
### Operating instructions


1. Log in and go to the stopped experiment details page, click **More** \> **Restore experiment** in the upper right corner.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ab136bfface4896893269ca08f99bd7~tplv-goo7wpa0wc-image.image) </span>

2. Click Confirm in the pop\-up window to restore the experiment immediately.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/446251ed6b7d47e6ac38897835df20fb~tplv-goo7wpa0wc-image.image) </span>
