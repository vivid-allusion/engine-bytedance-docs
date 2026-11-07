---
title: "Dashboard Version Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Dashboard_Version_Management"
---

<span id="_1-概述"></span>
# Overview

DataWind dashboards support version management. After enabling version management, saving a dashboard is divided into two steps: "Save" and "Publish." Each time you save, a historical version is stored. Up to three versions can be saved, and saved versions support rollback.

**Caution: The version publishing feature is enabled at the project level. Once enabled, it cannot be reverted to real\-time publishing.** 

**Applicable scenarios:** 


* To control dashboard publishing and prevent incidents caused by accidentally saving and publishing changes that are only partially complete

* To prevent unintended operations, such as being unable to recover a dashboard after accidentally deleting a chart and then saving the dashboard


<span id="b8d861ef"></span>
# Quick start

<span id="_2-1-开启版本发布功能"></span>
## Enable the version publishing feature

**Step 1:**  Go to the "Project Center" \- "Project Information" page and locate the "Dashboard Publishing Type" option

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f07f7650e57d49d48df1fae9c9e7792e~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Select "Version Publishing"


* **Caution: After switching the publishing type to "Version Publishing," you cannot switch back to "Real\-Time Publishing".** 


<span id="8f3b4b61"></span>
## Dashboard publishing and rollback

<span id="_2-2-1-仪表盘保存与发布"></span>
### Saving and publishing dashboards

**Step 1:**  After modifying the dashboard content, click the "Save" button in the upper right corner to save your current changes


* This save operation will not affect the live dashboard

* After saving and exiting the editing page, the next time you enter the dashboard editing page, the last saved content will be displayed


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40b3f3e271b04dbea44167d531f8fadd~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  When you have confirmed that the dashboard changes are correct and ready to be published, click "Save and Publish" in the upper right corner

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fc72558e166457f93624b5f59b7208a~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  Optionally enter a version description. A dashboard can save up to three historical versions. If there are already three versions, you can choose to delete a specific version when publishing

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7550068dea474cf9a1caa42d4e748bb3~tplv-goo7wpa0wc-image.image) </span>

**Step 4:**  After entering the version description, click Confirm to publish the current dashboard content. The dashboard content will then be published live

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b64f715f441348d6b2a14b6bff363f32~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-2-仪表盘回滚"></span>
### Dashboard rollback

**Step 1:**  Enter the dashboard editing page and click "Historical Versions" at the top

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98466527eae0427ba2c44ea7877a0dc2~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  In the expanded pop\-up window, the three most recent historical versions of the dashboard are displayed. The version with the release status marked as 'Published' is the current online version.

**Step 3:**  You can click the "Preview" button next to the version to view the dashboard content of that version.

**Step 4:**  To roll back to a historical version, confirm which version to revert to, then click "Rollback" to return to the corresponding historical version.

**Step 5:**  To publish the dashboard online, confirm the content is correct, then click "Save and Publish".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/76dfc9cbf603421eb58c4ca08e95fcaf~tplv-goo7wpa0wc-image.image) </span>

<span id="adc2657a"></span>
# 3. Feature overview

<span id="_3-1-版本发布开启入口"></span>
## 3.1 Entry point for enabling version publishing

"Project Center" \- "Project Information" \- "Dashboard Publishing Type"


* **Required permission:**  Project management permission

* **Caution: After switching the publishing type to "Version Publishing", it cannot be switched back to "Real\-time Publishing".** 


<span id="78515662"></span>
## 3.2 Version description

When publishing a dashboard, you can enter a version description. The version description can be modified by clicking it in the historical versions.

<span id="71b71ff4"></span>
## 3.3 Dashboard preview and sharing

The dashboard preview page supports sharing links. Other users can view the content of the preview page via the link.

Applicable scenario: After modifying the dashboard, users need to provide the current content to business stakeholders or LD for review before saving.

Operation steps: Click the expand button next to "Preview", select "Copy Preview Link", and other users can view the preview content via this link.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4050d82603c4839ae48ca846ee3324d~tplv-goo7wpa0wc-image.image) </span>

<span id="cd11457e"></span>
## 3.4 Dashboard editing cache


* When operating in the dashboard editing interface, the current dashboard editing content is cached locally in the browser every minute.

* In the event of an abnormal exit, such as a browser crash, when re\-entering the dashboard editing interface, a pop\-up reminder will appear, allowing you to restore the dashboard editor content from the cached version.


**Impact on each feature:** 

When the version release feature is enabled, if the current changes to the dashboard are only saved but not published, the online version and the latest saved version may differ, which will affect various features.

**Differences in content display for each feature:** 


|**Features** |**Whether the displayed content is the dashboard's most recently saved content or the currently published version** ||
|---|---|---|
||**Most recently saved content** |**Currently published version** |
|**Enter the dashboard editing page** |✅ | |
|**Enter the chart visualization page** |✅ | |
|**Subscription** | |✅ |
|**Monitoring** | |✅ |
|**Download** | |✅ |
|**Copy dashboard** |✅ | |
|**Chart management (redirects to visualization)**  |✅ | |
|**Monitoring management (redirects to visualization)**  |✅ | |
|**Metric broadcast (redirects to visualization)**  |✅ | |


**Viewing an unpublished dashboard:** 

After a dashboard is created but has not been published, other users who open the dashboard link will see the message: The dashboard has not been published.

**Resource import and export:** 


* **Real\-time** indicates a dashboard with the version release feature **disabled**.

* **Version** indicates a dashboard with the version release feature **enabled**.



|Real\-time |to |Real\-time |Export: Latest published version<br><br>Import: The content imported as a draft is the published version, which is considered already saved. |
|---|---|---|---|
|Version ||Real\-time ||
|Version ||Version |Export: Latest published version<br><br>Import: The content imported as a draft is the published version (after import, publishing is required). |
|Real\-time ||Version ||
