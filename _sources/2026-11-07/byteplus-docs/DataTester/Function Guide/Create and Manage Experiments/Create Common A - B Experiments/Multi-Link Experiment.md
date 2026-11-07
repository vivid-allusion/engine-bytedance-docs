---
title: "Multi-Link Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Multi-Link-Experiment"
---

DataTester provides you with a multi\-link experiment, also known as a split url experiment, that allows users to access different versions of page URLs based on the splitting results. This article introduces the application scenarios and operation points of multi\-link use.

<span id="8661306c"></span>
# Feature Overview

The multi\-link experiment allows users to access different versions of page URLs based on streaming results, for example:


* Example scenario: When you have two different styles of landing pages `https://example.com/1.html`and `https://example.com/2.html`, you want to compare the conversion effect of the two pages.

* Multi\-link experimental version settings: You can choose to set `https://example.com/1.html`as a control version link and `https://example.com/2.html`as an experimental version link.

* Experimental logic:

   * After the experiment starts running, the control version link is pushed to the user. If 50% of the traffic is allocated to each of the two versions, then when the user accesses the control version link `https://example.com/1.html`, 50% of the users will enter the original version, and the remaining 50% will enter the experimental version and jump to `https://example.com/2.html`.

   * If accessed directly `https://example.com/2.html`will not enter the experiment.


<span id="a9c40ed7"></span>
# **Preconditions and limitations**


|Limitations/Prerequisites |Description |
|---|---|
|Types of supported experiments |* The visual experiment type is **client side** experiment.<br><br>* Currently supports **Web and H5 pages**. |
|Prerequisite |* Before using the multi\-link experiment, you need to integrate DataTester's data access SDK, see details [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataTester/Web-JavaScript-SDK-Integration). |


<span id="9a7779f0"></span>
# Application scenario


* Market students test different ad landing pages in order to compare the conversion rate of each landing page and select the winning page.

* The operation students tested different content pages, especially the H5 activity page, in order to compare the conversion of each activity page and select the winning activity page.

* Product students test different registration process pages in order to compare the user registration attrition rates brought by different processes.


<span id="031d2cdf"></span>
# Operation demonstration

**Quickly understand the multi\-link experiment creation process👇** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/915fb2c5fb684c23bbe535b972f333ae~tplv-goo7wpa0wc-image.image) </span>

<span id="939bc869"></span>
# Create an experiment

Click "+ Create Experiment" on the experiment list page, select Multi\-link Experiment, and enter the experiment creation process.

<span id="2aa9e95c"></span>
## **Step1 Enter basic information**

**Experimental basic information** related parameters are mainly used to identify experiments, clear experimental types, etc. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64b2c9992c9e49a4a352b1e588600289~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experiment Name & Experiment Description** |* **Experiment name:**  It is recommended to set it to the name related to the experimental content. If there is an experimental version iteration, you can add the version number suffix, so that your partners can quickly understand what the experiment is doing and which iteration version is in.<br><br>* **Experiment description:**  The content of the experiment is briefly described, which can make the project related personnel more clearly know how the experiment is done and what problems to solve, and also facilitate the later viewing and management of historical experiments at a glance. |
|**Experimental label** |You can select an existing experimental label in the drop\-down box, or you can directly enter a new label.<br><br>Generally, keywords such as business line and optimization direction are used as tags to screen and classify experiments. After the subsequent experiments are created, relevant experiments can be quickly searched through the experiment tags in the experiment list. |
|**Type of experiment** |Currently only client side experiments are supported. |
|**Experiment duration** |Refers to the duration of the experiment, generally in order to avoid differences in user behavior in different time periods (weekdays and weekends), it is recommended to observe at least 2 complete test schedules.<br><br>For example, when considering the impact of weekdays and weekends, the test schedule takes at least one week, and the recommended duration of the experiment is 14 days. |
|**Experiment leader** |Default is the experiment creator. |


<span id="2630a79f"></span>
## **Step2** Set the **effective policy**

**Effective strategy** related parameters are mainly used to set the subsequent opening AB test, which users will enter the A experiment, which users will enter the B experiment, through scientific experimental traffic allocation, to achieve a sufficient number of users participating in the experiment, and the experiment between each other do not interfere with the effect of credibility.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting up experimental traffic, you need to understand some basic concepts of experimental traffic:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Traffic</strong> & <strong>Audience Users</strong> & <strong>Experiment Traffic</strong> :</div>


   * <div data-tips="true" data-tips-type="warning">Traffic refers to the total number of users a product has.</div>


   * <div data-tips="true" data-tips-type="warning">Audience Users: In the overall user, all users selected by some filter conditions to participate in the AB test.</div>


   * <div data-tips="true" data-tips-type="warning">Experimental traffic: among audience users, the proportion of users participating in an AB testing. After enabling audience rules, the system will <strong>first filter users who meet the rules</strong>, and then take effect according to the configured <strong>experimental traffic ratio</strong>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Flow layer</strong> / <strong>experimental layer</strong> / <strong>mutual exclusion group</strong> / <strong>mutual exclusion layer & mutual exclusion experiment</strong> :</div>


   * <div data-tips="true" data-tips-type="warning">Flow layer, also known as mutual exclusion group, also known as mutual exclusion layer, experimental layer.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Mutual exclusion experiments</strong> , that is, experiments in <strong>the same flow layer</strong>. The traffic between mutual exclusion experiments is mutual exclusion, that is, all experiments in the mutual exclusion group do not share users: if a user hits Experiment 1 in the mutual exclusion group, it will not hit other experiments in that mutual exclusion group.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/091db40fe295411fbd8159dceab4da5c~tplv-goo7wpa0wc-image.image) </span>


* **Traffic setting**

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Whether mutual exclusion** |When you need to conduct multiple AB test, you need to configure whether the currently created experiment needs mutual exclusion with other experiments according to the experimental situation, so as to avoid the same user being assigned to two experiments that will affect each other, thus affecting AB test results.<br><br>For example, if you want to do an experiment on button color and button shape at the same time, and the two experiments affect each other, you need to add the two experiments to a mutual exclusion group.<br><br>Learn more about traffic tiers and how to create one at: [Traffic Layer and Mutual Exclusion Domain](https://docs.byteplus.com/docs/DataTester/Traffic-Layer-and-Mutual-Exclusion-Domain). |
   |**Experimental traffic** |The proportion of users who satisfied the user audience in the effective experiment. The system defaults to 100% traffic, you can estimate the traffic through the suggestion tool (click the traffic calculator), and see how much traffic is set appropriately, see [Traffic Calculator](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator).<br><br>After enabling audience rules, the system will **first filter users who meet the rules** , and then take effect according to the configured **experimental traffic ratio**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When estimating the experimental traffic, it is usually necessary to combine the experimental business metrics with the <strong>MDE</strong> (test sensitivity) for estimation. Usually, the experimental metrics are to improve/decrease xx (a certain business metric value). The MDE recommends estimating less than this metric value. Try to avoid the MDE value being large and unable to detect the real experimental results.</div><br> |
   

* **User audience rules**

   You can create multiple filter groups, filtering the logical relationships between the groups as "or"; you can set multiple filter conditions within each filter group, and the logical relationships between the filter conditions as "and".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f1e96e0372e42d3b5dc68ccd8fb5a4b~tplv-goo7wpa0wc-image.image) </span>

   Detailed instructions for configuring each filter group are as follows.

   
   |**Filter condition** |**Configuration instructions** |
   |---|---|
   |**Add and condition** |For client side experiments, after clicking **Add Filter Criteria** , you can use **user properties** as filters for user audiences, support using system\-provided **preset properties**, or create **custom properties** for filtering.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a357abcb35249deb7e783261c8fd440~tplv-goo7wpa0wc-image.image) </span><br><br>You can view existing preset and custom properties on the **Data Management** \> **Metadata Management** \> **User Properties** page, or you can create new custom properties.<br><br>**Scenario Example: New User Experiment**<br><br>In the "Select Target Audience" filter, you can add a "User First Installation Time" filter for new users, and use the first installation time to identify new users, that is, all users whose first installation time is later than the opening time of the experiment are classified as "New Users". During the start of the experiment, only new users enter the experimental group, and other existing users do not enter the group.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d0e1e462d6c4fafb17023f0fb4b0961~tplv-goo7wpa0wc-image.image) </span> |
   |**Add cluster** |For client\-side experiments, after clicking **add cluster**, you can filter users using the user cluster you created. See activity details for creating user groups [User Cohorts](https://docs.byteplus.com/docs/DataTester/User-Cohorts). |
   

* **Experience consistency**

   After opening, the effective version of the user during the experiment does not change with the adjustment of traffic and audience conditions, which can ensure that the same user can only enter one experimental version during the experiment. After opening, as long as the user has entered the current experimental version (unless the experiment is suspended or closed), the experiment will no longer be released.


<span id="75e6e3d8"></span>
## Step3 configuration experimental version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring the experimental version, you need to understand some basic concepts of the experimental version:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Experimental version</strong> & <strong>experimental group</strong> & <strong>control group</strong></div>


   <div data-tips="true" data-tips-type="warning">AB test is usually a set of controlled experiments: <strong>experimental version</strong>, <strong>control version</strong>. By setting different logical strategies for the experimental version and the control version, it is verified which strategy is better while keeping other conditions stable. <strong>The control version</strong> is generally the current strategy, and the <strong>experimental version</strong> is generally the new strategy we want to try.   </div>
   

* <div data-tips="true" data-tips-type="warning"><strong>Test User</strong> & <strong>User ID: SSID</strong> and <strong>UUID</strong></div>


   * <div data-tips="true" data-tips-type="warning"><strong>Test users:</strong> Before the experiment is officially opened, it is usually necessary to select several users to test, observe whether the experiment can normally obtain the data you want to collect, and test whether there are bugs in the business functions after adding the experimental logic. Test users who participate in the test are also called "whitelisted users". When configuring the experimental version, you need to add test users for the experimental group and the control group.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>SSID:</strong> that is, Standardized Service ID (Standardized Service Id), is the user ID provided by BytePlus Growth Marketing Suite series products to mark and identify users. The SSID is automatically generated and maintained by the system, and you can use it as needed. When adding test users to the experimental version, the users participating in the test are identified by the SSID generated by the system.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>UUID:</strong> that is, User Unique Id, which is usually the user ID used in the product business, generally corresponds to the user's login ID (such as mobile phone number, email, etc.) one\-to\-one, UUID is maintained by you.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7d47498c973448f9c4ccc16b64dfece~tplv-goo7wpa0wc-image.image) </span>


* **Test user hit condition**

   When selecting the experimental version corresponding to the test user hit, whether the audience rule set in the previous step needs to be satisfied. Since the test user is mainly used for debugging and verification before the experiment is officially launched, the choice of the test user can be inconsistent with the final experimental hit user, and you can configure it according to your actual needs.

* **Heat map**

   Support turning on the page heat map. If you want to see the heat map data on the page to be tested later, you can turn on the heat map switch here, and turn on the full event tracking function switch when integrating the data access SDK in advance. Heat map analysis function introduction see [heat map analysis](https://docs.volcengine.com/docs/6285/65951?lang=en).

* **Configure URL rules**

   Configure the rule logic of the URL hit experiment accessed by the user. A URL that can match the rule means that the experiment can be hit, and a mismatch means that the experiment cannot be hit.

   
   |Matching rule |Rule description |
   |---|---|
   |Simple match |In the case of URL matching, simple matching ignores the query parameters and anchors in the URL, and can hit the experiment if the URL domain name and path of the user visiting the page match.<br><br><br>* Simple matching ignores the following parts of the URL:<br><br>   * query parameters<br><br>   * hash or anchor tag<br><br>   * Does www exist in the URL?<br><br>* The URL simple match compares the following sections:<br><br>   * subdomain<br><br>   * subdirectory<br><br>   * File extension (.html, .php, etc.) |
   |Exact match |URL exact match, that is, an exact match, does not ignore any part of the URL, and the experiment will only run after the URL is exactly matched. When you need to exclude pages with parameters, you can use "exact matching". |
   |Parameter matching |Support user\-defined page domain name, path, and parameters. Applicable to some delivery scenarios, the delivery channel will randomly increase the parameters of the scene, in this scenario, simple matching can not distinguish between some media buy channels, accurate matching can not predict the specific link in advance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The functions of "heat map" and "URL parameter matching" cannot be turned on at the same time. If you want to use "URL parameter matching", please click Close at the heat map location.</div><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0b669456e1f4b529fe6ecaef085800f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* The user enters the domain name as: `https://www.volcengine.com`<br><br>* The path is:/docs/search<br><br>* The parameters are: **q** contains [aaa] [bbb], **c** is equal to [111] [222]<br><br>* Then, when the user accesses the following URL, the matching situation is as shown in the table:<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13e9052d32ad4397a162b88d21709d57~tplv-goo7wpa0wc-image.image) </span> |
   

* **Redirect Rules & Experimental Versions**

   In the multi\-link experiment, it is only necessary to configure the URLs of the control version and the experimental version according to the actual scene, where the control version is the basic URL of the shunt.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The URL and URL match type filled in here are the basis for determining whether the page visited by the user can hit the experiment, and which version will be accessed after the hit experiment is determined by the streaming service.   </div>
   

   In the multi\-link experiment, the option "Keep the parameters and anchors of the original URL when redirecting" is provided. When the user checks the box, the parameters and anchors in the URL of the user's visit address will be retained and merged with the parameters and anchors of the URL in the version that the user actually hits. If there is a conflict between the parameter values, the parameter values and anchor values in the filled URL shall prevail.

   For example, if the user ticks "Keep the parameters and anchors of the original URL when redirecting" in the case of a **simple match**:

   * **The comparison version URL is:**  `https://app.test.com?param1=origin#frag1`

   * **The experimental version URL is:**  `https://miniapp.test.com/path?param1=redirect#frag1`

      The redirection results are as follows:

   
   |Serial number |URL |Does it match |After hitting the comparison version, the final URL |After hitting the experimental version, the final URL |
   |---|---|---|---|---|
   |1 |`https://app.test.com` |match |`https://app.test.com?param1=origin#frag1` |`https://miniapp.test.com/path?param1=redirect#frag1` |
   |2 |`https://app.test.com?utm_source=5&utm_medium=sembaidu&userid=23` |match |`https://app.test.com?utm_source=5&utm_medium=sembaidu&userid=23&param1=origin#frag1` |`https://miniapp.test.com/path?utm_source=5&utm_medium=sembaidu&userid=23&param1=redirect#frag1` |
   |3 |`https://app.test.com/#AKYlHl` |match |`https://app.test.com?param1=origin#frag1` |`https://miniapp.test.com/path?param1=redirect#frag1` |
   |4 |`https://app.test.com/?param1=origin&utm_medium=sembaidu&userid=23#frag2` |match |`https://app.test.com?param1=origin&utm_medium=sembaidu&userid=23#frag1` |`https://miniapp.test.com/path?param1=redirect&utm_medium=sembaidu&userid=23#frag1` |
   |5 |`https://test.com` |mismatch |\-\- |\-\- |
   |6 |`https://miniapp.test.com` |mismatch |\-\- |\-\- |
   |7 |`https://app.test.com/index.php` |mismatch |\-\- |\-\- |
   |8 |`https://app.test.com/subdirector` |mismatch |\-\- |\-\- |
   |9 |`https://docs.app.test.com/` |mismatch |\-\- |\-\- |
   |10 |`https://docs.test.com/` |mismatch |\-\- |\-\- |
   


<span id="35fab2ec"></span>
## Step4 Experimental metrics

Experimental metrics are used to evaluate the policy effect of each experimental version, and whether the functions of assisting decision\-making AB test can meet business expectations. By configuring the experimental core metrics and experimental attention metrics, after the follow\-up experiment is completed, the experimental report related to the metrics will be automatically output for you according to the metrics you configured to assist you in analyzing the experimental results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bf3852a49524e189cdafd6865471414~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental core metric configuration** |* **Core metric configuration** :<br><br>   To determine whether the experimental function meets the expected "direct effect metrics" or "success metrics", you can select the metrics as the core metrics of the experiment in the existing metric group in the drop\-down box. It is recommended to conduct the experimental design reasonably and choose carefully. For more experience guidance on experimental metric setting, please check it [1. Identify evaluation metrics](https://docs.byteplus.com/docs/DataTester/How-to-Interpret-the-Experiment-Report#_1-%E7%A1%AE%E5%AE%9A%E8%AF%84%E4%BC%B0%E6%8C%87%E6%A0%87).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the experimental metrics are configured, after the subsequent experiments are created, if there are special circumstances that need to modify the experimental metrics, please enter the experimental details page to modify them.   </div><br>   <br><br>* **Monitoring alarm:**  You can select the target metric and click "Monitoring alarm", fill in the specific required alarm strategy, choose whether to tick "Significant effect", and choose the effective way of the alarm strategy.<br><br>* **Edit metrics:**  Click on the 3 position in the legend to enter the metric editing page, and edit the name, metric type, and whether it is set as a must\-see metric for metrics. |
|**Experimental attention metric configuration** |Configure the metrics that need attention. You can select the metrics you need to pay attention to in the drop\-down list of the page, or you can click the **New metric** or **Remove metric** button on the page to quickly adjust the metrics you need to pay attention to. |
|**Confidence level** |Confidence level (also known as confidence level, confidence coefficient, statistical significance) refers to the probability that there is a real difference in performance between the experimental group and the control group.<br><br>For example, when the confidence level is 95%, if the confidence level p value of an experimental metric is < 0.05, it means that the metric is significantly different from the control group. To set the confidence level parameter value, you need to contact the group administrator or app administrator and go to " [System Settings](https://docs.byteplus.com/docs/DataTester/System-Settings)" to set it up. |


<span id="1e04fb08"></span>
# Debug, start, stop experiments

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list and check the experiment status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>


* **Debugging:**  The newly created experiment is **debugging**. At this stage, you can invite users who have been added as test users to conduct experimental tests to confirm that the experiment meets expectations.

* **In progress:**  After the experiment is debugged, you can click "Start" on the experiment list page to start the experiment. After the start of the experiment, the state of the experiment becomes "I**n Progress"** . At this time, the user can view the group in real time, and the metric confidence level will be produced on the second day.

* **Closed:**  After the experiment starts, the experiment will automatically stop when the experiment duration reaches the **experiment duration** configured when the experiment was created; if the experiment duration is not reached, you want to stop the experiment immediately, or you can manually stop the experiment in the experiment list. After stopping the experiment, the experimental state changes to **has ended**.


<span id="af27c9e7"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, please refer to the details [Experimental Report Overview](https://docs.byteplus.com/docs/DataTester/Experimental-Report-Overview).
