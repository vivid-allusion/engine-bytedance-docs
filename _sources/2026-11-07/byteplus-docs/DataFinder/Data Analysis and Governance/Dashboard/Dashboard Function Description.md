---
title: "Dashboard Function Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Dashboard_Function_Description"
---

If you have "public space management permissions", you can create Dashboards in public or personal spaces.

If you don't have "public space management permission", you can only create Dashboards in your personal space.

Dashboard created in public space: After creation, it is visible to all members by default, and you can modify the viewing scope through the "Share" function.

Dashboard created in personal space: After creation, it is only visible to yourself by default. You can share the Dashboard with others for viewing (corresponding to viewing permissions) or collaborative editing (corresponding to editing permissions) through the "Share" function.

<span id="_1-新建看板"></span>
# Step 1 Create a new dashboard

After the Dashboard is created, it is only visible to yourself by default. You can share the Dashboard with others through the "Share" function (corresponding to viewing permissions) or collaborative editing (corresponding to editing permissions). If you need to create a folder that is visible to everyone in the public space, please contact your app administrator to open "Dashboard public space management permissions" for you.


* Entry 1: Created from the Dashboard directory, currently supports 2 Dashboard types

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/07efb2880007429bb5a97ea71dc90d69~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31873d9484a949d78e5beae52fa3fc6d~tplv-goo7wpa0wc-image.image) </span>

* Entry 2: Create from the Advanced Analytics page

   When you use advanced analysis and want to save the analysis results to a Dashboard board, you can click "Save to Dashboard" and choose to save to an existing Dashboard board or create a new one.

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/986565d4763842249f6d36562ca70898~tplv-goo7wpa0wc-image.image) </span>


<span id="_1-1-新版看板（支持编辑态）"></span>
## 1.1 New version of Dashboard (supports editing mode)

The new version of Dashboard: distinguish between Dashboard editing state and viewing state

<span id="_1-1-1-编辑看板"></span>
### 1.1.1 Editorial Dashboard

Click "Edit" to enter the Dashboard editing state (requiring editing permission of the current Dashboard). In the editing state, it supports modifying the name and description of the Dashboard; adding charts, modifying chart configuration, layout and data configuration, etc.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88e1a637e674499085ccb7d932497dc4~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c2c077b6ac24c1298fcbea5b12d2696~tplv-goo7wpa0wc-image.image) </span>


* **Add chart**

   * Click New Chart and select Analytics to create a chart.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7f99a9d628240cca29b96fdb75985ba~tplv-goo7wpa0wc-image.image) </span>

   * Click on the existing chart to support adding charts with editing rights in batches.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01122fb75f8946779088fce1ef257d8b~tplv-goo7wpa0wc-image.image) </span>

   * Click Add Text to edit rich text in the editor. At the same time, the text editing area on the right supports filling in remarks, hiding text titles, and borders.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4da7ec28f7e487a86f02851a4256c06~tplv-goo7wpa0wc-image.image) </span>

   * Click to embed the chart to support filling in the chart name and address; at the same time, the chart editing area on the right supports filling in remarks and hiding the head area.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09d7409a6c30482a876ff925a2684f3e~tplv-goo7wpa0wc-image.image) </span>

* **Chart action item**

   1. Each chart supports: editing, copying, deleting.

   2. Click the blue name to support closing the side chart configuration area.

   3. Chart configuration area, support editing chart name, remarks, switching chart type, etc.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09ba2bf256da4c5784bad379de96cf1e~tplv-goo7wpa0wc-image.image) </span>

* **Dashboard configuration area**

   Dashboard configuration area: Enter the "edit state" from the Dashboard or click any blank area in the edit state to evoke the Dashboard configuration area.

   1. Support for modifying the name, description, and layout of the Dashboard board.

   2. Layout: Supports four shortcut layouts and custom drag\-and\-drop sorting.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d76d0ec23b7d43859c7c8e92cf483a2d~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebb2ec935b7445828f95f0a86fad34a3~tplv-goo7wpa0wc-image.image) </span>

* **Data configuration area**

   Data Configuration Area: Supports replacing events, event attributes, and user attribute parameters of charts in the Dashboard board.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6debaed7e9ee4ea19a6e190505f0296a~tplv-goo7wpa0wc-image.image) </span>

   * Use scenario:

      Business A & B requires active user\-related metrics, which have the same calculation logic but use different events and attribute fields.

   * Scope of application:

      1. Only the full chart editing rights can be used for this function.

      2. Only replacement chart data for "Event Analysis, Conversion Analysis, Retention Analysis, Distribution Analysis, and User Lifecycle" is supported.

   * Applicable conditions:

      [Configuration Metrics] List of events and event attribute fields used by Dashboard charts. You can change existing events and event attributes to other events and event attributes.

      [Configuration Properties] List of user attributes or event public attribute fields used by Dashboard charts; user attributes/event public attributes of the same type (string, list, etc.) can be replaced with each other.

   * Common problem:

      1. Event attribute replacement range: The selection range of event attributes is influenced by the association of behavioral events. For example, replace the original event "page access" with "user registration"; then the original event association attribute "whether out\-of\-app access" can only be replaced from the association attribute of the event "user registration".

      2. Attribute type restrictions: The original attribute type is string, and the replacement attribute must also be of string type. Other types of properties do not currently support substitution.


<span id="_1-1-2-查看看板"></span>
### 1.1.2 View dashboard

View status in Dashboard, support adding filter criteria for single filter queries, and operate top area buttons such as Subscribe, Full Screen, etc.

View state does not support chart sorting and resizing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ff769296187447c9ccd8d2939375082~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-旧版看板"></span>
## 1.2 Old version of Dashboard

The old version of Dashboard: no viewing state and editing state page distinction, only editing permission distinction.

<span id="_1-2-1-新建图表"></span>
### 1.2.1 New Chart


* Add a chart from Dashboard.

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/400ac0361e6b4472ac5cd8d1239e6cb1~tplv-goo7wpa0wc-image.image) </span>

* Entry 2: Save the chart to Dashboard from the Advanced Analytics page

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/986565d4763842249f6d36562ca70898~tplv-goo7wpa0wc-image.image) </span>


<span id="_1-2-2-编辑图表"></span>
### 1.2.2 Edit Charts


* **Method 1** : You can click on the chart name to jump to Advanced Analysis, re\-edit the chart configuration and save it to Dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50a5cdfef2884525b70926b0e5dd6213~tplv-goo7wpa0wc-image.image) </span>

* **Method 2** : Users with chart editing permissions can select  **· · ·**  \> **Edit chart** in the upper right corner of Dashboard, jump to Advanced Analysis, re\-edit chart configuration and save to Dashboard.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91c65fe30d9444958b0bc770638dfed1~tplv-goo7wpa0wc-image.image) </span>


<span id="_1-2-3-切换图表类型"></span>
### 1.2.3 Switch Chart Type

You can switch between chart types while viewing the Dashboard board, such as a line chart to a table. Switching the chart type doesn't change the configuration, and it will revert to the default type the next time you open Dashboard.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1109f19660dd42689f493c3e2e3b8687~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-4-删除图表"></span>
### 1.2.4 Delete Chart

If you have edit permissions to the current Dashboard board, you can delete the charts in it. After the chart is deleted, it cannot be retrieved. Please proceed with caution.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6322b963d0b46fcbbc3be7730697157~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-5-下载图表数据"></span>
### 1.2.5 Download Chart data

If you need to get the original data source in the chart, you can click "Download Data" to get the excel document.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/151b85547ebd4b9a9e1f20748b67134e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-看板目录-权限功能"></span>
# 2. Dashboard Directory & Permissions Function

<span id="_2-1-查找看板"></span>
## 2.1 Finding Dashboard

You can search for Dashboard by searching for the Dashboard/Folder keyword.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90918bc701764fe49d95ba18f354eff9~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-过滤看板"></span>
## 2.2 Filtering Dashboard

You can filter Dashboard by My creation, My collection, and share with me.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88e5ef5cc2f740c5a0e71784477d812d~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-收藏看板或文件夹"></span>
## 2.3 Favorite Dashboard or Folder

You can click "Favorites" to collect the Dashboard or folder, and click again after collecting to cancel the collection.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9de2080c29f1449998cafda5e5a4d3c6~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-4-复制看板"></span>
## 2.4 Copy Dashboard

You can copy a Dashboard board that you have permission to edit.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">In order to prevent abuse of the copy Dashboard function, each user can only copy Dashboard once across applications/projects within 30s. When copying for the second time within 30s, the page will prompt the <strong>batch copy Dashboard reaches the number of times limit, please try again later</strong> .</div>


Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cac85a052b034f30a1b9e21d1aa8ab2f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-5-分享-授权看板与图表"></span>
## 2.5 Share/Authorize Dashboard and Charts

According to different permissions, Dashboard users are divided into owners, editors, and viewers.

Users with edit privileges can authorize others to view/edit the board, as well as to edit charts.


* Dashboard:

   * The owner is usually the Dashboard creator, who has the highest privileges of the current Dashboard and can modify or delete it. The Dashboard owner can set who can authorize the current Dashboard, and can choose only the owner, the editor, and the viewer.

   * Editors can co\-edit the current board with the owner, and can add or modify charts in the board.

   * Viewers can only view the content of the Dashboard board and cannot modify it.

* Chart:

   * The chart owner has the highest authority on the chart and can modify or delete the board.

   * There is at least one chart editing permission user in the current Dashboard board, which can grant chart permission to others for editing operations.


Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ce02878ab6c4d9ab6155eca1d15451e~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-6-调整目录排序"></span>
## 2.6 Adjust directory sorting

You can drag Dashboard or folders in the Dashboard personal space directory to adjust the order. After adjustment, it will only affect your own directory sorting and will not take effect on other users. Dashboard public space directory order is administrator\-only.

<span id="_2-7-删除看板"></span>
## 2.7 Delete the board

Dashboard owners can delete Dashboards, but non\-owners cannot. Attention: Dashboard cannot be retrieved after being deleted.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8642a39dd1124760a72e6f255fbb74d1~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-看板文件夹功能"></span>
# 3. Dashboard folder function

<span id="_3-1-新建文件夹"></span>
## 3.1 New Folder

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you need to create a folder that is visible to everyone in the public space, please contact your app administrator to open "Dashboard public space management permissions" for you.</div>



* Entry 1: Create from the Dashboard directory

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cb1054570c6414cbaaffe70272132ee~tplv-goo7wpa0wc-image.image) </span>

* Entry 2: Create from the Advanced Analysis page

   Operation diagram:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6eab11341f934bc4bd04ebc23324239c~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-2-编辑文件夹"></span>
## 3.2 Edit Folder

If you are the folder owner, you can modify the name, directory, and transfer ownership by editing the folder.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45bb82d68d274663a1a8b26f85299aab~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-分享-授权文件夹"></span>
## 3.3 Share/Authorize Folders

You can authorize the Dashboard package by authorizing the folder. Users who are granted folder permissions will have permissions to all Dashboards and subfolders in the folder.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b8ed1fb2ee141e789c970d0df73d2ce~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-看板顶部操作区"></span>
# 4. Dashboard top operation area

<span id="_4-1-看板筛选条件配置（全局过滤器）"></span>
## 4.1 Dashboard Filter Configuration (Global Filter)

You can configure Dashboard global filter criteria to apply to all charts in Dashboard to improve filtering efficiency.

Current filter support: attribute filtering, add control group, modify time range.


* Attribute filtering: Support event public attributes, non\-public attributes, user attributes, and user grouping.

* Control group: Only 1 new control group is supported and applied to all charts.

* Time Range: Supports hourly, heavenly, and weekly granularity and applies to all charts.


Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e80e0d78776425787d5f273842e7a5a~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For ease of selection, the Finder divides event properties into two cases: <code>public event properties</code>and <code>non-public event properties</code>. The <code>public event attribute</code>is the attribute reported by each event in the Dashboard board, and the rest will be classified into the <code>non-public event attribute</code>.</div>


<span id="_4-2-看板全屏模式"></span>
## 4.2 Dashboard full screen mode

You can view the board in full\-screen mode, which hides the left table of contents and top navigation of the board, allowing you to focus more on the chart itself. After entering full screen mode, click the ESC button to exit full screen.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/723d4f09140045a78f270c4a37abfddb~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-3-刷新看板数据"></span>
## 4.3 Refresh Dashboard data

If you need to refresh the board to get the latest data results, you can click the refresh button at the top of the board.

Operation diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a2c570460ff4039aff28d0141731e40~tplv-goo7wpa0wc-image.image) </span>

<span id="_4-4-下载png"></span>
## 4.4 Download PNG

Dashboard supports downloading the current page display data into PNG format.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This function requires the page to load before it can be used.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8de49c338c71425eaeb70dde5dddec59~tplv-goo7wpa0wc-image.image) </span>
