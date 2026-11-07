---
title: "Create Event Metric"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-Event-Metric"
---

<span id="一、新建事件指标"></span>
# New event metric

<span id="37c4599a"></span>
## Usage restrictions

The current event metric group supports adding up to 100 event metrics.

<span id="8e085f47"></span>
## **Operation entrance**

After logging in to the A/B test console, click **Metrics Management** \> **Metric Groups** on the left list page, click "**Create Metric Group**" in the upper right corner of the user metric group page, select "Event metric" for the basic information, and start configuring event metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/452f53861ef94adb8db6a377ca91a32d~tplv-goo7wpa0wc-image.image) </span>

<span id="5d75a4b2"></span>
## **Configuration metric information**


1. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9eab700f1d5d487e9c508b8cf34fc92e~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Metric group type** |The default is the event metric. |
   |**Metric group** |By default, the first metric group of the **same type** created in the current user history will be selected. Support re\-select metric group & create a new metric group and select. |
   

2. Configure metric settings. You can click Add Metrics to add multiple metrics to the metrics group. The configuration parameter types for each metric and the detailed configuration instructions for each parameter are as follows.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41195d67499b41068ec7313fee29152a~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Metric name** |It is recommended to take a name related to the content of the event, such as "number of times per person clicking the login button", so that you can quickly know which event is the metric about; the name is unique in the metric group, and the maximum length should not exceed 50 characters. |
   |**Metric description** |Briefly describe the meaning, calculation logic, purpose, etc. of the metrics, so that business stakeholders can use the metrics more reasonably. |
   |**Metric type** |For event metrics, from the perspective of metric calculation logic, they can be divided into two types:<br><br><br>* **Single metric:**  refers to the metric established for a certain event.<br><br>* **Combination metrics:**  refers to the combination metrics established for multiple events, such as A/B type combination metrics CTR, CVR, PV/SUM, etc., which can support confidence level calculation. |
   |**Calculation aperture** |To set the calculation caliber of the corresponding metric, you need to select the "event" that the metric focuses on, and clarify the "event calculation method" and [event filter conditions] corresponding to the metric value.<br><br><br>* **Select events:**  You can select general events, virtual events, and circled events, as follows:<br><br>   * **General Events:**  Refers to events reported through event tracking, with the same name as the event report you added to your code.<br><br>   * **Virtual events:**  refers to the combination of multiple original events (such as general events, circled events) through the relationship of "or", and the combined events are called "virtual events". If the user clicks on any original event in the virtual event, it indicates that the conditions are met and will be triggered.<br><br>   * **Circle event:**  Refers to the event created by selecting an element.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After selecting the metric, the interface will prompt you whether the currently selected metric can calculate the confidence level, but the metric of the confidence level cannot be calculated. That is, after the experimental results are output, the experimental version and the control version data of the metric can be calculated, but it cannot be determined whether it is credible. You need to make your own judgment. For details on whether metrics support confidence level calculations, see the <strong>Reference 2: Event metrics confidence level</strong> section below.   </div><br>   <br><br>* **Select the** **calculation method:**  You can select the calculation method of the metric in the drop\-down box, such as the total number of times, the total number of people, etc. For details, please refer to the **Reference 1: Calculation method (operator) of the event metric** section below.<br><br>* **Add filter conditions:**  Support "event attributes, public attributes" as the filter conditions for events; support metric attribute aggregation function filtering ability, that is, when the user selects the event definition caliber including "UV", "PV/UV", "PV/AU", "UV/AU", "SUM/UV", when the event attribute is numerical, it can be aggregated according to the aggregation dimensions of "person", "event attribute", "public attribute" (including "custom attribute"), the default value is "person".<br><br>* **Advanced Settings: Flexible Properties**<br><br>   You can choose whether to turn on the flexible attribute switch according to your needs. After turning it on, you can add flexible attributes to each event of the metric. After adding, you can choose when experimentally creating and selecting metrics, and specify the selected metrics to define, calculate and display the experimental results according to the selected attributes and attribute values. |
   |**Metric relationship** |Only the combined metric needs to be filled in, which refers to the calculation formula of the combined metric. It allows event numbers to be capitalized, supports a layer of parentheses (), plus +, minus \-, multiplication \*, and division/calculation formulas to be combined arbitrarily. |
   |**number format** |You can choose the number/percentage format and set the number of decimal places. |
   |**Must\-see metrics** |Turn on "Set as a must\-see metric", and the metric will be automatically added to each experiment. |
   

   After the above information is filled in/set, an metric is added. Similarly, you can click the  **"Add Metric"**  button to create multiple metrics at one time in the current metric group. Don't forget to click the "Save" button in the upper right corner to modify and submit.

3. **Other operations**

   1. Modify the metric: The metric can be modified. (Note: If the metric has been experimentally followed after creation, only the name and description can be modified.)

   2. Replicable metrics: Replicable metrics

   3. Delete metrics: reproducible metrics (Note: metrics that have been experimentally followed are not allowed to be deleted)


<span id="二、事件指标的计算方式-（算子）"></span>
# Reference 1: Calculation method of event metric (operator)


|Serial number |Metric calculation method |Meaning |Example (Take the " **payment" event and its attribute "payment amount" as an example:**  ) |
|---|---|---|---|
|1 |Number of entries per person |Number of occurrences per incoming user that triggered the current event. pv/au, the total number of current events/the number of incoming users. |PV/au, average number of payment activities = number of clicks on the payment event/number of samples entering the payment experimental group |
|2 |Conversion rate |Percentage of incoming users who triggered the current event. Uv/au, the total number of incoming users/incoming users for an event. |UV/au, payment conversion rate = the number of clicks on the payment event/the number of samples entering the payment experimental group (au represents the active users entering the experimental group) |
|3 |Press... to find the average number of people in the group |sum/au, the number of users that a property value sums/groups. |Sum/au, find the experimental active mean according to the payment amount (select pay_amount attribute) |
|4 |Find the average daily activity by |Sum/sum (dau), the sum of a property value/user active days. |Sum/sum (dau), find the average daily activity by the payment amount (select pay_amount attribute) |
|5 |Daily activity average |Pv/sum (dau), the total number of events/days of user activity. |PV/sum (dau), average daily payment activity = total number of payment events/user active days |
|6 |Per capita |Number of events per capita. Pv/uv, the total number of occurrences of the current event by the incoming user/the number of people reported by the incoming user. |pv/uv, the number of payers per capita = the number of payments/the number of payers |
|7 |Per person |sum/uv, the sum of a property value/event triggers the number of people entering the group. |Sum/uv, average by payment amount (select pay_amount attribute) |
|8 |Average by |sum/pv, the sum of a property value/the number of events. |Sum/pv, average by payment amount (select pay_amount attribute) |
|9 |Total number of times |PV, the number of times the event occurred. |pv, number of payments = number of payment events triggered |
|10 |Total headcount |UV, the total number of people who triggered the event. |uv, the number of payers = the number of payers triggered by the event |
|11 |Sum by |Sum, the sum of the values of a property (only sums of numeric types are supported, not sums of string types). |Sum, sum by payment amount (select pay_amount attributes) |
|12 |Press... to deduplicate |The number of deduplicates for a property value |If the event [Application Exit] deduplicate the number according to [Session ID], that is, the number of session IDs for which the application exits (count distinct session_id) |
|13 |Calculate the average value of the group according to the latest value |Sum/group the number of users by the latest value of the selected event property in the time interval |For example: points per member = member points/number of users entering the group |
|14 |Calculate the average value of the incoming group according to the earliest value |Sum/group the number of users by the first non\-null value of the selected time attribute in the time interval. |Calculate the per capita first conversion order amount after the user enters the group, it is calculated: `sum (all users`**`first non-empty order amount`**`)/uv`. |


<span id="三、事件指标置信度"></span>
# Reference 2: Event metric confidence level

<span id="_1-哪些指标支持计算置信度？"></span>
## **What metrics support calculating confidence levels?** 

<span id="以下算子的单一指标："></span>
#### **A single metric for the following operators:** 


* Number of group entries per person: The number of occurrences per person of the group that triggered the current event. pv/au, the total number of current events/the number of incoming users.

* Conversion rate: The percentage of incoming users who triggered the current event. Uv/au, the total number of incoming users/incoming users for an event.

* Press... to find the average value of the group: sum/au, sum the value of a certain attribute/the number of users in the group.

* Number of events per person: The number of events triggered per person. Pv/uv, the total number of occurrences of the current event by the incoming user/the number of people reported by the incoming user.

* According to... Average number of people: sum/uv, the sum of a certain attribute value/event triggers the number of people entering the group.

* Press... to find the average: sum/pv, sum the value of a certain attribute/the number of events.


<span id="组合指标："></span>
#### **Combination metrics:** 


* The numerator is of type UV and the denominator is of type UV.

* The numerator is of type PV and the denominator is of type PV.

* The numerator is of type PV and the denominator is of type UV.

* The numerator is of type PV and the denominator is of type Sum.

* The numerator is of type sum and the denominator is of type sum.

* The numerator is of type sum and the denominator is of type uv.

* The numerator is of type sum and the denominator is of type pv.


<span id="_2-哪些指标不支持计算置信度？"></span>
## **Which metrics do not support calculating confidence levels?** 

<span id="以下算子的单一指标："></span>
#### A single metric for the following operators:


* Total: The number of times an event has occurred.

* Total number of people: the total number of people who triggered the event.

* Sum: the sum of the values of an attribute.

* Press deduplicate: The number of deduplicates for a property value.
