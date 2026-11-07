---
title: "Microscope Function"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Microscope_Function"
---

DataFinder provides you with microscope functions, which can further drill\-down analysis of the queried charts. By clicking on a query result data, you can operate "New Date Annotation", "Save as User Group", "Export User ID", "View User List" and other analysis and annotation functions, which is convenient for in\-depth research and analysis of key data.

<span id="_2-功能显示"></span>
# Function introduction

<span id="_2-1-什么时候显示显微镜"></span>
## Evoke microscope function

When using DataFinder's analysis tool to query and analyze data, it will show you the result graph and detailed data table, and you can invoke the microscope function in the result graph.


|In the query result graph |In the query result detail data table |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f3af2f404544810b63cebfdd79271cd~tplv-goo7wpa0wc-image.image) </span><br><br>Click on the data in the chart to bring up the microscope function. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f26db77bc4a04740be0cb20df5f36c0e~tplv-goo7wpa0wc-image.image) </span><br><br>Click on the data in the data table to bring up the microscope function. |


<span id="304331ae"></span>
## Supported drill\-down analysis capabilities

After arousing the microscope, the following operations are mainly supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Most of the current DataFinder analysis tools support microscope functions (Bitable analysis, heat map analysis, business dimension analysis, etc.), but the support of microscope function segmentation capabilities is affected by factors such as the configuration of current analysis tools and the type of result charts. The actual support situation is subject to the product interface.</div>



|Segmentation capability |Function Description |Typical application scenarios |
|---|---|---|
|New Date Annotation |* When the horizontal axis in the query graph is'day\-level 'time, the display mirror function includes'create date annotation', otherwise there is no'create date annotation 'function item.<br><br>* When creating a date annotation, you can configure the visible range of the date annotation; after the date annotation is created, you can edit, delete, and other operations in the Project Center \> Date Annotations.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f74902a04f1c44d3a7362e630f6e9fa8~tplv-goo7wpa0wc-image.image) </span><br><br>* The date annotation function is mainly to annotate the line chart, stack chart, percentage chart, etc. of the query results. Other chart types and detailed data tables of the query results do not support the use of date annotation function. |When viewing the analysis result graph, if an outlier is found, the outlier data can be annotated with the creation date annotation. Users who have the permission to view the date annotation after the annotation can see the annotation and understand the cause of the data abnormality. |
|Save as user group |* **Statistical criteria are** only supported by **users**.<br><br>* Users circled by a query result can be saved directly as a user subgroup. |For example, after querying the client base of an event through event analysis, the user is stored as a user subgroup, which can directly perform retention analysis and conversion analysis on the corresponding user subgroups to improve analysis efficiency. |
|Export user ID |* The user selected by a query result can be directly downloaded to the local user ID.<br><br>* **When the statistical criteria** is a **user** , the user ID that supports export includes multiple user ID criteria data such as supported uuid, ssid, and did.<br><br>* **When the statistical criteria** is not a **user** , it supports exporting the corresponding subject ID.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e49af0e89a5a4731817480db44c0e9f9~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning"><strong>The derived user ID</strong> refers to the user ID of the crowd in the event circle, not the user in the operator circle. For example, in the configuration of the event analysis tool, when the event calculation operator selects "press... to find the maximum value", "press... to find the minimum value", and "press... to find the percentiles", the user exported by the microscope is still the person circled by the event, not the person corresponding to the maximum value, minimum value, and a certain percentile.</div><br> ||
|View user list |* **Statistical criteria are** only supported by **users**.<br><br>* Support to view the list of selected users, and display the user ID and user\-related attribute values of the corresponding user.<br><br>* Support saving the user list as a user group, or check the corresponding attribute value to download the user list information locally.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa3d704c6857459a8013c0e7077db645~tplv-goo7wpa0wc-image.image) </span> ||
|Other features |The user path analysis tool, after evoking the microscope function, also supports adding attribute grouping, not analyzing the node, and temporarily hidden segmentation functions.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74e54a6bb09f4eb284d56038a5861f20~tplv-goo7wpa0wc-image.image) </span> ||


<span id="_2-2-哪些功能页面、哪些图表支持显微镜哪些功能"></span>
## Microscope function example

<span id="_2-2-1-事件分析"></span>
### Event Analysis


* Event analysis, sky\-level line chart, click the point on the line, support "microscope" function (new date annotation, save as user group, export user ID, view user list);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a0274fbd6ef4c4a9cc68d1691090f52~tplv-goo7wpa0wc-image.image) </span>

* Event analysis combination indicator, sky\-level line chart, click the point on the line, support "microscope" function (Create date annotation);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80c9b90c022048f1ad95e90605f43222~tplv-goo7wpa0wc-image.image) </span>

* Event analysis \- stack chart, click on the point on the stack chart, support "microscope" function (new date annotation, save as user group, export user ID, view sample);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/861443fd90ee491798f41933ce5f90ba~tplv-goo7wpa0wc-image.image) </span>

* Event analysis \- column chart, click the column chart to support the "microscope" function (save as user group, export user ID, view user list);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/635a0de80a154dd78050934fe9b6ddac~tplv-goo7wpa0wc-image.image) </span>

* Event analysis \- table, click the number in the table, support "microscope" function (save as user group, export user ID, view user list);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8556c815fc9d42efbf80b522f160a032~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-2-留存分析"></span>
### Custom Retention


* Retention analysis \- trend analysis. When "specific time" is selected, click the dot on the polyline to support the "microscope" function (save as user group, export user ID, view user list);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/effb97bd8c4f4b04b77fc282a36d1f06~tplv-goo7wpa0wc-image.image) </span>

* Retention Analysis \- Trend Analysis. When "Overall Retention Trend" is selected, click the dot on the polyline to not display the'Microscope 'function. (Because it is of no practical significance at this moment.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac2762cf9a814b26b170bbd3503935bf~tplv-goo7wpa0wc-image.image) </span>

* Retention analysis \- Retention comparison, both support microscopy (new date annotation, save as user grouping, export users, view samples).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7810f64f313542079c1004944628f62a~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-3-转化分析"></span>
### Funnel Analysis


* Column chart, support "microscope" function (save as user group, export user ID, view user list);

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b40078b949b40a0920b67a9b754e0f0~tplv-goo7wpa0wc-image.image) </span>

* Funnel chart, support "microscope" function (save as user group, export user ID, view user list).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb49487b02bc4a84af469557b37e7a98~tplv-goo7wpa0wc-image.image) </span>


<span id="b486b299"></span>
### Distribution Analysis

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f70cc52adaa14dd98fe57f422dfeeb5f~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-4-成分分析"></span>
### User Composition


* When the ring image is used, the microscope function is supported (save as user group, export user ID, view user list).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a774ba14e9884a81b957eeb0570e4a26~tplv-goo7wpa0wc-image.image) </span>

* When the bar chart is used, the microscope function is supported (save as a user group and view samples).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fc9e678fd6e4358b37da955ff64d7f3~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-5-用户路径"></span>
### User Path


* Support microscope functions (save as user group, export user ID, add attribute analysis, do not analyze the node, temporarily hide, etc.)

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed78624b43a4e07b03ebce803d95f6c~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-6-用户生命周期"></span>
### User Lifecycle


* When it comes to column charts, microscope functions are supported (save as user group, export user ID, view user list).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27fb5c1a338b42a18c60935e413e16bc~tplv-goo7wpa0wc-image.image) </span>


<span id="8dd6c0b6"></span>
### LTV Analysis

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe1880a4fed7458a94ae636445d41732~tplv-goo7wpa0wc-image.image) </span>

<span id="915e1cf6"></span>
# Common problem


* Problem phenomenon:

   When using the microscope function in the analysis chart, after clicking View User List, the user list data is empty and the resulting data is not displayed properly.

* Possible reasons:

   During analysis, custom attribute values are used for user segmentation filtering, where custom attribute values include special characters such as "\ n".

* Solution:

   * You can modify the value of a custom property to remove any special characters. Modification example:

   ```SQL
   replaceAll('dadaf\ndafa','\n','');
   replaceAll(event_params.msg, '\n','')
   ```
   

   * You can use the virtual properties feature to implement the requirements of this scene, see the creation and use of virtual properties for details [Virtual Properties](https://docs.byteplus.com/docs/DataFinder/Virtual_Properties).
