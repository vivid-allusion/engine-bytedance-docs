---
title: "Data Query Anomaly Detection"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Data_Query_Anomaly_Detection"
---

DataFinder provides you with the new version of data query anomaly detection and outlier intelligent attribution capabilities. When using advanced analysis tools \- event analysis or Kanban to query data, DataFinder will predict the data range through algorithms, mark the data outliers, and provide corresponding anomaly analysis reports, which can improve your sensitivity to indicator fluctuations, quickly locate problems, and help you deeply understand the reasons for data changes. This article introduces the operation points of the new version of the data query anomaly detection function.

<span id="1b37f16f"></span>
# Precautions


* Currently this feature is only available for Advanced Analytics \- Event Analytics and Kanban functions.

* At present, this function is turned off by default. If you want to use this function, you can contact the BytePlus technical support staff to apply to turn on the function switch.

* When the current data query time granularity is at the level of minutes and 5 minutes, the use of anomaly detection is not supported for the time being.


<span id="86e9d84d"></span>
# Operation steps

The following is an example of using anomaly detection in event analysis to illustrate the detailed steps.


1. After applying to turn on the anomaly detection function switch, when querying data with the event analysis tool, you can see the configuration entry of anomaly detection on the query result graph.

2. Click the Settings button for Anomaly Detection to configure the confidence interval for exception attribution and the number of days to trace back.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92235157de8048d280670f2a8d69b2c1~tplv-goo7wpa0wc-image.image) </span>

   * The DataFinder will take the data within the traceback days for calculation, and the prediction will fit the data within the current query time range and be displayed in dotted lines in the graph.

   * The lighter color ribbon behind the dotted line indicates the expected data range, and the width of the color ribbon is determined by the "confidence interval". The default confidence interval is 95%, with values ranging from 80% to 99%.

      * The larger the confidence interval value, the higher the tolerance, the more actual data on the solid line will appear in the color ribbon range.

      * And those data points that do not appear on the solid line within the color ribbon range, **will be marked as "abnormal" points and displayed with red high highlights**, which can be viewed through the micromirror function.

3. Click the red dot in the solid line in the query result chart to evoke the microscope pop\-up window, and click "Intelligent Attribution of Outliers" to view the attribution analysis report of the outlier on the right.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1fa233de70b4b569181dfca88b3f994~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2810ad9a9264d2fadbc070c7ce28fcc~tplv-goo7wpa0wc-image.image) </span>

   The key analytical indicators are described below.

   
   |Abnormal attribution metric |Indicator description |Index interpretation skills |
   |---|---|---|
   |Observation period indicator value & base period indicator value |The analysis report will show you the indicator value of the current outlier observation date, as well as the increase in the indicator value compared to a certain benchmark date.<br><br><br>* The observation date was 09\-23, and the total PV value of the indicator page access event was 11459; the total PV value of the indicator page access event on the base day was 2460; therefore, the observation day was 79% higher than the base day, i.e., `(11459-2460)/11459`.<br><br>* The default base day is a point in time before the observation day. You can also manually modify the dates of the observation day and the base day, and DataFinder will automatically calculate the corresponding metric increase for you. |1. You can check the indicator value on the observation date and adjust the date of the base day to see if the change of the indicator on the observation date relative to the indicator on the base day is as expected.<br><br>   * If the change is as expected, it may not be a true anomaly.<br><br>   * If the change is not as expected, you can proceed to the next step to see what the main event properties that generated the exception were.<br><br>2. You can choose the event attributes that may have an impact on the exception of the indicator based on the actual business situation, and then further analyze the reasons for the exception of the indicator based on the event attributes of the TOP positive contribution and negative function displayed in the report. |
   |Dimensional disassembly |* You can select the properties that need to be broken down for detailed analysis in the drop\-down box of dimension dismantling. Optional properties include event properties for metric events and event public properties.<br><br>* After selecting the attributes, the DataFinder will calculate the values of each attribute, including the co\-contribution and negative contribution of the exception attribution, and sort the co\-contribution and negative contribution of all the values of all attributes, respectively. The values of the attributes of the TOP5 co\-contribution and negative contribution are displayed at the top of the report.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Co\-directional contribution: refers to the fact that the value of the attribute is consistent with the direction of the overall abnormal change, which exacerbates the generation of anomalies.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Negative contribution: refers to the fact that the value of the attribute is opposite to the overall abnormal change direction, alleviating the generation of the exception.   </div><br>    ||
