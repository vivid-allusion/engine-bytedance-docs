---
title: "Efficiency Improvement Function: Event Tracking Bloodline"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Efficiency_Improvement_Function_Event_Tracking_Bloodline"
---

DataFinder provides you with event tracking lineage function, which shows you the lineage of the corresponding event/property data based on the application of events/properties in charts, clusters and other scenarios (which charts and clusters are used for events/properties), so that you can refer to it when querying or editing and modifying, and evaluate the scope of impact. This article introduces you to the main points of using the event tracking blood function.

<span id="5907d8b6"></span>
# Precautions


* The current event tracking blood function is a value\-added function. You need to purchase the "event tracking governance module" separately to use it. For purchase consultation, you can contact BytePlus technical support staff or your account manager.

* Linearity supports viewing "General Events", "Event Properties", "User Properties" event tracking data on charts and groupings of lineages; overrides preset events/properties and custom events/properties.


<span id="9d032592"></span>
# Event tracking blood statistics

The event tracking bloodline function currently displays the bloodline relationship of the corresponding event/property data for you based on the application of events/properties in charts and clustering scenarios.


* When counting blood relations, event tracking is divided into "**direct reference**" and "**indirect reference**":

   * **Direct reference:**  Events or properties are applied directly to the chart as a chart analysis metric or filter/group criteria.

   * **Indirect reference:**  Events or properties through virtual events, virtual properties, property custom grouping, user clustering, metrics, you may not be able to directly see metadata information from the query conditions, you can view the corresponding indirect reference scene in the chart.

      For example, if event A is referenced to virtual event C through cluster B, and virtual event C is referenced to graph D, then the graph consumption of event A will include graph D, but since event A is contained in cluster B, you cannot directly see the information of event A in the page of graph D.

* Property event tracking The lineage of the dictionary value of the data accurately recognizes the dictionary value value.

   For example, is_login property, Chart A only uses the dictionary value of is_login = ture, then when you edit the dictionary, only if the dictionary value changes to ture, the kinship will show that the scope of influence includes Chart A.


<span id="f6b96d2d"></span>
# View event tracking lineage

<span id="0904666d"></span>
## View bloodline on the metadata page

Taking the "General Events" page as an example, you can view the "Chart bloodline" and "Cohort blood" of the corresponding event in the event details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bd2ab7dc8cf4b74bce0a0bff9c9acec~tplv-goo7wpa0wc-image.image) </span>


* Chart lineage: Which charts the current event/property is applied to, as well as the board to which the chart belongs, the type of analysis tool, and whether it is a direct or indirect reference.

* Cluster lineage: Which cohorts the current event/property is applied to, as well as the number of people in the cohort, the number of times the cohort has been queried in the past 30 days, etc.


<span id="b9b74e8d"></span>
## Other pages

If you purchased the event tracking blood function:


* When the corresponding event/property is used by the analysis tool later, the blood relationship of the corresponding event/property can be easily queried.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46d63e3f27dc49989495b8a8087740e9~tplv-goo7wpa0wc-image.image) </span>

* In the future, when disabling or editing the corresponding event/property, and uploading/deleting/editing the property dictionary, the interface will show you the application of the event/property data on charts and clusters, so that you can easily evaluate the scope of impact.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d36d435fe4a422bbe574ad515e9b824~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Property event tracking The lineage of the dictionary value of the data accurately recognizes the dictionary value value. For example, is_login property. Chart A only uses the dictionary value of is_login = ture, then when you edit the dictionary, only if the dictionary value changes to ture, the kinship will show that the scope of influence includes Chart A.   </div>
