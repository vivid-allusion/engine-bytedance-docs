---
title: "BytePlus Recommend API Monitoring Dashboard"
product: "BytePlus Recommend"
product_code: "recommend"
source: "https://docs.byteplus.com/en/docs/recommend/docs-api_monitoring_dashboard"
---

The API Monitoring dashboard in the BytePlus Recommend Console enables users to monitor the status of APIs, and identify and resolve any errors or abnormalities detected in the metrics. Its primary objective is to instill confidence in the stability and reliability of the BytePlus Recommend service. By providing real\-time insights and the ability to address issues promptly, the API Monitoring dashboard empowers users to maintain a robust and dependable recommendation system.

<span id="efd849d8"></span>
# Accessing the API Monitoring dashboard

Access the API Monitoring dashboard through the BytePlus Recommend Console. Gain valuable insights into API performance and status, enabling effective monitoring and troubleshooting for a reliable recommendation system.

**To access the API Monitoring dashboard:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

   The Recommendation Projects screen appears.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/d6919d0-RecommendProjects.png) </span>

2. Click on the project you want to access.

3. Click **Monitoring**.

   The API Monitoring screen appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/72d4bb727e38491c93b7f1377045e27a~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the API Monitoring screen has the following message, "You don't have any API status yet", it means that you have yet to call any APIs. Revisit the dashboard after you have called the APIs and the data should appear.   </div>
   

<span id="101ae379"></span>
# API Monitoring Dashboard graphs

The API Monitoring Dashboard graphs provide users with insights and metrics related to API performance, including data on success rates, error counts, latency, and more. These graphs enable users to monitor, analyze, and optimize the performance of their APIs for enhanced reliability and user experience.

<span id="ab9c2d21"></span>
## Setting API monitoring graph alerts

Additionally, in the BytePlus Recommend demo project, you have the ability to set alerts for each monitoring dashboard. By configuring the threshold and frequency, you can receive alerts to stay informed about critical events and performance thresholds. This allows you to proactively address any issues and ensure the smooth operation of your recommendation system.

**To set an API monitoring graph alert:** 


1. Sign in to [BytePlus Recommend](https://console.byteplus.com/recommend/home).

   The Recommendation Projects screen appears.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/d6919d0-RecommendProjects.png) </span>

2. Click on the project you want to access.

3. Click **Monitoring**.

4. The API Monitoring screen appears.

5. Click the alert icon.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c13d1a115e543a087d270c549b9c41d~tplv-goo7wpa0wc-image.image) </span>

   The Set alert pop\-up window appears.

6. Set the conditions in which the alarm will activate.

7. Click **Save**.

   The alert is set.


<span id="7fc7df64"></span>
## Data Synchronization API Success Rate

The Data Synchronization API Success Rate graph provides insights into the success rate of API calls over time. It helps users understand the percentage of successful API calls relative to the total count of both successful and failed API calls.

<div style="text-align: right">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42943187c95546a1af24090cb7f6f104~tplv-goo7wpa0wc-image.image" width="864px" /></div>


**Graph legend:** 


* **Legend**: Product, User, User events

* **X\-axis (Time)** : The graph displays data over a timeline of up to 30 days, allowing users to analyze trends and identify any changes in the API success rate.

* **Y\-axis (API success rate (%))** : The API success rate is calculated as the count of successful API calls divided by the sum of successful and failed API calls. This calculation gives a comprehensive view of the performance of synchronization APIs.


**Default Alert Threshold:** 

The default threshold for triggering an alert is set when the total API success rate falls below 80%. This threshold acts as an indicator to notify users when the API performance requires attention or investigation.

<span id="ae64719f"></span>
## Data Synchronization API Success Count

The Synchronization API Traffic graph in the BytePlus Recommend API monitoring dashboard displays the count of total API queries per second that succeeded for data synchronization API. It provides insights into the traffic patterns of different API categories over time.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47e5658ce00c460b9255a41f6c8e6354~tplv-goo7wpa0wc-image.image) </span>

**Graph Legend:** 


* **Legend:**  Product, User, User events

* **X\-axis (Time)** : The graph displays data over a timeline of up to 30 days, allowing users to analyze trends and identify any changes in the API traffic patterns.

* **Y\-axis**  **(Count of total API queries per second that succeeded)** : The graph shows the number of successful API queries per second, giving an overview of the traffic volume for each API category.


**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the total API success queries per second of any legend falls below a specified value.

* When the percentage of API success count fluctuation is higher than 50% compared to the count of the last 1 hour.


These thresholds help users identify potential issues in API performance and trigger alerts for further investigation.

<span id="b3242800"></span>
## User Event Count

The User Event Count graph in the BytePlus Recommend API monitoring dashboard provides a breakdown of user event data, allowing users to analyze and troubleshoot any decrease or loss in user event data. It offers valuable insights to identify and resolve issues related to user events.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b21525fb1c444e3695d85a3991fca297~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend:**  Any user event defined in the schema such as impression, click, or purchase

* **X\-axis**: Time

* **Y\-axis**: Count of successful Sync API queries per second per user event


**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the total API success queries per second of a user event legend falls below a specified value.

* When the percentage of API success count fluctuation is higher than 50%. The API success count fluctuation is calculated as the percentage change compared to the previous 1\-hour count.


These thresholds help users identify any anomalies or significant fluctuations in the user event data and trigger alerts for further investigation.

<span id="29ec936b"></span>
## Predict API Count

The Predict API Count graph within the API Monitoring Dashboard allows users to monitor the throughput of Predict APIs. It provides insights into the performance of multiple Predict APIs serving different models within the API monitoring dashboard.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3143661ea15949bd85f6e2f51f6aac0d~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend**:

   * Predict 1, 2, 3... API (multiple legends corresponding to Predict APIs serving different models).

   * Each legend represents a model name created by the customer or the BytePlus Recommend team.

* **X\-axis (Time)** : The graph displays data over a timeline of up to 30 days, allowing users to analyze trends and identify any changes in the Predict API patterns.

* **Y\-axis**: Count of total API queries per second that succeeded.


**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the total API success queries per second of a legend is less than a specified value.

* When the percentage of API success count fluctuation is higher than 50% (API success count fluctuation is calculated as the percentage change compared to the previous 1\-hour count).


<span id="3bcd2ff4"></span>
## AckserverImpressions API Count

The AckserverImpression API Count graph within the API Monitoring Dashboard allows users to monitor the throughput of the AckserverImpression API and gain insights into its performance.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/801508bcd4e34709925343f591b25d77~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend**: AckserverImpression API

* **X\-axis (Time)** : The graph displays data over a timeline of up to 30 days, allowing users to analyze trends and identify any changes in the Predict API patterns.

* **Y\-axis**: Count of total API queries per second that succeeded.


**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the total API success queries per second of the AckserverImpression API falls below a specified value.

* When the percentage of API success count fluctuation is higher than 50%. The API success count fluctuation is calculated as the percentage change compared to the previous 1\-hour count.


These thresholds enable users to identify any anomalies or significant fluctuations in the AckserverImpression API's performance and trigger alerts for further investigation.

<span id="134ca94f"></span>
## Error Rate

The Error Rate graph provides users with metrics related to API errors, allowing them to monitor and analyze the error rate and identify categories of API errors.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6be91c01a1584192869bff333ae9c5d1~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend:**  User, Product, UserEvent, Predict, AckserverImpression

* **X\-axis:**  Time

* **Y\-axis:**  The graph presents the error rate as a percentage over time for each API category, providing insights into the occurrence of errors and their impact on the system.


**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the API error rate of any legend exceeds 50%.


This threshold helps users identify and address significant increases in error rates, ensuring timely response and issue resolution.

Additionally, the API error by category can be displayed with the following specifications:


* **Graph Title:**  API Error by Category

* **Legend:**  Product Sync API, User Sync API, UserEvent Sync APIs, Predict API, Ackserver API

* **Count of API Errors by Category**


This graph allows users to view the count of API errors categorized by specific API types, providing further insights into the nature and distribution of errors across different API functionalities.

<span id="afa8ee65"></span>
## Error Count

The Error Count graph provides users with metrics related to API errors, enabling them to monitor the error count and identify the categories of API errors.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86b7aea55d174d52af89ace5816542f8~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend:**  User, Product, UserEvent, Predict, AckserverImpression

* **X\-axis:**  Time

* **Y\-axis:**  Count of Total Error Queries per Second


By analyzing the error count, users can identify any abnormal patterns or spikes in error rates, helping them pinpoint and resolve issues that may impact the system's performance and stability.

<span id="7c860df8"></span>
## API Latency

The API Latency graph allows users to monitor the response time of various APIs, including Data Synchronization APIs, Predict APIs, and AckserverImpression APIs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1ae8b24168146319d895359e991bff9~tplv-goo7wpa0wc-image.image) </span>

**Graph legend:** 


* **Legend:**  User, Product, User Event, Predict (multiple APIs for different models), AckserverImpression.

* **X\-axis:**  Time

* **Y\-axis:**  Milliseconds


The graph displays the latency of each API over time, providing a visual representation of their response times.

**Default Alert Threshold:** 

The default threshold for triggering an alert is defined as follows:


* When the API latency of any legend exceeds 300 milliseconds.

* When the percentage of API latency fluctuation is higher than 50%. The API latency fluctuation is calculated as the percentage change compared to the previous 1\-hour latency count.


These thresholds help users identify any significant increases or fluctuations in API latency, allowing them to take proactive measures to optimize performance and improve the overall user experience.
