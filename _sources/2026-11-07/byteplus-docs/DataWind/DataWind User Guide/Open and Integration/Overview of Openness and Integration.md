---
title: "Overview of Openness and Integration"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Overview_of_Openness_and_Integration"
---

<span id="bd6b0c91"></span>
# 1. Overview

Openness and integration refers to one of the product capabilities provided by Intelligent Data Insight for enterprise customers, enabling the product to be open and integrated with multiple system modules. This covers data ingestion, visual modeling, visual querying, dashboards, business system integration, and security management, providing enterprises with a flexible and scalable integration model as well as an efficient, low\-cost experience. DataWind's openness and integration capabilities can meet the needs of different enterprises and ecosystem partners, supporting varying degrees of integration into business systems and scenarios, and offering extremely high flexibility.

The openness and integration capabilities currently support four main features: office system integration, embedded analytics, OpenAPI, and custom extensions (custom visualization plugins):


* **Office system integration**: Supports connecting to Lark, WeCom, Webex, and DingTalk office systems, enabling product feature linkage across multiple stages from data ingestion and data delivery to data sharing, providing users with a more convenient collaborative office experience.

* **Embedded analytics**: Supports embedding dashboards and charts within dashboards into third\-party platforms for relevant personnel to view. For example, users can embed completed dashboards or charts into business systems such as CRM or ERP to enable monitoring of business data.

* **OpenAPI**: Through OpenAPI, users can invoke various operational scenarios, such as managing user groups, setting dataset/dashboard/row and column permissions, retrieving datasets/dashboards/charts, and creating or deleting fields.

* **Custom extensions (custom visualization plugins)** : Supports users in creating personalized data presentations according to their needs, such as custom configuration options. Users can also leverage the component software development kit (SDK) and popular tools from the community to further develop and customize dedicated charts and controls.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3848240289e54c18a9507b2240e1d58f~tplv-goo7wpa0wc-image.image" width="1206px" /></div>


<span id="fc1a3121"></span>
# 2. Application benefits

 **(1) Application scenario one**

The platform provides office system integration capabilities that can effectively break down data silos between systems, creating a unified, coordinated, and efficient office environment and work platform. Users can utilize DataWind capabilities for data analysis within the enterprise OA system, reducing the time spent switching between multiple platforms and significantly improving office efficiency. Examples of scenarios are as follows:


* DataWind can be integrated with Lark, allowing managers to directly receive subscription or alert messages sent by DataWind in Lark, view business statistics on dashboards, share and comment on dashboards, and remind relevant personnel to stay informed about business developments.

* When the task status on a dashboard changes, such as when a task changes from "In Progress" to "Pending Review", instant messaging notifications can be automatically sent to relevant personnel via their office software. The personnel responsible for review will immediately receive a notification to conduct the review in a timely manner. This ensures smooth task flow and avoids delays caused by untimely communication of information.

* When a newly onboarded employee does not have dashboard permissions, they need to request access from the administrator. After configuring the integration between Lark and DataWind, administrators can directly approve and grant permissions in Lark without needing to switch to DataWind.


**Scenario 2:** 

The platform's embedded analytics capabilities have broad applicability and significant value. When an enterprise expects to embed charts or dashboards into its own business systems or other platforms for display and analysis, enabling convenient visualization of business system\-related data, this capability becomes especially critical. Examples of scenarios are as follows:


* Charts or dashboards used for inventory analysis can be embedded into the ERP system. Within the ERP system, enterprises can easily view key indicators such as inventory levels for different product lines, procurement costs, and production progress. This helps management quickly gain insight into supply chain dynamics, promptly identify potential supply bottlenecks or cost overruns, and thereby optimize procurement plans and production arrangements.

* Financial analysis dashboards can be embedded into financial systems, enabling finance personnel to monitor various financial metrics in real time, such as budget utilization by different departments, comparative analysis of revenue and profit, and more. This enables enterprises to promptly detect financial anomalies and make reasonable fund allocations and budget adjustments.


 **(3) Application scenario three**

This platform provides OpenAPI functionality, allowing different applications or services to "communicate" with each other and share data and functions. Enterprises can leverage OpenAPI for customized development based on their own business characteristics and requirements, providing more options for the enterprise and meeting the personalized needs of different organizations. The following are example scenarios:


* In e\-commerce enterprises, OpenAPI can be used to connect their own sales data with suppliers' inventory management systems. When there are changes in the sales performance of the enterprise's products, suppliers can use the API to obtain sales data in real time, enabling timely adjustments to production and supply plans, ensuring that the enterprise's product inventory is replenished promptly, and improving the operational efficiency of the entire supply chain.


 **(4) Application scenario four**

The custom plugin functionality provided by this platform enables developers to meet the diverse needs of more business units, adapt to different business processes, address unique data presentation requirements, and enhance the diversity of data presentation. The following are example scenarios:


* In the consumer goods industry, custom chart plugins can be developed to analyze product sales performance, allowing for the simultaneous display of multiple elements such as product main images, sales volume, order quantity, and average transaction value within the chart, providing a more intuitive presentation of product sales performance.

* In the e\-commerce retail industry, to view the sales share and specific sales volume of different types of products across various regions, a custom matrix chart plugin can be created. This plugin utilizes matrix space to present the market share of each segment, and differences in color and size make it easy for users to quickly identify the market segments with the largest share.


<span id="4d23a669"></span>
# 3. Feature introduction

<span id="b05e7c2c"></span>
## 3.1 Office system integration

Office system integration refers to integrating independent office systems with DataWind to create a unified, coordinated, and efficient office environment and work platform. Currently, DataWind supports integration with Lark, WeCom, Webex, and DingTalk office systems, enabling product feature linkage across multiple stages from data ingestion and data access to data sharing. Once adaptation is completed, users can search for applications on the office platform, open the DataWind mobile app, conveniently view reports, receive message notifications, and achieve seamless access to data. (For details, see [Office Platform Integration](https://docs.byteplus.com/docs/undefined/69c3469a50cba904c1f57e28).)


|**Office platforms** |**Supported features** |
|---|---|
|[Basic Configuration for Lark Integration](https://docs.byteplus.com/docs/DataWind/Basic_Configuration_for_Lark_Integration) |Open DataWind within the platform, dashboard subscription, chart monitoring and alerting, dataset synchronization result notification push, resource permission approval, dashboard comment reminders, one\-click contact with chart owner, one\-click authorization |
|[Integrate the WeCom Application](https://docs.byteplus.com/docs/DataWind/Integrate_the_WeCom_Application) |Open DataWind within the platform, dashboard subscription, chart monitoring and alerting, dataset synchronization result notification push |
|[Integrate the Webex Application](https://docs.byteplus.com/docs/DataWind/Integrate_the_Webex_Application) |Dashboard subscription, chart monitoring and alerting, dataset synchronization result notification push |
|[Integrate the DingTalk Application](https://docs.byteplus.com/docs/DataWind/Integrate_the_DingTalk_Application) |Dashboard subscription, chart monitoring alerts, dataset synchronization result notification push |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/747dec3b9bc142aeacf93f6ec60c038c~tplv-goo7wpa0wc-image.image" width="1426px" /></div>


<span id="cf4bccf1"></span>
## 3.2 Embedded analytics

Embedded analytics allows users to embed dashboards and charts that have already been created into third\-party platforms for relevant personnel to view. For example, users can embed dashboards or charts into business systems such as CRM or ERP, making it easy to understand data changes without repeatedly switching between platforms, thereby improving work efficiency. In addition, embedded analytics is often accompanied by theme and feature configuration settings to meet personalized requirements, enabling deeper and more intuitive understanding of business data and providing strong support for business decision\-making.

**Core capabilities**


* Supports multiple scenarios: dataset, dashboard, single chart, visual query, and AI insights embedding

* Automatic adaptation for multiple terminals (PC, mobile, mini program)

* No login required (see 3.3 for jwtToken details)

* Personalized configuration (feature differentiation configuration switch)

   * Feature configuration for theme background color, display header, display title, action operation configuration, and more.

      * Usage scenario: Customize showing or hiding standard features in embedded dashboards/queries

   * Overview query parameters or filter logic parameters .

      * Usage scenario: After configuring a global filter, the embedding application can dynamically pass parameters to enable interactivity


**Integration methods:**  SDK, iframe


|**Integration method** |Event listener |Method invocation |Token update |Ease of getting started |
|---|---|---|---|---|
|**iframe integration** |❌ |❌ |❌ |🟢 |
|**SDK integration** |✅ |✅ |✅ |🟠 |


<span id="f4a29284"></span>
### 3.2.1 Dashboard embedding

Supports dashboard embedding. On the dashboard page, click the three dots in the upper right corner, select "Embed dashboard", choose the content to embed, and copy the embed link. After "Copy successful" is displayed, paste the link into a browser window to view the chart component. It can be quickly added to any application that supports embedding. (*See* [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) *for details.)* 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc66ebc8eb8c4487b0c2f9302ac50a53~tplv-goo7wpa0wc-image.image" width="2150px" /></div>


<span id="db63af1b"></span>
### 3.2.2 Single **chart embedding**

Supports embedding a single chart. On the dashboard editing page, click the upper right corner of a chart, select "Embed chart", and copy the embed link. After "Copy successful" is displayed, paste it into a browser window to view the chart component. It can be quickly added to any application that supports embedding. (*See* [Chart Embedding](https://docs.byteplus.com/docs/DataWind/Chart_Embedding) *for details.)* 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d11f1c27204b4a0e862fb15fef07e517~tplv-goo7wpa0wc-image.image" width="850px" /></div>


<span id="47c13bd5"></span>
### 3.2.3 Visual query embedding

Helps customers quickly build personalized data analysis scenarios and save them to the required dashboard with one click. After completing personalized chart configuration, you can flexibly customize and display data, and preview various chart types (charts, pivot tables, bar charts, and more) in real time.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/20c41d336b0f4651ab205b69a838bf2d~tplv-goo7wpa0wc-image.image" width="2194px" /></div>


<span id="52e8bc7a"></span>
## 3.3 OpenAPI

OpenAPI allows users to send HTTP requests to obtain and manage resources such as dashboards, datasets, and charts. Simply put, it acts as a "door" that allows different applications or services to communicate and share data and functions with each other.

**Currently, OpenAPI usage scenarios include the following:** 


* Users, user groups (permission management)

* Data integration (third\-party data platform data connection and import)

* Metadata management: dataset (list, details), dashboard list, lineage, user permission list


*For details, see* *OpenAPI*\*.\*

**Actual customer cases:** 


* Data integration for a commercial bank client's internal platform: Data links from “XX台” are imported into DataWind via OpenAPI for unified permission management, authorization, and related operations.

* Data integration for a large securities firm client: Batch import of data links from the data platform and batch user authorization.


<span id="8b64930b"></span>
## 3.4 Plugin system

The DataWind plugin system is one of its open capabilities, designed to meet the diverse customization needs of business teams. Through the plugin system, users can develop, publish, and review plugins based on specific business scenarios, thereby flexibly extending various functionalities. The types currently supported in the plugin marketplace include: visualization chart plugins and dashboard plugins.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d7577f646b9465595f4813fa27e51c4~tplv-goo7wpa0wc-image.image" width="3516px" /></div>


<span id="77156e30"></span>
### 3.4.1 Visualization chart plugins

Supports users in creating personalized data presentations as needed. This capability not only includes custom fields and configuration options, but also covers compatibility with multiple frameworks. Supports mainstream chart frameworks such as [Echart](https://echarts.apache.org/zh/index.html), [vChart](https://visactor.io/vchart) (recommended for UI consistency), and more.  *(For details, see* [Custom Visualization Overview](https://docs.byteplus.com/docs/DataWind/Custom_Visualization_Overview) *.)* 

**Feature entry point**: Visualization Query \- Chart \- Add Plugin

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a27feda80fc34de1a0ad582738f52fc1~tplv-goo7wpa0wc-image.image" width="3420px" /></div>


<span id="a024f0bb"></span>
### 3.4.2 Dashboard plugins

Dashboard plugins are one type of plugin system, generally used to enhance and enrich the display content and functionality of dashboards. Officially provided plugins include: rich text editor and custom graphics.

The feature entry point is shown in the following figure:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61f09a66ff4e4a65961f698a81941b7e~tplv-goo7wpa0wc-image.image" width="3320px" /></div>


<span id="3e115813"></span>
# 4. Best practices

<span id="cda3e6a0"></span>
### 4.1 Embedded analytics


|**Scenario** |**Screenshot/description** |
|---|---|
|Lark document |> Integrate charts, dashboards, and visual queries with preview in Lark documents<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7504a2e46f41de88a9b7abe9206f8b~tplv-goo7wpa0wc-image.image) </span> |
|Data portal |* Self\-service analysis (visual query embedding)<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c206ba108c7c4af284a409ad31cd3a9f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Data portal dashboard (dashboard embedding) |


<span id="41fba82f"></span>
### 4.2 Custom chart plugins

Official scenario list: treemap, Mekko chart, calendar heatmap, and more. (*For details, see* [Publishing Custom Plugin Packages and Plugin Package Resources](https://docs.byteplus.com/docs/DataWind/Publishing_Custom_Plugin_Packages_and_Plugin_Package_Resources).)


|Customer |Industry |Custom chart introduction/screenshot |Detailed introduction |
|---|---|---|---|
|Customer A |Consumer goods |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfb9f975afc148799b0a887716ff50fa~tplv-goo7wpa0wc-image.image) </span> |Features<br><br><br>* Support for region label configuration<br><br>* Support for basic product style configuration (image size, spacing) |
|Customer B |E\-commerce retail |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bbe71ca93bef406c89ecadac6c96ede0~tplv-goo7wpa0wc-image.image) </span> |Features<br><br><br>* Support for a temporary version that allows assigning specific colors to fields<br><br>* A version that removes the maximum stacking limit<br><br>* Remove the limit on the number of dimension metrics, allowing additional dimensions to sort query results<br><br>* Support for legend position selection (currently, due to chart library limitations, the default behavior is pagination for vertical orientation and line break for horizontal orientation. This will be updated after the chart library is fixed) |
