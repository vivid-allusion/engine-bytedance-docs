---
title: "Create Retention Metrics"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Create-Retention-Metrics"
---

Retention metrics are generally used to validate user stickiness and measure user stickiness and loyalty. In general, retention is defined as active users (visiting an app or visiting a website). BytePlus AB testing supports custom creation of retention metrics based on your business scenarios and needs to analyze the retention impact of different strategies on specific businesses or functions.

<span id="一、概述"></span>
# Usage restrictions

**Retention metrics Only one metric can be created per metric group.** 

Reason: Compared to other event metrics, which are themselves a group of metrics, the retention metric defaults to the day 30 retention rate, which will be displayed as a group of 30 metrics by default on the report page.

<span id="二、应用场景"></span>
# Application scenario


* Scenario 1: Focus on the retention of a certain function \- customize the retention analysis of the same event. Taking the camera app as an example, the product pays more attention to the usage of the [shooting] function in users. By customizing the retention function, setting the initial behavior and retention behavior to [Shoot], you can understand the retention of users who use the [Shoot] function for the first time and use this function again.

* Scenario 2: Focus on the impact of a function or strategy on users \- customize the retention analysis of different events. Take the short video app as an example. The quality of the short video content determines whether the user will open the app again. Through the custom retention function, select the initial event as [Play Short Video] and the return visit event as [Open APP] to understand the retention of the user's second opening of the App.


<span id="三、使用留存指标"></span>
# Use retention metrics

<span id="方式1-推荐-创建自定义留存指标"></span>
## **Method 1 (recommended): Create custom retention metrics**

Create a custom retention metric first, and later experiments can choose the created retention metric as a focus metric.

Entry: Click "Create Metric Group" on the list page \- Metric Group Type: Retention Metric

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c73bd9870486423fb23b7180689454f2~tplv-goo7wpa0wc-image.image) </span>

<span id="基本信息："></span>
### **Basic information:** 


* **Metric Group Type:**  Select Retention Metric

* **Belonging metric group:**  By default, the first metric group of the **same type** created in the current user history will be selected. Support re\-select metric group & create a new metric group and select


<span id="指标设置："></span>
### Metric **settings:** 


* Metric name: Required, it is recommended to take a name related to the content of the event, such as "number of times per person clicking the login button", so that you can quickly know which event is the metric about; the name is unique in the metric group, and the longest is no more than 50 characters.

* Metric description: Optional, briefly describe the meaning, calculation logic, purpose, etc. of the metric, so that business related personnel can use the metric more reasonably.

* Calculation criteria:

   * Retention metrics require the definition of initiation events and return events

      * Initial event: that is, define the target user group that needs to be analyzed, such as users who use the shooting function.

      * Return visit event: Users who did a return visit event on the nth day after the initial event, retained users on the nth day, such as using the shooting function again on the nth day.

         The figure on the right is a preview of the criteria of the retention metrics

         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8205527b7b5a4fcca192ad2b8a174c94~tplv-goo7wpa0wc-image.image) </span>

   * Both the starting event and the return visit event support adding filtering conditions to the event, that is, further circling of the selected user, such as filtering out only new users to see the retention of new users using the shooting function.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a1d989578bb4d6eb3819fabef165100~tplv-goo7wpa0wc-image.image) </span>

   * Advanced Settings: Flexible Properties

      You can choose whether to turn on the flexible attribute switch according to your needs. After turning it on, you can add flexible attributes to each event of the metric. After adding, you can choose when experimentally creating and selecting metrics, and specify the selected metrics to define, calculate and display the experimental results according to the selected attributes and attribute values.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f21c2a1a00843a0a8e46963e74b9b4e~tplv-goo7wpa0wc-image.image) </span>

* **Number Format:**  Select number/percentage format and set decimal places

* **Must\-see metrics:**  Turn on "Set as must\-see metrics", and the retention metrics will be automatically added to each experiment.


<span id="查看留存指标："></span>
### Review retention metrics:

Entry: Experimental Report \> \> Retention Metrics


* In Retention metrics, you can filter the retention metrics that have been created

* Note: The preset retention metric is the active retention metric preset by the system


<span id="方式2-报告页自定义分析"></span>
## **Method 2: Custom analysis of the report page**

Add start and return events to the report page for custom retention analysis \- typically for ad hoc query analysis scenarios.


* Under Retention metrics on the report page, the retention criteria can be customized

* Retention metrics require the definition of initiation events and return events

   * Initial event: that is, define the target user group that needs to be analyzed, such as users who use the shooting function.

   * Return visit event: Users who did a return visit event on the nth day after the initial event, retained users on the nth day, such as using the shooting function again on the nth day.

* Both the starting event and the return visit event support adding filtering conditions to the event, that is, further circling of the selected user, such as filtering out only new users to see the retention of new users using the shooting function.


After defining the starting and return events, click Query to view the corresponding retention metrics.
