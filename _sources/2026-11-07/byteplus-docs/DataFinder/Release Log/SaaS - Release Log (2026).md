---
title: "SaaS - Release Log (2026)"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/SaaS-Release_Log_2026"
---

<span id="55129c9c"></span>
# April 16, 2026


|**Function module** |**Update description** |
|---|---|
|dashboard |Dashboard is based on large model capabilities and built\-in standard templates, providing intelligent summary functions and automatically generating key indicator analysis reports to help you efficiently gain insight into key Dashboard data and trends.<br><br>Please see for details [Dashboard Intelligent Summary](https://docs.byteplus.com/docs/DataFinder/Dashboard_Intelligent_Summary). |


<span id="3a9094a2"></span>
# March 12, 2026


|**Function module** |**Update description** |
|---|---|
|User Research Agent\-AI Behavior Research |In the AI Behavior Research Summary report, the behavior breakdown allows you to view a list of events for all sessions or for a given session. Select all sessions and search for events or parameters to enable cross\-session search capabilities.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/906a7ca8d08d44bbb50067d6229ff507~tplv-goo7wpa0wc-image.image) </span><br><br>See the [behavior breakdown results ](https://docs.volcengine.com/docs/85637/1873419?lang=en#behavioral-breakdown-results)for details. |
||When rerunning the summary report of AI behavior research, you can add a prompt word, and the system will rerun the summary report according to the prompt word requirements.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d6b12af0e5143138f5655c6e489027e~tplv-goo7wpa0wc-image.image) </span><br><br>See [Interrogation and Reanalysis ](https://docs.volcengine.com/docs/85637/1873419?lang=en#interrogation-and-reanalysis)for details. |


<span id="db0fa866"></span>
# February 9, 2026


|**Function module** |**Update description** |
|---|---|
|Analysis Tools \- Event Analysis |On the **Event Analysis** page, after property grouping is configured, the Property Grouping column supports filtering the specified range of property values in the **detailed data** list at the bottom of the page.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf79a4ddba14aa5b9fc4f68cfaaff87~tplv-goo7wpa0wc-image.image) </span> |


<span id="542ea6f6"></span>
# January 29, 2026


|**Function module** |**Update description** |
|---|---|
|Analysis tool \- SQL custom query |SQL custom queries add support for syntax with common table expressions (CTEs) for creating temporary named result sets to improve the efficiency of multiple event correlation analysis. Please see for details [Complex queries using the WITH clause](https://docs.byteplus.com/docs/DataFinder/Custom_SQL_Query#89b8d6d8). |
|Data management \- request management |Download requirements support includes screenshots (maximum 100 for a single event). |
|Data management \- metadata management |The AI metadata diagnostic function has been discontinued **from January 22, 2026**. If you need to continue using it, you can contact your account manager. |


<span id="fd879eff"></span>
# January 15, 2026


|**Function module** |**Update description** |
|---|---|
|Data Management \- General Events |When creating a new general event, batch creation and on\-demand creation are supported.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/37d4a2b0d3c948ab95b602e32514ecbe~tplv-goo7wpa0wc-image.image) </span><br><br>For details see [Batch new event](https://docs.byteplus.com/docs/DataFinder/General_Events#_2-1-2-%E6%89%B9%E9%87%8F%E7%99%BB%E8%AE%B0), [Build on demand](https://docs.byteplus.com/docs/DataFinder/General_Events#e156e470). |
||General events support uploading event tracking screenshots (additional purchases are required).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5983918780742869182fa24346693f8~tplv-goo7wpa0wc-image.image) </span><br><br>Please see for details [View/upload event tracking screenshots](https://docs.byteplus.com/docs/DataFinder/General_Events#73449844). |
|Data management \- request management |* The request management page adds support for directly uploading event tracking screenshots. You can synchronously upload the schematic screenshots of event tracking when adding event tracking, which is convenient for subsequent clarification of the specific events represented by event tracking, and helps to further explain the event tracking plan.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/949300615b4e44869a9c9ea65738fb14~tplv-goo7wpa0wc-image.image) </span><br><br>* Refinement of permission control for request management: After optimization, only the requirement creator and project administrator can delete the requirement; non\-project administrators cannot delete the requirement created by others.<br><br>* Verification and upgrade of requirements and event tracking solutions: After the upgrade, it will verify whether the requirements are filled in completely before the requirements are submitted, whether there is an event with the same name in the requirements, and support reuse of historical events (display name, classification, description information of the reuse event, etc.) when adding events.<br><br><br>Please see for details [Request Management](https://docs.byteplus.com/docs/DataFinder/Request_Management). |
|User Research Agent\-AI Behavior Research |Added question templates for question discovery, behavior summary, and intent analysis modules. You can choose the matching template according to your needs, and modify it based on the template to quickly build question content.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d50fcc546cad4b6aa6d3b57594518870~tplv-goo7wpa0wc-image.image) </span> |
|Advanced Analysis \- LTV Analysis |LTV Analytics adds support for property grouping.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359104d12dfa47a193f3aa21a3fc026b~tplv-goo7wpa0wc-image.image) </span><br><br>As shown in the figure above, when you use the LTV analysis tool, after configuring parameters such as starting events and revenue events, you can add support for configuring property grouping, and you can choose whether the data query analysis results should be displayed in groups according to a certain property.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Property grouping supports grouping by event properties, user properties, user labels, etc. A total of up to 20 layers of grouping are supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Selecting revenue event related properties for grouping properties of query analysis results is not currently supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After setting the property grouping, in the subsequent data query chart, if a group has multiple values, for example, there are iOS and android two property groupings after grouping according to the "system platform" property, when a user uses iOS and android at the same time. After reporting the revenue event, in the query results of LTV, the data results of the two groupings will respectively count the data of the user with the corresponding property (that is, ios and android will be counted, and in the scenario without grouping, a user will only be counted once).</div><br><br><br><br>Please see for details [LTV Analysis](https://docs.byteplus.com/docs/DataFinder/LTV_Analysis). |
|Dashboard |Users with chart editing permissions can select  **...**  \> **Edit chart** in the upper right corner of Dashboard, jump to Advanced Analysis, re\-edit chart configuration and save to Dashboard.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d59d188325448a9aa3bc9e676cb3d90~tplv-goo7wpa0wc-image.image) </span><br><br>Please see for details [1.2.2 Edit Charts](https://docs.byteplus.com/docs/DataFinder/Dashboard_Function_Description#_1-2-2-%E7%BC%96%E8%BE%91%E5%9B%BE%E8%A1%A8). |
|User Cohorts |When a rule creates a user cluster, the rule configuration is updated:<br><br><br>* Added: The **user has not made a global** rule.<br><br>* Optimization: Optimization **users have not done** rules, removing **users is not a** rule.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The rule configuration for historical user grouping is not affected and continues to take effect, and the rules are still optionally available when replicating historical user grouping.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Subsequent new user clusters will only be adapted to the new rule configuration.</div><br><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7daccf3477c147bf9b80e7dc63ee0ea4~tplv-goo7wpa0wc-image.image) </span><br><br>Please see for details [Creation method 1: Rule creation](https://docs.byteplus.com/docs/DataFinder/Cohorts_User_Grouping#ec9d7389). |
