---
title: "Funnel Analysis"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Funnel_Analysis"
---

The conversion analysis in the BytePlus Growth Analysis platform is called funnel analysis, which is mainly used to analyze the conversion of users in the process. First, the entire process is broken down into individual steps, and then the conversion rate is used to measure the performance of each step. Finally, the problem is identified through abnormal data indicators, so as to solve the problem, optimize the step, and finally achieve the goal of improving the overall conversion rate. This article introduces you to the computational logic and operational essentials of transformation analysis.

<span id="91c23e81"></span>
# Background information

<span id="9ae4d0f3"></span>
## Basic concept

According to the definition of funnel analysis, we can abstract three elements of conversion: time (conversion window), node (funnel event), and flow (UV or PV).


|Term |Concept introduction |
|---|---|
|Time (conversion window) |Refers to the conversion cycle of a process, which is the set of time required to complete each layer of transformation, expressed in the DataFinder as the conversion window period.<br><br>In general, the shorter the conversion cycle of a process, the better, especially in some industries with longer conversion cycles, such as online education and B2B e\-commerce.<br><br>In addition, looking at the conversion time of each layer individually can also reveal some issues. For example, if it is found that the traffic imported from a certain channel takes surprisingly consistent time to convert at a certain layer, it indicates that the traffic of that channel is likely to be abnormal. |
|Node (funnel event) |Each layer of events is a node. For nodes, the most crucial metric is the conversion rate. By analyzing the conversion rate of the entire process and the conversion rate of each layer, we can clarify the direction of optimization: find nodes with low conversion rates and find ways to improve them. |
|Flow rate (UV or PV) |That is, crowds, and DataFinder's funnel analysis calculation logic supports switching between number of people (UV) or number of times (PV) to calculate crowd flow. The performance of different groups of people under the same conversion path must be different. For example, in Taobao's shopping funnel, the conversion rates of men and women are different, and the conversion rates of young people and the elderly are also different. By classifying the population, we can quickly see the conversion rate of a specific population, enabling us to better identify the problem. |
|Conversion step |DataFinder provides you with an analysis chart of conversion steps, using funnel/bar charts to view the overall time (conversion window period) range, conversion rate for the entire funnel or each step, number of conversions, etc. |
|Conversion trend |DataFinder provides you with an analysis chart of conversion trends. Through a line chart, it shows the change trend of the conversion rate, the number of conversions, and the conversion time interval for the entire funnel or each step within the time (conversion window period) according to the selected time granularity. |
|Conversion time |DataFinder provides you with an analysis chart of conversion times, using a bar/box chart to view the distribution of the entire funnel or conversion intervals per step over a time frame. |


<span id="a3ed184b"></span>
## Ordered and disordered funnels

The conversion funnel calculation logic of the funnel analysis function provided by DataFinder includes both ordered and unordered funnels.


* **Ordered funnel** : The order of occurrence between each step of the funnel is strictly defined within the period of the funnel.

* **Disordered funnel** : The order in which events occur between multiple steps of the funnel is not limited during the period of the funnel.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A more detailed description of the computational logic of ordered and disordered funnels can be found in the following <a href="https://docs.byteplus.com/docs/DataFinder/Funnel_Analysis#07f36daf">Example of use (detailed example of calculation method)</a>sections, and the following is a simple example to give you an overview of the differences between the two funnels.</div>



|Funnel event |Number of conversions |Example of an ordered funnel |Disordered funnel example |
|---|---|---|---|
|Event A |Number of users in which A has occurred in the time frame |* Suppose a funnel contains three funnel events, A, B, and C. The occurrence time of the A event must precede the B event, and the user's behavior order must be A\- \> B\- \> C.<br><br>* Like a disordered funnel, funnel steps interspersed with other event steps are still considered a successful funnel conversion for the user. |* Suppose a conversion funnel contains three funnel events, A, B, and C. The occurrence time of the A event can be before or after the B event. The user's sequence of actions is a combination of A, B, and C, all of which count as successful funnel conversions.<br><br>* Even if the funnel events are interspersed with other events, the user is still considered to have completed a successful funnel conversion. |
|Event B |Number of users who have had A and (and) B in the time range |||
|Event C |The number of users in the time range who have experienced A and (and) B and (and) C |||


<span id="4af8a5a4"></span>
## Computational logic


* **Number of people (UV)** 

   * Overall conversion rate = the number of people reaching the current funnel event/the number of people at the first funnel event

   * Previous conversion rate = the number of people reaching the current funnel event/the number of people in the previous funnel event

* **By number of times (PV)** 

   * Overall conversion rate = the number of times the current funnel event was reached/the number of times the first funnel event was reached

   * Previous conversion rate = number of times the current funnel event was reached/number of previous funnel events


Detailed conversion calculation method and calculation details can be found below [Example of use (detailed example of calculation method)](https://docs.byteplus.com/docs/DataFinder/Funnel_Analysis#07f36daf).

<span id="64ae5be6"></span>
## **Typical scene**

Funnel analysis (i.e. funnel analysis) is widely used for statistical analysis of user process conversions. Typical use cases include, but are not limited to:


* Conversion rate analysis of user process in the product: such as analysis of conversion rate, order payment conversion rate, etc.;

* Analysis of the conversion rate in the process of activity or user operation: such as the funnel analysis of activity red envelopes from collection to use, etc.;

* Transformation analysis of marketing channels, defining channel value and adjusting operating strategies accordingly.


Examples of scenarios are as follows:


|Example scenario |Conversion step |Calculation logic (take the computation logic of an ordered conversion funnel as an example) |
|---|---|---|
|Scenario 1: Video products, the conversion of users watching videos |The complete process for a user to watch a video may involve the following steps:<br><br><br>1. Click for video<br><br>2. video loading<br><br>3. video playback<br><br>4. Video playback complete |If the window period is set to 10 minutes, only users who have completed "video loading", "video playback", and "video playback complete" in sequence within 10 minutes after "clicking video" will be counted as users who have completed the conversion. If a user completes only the "Video Load" event within 10 minutes, then that user is counted as a user lost during the "Video Load" \> "Video Play" process. |
|Scenario 2: E\-commerce products, the conversion of user purchases |The completion process for a user to purchase a product may include the following steps:<br><br><br>1. Browse products<br><br>2. Add shopping cart<br><br>3. Submit an order<br><br>4. Complete payment |The above process can be set as a funnel, for example, the conversion period is set to 1 day, the system will sort the behavior according to the actual time that the user client side occurs. After the user browses the goods, he needs to proceed in sequence within the next 24 hours **Add shopping cart \> Submit order \> Complete payment** , will be counted as the user who completes the conversion; if only the **Browse product \> Add shopping cart** is completed within 24 hours, then the user is counted as the user who lost in the **Add shopping cart \> Submit order** link. |


<span id="f21ef284"></span>
# Function usage

After logging in and entering the DataFinder console, click **Analysis Tools** \> **Advanced Analysis** \> **funnel analysis** in the top navigation bar. After entering the funnel analysis page, refer to the following to configure.

<span id="dafe74cc"></span>
## Configuration calculation calculation method

Configuration parameters related to the calculation logic of the entire funnel analysis can be configured at the top of the page.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Only the default principal supports switching the calculation mode. The non\-default principal calculation method only supports the number of people.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b8550c1511b440e86647c03eadbcb75~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Calculation mode |Choose whether to use **an ordered funnel** or a **disordered funnel** according to the actual business situation. Defaults to an ordered funnel.<br><br>The privatized 4.9.2 version begins to support the unordered funnel mode, please refer to the **background information** section above for details. |
|Subject |If you have enabled the multi\-principal function, you can switch which principal to use at the top, see for details [Multi-Application/ Multi-Agent/ Multi-ID Type Overview](https://docs.byteplus.com/docs/DataFinder/Multi-Application_Multi-Agent_Multi-ID_Type_Overview). |
|Statistical caliber |The current DataFinder uses the user (ssid) as the statistical caliber of the analysis data by default. If you want to use other statistical calibers, you can create a good caliber and switch it. Please refer to the details . |
|Calculation method |Select whether the calculation method is "number of people" or "number of times", that is, whether the funnel analysis data is calculated according to UV data or PV data. |
|Sssociated attribute |Select whether you need to turn on the associated property switch according to the business situation. Associated properties are used to keep a property value consistent between any two or more funnel steps, and are often used for things like activity names, page titles, or product names.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">All configured associated properties must have values, and the value types must be consistent.</div><br> |


<span id="73d8efd8"></span>
## Configure/save metrics


* You can configure metrics for funnel analysis directly in the Configure metrics area by defining conversion window periods and funnel events for conversion funnels.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/751079c0388d4398884f81249c1056b5~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Transition window |The window period refers to the time when the user completes the conversion, and the user completes the complete conversion process within the set window period to be considered a successful conversion.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Unordered funnel mode does not require configuration, only ordered funnel mode requires configuration.</div><br><br><br><br>* When the conversion window is selected as "Custom", select "Seconds, Minutes, Hours, Days", and the default is 10 minutes.<br><br>* The conversion window period also supports selecting "same day".<br><br><br>You can set the rules for the window period.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba1120db2428455faae8fc03f029775b~tplv-goo7wpa0wc-image.image) </span> |
   |Funnel event |You can click "+ Funnel Events" to add a funnel event, and the following detailed configuration of the funnel event is supported.<br><br><br>* Modify aliases: For ease of understanding, you can set an alias name for each funnel event. The default is the event name of the selected funnel event. Click the Modify button after the default name to customize the modification.<br><br>* Copy metrics: Click the Copy button after the configured funnel event to copy the added funnel event with one click.<br><br>* Support for adding filter conditions to funnel events.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd81f1266a2a4a88a99b27ea49b93095~tplv-goo7wpa0wc-image.image) </span><br><br>   * Support adding multiple filters, and support switching the logical relationship between multiple filter conditions to "AND" and "OR".<br><br>   * Supports two\-layer filtration conditions.<br><br>* **Support for adding multi\-path comparison analysis.** <br><br>   **Multi\-path comparison** refers to changing any event link in the original conversion path (including the starting point event and the end point event), so as to form multiple path branches, and compare and analyze the conversion funnel of multiple path branches. See below for details [Reference: Multipath Comparative Analysis](https://docs.byteplus.com/docs/DataFinder/Funnel_Analysis#47a47526). |
   

* For solidifiable metrics, you can click the Create Metrics button above to create them. After the creation is completed, you can directly select the corresponding metrics in the drop\-down box for selecting metrics during funnel analysis to improve the efficiency of funnel analysis configuration.

   1. Click the Create Metric button.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0b71bd8df534d50bc759132a3c89041~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can also create conversion metrics on the metrics management page. The metrics configuration details are as follows.      </div>
      

   2. Configure the indicator creation parameters in the pop\-up window. The parameter configuration for creating the indicator is consistent with the parameters for manually configuring the indicator above. After the configuration is completed, click **Save** to complete the indicator creation.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dfbc10880f004cd198dfede85603473c~tplv-goo7wpa0wc-image.image) </span>

   3. After creating the metrics, you can directly select the created metrics on the funnel analysis, and you can also view all the created conversion metrics on the metrics management page.

      
      |Select directly from the funnel analysis page |View the list of created metrics on the metrics management page |
      |---|---|
      |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/584155d68e454107bc0a651bb8fe01a1~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7377e25dccd148799c805b52acb6288d~tplv-goo7wpa0wc-image.image) </span> |
      


<span id="e604d119"></span>
## Configure Segmentation Filtering


1. Configure Segmentation Filtering

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e48e08b9cf28417baf46dd477bfc8e43~tplv-goo7wpa0wc-image.image) </span>

   * Select the first filter condition of the user to be analyzed in the sub\-filter area, and refer to the filter logic details [In-Text Grouping (Segmentation Filtering)](https://docs.byteplus.com/docs/DataFinder/In-Text_Grouping_Segmentation_Filtering).

      * **Attribute filtering** : event attributes, user grouping, user attributes, user tags (such as open), etc. The user group selects the latest one\-day calculation result by default, and can switch the calculation logic by clicking "Latest Data" to specify a certain one\-day result.

      * **Behavior Circle** : Users who have "done/not done/done XX behavior in turn" within the specified time frame.

      * **Dynamic matching** : Filter by dynamically matching events with the crowd at specified intervals.

      * You can click  **+ Attribute Filter**,  **+ Behavior Circle Selection**,  **+ Dynamic Circle Selection** below to add multiple first\-level filter conditions, and the logical relationship between multiple filter conditions can be set to **AND** or **OR**.

   * You can hover the mouse behind the filter to add a secondary filter to the filter. Supports the addition of multiple secondary filter conditions, and the logical relationship between multiple secondary filter conditions can be set to **AND** or **OR**.

2. Add a control group.

   * You can click  **+ control group** , which is equivalent to grouping and comparing the results.

   * Supports the creation of multiple control groups, and replicates created control groups.

3. Other supported operations:

   * Modify the name of each filter group.

      You can click the "small pencil" button after the filter group name to rename the filtered user group for easy memory.

   * Batch entry filter criteria.

      You can click the "small pencil" button after the filter conditions, and enter the filter conditions in batches according to the interface prompts to improve the configuration efficiency.


<span id="c9735bd0"></span>
## Configure attribute grouping

After configuring attribute grouping, the result chart of subsequent query analysis will be grouped and displayed according to the dimension of each attribute value configured, which is convenient for more refined analysis.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Grouping behavior cannot be performed when performing multipath comparisons.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed94ac10b55c4e5482fcaa9eb795ad98~tplv-goo7wpa0wc-image.image) </span>


* You can set the event attributes, user attributes, and user labels of the grouping (label capability needs to be enabled), so that the statistical results can be compared according to the selected attribute dimension.

* After selecting the properties for grouping, the first funnel event is finally grouped into properties, with no effect on the other funnels. You can manually configure which funnel events are the event scope of the grouped application.

* Currently, up to 10 properties can be selected for grouping display, and you can quickly find the properties to be grouped by searching in the search box.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the ordered funnel, when using conversion metrics, if the calculation method of conversion metrics is "times", setting multi\-attribute grouping is not supported for the time being.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When multiple properties are selected to be grouped, properties of type List cannot be used with properties of other types.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">After configuring multiple attribute groupings, viewing conversion time charts will not be supported in subsequent query charts.   </div>
   


<span id="fd915512"></span>
## Configure and view result graphs


1. Configure query time granularity and time range.

   By default, DataFinder automatically displays conversion statistics for the last 30 days. You can adjust the analysis time granularity and time range according to your needs, and support the selection of time comparisons.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78edf6c2e8df4ab3a4728d617ecc211f~tplv-goo7wpa0wc-image.image) </span>

   * Configure time granularity: Support viewing hourly, daily, and weekly data.

   * Configuration time range: Support selecting the time range to be analyzed in the time configuration box. The system presets some shortcut options for common time ranges for you to improve configuration efficiency.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">warning      </div>
      

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Under different time granularities, the time range supported by the query is inconsistent. When the current manually selected time range exceeds the maximum time range supported by the query, the actual query result will automatically adjust the time range for you.      </div>
      

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For example, when the time granularity is hourly, the time range for supporting queries is 7 days. If you choose a time range longer than 7 days, the actual query will automatically adjust to 7 days for you.   </div>
   

      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">If the time granularity is weekly, and the time range is less than one week when you select it, the actual query results automatically complete one week's worth of data for you.      </div>
      

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">For example, time granularity is weekly, and if you select data with a time range of 3 days, the actual query results automatically complete a week's worth of data for you.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f5cff9729d284b17a9ec69cfab164e01~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   

   * Configuration comparison time:

      * You can add "comparison time", and you can set a time interval to compare with the target time indicator.

      * You can select the start and end points of the comparison period interval in the icon area. By default, the comparison period interval is the same length as the original focus period.

2. Select the chart type. In the analysis chart, we can perform the following analysis modes:

   
   |**Analysis mode** |**Corresponding chart type** |**Function introduction** |
   |---|---|---|
   |Conversion step |Column chart, funnel chart |View the conversion rate, number of conversions, etc. for the entire funnel or each step in the overall time frame. |
   |Conversion trend |Line chart |View trends for the entire funnel or conversion rate per step, conversion count, and conversion interval over the time range at the selected time granularity. |
   |Conversion time |Column chart, boxline chart |View the distribution of the entire funnel or each conversion interval over the time range by set interval and start and end interval.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">In this mode, the switching time granularity of the chart area does not change the result as expected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disordered funnels do not currently support viewing conversion times.</div><br> |
   

   The following is a detailed introduction to the various types of charts.


<span id="3b45a302"></span>
### Analysis Chart: Transformation Steps


* **Conversion funnel**

   The conversion funnel chart directly shows the conversion rate from [previous step] to [current step] (ie, the conversion rate of the previous step). You can click the chart to view the overall conversion rate.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52650fc9bd0b475bb314c5f0ee686c75~tplv-goo7wpa0wc-image.image) </span>

   * The funnel chart will be compared and displayed according to different grouping values or multipaths.

   * The graph highlights the conversion rate, attrition rate, maximum attrition rate, and other data for each funnel event.

   * Support click on the funnel map after evoking the microscope, you can view the overall conversion rate of each funnel event, the conversion rate of the previous step, and support the query of the user to save the user group, export users and other operations, more detailed microscope functions, you can click: [Microscope Function](https://docs.byteplus.com/docs/DataFinder/Microscope_Function).

   * You can set different comparison items to compare different grouping values according to your own needs.

* **Funnel chart**

   The basic funnel chart shows the conversion rate (ie, the overall conversion rate) from [first step] to [current step], and the resulting data will be different from the data of the conversion funnel chart.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5441375104d1444bad11061e44066d63~tplv-goo7wpa0wc-image.image) </span>

* **Bar chart**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc934cad78be4102bfba9bd48eb9a4eb~tplv-goo7wpa0wc-image.image) </span>

   * The histogram will be displayed according to the aggregation of different funnel events, with the same event spacing smaller and the different event spacing larger;

   * The order and color of the columns in the same group are the same in different steps.

   * The legend shows the grouping values of different groups. You can click on different groups. If the color changes to gray, it means that the group is not displayed, such as the gray "Shaanxi, Jiangsu" group;

   * You can drag the "gray progress bar" below left and right to view all group conversions.


<span id="4339807a"></span>
### Analysis Chart: Conversion Trends

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f705f5bd0a9b4c1cb3d31a26cc2a9bc3~tplv-goo7wpa0wc-image.image) </span>


* Default support line chart for the optimal display form, horizontal axis for the date, vertical axis for the conversion rate;

* There is a flowchart on the right side of the line chart, marking an n\-step transformation process, n\-1 transformations (event 1 to event 2, event 2 to event 3... event n\-1 to event n), click to switch the line chart display;

* When multi\-grouping and multi\-funnel, the line graph becomes multi\-line display, similar to event analysis.

* You can drag the "gray progress bar" below to view all group conversions;

* Click on the dot on the polyline to use the ability to create a new date annotation, save as a user group, export a user ID, view a user list, and more.


<span id="fdb3e00c"></span>
### Analysis Chart: Conversion Time


* **Interval setting**

   You can set the interval and the specific steps to be viewed through the settings area in the upper right corner of the chart. The interval supports "seconds, minutes, hours, days". The specific display depends on the time granularity of the selected window period, and the number of conversion steps depends on the number of event funnels created.

* **Interval distribution map**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4d76a35e964458189f12bde689b5e61~tplv-goo7wpa0wc-image.image) </span>

   * The horizontal axis is the time interval, and the vertical axis is the proportion of the number of completed conversions;

   * The bar where the median value is located is the bar where the median value of all conversion times is located;

* **Box diagram:** 

   Through the boxplot, you can clearly see the distribution of the overall conversion and the conversion time between steps. We provide the maximum, minimum, median, average, 75th, 25th, and other indicators to help users gain insight into the distribution of time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89d7298163584f13bba114857d5db93a~tplv-goo7wpa0wc-image.image) </span>


<span id="1c34cef1"></span>
## View detailed data

Detailed data table showing statistical results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff52a612495341289750d44b28ffecaf~tplv-goo7wpa0wc-image.image) </span>


* Support clicking "+" in front of the data table to expand the detailed data. If the comparison time range is checked, the detailed data table will display the data in this period and the comparison period at the same time.

* The following operations are supported:

   * Sort the statistical results.

   * Download as an excel file.


<span id="07f36daf"></span>
# Example of use (detailed example of calculation method)


|Funnel event example |Ordered funnel |Disordered funnel |
|---|---|---|
|configuration example |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/611454b0c2fc48148d51130fa1a053c5~tplv-goo7wpa0wc-image.image) </span> |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/690fc9a0c18941fe84698a1f905c5a05~tplv-goo7wpa0wc-image.image) </span> |
|Step 1 Product exposure |Result data:<br><br><br>* Number of people: 84,174<br><br>   The number of people who experienced the Step 1 product exposure event.<br><br>   In Event Analysis, you can view the total UV values for the first funnel event that occurred over the event period.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/412224e382dc4a44a0aff1779c37041d~tplv-goo7wpa0wc-image.image) </span><br><br>* Overall conversion rate 100% (84,174/84,174)<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you use event analysis to query data that validates the results of funnel analysis, be sure to pay attention to the time impact of the window period, which may result in slightly fewer query results than funnel analysis results in event analysis. For example, the window period is 10 minutes, and the data for funnel analysis is actually within the time range of 00:10 from 20240707 to 20240713.</div><br> ||
|Step 2 Product Click |Result data:<br><br><br>* Number of people: 63,179<br><br>   The Step 1 product exposure event occurs first, and it occurs within the window period. The number of people who click on the Step 2 product event.<br><br>* Previous conversion rate: 75.06%<br><br>   = **Number of people reaching the current funnel event/Number of people in the previous funnel event**<br><br>   = 63,179 / 84,174<br><br>   ≈ 75.06%<br><br>* Overall conversion rate: 75.06%<br><br>   = **Number of people reaching the current funnel event/Number of people at the first funnel event**<br><br>   = 63,179 / 84,174<br><br>   ≈ 75.06%<br><br>* Overall attrition rate: 24.94%<br><br>* Previous attrition rate: 24.94% |Result data:<br><br><br>* Number of people: 65,506<br><br>   The Step 1 product exposure event occurred, and it occurred within the window period. The number of people who clicked on the product in Step 2 has no order limit for Steps 1 and 2. You can perform query validation in event analysis.<br><br>* Previous conversion rate: 77.82%<br><br>   = **Number of people reaching the current funnel event/Number of people in the previous funnel event**<br><br>   = 65,506 / 84,174<br><br>   ≈ 77.82%<br><br>* Overall conversion rate: 77.82%<br><br>   = **Number of people reaching the current funnel event/Number of people at the first funnel event**<br><br>   = 65,506 / 84,174<br><br>   ≈ 77.82%<br><br>* Overall attrition rate: 22.18%<br><br>* Previous attrition rate: 22.18% |
|Step 3 Check the product details |Result data:<br><br><br>* Number of people: 59,828<br><br>   During the window period, the Step 1 product exposure event, the Step 2 product click event, and the number of people who viewed the product details in Step 3 occurred in sequence.<br><br>* Previous conversion rate: 94.7%<br><br>   = **Number of people reaching the current funnel event/Number of people in the previous funnel event**<br><br>   = 59,828 / 63,179<br><br>   ≈ 94.7%<br><br>* Overall conversion rate: 71.08%<br><br>   = **Number of people reaching the current funnel event/Number of people at the first funnel event**<br><br>   = 59,828 / 84,174<br><br>   ≈ 71.08%<br><br>* Previous attrition rate: 5.3%<br><br>   = **churn of current funnel event/previous funnel event**<br><br>   = （63,179 \- 59,828） / 63,179<br><br>   ≈ 5.3%<br><br>* Overall attrition rate: 3.98%<br><br>   = **Number of churns from the current funnel event/Number of funnel events in the first step**<br><br>   = （63,179 \- 59,828） / 84,174<br><br>   ≈ 3.98% |Result data:<br><br><br>* Number of people: 62,729<br><br>   The number of people who have experienced the Step 1 product exposure event, the Step 2 product click event, and the Step 3 product details during the window period has no event sequence limit.<br><br>* Previous conversion rate: 95.76%<br><br>   = **Number of people reaching the current funnel event/Number of people in the previous funnel event**<br><br>   = 62,729 / 65,506<br><br>   ≈ 95.76%<br><br>* Overall conversion rate: 74.52%<br><br>   = **Number of people reaching the current funnel event/Number of people at the first funnel event**<br><br>   = 62,729 / 84,174<br><br>   ≈ 74.52%<br><br>* Previous attrition rate: 4.24%<br><br>   = **churn of current funnel event/previous funnel event**<br><br>   = （65,506 \- 62,729） / 65,506<br><br>   ≈ 4.24%<br><br>* Overall attrition rate: 3.3%<br><br>   = **Number of churns from the current funnel event/Number of funnel events in the first step**<br><br>   = （65,506 \- 62,729） / 84,174<br><br>   ≈ 3.3% |


<span id="b581d868"></span>
# Related operations: Save to Dashboard

Add indicator charts that require long\-term monitoring to the Dashboard board.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6932185f827e4020b4231a5ee71a45ab~tplv-goo7wpa0wc-image.image) </span>

Operation steps:


1. Click "Save to Dashboard" in the upper right corner.

2. Name the chart and select the target dashboard to save.


<span id="47a47526"></span>
# Reference: Multipath Comparative Analysis

**Multi\-path contrast:**  It refers to changing any event link in the original transformation path (including the starting point event and the ending point event), thereby forming multiple path branches.

Constraints include:


* The order of events and the number of events in multiple paths are exactly the same, and the events with only one identical link are different from each other;

* Support up to 5 path comparisons;

* Grouping behavior cannot be performed when performing multipath comparisons.


The following figure is an example of two multipath conversions:


* Transformation Path 1:

   <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI2ODVweCIgaGVpZ2h0PSIzNjVweCIgdmlld0JveD0iLTAuNSAtMC41IDY4NSAzNjUiPjxkZWZzPjxsaW5lYXJHcmFkaWVudCB4MT0iMCUiIHkxPSIwJSIgeDI9IjAlIiB5Mj0iMTAwJSIgaWQ9Im14LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wIj48c3RvcCBvZmZzZXQ9IjAlIiBzdHlsZT0ic3RvcC1jb2xvcjojZmZmZmZmIi8+PHN0b3Agb2Zmc2V0PSIxMDAlIiBzdHlsZT0ic3RvcC1jb2xvcjojQ0NDQ0NDIi8+PC9saW5lYXJHcmFkaWVudD48L2RlZnM+PGc+PHBhdGggZD0iTSAxMDIgMTgyIEwgMTMzLjc2IDE4MiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTM5Ljc2IDE4MiBMIDEzMS43NiAxODYgTCAxMzMuNzYgMTgyIEwgMTMxLjc2IDE3OCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTUyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+MS5DaG9vc2UgYSBjYXI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjQyIDE4MiBMIDI3My43NiAxODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3OS43NiAxODIgTCAyNzEuNzYgMTg2IEwgMjczLjc2IDE4MiBMIDI3MS43NiAxNzggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE0MiIgeT0iMTUyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxODJweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj4yLiBCcmFuZCBzZXJpZXMgdGFibGU8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMzgyIDE4MiBMIDQxMiAxODIgTCA0MTIgMzIgTCA0MzMuNzYgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzOS43NiAzMiBMIDQzMS43NiAzNiBMIDQzMy43NiAzMiBMIDQzMS43NiAyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAzODIgMTgyIEwgNDEyIDE4MiBMIDQxMiAzMzIgTCA0MzMuNzYgMzMyIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MzkuNzYgMzMyIEwgNDMxLjc2IDMzNiBMIDQzMy43NiAzMzIgTCA0MzEuNzYgMzI4IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDM4MiAxODIgTCA0MTIgMTgyIEwgNDEyIDEzMiBMIDQzMy43NiAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQzOS43NiAxMzIgTCA0MzEuNzYgMTM2IEwgNDMzLjc2IDEzMiBMIDQzMS43NiAxMjggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMzgyIDE4MiBMIDQxMiAxODIgTCA0MTIgMjMyIEwgNDMzLjc2IDIzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDM5Ljc2IDIzMiBMIDQzMS43NiAyMzYgTCA0MzMuNzYgMjMyIEwgNDMxLjc2IDIyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMjgyIiB5PSIxNTIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy0zMDYyLTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogMjgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjMuQ2FyIHNlcmllcyBwYWdlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDU0MiAzMiBMIDU3My43NiAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNTc5Ljc2IDMyIEwgNTcxLjc2IDM2IEwgNTczLjc2IDMyIEwgNTcxLjc2IDI4IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI0NDIiIHk9IjIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy0zMDYyLTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiA0NDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+NC0xLiBDYXIgc2VyaWVzIHBhZ2Ugb3ZlcmFsbCB0YWI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTQyIDEzMiBMIDU3My43NiAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU3OS43NiAxMzIgTCA1NzEuNzYgMTM2IEwgNTczLjc2IDEzMiBMIDU3MS43NiAxMjggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMTAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMzJweDsgbWFyZ2luLWxlZnQ6IDQ0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj40LTEuIENhciBzZXJpZXMgcGFnZSBjYXIgdHlwZSB0YWI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTQyIDIzMiBMIDU3My43NiAyMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU3OS43NiAyMzIgTCA1NzEuNzYgMjM2IEwgNTczLjc2IDIzMiBMIDU3MS43NiAyMjggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMjAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzJweDsgbWFyZ2luLWxlZnQ6IDQ0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj40LTEuIENhciBzZXJpZXMgcGFnZSB2aWRlbyB0YWI8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTQyIDMzMiBMIDU3My43NiAzMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDU3OS43NiAzMzIgTCA1NzEuNzYgMzM2IEwgNTczLjc2IDMzMiBMIDU3MS43NiAzMjggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMzAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMzJweDsgbWFyZ2luLWxlZnQ6IDQ0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj40LTEuIENhciBzZXJpZXMgcGFnZSBRJmFtcDtBIHRhYjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTgyIiB5PSIyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzMnB4OyBtYXJnaW4tbGVmdDogNTgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjUuIFEmYW1wO0EgZGV0YWlscyBwYWdlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI1ODIiIHk9IjEwMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI2MCIgZmlsbD0idXJsKCNteC1ncmFkaWVudC1mZmZmZmYtMS1jY2NjY2MtMS1zLTMwNjItMCkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTMycHg7IG1hcmdpbi1sZWZ0OiA1ODNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+NS4gUSZhbXA7QSBkZXRhaWxzIHBhZ2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjU4MiIgeT0iMjAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtMzA2Mi0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzJweDsgbWFyZ2luLWxlZnQ6IDU4M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj41LiBRJmFtcDtBIGRldGFpbHMgcGFnZTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNTgyIiB5PSIzMDIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy0zMDYyLTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMzMnB4OyBtYXJnaW4tbGVmdDogNTgzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjUuIFEmYW1wO0EgZGV0YWlscyBwYWdlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48L2c+PC9zdmc+" />

* Transformation Path 2:

   <img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI0NjVweCIgaGVpZ2h0PSIyNjVweCIgdmlld0JveD0iLTAuNSAtMC41IDQ2NSAyNjUiPjxkZWZzPjxsaW5lYXJHcmFkaWVudCB4MT0iMCUiIHkxPSIwJSIgeDI9IjAlIiB5Mj0iMTAwJSIgaWQ9Im14LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtOTY2OS0wIj48c3RvcCBvZmZzZXQ9IjAlIiBzdHlsZT0ic3RvcC1jb2xvcjojZmZmZmZmIi8+PHN0b3Agb2Zmc2V0PSIxMDAlIiBzdHlsZT0ic3RvcC1jb2xvcjojQ0NDQ0NDIi8+PC9saW5lYXJHcmFkaWVudD48L2RlZnM+PGc+PHBhdGggZD0iTSAxMDIgMzIgTCAxMzMuNzYgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDEzOS43NiAzMiBMIDEzMS43NiAzNiBMIDEzMy43NiAzMiBMIDEzMS43NiAyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI2MCIgZmlsbD0idXJsKCNteC1ncmFkaWVudC1mZmZmZmYtMS1jY2NjY2MtMS1zLTk2NjktMCkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+MS4xIENsaWNrwqByb3RhdGluZyBicm9hZGNhc3RpbmcgYXJlYTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMDIgMTMyIEwgMTMzLjc2IDEzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTM5Ljc2IDEzMiBMIDEzMS43NiAxMzYgTCAxMzMuNzYgMTMyIEwgMTMxLjc2IDEyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMTAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtOTY2OS0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+MS4yIENsaWNrIHBhZ2UgdG9wIHRhYjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAxMDIgMjMyIEwgMTMzLjc2IDIzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMTM5Ljc2IDIzMiBMIDEzMS43NiAyMzYgTCAxMzMuNzYgMjMyIEwgMTMxLjc2IDIyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMiIgeT0iMjAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtOTY2OS0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzJweDsgbWFyZ2luLWxlZnQ6IDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+MS4zIENsaWNrIGNvbnRlbnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjM2MiIgeT0iMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI2MCIgZmlsbD0idXJsKCNteC1ncmFkaWVudC1mZmZmZmYtMS1jY2NjY2MtMS1zLTk2NjktMCkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDM2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj40LTEuIENhciBzZXJpZXMgcGFnZSBRJmFtcDtBIHRhYjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAyNDIgMzIgTCAzNTMuNzYgMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzU5Ljc2IDMyIEwgMzUxLjc2IDM2IEwgMzUzLjc2IDMyIEwgMzUxLjc2IDI4IFoiIGZpbGw9IiM3ZWE2ZTAiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIxNDIiIHk9IjIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy05NjY5LTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAxNDNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+Mi4gU3RhcnQgcXVlc3Rpb25pbmc8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjQyIDEzMiBMIDM1My43NiAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzdlYTZlMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMzU5Ljc2IDEzMiBMIDM1MS43NiAxMzYgTCAzNTMuNzYgMTMyIEwgMzUxLjc2IDEyOCBaIiBmaWxsPSIjN2VhNmUwIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTQyIiB5PSIxMDIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy05NjY5LTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogMTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjIuIFN0YXJ0IHF1ZXN0aW9uaW5nPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI0MiAyMzIgTCAzNTMuNzYgMjMyIiBmaWxsPSJub25lIiBzdHJva2U9IiM3ZWE2ZTAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDM1OS43NiAyMzIgTCAzNTEuNzYgMjM2IEwgMzUzLjc2IDIzMiBMIDM1MS43NiAyMjggWiIgZmlsbD0iIzdlYTZlMCIgc3Ryb2tlPSIjN2VhNmUwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjE0MiIgeT0iMjAyIiB3aWR0aD0iMTAwIiBoZWlnaHQ9IjYwIiBmaWxsPSJ1cmwoI214LWdyYWRpZW50LWZmZmZmZi0xLWNjY2NjYy0xLXMtOTY2OS0wKSIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogOThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyMzJweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj4yLiBTdGFydCBxdWVzdGlvbmluZzwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMzYyIiB5PSIxMDIiIHdpZHRoPSIxMDAiIGhlaWdodD0iNjAiIGZpbGw9InVybCgjbXgtZ3JhZGllbnQtZmZmZmZmLTEtY2NjY2NjLTEtcy05NjY5LTApIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiA5OHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogMzYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjUuIFEmYW1wO0EgZGV0YWlscyBwYWdlPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzNjIiIHk9IjIwMiIgd2lkdGg9IjEwMCIgaGVpZ2h0PSI2MCIgZmlsbD0idXJsKCNteC1ncmFkaWVudC1mZmZmZmYtMS1jY2NjY2MtMS1zLTk2NjktMCkiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDk4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjMycHg7IG1hcmdpbi1sZWZ0OiAzNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+NS4gUSZhbXA7QSBkZXRhaWxzIHBhZ2U8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjwvZz48L3N2Zz4=" />


<span id="bd0f37d9"></span>
# Reference: FAQ

<span id="6880e87e"></span>
## Q1: Funnel analysis configures attribute grouping, and when applied to an event, unreach appears in the analysis result graph. What is the reason?

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/032c59eb419c4ff2821cc22335f7d3fa~tplv-goo7wpa0wc-image.image) </span>

As shown in the figure above, the attribute grouping is applied to "event 2", and among all users who have passed step 1, there may be some users who have not passed step 2. At this time, the grouping is configured to start with step 2, and the part of users who have not passed step 2 will be uniformly grouped into the unreach packet.

<span id="ecceb266"></span>
## Q2: What is the difference between "conversion funnel chart" and "base funnel chart", and why is the conversion rate different?

The conversion funnel chart shows the conversion rate from [previous step] to [current step], and the base funnel chart shows the conversion rate from [first step] to [current step].

<span id="4cbe236a"></span>
## Q3: Why is the conversion rate of a certain step grouped by a certain step 100%?

For example, if you start grouping with Event 2, the conversion rate of Step 2 is 100% in all groupings except for the overall data and the unreached data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/217d288fa1ff4cffa6da38fb8a5407e2~tplv-goo7wpa0wc-image.image) </span>

The above phenomenon occurs because grouping from a certain step means that starting from a certain step, the conversion rate of the current step is naturally 100%, and the subsequent steps will be diverted, and the conversion rate data will be different.
