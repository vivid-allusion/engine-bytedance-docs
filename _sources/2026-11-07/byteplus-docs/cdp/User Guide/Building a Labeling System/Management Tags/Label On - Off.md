---
title: "Label On/Off"
product: "BytePlus CDP"
product_code: "cdp"
source: "https://docs.byteplus.com/en/docs/cdp/Label_On_Off"
---

<span id="_1-功能概述"></span>
# 1. **Function Overview**

Support administrators to perform "tag on" and "tag off" operations, controlling the usage status of tags. Tags that are "on" can perform computations and updates normally, available for downstream tasks and applications; tags that are "off" are temporarily considered invalid, interrupting task updates, not available for downstream calls, but with the possibility of recovery.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This feature is an add\-on module. If you want to experience it, please contact the BytePlus business team.</div>


<span id="_2-功能介绍"></span>
# 2. Function Introduction

<span id="_2-1-流程图"></span>
## 2.1 Process Flow

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8c979734a64099e513606eed96b4335.png) </span>

<span id="_2-2-标签状态"></span>
## 2.2 Label Status


| |Definition of Terms |
|---|---|
|Draft |Only metadata (name, rules, etc.) is saved without calculating data, which is not available downstream. |
|Online |Support manual or automatic data updates that downstream can be used for various applications such as selection, insights, asset output, etc. |
|Offline |Label temporarily paused. If the label has downstream impacts affecting downstream data (such as tags, segments), interrupt the update task and allow recovery. |
|Deleted |Label\-related metadata cleared, cannot be used, and cannot be recovered. If the label has downstream impacts, it interrupts downstream data (such as tags, segments) update tasks. |


<span id="_3-使用限制"></span>
# 3. **Usage Restriction**

Project administrators need to enable the Tag On/Off permission for corresponding users in Project Cen**Tag On/Off permission for corresponding users in Project Center\-Permissions\-Modules**. Once enabled, users can use this function.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_56da6ec301fe30c6491c8d13e5e8d4e0.png) </span>

<span id="_4-功能说明"></span>
# 4. **Function Description**

<span id="_4-1-上架标签"></span>
## 4.1 Label On\-Shelf

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Label Status: Online, supports manual or automatic data updates that downstream can be used for various applications such as selection, insights, asset output, etc.</div>


2. <div data-tips="true" data-tips-type="tip">Target User: Users managing the label system</div>


3. <div data-tips="true" data-tips-type="tip">Required User Permissions: (1) Module Permissions \- Labels [Label Display] (2) Specify Label Resources \- View Permissions</div>



After the user [creates a label](https://www.volcengine.com/docs/7139/191741), the label is initially in draft status, at this point, the label only saves metadata (name, rules, etc.), does not perform any tasks, and does not support downstream usage. Therefore, users managing the label system also need to manually put the labels on the shelf so that the labels can be used normally.

This process is enabled by default, and companies can also choose to disable it to skip this process. If this process is disabled, when a user creates a label, the label will automatically default to the on\-shelf status.


| |Operation Instructions |Schematic |
|---|---|---|
|Single shelving |Shelving entrance one:<br><br>In **Labeling System \> Draft/Offline**, click on 'More' on the right side of the label, click the **Shelf** button. After confirming the shelving, the label will begin the update task. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9c5fc02d6e4b3e1b2665f3d7c84592e2.png) </span> |
||Shelving entrance two:<br><br>In **Label Management \> Draft/Offline**, click on 'More' on the right side of the label, click the **Shelf Label** button. After confirming the shelving, the label will begin the update task. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_58d2bf550ff15c7a520d0c2e1c3dff3b.png) </span> |
|Batch shelving |In **Label Management \> Draft/Offline**, select the labels that need to be shelved, click the **Batch Shelve** button at the bottom. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6fac3a9d479beda47d9555d331fc8fac.png) </span> |


**On\-shelf status display:** 

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8414ea5e97f7fca226c8f2cddc67e59b.png) </span>

<span id="_4-2-下架标签"></span>
## 4.2 Off\-shelf Tags

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Label Status: Offline. The label is temporarily not in use. If the label has downstream effects, it may interrupt downstream data (such as labels, segments) update tasks. Restoration is allowed.</div>


   1. <div data-tips="true" data-tips-type="tip">Downstream cannot use this label for label creation, segment selection, analytical insights, and related API calls, and it will no longer be updated.</div>


   2. <div data-tips="true" data-tips-type="tip">Downstream associated resources (tags, segments) are interrupted from updates when the rule includes this off\-shelf tag. They can be restored after being put back on the shelf.</div>


2. <div data-tips="true" data-tips-type="tip">Target users: users managing the label system</div>


3. <div data-tips="true" data-tips-type="tip">Operational user permissions required: (1) Module Permissions \- Labels [Label On/Off\-shelf] (2) Specified Label Resources \- View Permissions</div>


1. Operation Instructions:



| |Operation Instructions |Illustration |
|---|---|---|
|Single Off\-shelf |In **Label Management \> On Shelf**, click on "More" on the right side of the label, then click on **Off\-shelf tag** button. After confirming the off\-shelf action, the label will no longer perform tasks. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_613c542ede14eb103ed932657d411efc.png) </span> |
|Batch Off\-shelf |In **Label Management \> On Shelf**, select the labels that need to be off\-shelf, then click the **Batch Off\-shelf** button at the bottom. |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f1940f456a8e6ff0b06c4f6ebfa8b43f.png) </span> |



2. Display of Off\-Shelf Status:


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_664d75bc057bfcfe9be1a55889771371.png) </span>

<span id="_4-3-删除标签"></span>
## 4.3 Delete Tag

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



1. <div data-tips="true" data-tips-type="tip">Label Status: Deleted. The label's related metadata is cleared and cannot be recovered or used. If this tag has downstream impact, it will interrupt downstream data (such as tags, segments) update tasks.</div>


2. <div data-tips="true" data-tips-type="tip">User Type: Users who manage the labeling system</div>


3. <div data-tips="true" data-tips-type="tip">Required User Permissions: Specify label resources \- manage permissions</div>



In **Label Management**, click more on the right side of the tag, scroll down, click the **Delete Tag** button, and confirm deletion.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f68e6b910d052de9232a5f847d345c3.png) </span>
