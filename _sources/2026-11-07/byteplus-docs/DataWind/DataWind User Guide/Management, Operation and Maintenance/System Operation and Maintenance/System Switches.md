---
title: "System Switches"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/System_Switches"
---

This article introduces the effects of specific switches within the system switches module.

<span id="c2837ae4"></span>
# Feature overview

The system management section provides a system switches module.


* Enterprises can customize product feature interfaces based on their own business needs, enabling only certain features for internal users.

* System administrators can configure switches for specific features in this module. When a feature is disabled, it will not be displayed in the user's interface.


Customizing system feature switches makes the user interface more concise and clear, improves usability, and reduces violations and erroneous operations; restricting certain sensitive or important features can also lower the risk of information leakage and protect the enterprise's core data and confidential information.

<span id="7f8fbae4"></span>
# Feature entry

Click the settings icon in the upper right corner, then select system switches from the left sidebar to configure feature switches.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f315422589744284821dadfec9f3d244~tplv-goo7wpa0wc-image.image) </span>

<span id="5aa434bf"></span>
# Feature description

**System switches can be configured for the following features:** 


* **General settings**: Product name, development platform

* **Visualization module**: Dashboard templates, click dashboard icon name to enter visualization query, dashboard comments, networked charts, "trading day" filter, push downloaded and exported content to third\-party platforms, copy data, listening dataset scope for extended push functionality, dashboard subscription supports data push, metric broadcast, monitoring, mobile, dashboard subscription supports a rich text box for explanations or remarks

* **Data preparation module**: Custom database tables, visualization modeling output datasets can span multiple projects, basic information of data connections not displayed in plain text, datasets support the use of custom SQL in projects, datasets are directly connected by default, task instance status information Kafka push, allow use of associated datasets

* **Large screen module**: Public templates, public materials, public fonts

* **Project center:**  Operation log permission control, role creation permission, role authorization control



|**Module** |**System switches** |**Note** |**Diagram** |**Note** |
|---|---|---|---|---|
|General settings |Product name |Define the product name in the navigation bar in both Chinese and English |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c2993691074a1b82b122efb2b86d91~tplv-goo7wpa0wc-image.image) </span> | |
||Development platform |After enabling, the entry point for the open platform will appear in the navigation bar | | |
|Visualization |Dashboard template |After enabling, the entry point for dashboard templates will be added to the navigation bar |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/34c06806e20347939ab5000778a91d8f~tplv-goo7wpa0wc-image.image) </span> |[Dashboard Templates](https://docs.byteplus.com/docs/DataWind/Dashboard_Templates) |
||Click the dashboard chart name to enter visualization query |After enabling, clicking the chart name on the dashboard will take you directly to the visualization query page for that chart | | |
||Dashboard comments |After enabling, commenting on the dashboard is supported |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0dfb99bb31a489da28c10e461adf150~tplv-goo7wpa0wc-image.image) </span> |[Dashboard Comments](https://docs.byteplus.com/docs/DataWind/Dashboard_Comments) |
||"Trading day" filter |After enabling, the chart filter will add a filter for "trading day" | | |
||Push downloaded and exported content to third\-party platforms |After enabling, all downloaded and exported content from visualization and dashboards will be pushed to third\-party platforms, and users must download and use it from the third\-party platform | | |
||Copy data |After disabling, users cannot copy query results | | |
||Expand the scope of datasets monitored by the push feature |After enabling, the "trigger when data synchronization is complete" for subscriptions, monitoring, and metric broadcasting will also monitor the synchronization status of manually synchronized datasets. If synchronization is not completed on the day, no push will occur | | |
||Dashboard subscription supports data push |After enabling, subscriptions support selecting to push screenshots and PDFs | | |
||Metric broadcasting |After disabling, the entry point for metric broadcasting will not be displayed, and historical metric broadcasts will be hidden and not pushed |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26682d3d2ab641e291a7dfdf70b2c0ac~tplv-goo7wpa0wc-image.image) </span> | |
||Monitoring |After disabling, the entry point for monitoring will not be displayed, and historical monitoring will be hidden and not pushed. Enabled by default |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d09c5f1ffdf4b49a2979053ca5649c8~tplv-goo7wpa0wc-image.image) </span> | |
||Mobile |After disabling, mobile\-related entries will not be displayed in the product |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b750a8b72d004534805e2bcc7585401e~tplv-goo7wpa0wc-image.image) </span> | |
||Dashboard subscription supports rich text box for description/notes |After disabling, the rich text box for description/notes will not be displayed when creating a new subscription |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0388d016963b476f8da406bcb275c60b~tplv-goo7wpa0wc-image.image) </span> | |
|Data preparation |Support custom database table data source types in visual modeling |Enable customization of database tables for different dataset storage types in visual modeling | | |
||Datasets output by visual modeling can be shared across multiple projects |When enabled, datasets output by visual modeling can be made available to other projects. Dataset administrators can use these datasets as data sources in visual modeling tasks of other projects. | | |
||Basic information of data connections is not displayed in plain text |For the selected data connection type, all basic information except the data connection name is displayed in a non\-plain\-text format. | | |
||Projects that support using custom SQL for datasets |You can select projects. Selected projects support the use of custom SQL, while unselected projects will have custom SQL disabled. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b97c25641304db59286eafc559df19f~tplv-goo7wpa0wc-image.image) </span> | |
||Datasets use direct connection by default |When disabled, datasets use extraction by default. When enabled, when creating a new dataset, the dataset type changes from extraction by default to direct connection by default. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64baebe692c54ed9965c3092693ed202~tplv-goo7wpa0wc-image.image) </span> | |
||Task instance status information is pushed via Kafka. |Supports pushing task instance information, such as task name, instance name, business date, task running status, running time, number of data rows, and more, to eventbus's Kafka for external use. Due to the large number of lines in task logs, pushing is not supported. You need to use OpenAPI calls. This feature is currently only available on the customer data platform. | | |
||Allow use of related datasets |If Yes is selected here, you can create new datasets by associating existing datasets. If No is selected, the entry for associating datasets will not be visible in the product. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5827c207bd0e4224820a9ec37636d867~tplv-goo7wpa0wc-image.image) </span> | |
|Dashboard |Public templates |User list allowed to set templates as public | |[Vscreen Resource Management](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f62974) |
||Public assets |User list allowed to upload design assets (visible to all projects) | ||
||Public fonts |User list allowed to upload fonts (visible to all projects) | ||
|Project center |Operation log permission control |When enabled, only project administrators and users with higher permissions can view operation logs. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98ac7307b8d548a28966ce00c67eb8a6~tplv-goo7wpa0wc-image.image) </span> |[Operation Logs](https://docs.byteplus.com/docs/DataWind/Operation_Logs) |
||Role creation permissions |* Administrator creation: Only project administrators or system administrators can create roles.<br><br>* All project members: Users with project editing permissions can create roles. | | |
||Role authorization controls |* Role maintainers can authorize: When granting resource authorization, users can only select roles they maintain; project administrators, role administrators, and system administrators can select all roles.<br><br>* All users can authorize: When granting resource authorization, users can select all roles. | | |
