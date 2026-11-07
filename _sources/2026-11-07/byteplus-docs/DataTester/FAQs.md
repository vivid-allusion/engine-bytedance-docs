---
title: "FAQs"
product: "BytePlus DataTester"
product_code: "DataTester"
section: "Document"
source: "https://docs.byteplus.com/en/docs/DataTester/FAQs"
---

<span id="_1-tester提供哪些语言的sdk"></span>
## 1. What languages does Tester provide SDK for?


* Client side: iOS, Android, Web/H5/WAP, WeChat Mini Program

* Server side: Java, Python, Go, Node.js


<span id="_2-多少量级的产品可以开a-b实验？"></span>
## 2. How many products can be used for A/B experiments?

It is recommended to live more than 1,000 days.

<span id="_3-如何针对目标用户做a-b实验？"></span>
## 3. How to do A/B experiments for target users?

When creating an experiment, you can configure the filter conditions, such as to open the experiment only for new users.

<span id="_4-哪些指标支持计算置信度？"></span>
## 4. What metrics support computational confidence?

**Single metric:** 


* Number of group entries per person: The number of occurrences per person of the group that triggered the current event. pv/au, the total number of current events/the number of incoming users.

* Conversion rate: The percentage of incoming users who triggered the current event. Uv/au, the total number of incoming users/incoming users for an event.

* Press... to find the average value of the group: sum/au, sum the value of a certain attribute/the number of users in the group.

* Number of events per person: The number of events triggered per person. Pv/uv, the total number of occurrences of the current event by the incoming user/the number of people reported by the incoming user.

* According to... Average number of people: sum/uv, the sum of a certain attribute value/event triggers the number of people entering the group.

* Press... to find the average: sum/pv, sum the value of a certain attribute/the number of events.


**Composite metrics:** 


* The numerator is of type UV and the denominator is of type UV.

* The numerator is of type PV and the denominator is of type PV.

* The numerator is of type PV and the denominator is of type UV.

* The numerator is of type PV and the denominator is of type Sum.

* The numerator is of type sum and the denominator is of type sum.

* The numerator is of type sum and the denominator is of type uv.

* The numerator is of type sum and the denominator is of type pv.


<span id="_5-为什么埋点上报后，无法在tester中配置指标？"></span>
## 5. Why can't I configure metrics in Tester after event tracking reports?

After the event tracking report, it takes 6 hours to build the data, and after 6 hours you can configure the metric in Tester.

<span id="_6-互斥组是什么意思？"></span>
## 6. What does mutual exclusion group mean?

**Mutual exclusion group, also known as mutual exclusion layer, experimental layer. The "experimental layer" technology is a traffic layering technology developed to enable multiple experiments to be parallel without interfering with each other, and to obtain enough traffic.** 

> For example, let's say I have four experiments to run now, and each experiment requires 30% of the traffic to produce reliable results. In order to run these four experiments simultaneously, 4 \* 30% = 120% of the traffic is required, which means that 100% of the traffic is not enough to be allocated to these four experiments simultaneously.

> So at this point, we can only choose to sort the experiments and let several experiments be completed one after the other. However, this would result in inefficient experiments. Experimental layer technology can perfectly solve this problem.


We "duplicate" the overall traffic countless times to form countless traffic layers, so that the overall traffic can be reused countless times, thus improving the experimental efficiency. The traffic between the layers is orthogonal, which can be simply understood as: under the premise that the traffic layer is selected correctly, the traffic is scientifically allocated to ensure that the results of each experiment will not be disturbed by the experiments of other layers.

<span id="_7-vid是什么？"></span>
## 7. What is vid?

It is the short expression of version ID.

<span id="_8-停止的试验是否能重新开始？"></span>
## 8. Can a stopped experiment be restarted?

No. Because the client base may change during the time the experiment is stopped, the accuracy of the data cannot be guaranteed when the experiment is reopened.

<span id="_10-开实验后，多久才能看到数据？"></span>
## 9. After starting the experiment, how long will it take to see the data?

After starting the experiment, users in the group can view it in real time, and the metric confidence will be produced the next day.

<span id="_11-如何保证流量比例准确（如何控制10-，就是真实流量的10-）"></span>
## 10. How to ensure that the traffic ratio is accurate (how to control 10% is 10% of the real traffic)?

Mutual exclusion group = mutual exclusion layer = experimental layer

When the streaming service allocates traffic, it first distributes the traffic of each layer evenly into a fixed number of copies, such as 100 copies, each of which is called a "hash bucket". After processing the streaming service, we throw all the users into the bucket, so each of the 100 buckets has 1% of the traffic. When different experiments in the same layer call traffic, they will randomly receive different numbers of buckets according to the percentage of traffic required by the experiment (and the buckets do not coincide).

Please refer to the shunt principle: [here](https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/36500.pdf).

<span id="_12-如何保证人群没有特殊性？"></span>
## 11. How can we ensure that the population is not unique?

When the hash function groups users, it only uses the user ID and can hash the regular set of IDs evenly, so it can be evenly divided among other attributes (such as model, region, age, gender, etc.).

<span id="_13-如何保证用户不会跳组？（比如保证不会出现：上午在a版本，下午在b版本）"></span>
## 12. How to ensure that users do not skip groups? (For example, it is guaranteed not to appear: version A in the morning, version B in the afternoon)

In the streaming service, the "hash function" still bears this heavy responsibility. The reason why a "hash function" can perform this task is due to its property that if the input value is fixed, then the output value of the hash function is also fixed.

<span id="_14-如果获取ab参数失败，那么有没有重发的机制？如果有重发机制，那么ab参数下发的时间点是哪些？"></span>
## 13. If getting the AB parameter fails, is there a mechanism for resending it? If there is a retransmission mechanism, what is the time point when the AB parameter is issued?

After failing to obtain the AB parameter, if the app is in the foreground, it will be retrieved every 10 minutes, or it will be retrieved the next time the app starts.

<span id="_15-sum-dau-的数据口径是什么？"></span>
## 14. What is the calculation method of sum (dau)?

Sum (dau) is the direct addition of daily dau, expressing the pure numerical sum of dau, and does not deduplicate the "human" dimension of dau when summing.

<span id="_16-客户端是否支持采集页面停留时长，如何实现的？"></span>
## 15. Does the client side support capturing page dwell time and how?

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">iOS, Android, Web, Mp SDK all support page dwell time collection</div>


<span id="ios"></span>
### iOS


1. Turn on full event tracking and set up events to capture and leave the page. Supported 6.11.0 + version. The page where the application exits cannot be collected.


```objectivec
//Enable full event tracking
config.autoTrackEnabled = YES；
//BDAutoTrackDataTypePageLeave is an enumeration to collect $bav2b_page_leave events, including $page_duration page duration parameters, in milliseconds
//default is BDAutoTrackDataTypePage | BDAutoTrackDataTypeClick
config.autoTrackEventType = BDAutoTrackDataTypePage | BDAutoTrackDataTypeClick | BDAutoTrackDataTypePageLeave；
```



2. The user takes a closer look at the $page_duration parameters of the $bav2b_page_leave event.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e03b36983bb9484b9eb5c3f4c70c3f95~tplv-goo7wpa0wc-image.image) </span>


3. Event analysis viewing, which can be summed up according to the length of page browsing, the average person, etc


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38ef136b2ad046d1b2c4e50b9af88a59~tplv-goo7wpa0wc-image.image) </span>

<span id="android"></span>
### Android


1. Turn on full event tracking to collect, and set the event that collects and leaves the page. Supported 6.11.0 + version. The page where the application exits cannot be collected.


```java
config.setTrackPageLeaveEnabled(true);
//Default value: AutoTrackEventType.PAGE | AutoTrackEventType.CLICK////AutoTrackEventType. ALL: full event tracking all events//AutoTrackEventType.PAGE: full event tracking page events, turned on by default//AutoTrackEventType.CLICK: full buried point click events, turned on by default//AutoTrackEventType.PAGE_LEAVE: full event tracking page duration events, turned off by default//This function only supports 6.11.0 and above versions
config.setAutoTrackEventType(AutoTrackEventType.PAGE | AutoTrackEventType.CLICK | AutoTrackEventType.PAGE_LEAVE);
```



2. The user takes a closer look at the $page_duration parameters of the $bav2b_page_leave event. With iOS.

3. Event Analysis View iOS.


The page where the application exits cannot be collected.

<span id="小程序"></span>
### Mini Program


1. Enables acquisition of preset event predefine_pageview_hide (page hidden), including duration parameters, in milliseconds.


```json
//auto_report set to true
$$Rangers.init({
    auto_report: true, //Some predefined events will be reported after opening, such as app_launch, app_terminate, etc
});

//or set auto_report as an object
$$Rangers.init({
    auto_report: {
        //Report predefine_pageview_hide event, not when false, or not when pageShow is false
        pageShow?: true;
        pageHide?: true;  
}
});
```



2. user review


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d8b43a1033684b61acd8ad47713ab801~tplv-goo7wpa0wc-image.image) </span>


3. Event Analysis View


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/888efe9105ae4f00914d765c59ee3e52~tplv-goo7wpa0wc-image.image) </span>

<span id="web-js"></span>
### Web/JS


1. Open page dwell time during initialization


```javascript
window.collectEvent('init', {
    // ...... Other initialization configurations
    enable_stay_duration: true //true: turn on stay duration
});
```



2. After the start, report the incident introduction.

* Recommended predefine_page_alive collection time

   * When the function is turned on, predefine_page_alive event will be reported regularly every minute when the page is active, or once when it is switched to inactive. **Active state: The page is in a visual or actionable state.**  **Inactive state: The page is in the background, hidden, minimized, and other invisible states.** 

   
   |Event |Meaning |Params |Description |
   |---|---|---|---|
   |predefine_page_alive |active page |title |string |
   |||url |string |
   |||url_path |string |
   |||duration |Int, ms, milliseconds, typically 60s, less than or equal to 60 when switching to inactive state |
   |||tea_event_index |Variation of timestamp triggered by the current event |
   |||is_support_visibility_change |Int, does the browser support visibility_change |
   

   * **Analysis method:** 

      * Average screen time = sum (duration)/uv

      * Duration = sum (duration)/pv

* predefine_page_close

   * After the function is turned on, the timestamp of each time the user [enters the page, switches the state, leaves the page] will be recorded, and then the predefine_page_close event will be reported when leaving or closing the page, and the duration of each [active state] will be added as the overall usage duration.

   
   |Event |Meaning |Params |Description |
   |---|---|---|---|
   |predefine_page_close |page closed |title |string |
   |||url |string |
   |||url_path |string |
   |||duration |Int, ms, millisecond |
   |||active_times |page activity |
   |||total_duration |Int, ms, milliseconds, total time between page opening and closing |
   |||is_support_visibility_change |Int, does the browser support visibility_change |
   

   * **Analysis method:** 

      * Average screen time = sum (duration)/uv

      * Duration = sum (duration)/pv

      * Average usage time per activity = sum (duration)/sum (active_times)

      * Duration distribution
