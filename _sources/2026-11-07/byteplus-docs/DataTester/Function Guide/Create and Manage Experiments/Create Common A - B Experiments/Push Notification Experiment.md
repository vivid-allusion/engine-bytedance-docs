---
title: "Push Notification Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Push-Notification-Experiment"
---

Push notification experiments can test the title, content, click action, etc. of push notifications. When you want to publish a notification message to existing users or start a new marketing notification, but are unsure how effective it will be, you can use BytePlus A/B testing to create a push notification experiment by testing various groups of notification experiments in your selected user base to find the most ideal way to copy and present notifications. This article introduces the push experiment application scenarios and operation points of DataTester.

<span id="59f3f40a"></span>
# **Preconditions and limitations**


|Limitations/Prerequisites |Description |
|---|---|
|Types of supported experiments |* The type of experiment pushed is a **server level** experiment.<br><br>* Currently supports iOS and Android apps.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">You need to interact with the client side during the push process, so the target audience can use the client's properties.</div><br> |
|Prerequisite |* Before using the push experiment, you need to configure the corresponding push channel, please refer to the details [Push Channel Management](https://docs.byteplus.com/docs/DataTester/Push-Channel-Management).<br><br>* Before using push experiments, you need to integrate DataTester's data access SDK, see [iOS SDK Integration](https://docs.byteplus.com/docs/DataTester/iOS-SDK-Integration), [Android SDK Integration](https://docs.byteplus.com/docs/DataTester/Android-SDK-Integration)for details. |


<span id="4086968b"></span>
# Basic concept


* Scheduled reach: fetch the number of deduplicates triggered by the API.

* Actual reach: The number of deduplicates who received the push task.

* Number of goals completed: The number of people deduplicated according to the set goals.

* Scheduled hits: fetches the total number of API triggers sent.

* Actual reach: The total number of push tasks received.

* Number of goals completed: The number of times completed according to the set goal.


<span id="b9a20c9f"></span>
# Application scenario

Push experiments are mainly used to solve (1) the difficulty of choosing alternative solutions and unable to decide which effect is best; (2) the change has a large impact and dare not change easily, fearing the pain points of scenarios such as customer public opinion. For example:


* **Multi\-copy push experiment:**  For candidate copywriting, it is difficult for marketers to judge which effect is best through human experience, so they can open the A/B experiment method, analyze the experimental report of small traffic a priori, and select the best copy for the applicable scenario.

* **Intelligent copy tuning experiment:**  After conducting the multi\-copy push experiment, we can further set up the intelligent copy tuning experiment to send the better copy directly to a wider range of users.


**Scenario example:** 

On the occasion of the shopping festival, we have a variety of push messages for different copywriting that can be sent to users. Each push message focuses on different pain points, including low price, comfort, fashion, etc. The copywriting is as follows:


|Control group |The most explosive discount in 2021, grab No. 1 0\-2 points off 20% off, the audience is as low as 30% off, join the club and place an order to get a 100 yuan cat super card, miss it and wait for next year! |
|---|---|
|Experimental version 1 |What to buy on Double 11? Comfortable and versatile jeans, wearing a great sense of high\-end, choose new products now |
|Experimental version 2 |Idol of the same style, fashionable denim accessories, double 11 new products are folded up to help you open and hang in style |
|Experimental version 3 |Double 11 discount explosion, No. 1 sprint 0\-2 points off 20% off, the audience is as low as 30% off, members pay TOP1 to send Iphone, and there are exclusive large\-amount coupons, come and unlock the biggest discount of the year! |



* Before we push it on a large scale, we first edit different copywriting into different experimental versions and configure 10% of the traffic for experimentation.

* After a period of time, we checked the push click situation, post\-click payment rate, and paid total price of each experimental version, and selected the best copywriting strategy to push to a large number of users.


<span id="四-操作演示"></span>
# Operation demonstration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1088efd0db004b31b4d2af1c039f2383~tplv-goo7wpa0wc-image.image) </span>

<span id="五-创建实验"></span>
# Create an experiment

Click "+ Create Experiment" on the experiment list page, select User Touch Experiment \- Push Experiment, and enter the experiment creation process.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you can't find the user's access to the experiment in the creation of the experiment entrance, it may be because the function switch is turned off. You can contact the technical support staff to turn on the function switch.</div>


<span id="988d238d"></span>
## **Step1 Enter basic information**

**Experimental basic information** related parameters are mainly used to identify experiments, clear experimental types, etc. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6505c0228f794572a31d427210680a75~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experiment Name & Experiment Description** |* **Experiment name:**  It is recommended to set it to the name related to the experimental content. If there is an experimental version iteration, you can add the version number suffix, so that your partners can quickly understand what the experiment is doing and which iteration version is in.<br><br>* **Experiment description:**  The content of the experiment is briefly described, which can make the project related personnel more clearly know how the experiment is done and what problems to solve, and also facilitate the later viewing and management of historical experiments at a glance. |
|**Experimental label** |You can select an existing experimental label in the drop\-down box, or you can directly enter a new label.<br><br>Generally, keywords such as business line and optimization direction are used as tags to screen and classify experiments. After the subsequent experiments are created, relevant experiments can be quickly searched through the experiment tags in the experiment list. |
|**Experiment leader** |Default is the experiment creator. |
|**The duration of continuous observation after the experiment** |There is a delay in the collection of push data. Please enter the continuous observation time after the experiment according to the actual situation, up to 30 days. |


<span id="11319231"></span>
## **Step2 Setup experimental version**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7c31eca731d4e758f0ac091720dd86d~tplv-goo7wpa0wc-image.image) </span>

You can add multiple experimental versions to the Configuration Experimental Version page, configure the control version of the experiment and the push rules of each experimental version respectively. The configuration operation is similar, and the core configuration parameters are as follows:


1. **Whether to push:**  You can choose whether the experimental version is pushed to the user;

2. **Push channel and content settings:**  This part of the content is set according to different push channels

   1. **Push channel:**  Support "JPush channel", "Push channel" and Webhook channel. Webhook channels can be connected to own or other touch channels, which can be configured in push channel management, see "Growth Analysis" push channel management, address: [Push Channel Management](https://docs.byteplus.com/docs/DataTester/Push-Channel-Management)

   2. **Push platform:**  supports "Android" and "iOS".

   3. **Push title:**  word count ≤ 20 Chinese characters (40 bytes)

   4. **Push content:**  word count ≤ 50 Chinese characters (100 bytes)

   5. **Follow\-up actions:** 

      * Launching the app means that after the user clicks the push message, the app is directly opened.

      * Custom behavior means that after the user clicks the push message, the filled parameters are passed to the client side, and the client side can get the parameters to implement its own business logic, such as entering a new page.

   6. **Push channel description:** 


(1) Explanation of JPush and individual push channels


|Platform/Push Channel |JPushChannel |Push channel |
|---|---|---|
|Android |Launch the app:<br><br>(1) The number of corner marks increases.<br><br>(2) Notification reminder: ring, vibration, breathing light, App still reminds in the foreground, priority can be set.<br><br>Custom behavior:<br><br>(1) Pass the kv parameter to a specific application, and the specific behavior is determined by the application.<br><br>(2) The number of corner marks increases.<br><br>(3) Notification reminder: ring, vibration, breathing light, App still reminds in the front desk. Priority can be set. |Launch the app:<br><br>(1) Notification reminder: ringing, vibration. The importance of notification channels. Whether the notification can be cleared.<br><br>Custom behavior:<br><br>(1) Pass the kv parameter to a specific application, and the specific behavior is determined by the application. |
|iOS |Launch the app:<br><br>(1) The number of corner marks increases.<br><br>(2) Notification reminder: iOS optional production environment and development environment.<br><br>Custom behavior:<br><br>(1) Pass the kv parameter to a specific application, and the specific behavior is determined by the application.<br><br>(2) The number of corner marks increases.<br><br>(3) Notification reminder: iOS optional production environment and development environment. |Launch the app:<br><br>(1) The number of corner marks increases.<br><br>Custom behavior:<br><br>(1) Pass the kv parameter to a specific application, and the specific behavior is determined by the application.<br><br>(2) The number of corner marks increases. |
|Remarks |1. JPush channel, Android has more options for notification reminders (bell, vibration, breathing light, App still reminds in the foreground, priority) than iOS.<br><br>2. Different follow\-up actions (start application, custom behavior) on the same platform, the custom behavior only has more kv parameters passed through than the start application. |iOS functions as expected, i.e. customization has more kv options than opening the app<br><br>Android custom pass\-through and open applications do not overlap. |


(2) Webhook channel usage instructions


* When creating an experiment, you can choose the already configured webhook channel

* After selecting the channel, fill in the field value corresponding to the channel

* After configuration, you can directly enter the whitelist test.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/967eacad87b040039fff56ff38936c47~tplv-goo7wpa0wc-image.image) </span>


3. **Test user:**  Add whitelist test user

4. **Frequency control rules:** 

   * Global frequency control: Each user can receive up to 24 push messages per day, and up to 1 per hour. You can set frequency control rules in BytePlus Growth Analysis.

   * No Frequency Control: A user may receive multiple Pushes in one day.

5. **Push timing**

   * Single Immediate Push: After selecting Single Immediate Push, it will take effect immediately after starting the experiment.

   * Timed push: Support timed push. Support repeated routine push every day/week/month.

   * Event\-triggered push: After selecting event\-triggered push, you can set event triggering rules: trigger XX behavior after triggering XX behavior \- \> run push action. In the push operation scenario, compared with manual push methods such as timed push, the method of triggering push based on user behavior events is more suitable for user scenarios, which makes it easier to bring user conversion (for example, after the user adds the product to the shopping cart, it is easier to send the user a coupon, which makes it easier for the user to place an order).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a731e8b316074655b4e3e9cb0d70fd37~tplv-goo7wpa0wc-image.image) </span>

      The event triggering types are shown in the following table:

      
      |Event trigger type |Option |Paraphrase |Example |
      |---|---|---|---|
      |User triggered |Single action |The finger triggers an action |Run push actions when the user starts/exits the app. |
      ||Multiple actions |Refers to triggering multiple actions, such as doing A and doing B |The user starts the application and searches for products during use, then runs the push action. |
      ||Multiple actions (in order) |Refers to multiple actions triggered in chronological order, such as after doing A and then doing B. |After the user searches for a product, exit the application and run the push action. |
      |After |Wait for a while |Trigger behavior Wait for a certain period of time before pushing |After the user searches for the product, wait 5 minutes and run the push action. |
      ||No specific behavior was triggered |Refers to the triggered behavior that does not trigger other behaviors in the future |If the user does not submit the order within one day after searching for the product, the push action will be run. |
      ||Trigger specific behavior |Refers to the behavior that triggers other behaviors in the future |After the user searches for the product, if the order is submitted within one day, the push condition will be run. |
      

      Notes: There are limits on the number of events and filter conditions: number of events < = 3, filter conditions < = 5.

6. **Experiment type settings:** 

   1. regular push experiment

   2. Intelligent tuning push experiment: that is, copywriting horse racing, you can dynamically adjust the traffic to a better experimental version. If you need to use the recommended experiment, the number of people entering the group exceeds 100,000;

7. **Experimental traffic allocation setup**

   Experimental traffic allocation setting: that is, the proportion of traffic between each experimental version is allocated.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74f9beac3f4e430cbf1074ac304a1a16~tplv-goo7wpa0wc-image.image) </span>

   The actionable items are as follows:

* **Uniform distribution of traffic \- on:**  The default is on state, and the open state is to force the uniform distribution of traffic in each experimental version.

* **Traffic evenly distributed \- off:**  After closing, the relative proportion of traffic in the control version and the experimental version can be deployed. You can control the proportion of users hit by each experimental version by entering a value. For example, when the uniform distribution is turned off, the three experimental versions can be configured to account for 20% of the control version, 50% of the experimental version 1, 30% of the experimental version 2, and 100% of the overall sum.


<span id="1bdf9d3e"></span>
## Step3 Set the effective policy

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d444f6b638f64765a21217044d07a8da~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental traffic** |The proportion of users who satisfied the user audience in the effective experiment. The system defaults to 100% traffic, you can estimate the traffic through the suggestion tool (click the traffic calculator), and see how much traffic is set appropriately, see: [Traffic Calculator](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator).<br><br>After enabling audience rules, the system will **first filter users who meet the rules**, and then take effect according to the configured **experimental traffic ratio**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When estimating the experimental traffic, it is usually necessary to combine the experimental business indicators with the <strong>MDE</strong> (test sensitivity) for estimation. Usually, the experimental indicators are to improve/decrease xx (a certain business indicator value). The MDE recommends estimating less than this indicator value. Try to avoid the MDE value being large and unable to detect the real experimental results.</div><br> |
|**Audience rules** |* The push experiment is a special server level experiment. The experiment initiation process is the opposite of the way that the ordinary client side service pulls data, and the push server actively pushes down. Therefore, it is necessary to specify the selected target audience before downloading, and support the "user group" that has been built offline in advance as the audience filter condition, as shown in the figure above.<br><br>* Push number estimate: After clicking, the number of users who meet the rules can be calculated. |


<span id="e2e53180"></span>
## Step4 Adds experimental metrics

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bf3852a49524e189cdafd6865471414~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental default metrics** |The push experiment will follow and reach and click\-related metrics by default. |
|**Experimental core indicator configuration** |* **Core indicator configuration:** <br><br>   To determine whether the experimental function meets the expected "direct effect indicators" or "success indicators", you can select the indicators as the core indicators of the experiment in the existing indicator group in the drop\-down box. It is recommended to conduct the experimental design reasonably and choose carefully. For more experience guidance on experimental indicator setting, please check it [1. Identify evaluation metrics](https://docs.byteplus.com/docs/DataTester/How-to-Interpret-the-Experiment-Report#_1-%E7%A1%AE%E5%AE%9A%E8%AF%84%E4%BC%B0%E6%8C%87%E6%A0%87).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the experimental indicators are configured, after the subsequent experiments are created, if there are special circumstances that need to modify the experimental indicators, please enter the experimental details page to modify them.   </div><br>   <br><br>* **Monitoring alarm:**  You can select the target indicator and click "Monitoring alarm", fill in the specific required alarm strategy, choose whether to tick "Significant effect", and choose the effective way of the alarm strategy.<br><br>* **Edit indicators:**  Click on the 3 position in the legend to enter the indicator editing page, and edit the name, indicator type, and whether it is set as a must\-see indicator for indicators. |
|**Experimental attention indicator configuration** |Configure the metrics that need attention. You can select the indicators you need to pay attention to in the drop\-down list of the page, or you can click the **New Indicator** or **Remove Indicator** button on the page to quickly adjust the indicators you need to pay attention to. |


<span id="28dc7e23"></span>
# Debug, start, stop experiments

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list and check the experiment status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>


* **Debugging:**  The newly created experiment is **debugging**. At this stage, you can invite users who have been added as test users to conduct experimental tests to confirm that the experiment meets expectations.

* **In progress:**  After the experiment is debugged, you can click "Start" on the experiment list page to start the experiment. After the start of the experiment, the state of the experiment becomes "**In Progress"** . At this time, the user can view the group in real time, and the indicator confidence level will be produced on the second day.

* **Closed:**  After the experiment starts, the experiment will automatically stop when the experiment duration reaches the **experiment duration** configured when the experiment was created; if the experiment duration is not reached, you want to stop the experiment immediately, or you can manually stop the experiment in the experiment list. After stopping the experiment, the experimental state changes to **has ended**.


<span id="7824c2f3"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, please refer to the details [Experimental Report Overview](https://docs.byteplus.com/docs/DataTester/Experimental-Report-Overview).
