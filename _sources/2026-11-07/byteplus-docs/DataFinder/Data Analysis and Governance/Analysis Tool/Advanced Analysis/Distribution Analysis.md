---
title: "Distribution Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Distribution_Analysis"
---

Distribution analysis refers to the division of some intervals (distribution intervals) according to the calculation results under the whole or a certain dimension (the index of distribution analysis), and the distribution of the corresponding number of people in each interval is checked. For example, looking at the distribution of an application's user satisfaction score (index) in the three distribution ranges of less than 2 points, 2 to 5 points, and more than 5 points is used to analyze the overall user satisfaction of the application. This article provides you with instructions for using the DataFinder distribution analysis tool.

<span id="_1-概念介绍"></span>
# Background information

DataFinder distribution analysis supports a variety of distribution analysis scenarios, such as viewing the distribution of people by the frequency of events, viewing the distribution of people by the calculation results of attribute values, and viewing the distribution of people by the cumulative duration or number of days in a period of time.


|**Typical scene** |**scene example** |
|---|---|
|View the distribution of people by incident frequency |That is, within a certain period of time, divide the interval according to the number of times the user performs an event, and check the distribution of users, such as the distribution of users who play a game every day playing a certain mode game. |
|View population distribution by cumulative duration or number of days over a period of time |It means that within a certain period of time, the user accumulates the number of hours and days that the event is triggered to analyze the user's stickiness. The user triggers it at least once an hour, so remember that it occurs from time to time. Similarly, as long as the user triggers it once a day, they will remember that it happened that day. |
|Calculate Results by Attribute Value View Population Distribution |According to the distribution of event attributes, such as: by amount distribution, the amount is regarded as the attribute of the event, and the amount is divided into different ranges of less than 100 yuan, 100 yuan to 200 yuan, and more than 200 yuan. Observe the number of payers/times in different ranges. |


<span id="ebeb56a3"></span>
# Operation steps

After logging in to the DataFinder console, select **Analysis Tools \> Advanced Analysis \> Distribution Analysis** at the top, and after entering the Distribution Analysis page, you can refer to the following to perform distribution analysis on the reported business data.

<span id="a67d0541"></span>
## Step1: Select the indicator event

According to business needs, configure distribution analysis metrics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da93a96ade0f4ce4928aaac315631453~tplv-goo7wpa0wc-image.image) </span>


1. Select the indicator events to be analyzed, support the selection of `general events`, `virtual events`and `circled events`as indicator events for distribution analysis.

2. Select how the metric event is calculated. For example, the total number of corresponding events (PV), days, hours, and so on.

3. (Optional) You can add filters to events.


<span id="_3-3-选择分布区间"></span>
## Step2: Select the distribution range

The current DataFinder provides you with several commonly used preset grouping methods, which is convenient for you to quickly choose. It also allows you to customize grouping rules according to your business analysis needs.


|Grouping |Configuration instructions |
|---|---|
|Preset **shortcut options**<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8e8d7bafd4fd4f6498fac519a4204ee5~tplv-goo7wpa0wc-image.image) </span> |According to the different indicator event calculation methods you choose, the supported shortcut grouping methods are also slightly different. The details are subject to the optional methods of the interface. All currently supported shortcut grouping methods include:<br><br><br>* **Default** : The default grouping is the suitable distribution interval automatically calculated by the system according to the `sturges`algorithm. You can revert to the `default`grouping by clicking the Delete button on the range drop\-down menu.<br><br>* **Preset** : 1, 2, 3, 4, 5, 6\-10, 11\-20, 20\-50, 50\-100 and more than 100 times to group the corresponding number of people.<br><br>* **Equal points** : By default, the number of people corresponding to the indicator is grouped according to 5 equal points, 10 equal points and 15 equal points.<br><br>* **Customization** : You can freely set the number of equal groups and the interval of each group to make more flexible grouping. |
|Custom interval grouping<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da5c9c08e0d844a48c626cc0918c54b3~tplv-goo7wpa0wc-image.image) </span> |You can fully customize the metric data into several groups and the range of data intervals for each group according to your own business needs. |


<span id="_3-4-过滤用户"></span>
## Step3: Filter users

You can configure the filter criteria in the configuration area of the **sub\-filter** at the top right to filter the target user range to be analyzed, such as filtering: `New and old users = old users and cities = shenzhen and operating system = android`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea1553af65f548cd83ffb869e3c70118~tplv-goo7wpa0wc-image.image) </span>

Specifically, users to be analyzed can be filtered according to the following conditions or a combination of conditions:


* By user group: Select "By user group" as the filter criterion and specify the user group to filter.

* By Attribute: Select event/user attributes (e.g. operating system, software version, etc.) as the filter criteria, and refine the filter criteria.

* You can select and set multiple conditions simultaneously, and set the logical relationship between each condition.


Detailed functional introduction of segmentation screening can be found [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering).

<span id="_3-5-分布分析图表"></span>
## Step4: Set query time and chart type

Review the visualization chart of the analysis results and make adjustments as required.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c56dd09876cd4469abc05c47a85e5b9c~tplv-goo7wpa0wc-image.image) </span>


* Select the query time.

   * Set the time granularity of the analysis: day level;

   * Set the analysis time period: You can set it by "last xx days, up to 120 days" or "time range";

* Choose the distribution analysis chart as a **trend** chart or a **group** chart

* Trend Chart supports setting a segmented trend chart type at the top right of the chart.


<span id="_3-6-详细数据"></span>
## Step5: View detailed data

Detailed data table showing analysis results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0788365098ea4069b43a8fa1df2210c1~tplv-goo7wpa0wc-image.image) </span>

The detailed data table supports the following operations:


* Sort the statistical results.

* It can be downloaded as an excel file.


<span id="1b656a5b"></span>
# Analysis example

<span id="50a1e578"></span>
## Example scenario

Operators analyze the distribution of old users **the number of application launches** , and count the distribution of the total time each user uses the APP on the same day, that is, observe the daily start 1/2 times/3 times/4 times/5 times... How many users of the APP are there n times? Then check the health of the overall user and carry out refined operations.


* Select the `app launch (app_launch)`event;

* Select Calculate as `Total Count`.


<span id="33f77cb0"></span>
## Example action steps


1. Select **Analysis Tools \> Advanced Analysis \> Distribution Analysis** and go to the Distribution Analysis page.

2. Select the analyzed event `app launch (app_launch)` and view the distribution by total number of events.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32689fd557054da5ab163be299e7b074~tplv-goo7wpa0wc-image.image) </span>

3. Segmentation filter, "operating system = android";

4. View event analysis chart, you can choose line chart, bar chart, stack chart for display;

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24d6ea5771be4324a384669d25986dd7~tplv-goo7wpa0wc-image.image) </span>

5. Review the detailed data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a1e74db588e481d8e19b1574b097c62~tplv-goo7wpa0wc-image.image) </span>


<span id="_4-常见问题"></span>
# Common problem


1. What do the terms \- ∞ and + ∞ mean?

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5aec92d93e6e4f16995a36c95a9cfdf9~tplv-goo7wpa0wc-image.image) </span>

   That is, the reference of the minimum value to the maximum value of the selected indicator, and the required value can be filled in as needed.


<span id="_5-分布分析视频讲解"></span>
# Distribution analysis video explanation

<video src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_23192bed45d4af309b0f7bc93008cece.mp4" controls></video>
