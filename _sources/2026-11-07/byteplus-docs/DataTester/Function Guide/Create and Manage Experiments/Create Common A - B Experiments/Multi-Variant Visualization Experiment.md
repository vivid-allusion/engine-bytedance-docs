---
title: "Multi-Variant Visualization Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Multi-Variant-Visualization-Experiment"
---

Multi\-variate Visual Test (MVT) is the simultaneous AB test of two or more elements of a web page to see which combination produces the best results. This article introduces the key points of the multi\-variant visualization experiment.

<span id="761b9aaf"></span>
# **Preconditions and limitations**


|Limitations/Prerequisites |Description |
|---|---|
|Transport protocol |The page transfer protocol requires HTTPS (Hypertext Transfer Protocol Secure: HyperText Transfer Protocol Secure). |
|Browser suggestion |We recommend using the latest version Chrome and Windows Edge. Mainstream browsers can support; iOS system comes with Safari browser to support iOS10 and above (if the system version is lower, please upgrade to iOS10 and above). |
|Types of supported experiments |* The type of MVT experiment is **client side** experiment.<br><br>* Currently supports **Web and H5 pages**. |
|Prerequisite |* Before using MVT experiments, you need to integrate DataTester's data access SDK, see details [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataTester/Web-JavaScript-SDK-Integration). |


<span id="539f5416"></span>
# **Basic concept**


* **Element (Element):**  Element in the page, experiment with multiple Element elements in the page.

* **Variant (variant):**  Modifications in the element, the element is modified after the content and style are saved.

* **Combination (combination):**  combination is the experimental group, there are multiple variants under one element, different modifications of the same element under one variant, and different variants in the elements cross each other to form a version. For example, if you are testing three elements, each with two, three, and four variants, each with different elements modifying content and styles, there are 24 combinations (2x3x4).


<span id="1d101711"></span>
# Application scenario

MVT comparison is suitable for the following scenarios:


* When the web site/H5/APP has a high number of visitors, running a multi\-variant experiment is more useful and effective.

* When a user has a policy hypothesis that variants can be implemented in multiple ways, but cannot decide which combination to test, it is recommended to use multi\-variant experimental validation.


<span id="64bb909c"></span>
# Operation demonstration

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9b45054dc724990b4d89ac3a4618462~tplv-goo7wpa0wc-image.image) </span>

<span id="596d2e71"></span>
# Create an experiment

Click "+ Create Experiment" on the experiment list page, select the multi\-variant visual experiment, and enter the experiment creation process.

<span id="006b1ddd"></span>
## **Step1 Enter basic information**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c0b0271a17a4305b29c197d59306c30~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experiment Name & Experiment Description** |* **Experiment name:**  It is recommended to set it to the name related to the experimental content. If there is an experimental version iteration, you can add the version number suffix, so that your partners can quickly understand what the experiment is doing and which iteration version is in.<br><br>* **Experiment description:**  The content of the experiment is briefly described, which can make the project related personnel more clearly know how the experiment is done and what problems to solve, and also facilitate the later viewing and management of historical experiments at a glance. |
|**Experimental label** |You can select an existing experimental label in the drop\-down box, or you can directly enter a new label.<br><br>Generally, keywords such as business line and optimization direction are used as tags to screen and classify experiments. After the subsequent experiments are created, relevant experiments can be quickly searched through the experiment tags in the experiment list. |
|**Type of experiment** |Current multi\-variant visualization experiments only support client side experiments. |
|**Experiment duration** |Refers to the duration of the experiment, generally in order to avoid differences in user behavior in different time periods (weekdays and weekends), it is recommended to observe at least 2 complete test schedules.<br><br>For example, when considering the impact of weekdays and weekends, the test schedule takes at least one week, and the recommended duration of the experiment is 14 days. |
|**Experiment leader** |Default is the experiment creator. |


<span id="f1d81c0e"></span>
## Step2 Select effective policy

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23f9bc49fdd048a980ad50feead6e14e~tplv-goo7wpa0wc-image.image) </span>


* **Traffic settings**

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Whether mutual exclusion** |When you need to conduct multiple AB test, you need to configure whether the currently created experiment needs mutual exclusion with other experiments according to the experimental situation, so as to avoid the same user being assigned to two experiments that will affect each other, thus affecting AB test results.<br><br>For example, if you want to do an experiment on button color and button shape at the same time, and the two experiments affect each other, you need to add the two experiments to a mutual exclusion group.<br><br>Learn more about traffic tiers and how to create one at: [Traffic Layer and Mutual Exclusion Domain](https://docs.byteplus.com/docs/DataTester/Traffic-Layer-and-Mutual-Exclusion-Domain). |
   |**Experimental traffic** |The proportion of users who satisfied the user audience in the effective experiment. The system defaults to 100% traffic, you can estimate the traffic through the suggestion tool (click the traffic calculator), and see how much traffic is set appropriately, see: [Traffic Calculator](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator).<br><br>After enabling audience rules, the system will **first filter users who meet the rules**, and then take effect according to the configured **experimental traffic ratio**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When estimating the experimental traffic, it is usually necessary to combine the experimental business indicators with the <strong>MDE</strong> (test sensitivity) for estimation. Usually, the experimental indicators are to improve/decrease xx (a certain business indicator value). The MDE recommends estimating less than this indicator value. Try to avoid the MDE value being large and unable to detect the real experimental results.</div><br> |
   |**Traffic effective method** |"Immediate effect" and "Smooth effect" are supported.<br><br>The smoothing effect will take effect on the set size within the set time. For example, if the experimental flow is set to 30% and the smoothing effect time is set to 30 minutes, it will take effect linearly at a rate of 1% per minute. |
   

* **User audience rules**

   You can create multiple filter groups, filtering the logical relationships between the groups as "or"; you can set multiple filter conditions within each filter group, and the logical relationships between the filter conditions as "and".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b3f4dfb55c54853902fb918c4db77fb~tplv-goo7wpa0wc-image.image) </span>

   Detailed instructions for configuring each filter group are as follows.

   
   |**Filter condition** |**Configuration instructions** |
   |---|---|
   |**Add and condition** |For client side experiments, after clicking **Add Filter Criteria**, you can use **user properties** as filters for user audiences, support using system\-provided **preset properties**, or create **custom properties** for filtering.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a357abcb35249deb7e783261c8fd440~tplv-goo7wpa0wc-image.image) </span><br><br>You can view existing preset and custom properties on the **Data Management** \> **Metadata Management** \> **User Properties** page, or you can create new custom properties.<br><br>**Scenario Example: New User Experiment**<br><br>In the "Select Target Audience" filter, you can add a "User First Installation Time" filter for new users, and use the first installation time to identify new users, that is, all users whose first installation time is later than the opening time of the experiment are classified as "New Users". During the start of the experiment, only new users enter the experimental group, and other existing users do not enter the group.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d0e1e462d6c4fafb17023f0fb4b0961~tplv-goo7wpa0wc-image.image) </span> |
   |**Add cluster** |For client\-side experiments, after clicking **add cluster**, you can filter users using the user cluster you created. See activity details for creating user groups [User Cohorts](https://docs.byteplus.com/docs/DataTester/User-Cohorts). |
   

* **Experience consistency**

   After opening, the effective version of the user during the experiment does not change with the adjustment of traffic and audience conditions, which can ensure that the same user can only enter one experimental version during the experiment. After opening, as long as the user has entered the current experimental version (unless the experiment is suspended or closed), the experiment will no longer be released.


<span id="2b3bef38"></span>
## Step3 Configure experimental version


* **Test user hit conditions:** 

   When selecting the experimental version corresponding to the test user hit, whether the audience rule set in the previous step needs to be satisfied. Since the test user is mainly used for debugging and verification before the experiment is officially launched, the choice of the test user can be inconsistent with the final experimental hit user, and you can configure it according to your actual needs.

* **URL matching rules**

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c38bdbdb8cae44cd92f7c57c057b23db~tplv-goo7wpa0wc-image.image) </span>

   The URL matching rule only determines whether the URL visited by the user can hit the experiment. If it can match, it means that the experiment can be hit, and if it does not match, it means that the experiment cannot be hit. The specific version of the user hit experiment is determined by the streaming service. Under different url match types, we can pay attention to whether the visited url can successfully match the experimental version of the url. The URL address only supports the https protocol, not the HTTP protocol. The details are as follows:

   **1) Simple matching**

   In the case of URL matching, simple matching ignores the query parameters and anchors in the URL, and hits the experiment if the URL domain name and path of the user visiting the page match. For example, if the target URL of the experiment is https://app.test.com/path?param=a#frag1, the match is shown in the table when the user accesses the following URL:

   ```Plain Text
   | | | | \
   |Serial number |URL |Does it match |
   |---|---|---|
   | | | | \
   |1 |[https://app.test.com/path](http://app.test.com/?utm_source=5&utm_medium=sembaidu&userid=23) |match |
   | | | | \
   |2 |[https://app.test.com/path?param=](http://app.test.com/?param1=origina&utm_mediue=sembaidu&userid=23)a |match |
   | | | | \
   |3 |[https://app.test.com/path?param=a#frag1](https://app.test.com/path?param=a#frag1) |match |
   | | | | \
   |4 |[https://app.test.com/path?param=b](https://app.test.com/path?param=b) |match |
   | | | | \
   |5 |[https://app.test.com/path?param=b#frag2](https://app.test.com/path?param=b#frag2) |match |
   | | | | \
   |10 |[https://test.com](https://test.com/) |Do not match |
   | | | | \
   |11 |[https://app.test.com/path1](https://app.test.com/path1) |Do not match |
   | | | | \
   |12 |[https://docs.test.com/path?param=a#frag1](https://docs.test.com/path?param=a#frag1) |Do not match |
   | | | | \
   |13 |[https://docs.test.com/path/index.php](https://docs.test.com/path/index.php) |Do not match |
   
   Note:
   * **Match:** It means that the URL visited by the user can match the experimental version of the URL in the "simple matching" mode, that is, the user who visits this page can hit the MVT experiment.
   * **Do not match:** It means that the URL visited by the user cannot match the experimental version of the URL in the "simple match" mode, that is, the user visiting this page cannot hit the MVT experiment.
   ```
   

   **2) Accurate matching**

   That is, it is an exact match, and the experiment will only be hit if the url of the user visiting the page exactly matches the url of the experimental page. For example, the target URL of the experiment is https://app.test.com/path?param=a#frag1, then under the precise matching, only when the user accesses the https://app.test.com/path?param=a#frag1, the experiment will be hit. It is suitable for scenarios where users need to exclude pages with parameters and clearly know the page URL.

* **Configure the experiment URL and enter the visual editor**

   After the user enters the URL and clicks "Enter the Visual Editor", the visual editor is opened based on the original page

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f5445a99d0540fead32d0a3428b5334~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a776661d261c4f399ad03a32d490983c~tplv-goo7wpa0wc-image.image) </span>

   
   | |Product example diagram |Operation item description |
   |---|---|---|
   |**New variant** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/700512de4463467d9d6d7e315305628f~tplv-goo7wpa0wc-image.image) </span> |The element configuration entry is in the upper right corner of the visual editor, with a Tooltip prompt, which can be dragged and dropped. |
   |**Added variant entry 1** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba4c259a37c142c891a8b2ec4b75c914~tplv-goo7wpa0wc-image.image) </span> |Entry 1: Select Element (Element 1) = \> Modify Font Color = \> Click the "Add Variant" button = \> Show the selected variant X = \> Element Configuration Kanban Show Variant X |
   |**Added variant entry 2** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/154a969d6f704de49a533c37271ca792~tplv-goo7wpa0wc-image.image) </span> |Entry 2: Select Element Configuration Kanban = \> Select Element X or Original Variant = \> Edit Modifications = \> Click the "Add Variant" button = \> Show the selected variant X = \> Element Configuration Kanban Show Variant X |
   |**Modify variant** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e96f5752449d4447a0c78a805f435652~tplv-goo7wpa0wc-image.image) </span><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a489f787f7a40feaafeaf6b742b01af~tplv-goo7wpa0wc-image.image) </span> |When selecting a variant, the left Kanban is linked to display the current corresponding elements and variants, making it easier for users to edit more intuitively. **Modify entry:**  Variant already created = \> Select element configuration kanban = \> Select element X or original variant of element X = \> Edit changes = \> Click "Save changes" button = \> Show selected variant X = \> Element configuration kanban Show variant X<br><br><br>1. Editing and modifying the same property will update the previous property configuration (as shown in Figure 1 on the left).<br><br>2. For editing and modifying different properties, a new property configuration will be added (as shown in Figure 2 on the left). |
   |**Delete variant/rename variant/copy variant** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a22c3327e7454154845d7e9399ad6d2c~tplv-goo7wpa0wc-image.image) </span> |Can delete variants/rename variants/copy variants |
   |**Number of experimental versions** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0e06251b062439680ad6004c723d188~tplv-goo7wpa0wc-image.image) </span> |* An element, at least one original variant, and then there can be multiple variants X, the number of variants is not limited<br><br>* There can be multiple elements, and there is no limit to the number of elements.<br><br><br>Number of experimental versions = A \* B \* C \*... \* N<br><br>Here's an example.<br><br><br>* The selection modifies three elements, the first element has three variants, the second element has two variants, and the third element has two variants.<br><br>* Number of experimental versions = 3 variants of the first element \* 2 variants of the second element \* 2 variants of the third element<br><br>* Number of experimental versions 12 = 3 \* 2 \* 2 |
   |**Build version** |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2037d72ea22f435381d93393ac88956a~tplv-goo7wpa0wc-image.image) </span> |After clicking "Generate Version", go back to the third step of the experimental version. |
   

* **Configure experimental version information: generate element settings and version combinations**

   Includes a preview of element settings + version combinations.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53b77a86fd0347a5a871f8fddef74e84~tplv-goo7wpa0wc-image.image) </span>

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a3e82992c364b2c98ceb93bd0daac2e~tplv-goo7wpa0wc-image.image) </span>


<span id="a1247a97"></span>
## Step4 Experimental indicators

The experimental indicators can measure the success of the experiment. After the experiment starts, you can see the comparison of the attention indicators in the experimental version and the control version on the experimental report page. At this step, you need to select the experimental attention indicators.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/947941adfc854c9f953015eb71477873~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental core indicator configuration** |* **Core indicator configuration:** <br><br>   To determine whether the experimental function meets the expected "direct effect indicators" or "success indicators", you can select the indicators as the core indicators of the experiment in the existing indicator group in the drop\-down box. It is recommended to conduct the experimental design reasonably and choose carefully. For more experience guidance on experimental indicator setting, please check it [1. Identify evaluation metrics](https://docs.byteplus.com/docs/DataTester/How-to-Interpret-the-Experiment-Report#_1-%E7%A1%AE%E5%AE%9A%E8%AF%84%E4%BC%B0%E6%8C%87%E6%A0%87).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the experimental indicators are configured, after the subsequent experiments are created, if there are special circumstances that need to modify the experimental indicators, please enter the experimental details page to modify them.   </div><br>   <br><br>* **Monitoring alarm:**  You can select the target indicator and click "Monitoring alarm", fill in the specific required alarm strategy, choose whether to tick "Significant effect", and choose the effective way of the alarm strategy.<br><br>* **Edit indicators:**  Click on the 3 position in the legend to enter the indicator editing page, and edit the name, indicator type, and whether it is set as a must\-see indicator for indicators. |
|**Experimental attention indicator configuration** |Configure the metrics that need attention. You can select the indicators you need to pay attention to in the drop\-down list of the page, or you can click the **New Indicator** or **Remove Indicator** button on the page to quickly adjust the indicators you need to pay attention to. |
|**Confidence level** |Confidence level (also known as confidence level, confidence coefficient, statistical significance) refers to the probability that there is a real difference in performance between the experimental group and the control group.<br><br>For example, when the confidence level is 95%, if the confidence level p value of an experimental indicator is < 0.05, it means that the indicator is significantly different from the control group. To set the confidence level parameter value, you need to contact the group administrator or app administrator and go to " System Administration \- Confidence Level Settings " to set it. |


<span id="87bce5a2"></span>
## Debug, start, stop experiments

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list and check the experiment status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>


* **Debugging:**  The newly created experiment is **debugging**. At this stage, you can invite users who have been added as test users to conduct experimental tests to confirm that the experiment meets expectations.

* **In progress:**  After the experiment is debugged, you can click "Start" on the experiment list page to start the experiment. After the start of the experiment, the state of the experiment becomes  **"In Progress"** . At this time, the user can view the group in real time, and the indicator confidence level will be produced on the second day.

* **Closed:**  After the experiment starts, the experiment will automatically stop when the experiment duration reaches the **experiment duration** configured when the experiment was created; if the experiment duration is not reached, you want to stop the experiment immediately, or you can manually stop the experiment in the experiment list. After stopping the experiment, the experimental state changes to **has ended**.


<span id="43fa8f1b"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, please refer to the details [Experimental Report Overview](https://docs.byteplus.com/docs/DataTester/Experimental-Report-Overview).
