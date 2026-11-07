---
title: "Dashboard Comments"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Comments"
---

The dashboard comment feature allows users to add, view, and delete comments on charts in the dashboard, making it easier for users to collaborate in data\-driven scenarios. This document describes how to use the dashboard comment feature.

<span id="d65488f5"></span>
# Prerequisites


* **The comment feature** requires view or higher permissions for the dashboard.

* For the **comment notification** feature, it is necessary to complete the prerequisite configuration operations before comment notifications can be received.


<span id="_1-概述"></span>
# Feature overview

The product's dashboard supports adding comments to individual charts and viewing all comment information on the entire dashboard. This enables dashboard users to leave messages or record issues about the dashboard content at any time, serving as a collaboration tool for all data content users and meeting some collaboration needs in data\-driven scenarios.

<span id="_2-1-添加评论"></span>
# Add comments


1. On the dashboard view page, hover the mouse over the upper right corner of a chart to display the option to add a comment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/807cd87a7ec14628a29bd9919081e392~tplv-goo7wpa0wc-image.image) </span>

   V2.58.0 and later versions support commenting on points and cells in charts, available on both PC and mobile devices.

2. After clicking Add Comment, you will be redirected to the Add Comment page. A comment card will appear on the right. Enter your comment and click Send.

   * Comments support adding text and images.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51bf997db9214b998de9c9ef2585df43~tplv-goo7wpa0wc-image.image) </span>

3. You can click Add Comment in the upper right corner of the chart again on the Add Comment page to add more comments.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a43a865b1444d3fa57da6238f254362~tplv-goo7wpa0wc-image.image) </span>

4. You can also reply to comments.

5. After adding a comment, click the Return button in the upper right corner to go back to the view page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33e81d7f5b9846b9bdcf1d786c3e5edf~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-查看评论"></span>
# View comments


* If a chart has comments, an indicator will appear in the upper left corner of the chart, showing the number of comments. Click to go to the View Comments page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cbda3dab24940699278d6196f488e26~tplv-goo7wpa0wc-image.image) </span>

* If comments have been added, an Expand Comments button will appear on the right side of the dashboard. Click to go to the View Comments page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a42317329b284811aa563112c4f8b042~tplv-goo7wpa0wc-image.image) </span>

* For cell comments, you can move the mouse over the comment title to display a tooltip showing the dimensions and metric data for that cell at the time of the comment, making it easier for users to quickly locate the comment data.


<span id="_2-3-删除评论"></span>
# Delete comments


* On the comment viewing page, click "Mark as resolved and hide comment" in the upper right corner of the comment card to delete the comment.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2402be351d542f69543d9f3fd5827bf~tplv-goo7wpa0wc-image.image) </span>


<span id="4d34b2e9"></span>
# Comment notifications


* After a comment is added to a chart on the dashboard, the chart owner, dashboard owner, mentioned users, and replied users will all receive message notifications pushed by the message bot.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">You must follow the instructions in and complete the required steps before you can receive comment notifications.</div>



<span id="_2-6-关闭评论功能"></span>
# Disable the comment feature


* On the dashboard editing page, in the "Toolbar in view mode" section of the chart or page configuration, you can deselect the "Comment" option. After that, the comment option will no longer appear in the upper right corner of the corresponding chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/023d567b726d49189fc82d000ba67e19~tplv-goo7wpa0wc-image.image) </span>
