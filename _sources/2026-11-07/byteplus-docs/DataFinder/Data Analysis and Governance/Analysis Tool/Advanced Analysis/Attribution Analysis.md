---
title: "Attribution Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Attribution_Analysis"
---

<span id="_1-概念介绍"></span>
# 1. Background information

Attribution analysis is primarily used to measure the conversion contribution of in\-app multiple bits or events to business goal events.

For example, a common scenario is as follows:


1. The user conducted a search and finally completed the target conversion, hoping to understand the contribution of different search terms.

2. The user first visits from the advertisement of channel A, and then visits from the advertisement of channel B, and finally completes the goal conversion. They want to know the contribution of different channels to the goal.

3. In the process of visiting a webpage, users simultaneously open many pages, click on different bits, and finally complete the goal conversion. They want to understand the contribution of relevant bits to the goal.


In the above scenario, it is very likely that the user clicked multiple bits before completing the target conversion. So which bit should we credit for the conversion contribution? How do we evaluate the advantages and disadvantages of each bit?

This is where attribution analysis is required. We employed five commonly used attribution methods in the industry.


|**Attribution method** |**Detail** |
|---|---|
|**First Attribution** &<br><br>**Last attribution** |* First Attribution: Of all the attribution bits that complete a target event, the first attribution bit receives a 100% contribution.<br><br>* Last Attribution: Of all the attribution bits that complete a target event, the last attribution bit receives a 100% contribution.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The first and last decisions of the DataFinder are defined according to the chronological order of events.</div><br> |
|**Linear attribution** |Of all the attribution bits that complete a target event, all the attribution bits share the contribution equally. |
|**Location attribution** |Among all the attribution bits that complete a target event, the first and last attribution bits receive 40% of the contribution, and the remaining positions divide the remaining 20% equally. |
|**Time Decay Attribution** |Among all the attribution bits that complete a target event, the attribution bit that is closer to the conversion target time gets more contributions, and the contribution decay is calculated according to the half\-life formula: m = M (1/2) ^ (t/T), where M represents the index value of the target event, t represents the time interval between Attributed Events and the target event, and T represents the half\-life. |


Through attribution, we can see the contribution of different events to a goal's conversion, so we can adjust our product strategy more specifically to maximize benefits.

<span id="_2-快速上手"></span>
# 2. Operation steps

<span id="_2-1-整体介绍"></span>
## 2.1 Operation example scenario

To make it easier for you to understand the operation of attribution analysis, the following is an example of a typical example scenario to introduce the configuration recommendations in a typical scenario. You can configure it flexibly based on your own business scenarios.


* Example scenario: In an e\-commerce APP, users may go through multiple events such as product search, browsing, consultation, shopping cart addition, and payment during the process from logging in to browsing products to purchasing and payment. They hope to analyze the contribution of each event to the final product payment event.


<span id="_2-2-归因设置"></span>
## 2.2 Configuring event metrics

<span id="_2-2-1-配置目标事件"></span>
### 2.2.1 Configure target events


|**Parameter** |**Parameter description** |**Configuration example** |
|---|---|---|
|**Target event** |When performing attribution analysis, the target event needs to be selected first. The target event is usually an event that can represent a certain business. By looking at the data performance of the event, you can understand the operation status of the business. |* The most common event in the e\-commerce industry is the `purchase`or `payment success`, as in the example scenario above, which can be configured as the product payment success.<br><br>* For some registration\-oriented activities, the relevant target event may also be `successful registration`.<br><br>* For Enterprise Services, `retention completion`is also an appropriate target event. |


<span id="_2-2-2-配置待归因事件"></span>
### 2.2.2 configure the node to be attributed


|**Attribution node type** |**Parameter description** |**Configuration example** |
|---|---|---|
|**Event attribution** |Refers to event\-level attribution, that is, pit location attribution ("pit location" refers to various operation locations in the APP, such as home page banner click\ adaptable navigation bar jump and other traffic entrances in the station.), mainly for attribution analysis in the station.<br><br>Attributed Events, as the name implies, refers to events that need to be analyzed for their contribution to the `target event`, and the maximum number of additions is 10. In addition, you can group events by property, compare the differences between different property values, and set filters to narrow the query range. |For example, in the above example scenario, it can be configured for product search, product consultation, and so on. |
|**Attribute attribution** |It refers to attribute\-level attribution, that is, channel attribution, which is mainly used for post\-investment effect evaluation, focusing more on conversion post\-click. "Channels" can be identified by attribute values on specific events, such as utm parameters, scene values, applications, etc.<br><br>Attributes to be attributed support the selection of event public attributes and user attributes of allvalue, but do not support the selection of virtual attributes and item attributes. At the same time, DataFinder shows you a list of recommended properties based on the intersection of the optional range of enumeration list + the optional properties of the existing environment, and you can select the corresponding properties in the recommended property list. |For example, the operation responsible for the delivery, want to know how many new users after a certain activity, you can see the number of new user registrations in the attribution and which operation is responsible for the media buy channel. Attribute attribute attribute to select the media buy channel related attributes. |


<span id="_2-2-3-配置过程事件"></span>
### 2.2.3 Configuration process events


|**Parameter** |**Parameter description** |**Configuration example** |
|---|---|---|
|Process event |Process events refer to events that must occur before the completion of a target event. Some business scenarios may encounter a large `target event`coverage, this time can be increased by `process events`, configuration attribute filtering, so that the `target event`range more accurate, thereby enhancing the credibility of the analysis results. |Process events often used before payment success events include product details page browsing, product addition to shopping cart, etc. |
|Associated attribute |Associated properties are configured to ensure that `process events`and `target events`are indeed related by the same properties of `process events`and `target events`. |For example, by configuring the product ID, you can ensure that the product browsing details page and the product payment success are two events that occur with the same product ID, thus ensuring the accuracy of the `process event`. |


<span id="_2-2-4-也计算其他转化"></span>
### 2.2.4 Also calculate other conversions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>When the attribution node</strong> selects <strong>attribute attribution</strong>, it does not support checking <strong>and also calculates other conversions</strong>.</div>



|**Parameter** |**Parameter description** |
|---|---|
|Also calculate other transformations |Also calculate other conversions, which means that in some scenarios, such as not being familiar with the business process, waiting for too many Attributed Events, etc., you can't list all the Attributed Events completely, and you don't even know if they are fully configured. At this time, you can check the box `Also calculate other conversions`Let the model automatically calculate the contribution of other events that are not in the configuration list to the `target event`for you to help you understand the contribution more comprehensively.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2146fa86552430caa357fc53f9963eb~tplv-goo7wpa0wc-image.image) </span><br><br>**Logical explanation** : [Other events] do not participate in the attribution model logical allocation. [Other Events] is calculated as the number of times that no Attributed Events (or corresponding attribute metrics) have occurred before the conversion target in the attribution cycle, and is proportionally apportioned with the conversion target after the attribution model has been assigned when the contribution is calculated. For example, select A and B events as pending Attributed Events, and C as target events. Assuming a user action is A\-B\-D (other events) \-C, the report will still apply the attribution model to assign target conversions according to A\-B\-C as the attribution path when calculating; only if the D (other events) \-C category occurs in the conversion window, the path where no Attributed Events have occurred before the target event C will be attributed to the contribution of other events. |


<span id="4390199e"></span>
## 2.3 Configuring segmentation filtering

You can circle the target population for analysis through attribute filtering, behavioral circling, dynamic circling, and other methods in the segmentation filter. Configuration operations for attribution analysis are consistent with the general capabilities of DataFinder, see [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering).

<span id="_2-3-详细数据"></span>
## 2.4 Review the detailed result data

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80ec0340fef64677ab431448db347a87~tplv-goo7wpa0wc-image.image) </span>


1. Configure the time period and traceback period for querying data.

   
   |**Parameter** |**Parameter description** |**Configuration example** |
   |---|---|---|
   |Query cycle |You can configure the data query cycle for attribution analysis by clicking on the query cycle calendar at the top. |For example, if you want to analyze the correlation between Attributed Events and the target event in the past 7 days, you can choose a time frame of the past 7 days. |
   |Backtracking period |Set the time period for analyzing the attribution result data between the Attributed Events and the target event after the target event occurs. |For example, in the above example scenario, after the user's product search event, how long it takes to pay for a successful order can be attributed to this search action. |
   

2. Select the attribution method and view the detailed data of the attribution analysis results.

   * Attribution method. Support the selection of multiple attribution methods to compare and analyze the analysis results.

      
      |**Attribution method** |**Detail** |
      |---|---|
      |**First Attribution** &<br><br>**Last attribution** |* First Attribution: Of all the attribution bits that complete a target event, the first attribution bit receives a 100% contribution.<br><br>* Last Attribution: Of all the attribution bits that complete a target event, the last attribution bit receives a 100% contribution.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The first and last decisions of the DataFinder are defined according to the chronological order of events.</div><br> |
      |**Linear attribution** |Of all the attribution bits that complete a target event, all the attribution bits share the contribution equally. |
      |**Location attribution** |Among all the attribution bits that complete a target event, the first and last attribution bits receive 40% of the contribution, and the remaining positions divide the remaining 20% equally. |
      |**Time Decay Attribution** |Among all the attribution bits that complete a target event, the attribution bit that is closer to the conversion target time gets more contributions, and the contribution decay is calculated according to the half\-life formula: m = M (1/2) ^ (t/T), where M represents the index value of the target event, t represents the time interval between Attributed Events and the target event, and T represents the half\-life. |
      

   * Introduction to metrics with detailed data

      
      |**Indicator** |**Indicator explanation** |
      |---|---|
      |Relevance |Calculated according to the Pearson correlation coefficient, it represents the probability that event B will occur when event A occurs during the calculation period. It represents the degree of linear correlation between event A and event B. A is a linear positive correlation, which means that the correlation coefficient is + 1. A linear negative correlation means that the correlation coefficient is \-1. Otherwise, the correlation coefficient is between \-1 and + 1. A higher absolute value indicates a stronger correlation.<br><br>For example, after participating in an activity, most people have completed the purchase. The larger the value, the stronger the correlation between the two behaviors. It is recommended to stimulate more customer engagement in the activity. |
      |Number of triggers |Indicates how many times the "Attributed Events" has been triggered during the calculation period. |
      |Triggers/Rate of Effective Conversions |Indicates how many times during the calculation period, according to the currently selected "attribution model", the events that "pending Attributed Events" really contributed to the conversion of the "target event" were triggered. For example, in the last attribution, a total of 100 times occurred in the calculation cycle, but only 50 times were in the last attribution position, so the number of effective conversions triggered = 50 times, the ratio is 50%. |
      |Conversion target (number of times/sum by...) |Represents the results of the "target event" assigned according to the selected attribution model during the computation period. For example, the number of payments is attributed by position, setting the first 40% \- middle 20% \- tail 40%, assuming that a certain attribution path is a attribution bit A\-B\-A\- payment, then the payment will be assigned 0.4 (first) + 0.4 (last) = 0.8 times for A's contribution, 0.2 times for B's contribution, and the same is true for other indicators. |
      |Contribution |After the attribution model is calculated, the contribution to the Attributed Events accounts for the proportion of the whole, and the calculation logic is: the sum of the conversion target indicators/the overall conversion target under the current Attributed Events. |
      


<span id="_3-归因分析视频讲解"></span>
# 3. Attribution analysis video explanation

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ffa2c94b842b7430ee40487623a1b37.mp4" controls></video>
