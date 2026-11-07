---
title: "Programming Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Programming-Experiment"
---

**Programming experiment** refers to the method of embedding AB test version logic in **server side** or **client side** code and AB test through code programming, which can be widely used in front\-end optimization, policy optimization and back\-end algorithm optimization. This article introduces the application scenarios of programming experiments and instructions for creating operations.

<span id="二-应用场景"></span>
# Experimental subdivision types and applicable scenarios


* Programming experiments are suitable for experimenters with certain code development capabilities, and can be applied to almost all common scenarios that require AB test.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">A/B experiments also provide you with a variety of experiment types, such as visual experiments and MAB experiments, which can meet scenarios such as conducting experiments without code visualization and intelligent experiments.   </div>
   

* According to the type of code embedding, programming experiments can be further subdivided into **server side experiments** and **client side experiments**. The comparative description and applicable scenarios of the two experiments are as follows.

   
   |**Type of experiment** |**Experimental comparison description** |**Applicable scenario** |
   |---|---|---|
   |**Client side experiment** |It refers to the experiment in which the experiment logic is embedded in the client side experiment code, and the experiment grouping information is obtained through the client side and the configuration is controlled. |* Suitable for scenarios where only functions controlled by the client side can be AB test.<br><br>   For example, client\-side UI style, interaction function design, etc.<br><br>* Applicable to the scene where the AB test configuration needs to take effect when the APP is evoked.<br><br>   For example, it is necessary to conduct A/B experiments for the opening page of the APP. As soon as the user opens the APP, the client side needs to show the opening interface to the user. In this case, the client side may not have time to request the experimental configuration parameters from the server side. |
   |**Server side experiment** |It refers to the experiment that embeds the experiment logic into the server side code, obtains the experiment grouping information through the server side, and controls the experiment that the configuration takes effect or is issued. |* Suitable for scenarios where only functions controlled by the server side can be AB test.<br><br>   For example, information delivery algorithms (such as what users will see in the feed stream after opening Jinri Toutiao), product functions controlled by server side logic (such as push), etc.<br><br>* It is suitable for scenarios where AB test configuration takes effect without requiring the APP to be evoked. In this scenario, the client side usually has enough time to make a request to the server side, obtain the experimental configuration, and then show the experimental policy to the user. |
   |**Client side local offloading experiment** |It is also a kind of client side experiment, which is an experiment triggered by the experimenter implementing random shunt locally on the client side instead of requesting Tester's shunt service. See the client side local offloading experiment for details and activity details [Programming Experiment - Client Side Local Allocation](https://docs.byteplus.com/docs/DataTester/Programming-Experiment-Client-Side-Local-Allocation). |For example, new users of an app can start an experiment with a client side\-local offload, which is usually too late to generate a device ID (did) and usually handles non\-login status. Such experiments can be implemented within the client side shunt and experimental exposure logic. |
   


<span id="73e7d152"></span>
# **Prerequisite**

Before starting to create an experiment, you need to complete the tracking event access required for the experiment according to the experimental design. You can access the data through the client side SDK or server side SDK according to the experimental type. See: [Data Access Overview](https://docs.byteplus.com/docs/DataTester/Data-Access-Overview).

<span id="三、操作演示"></span>
# Operation demonstration

The following animation helps you quickly understand the process of creating a programming experiment. For detailed operation steps, please refer to the **Creating an Experiment** section below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/286f287c42384ee7bc43e1cb57eb3bd1~tplv-goo7wpa0wc-image.image) </span>

<span id="四-操作说明"></span>
# Create an experiment

Click "  **+ Create Experiment** " on the experiment list page, select Programming Experiment, enter the experiment creation process, and refer to the following steps to configure the details of the experiment.

<span id="b1010963"></span>
## Step1 Enter basic information

**Experimental basic information** related parameters are mainly used to identify experiments, clear experimental types, etc. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f144a74869ec4aed845e1e3e9ba1cdcd~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experiment Name & Experiment Description** |* **Experiment name:**  It is recommended to set it to the name related to the experimental content. If there is an experimental version iteration, you can add the version number suffix, so that your partners can quickly understand what the experiment is doing and which iteration version is in.<br><br>* **Experiment description:**  The content of the experiment is briefly described, which can make the project related personnel more clearly know how the experiment is done and what problems to solve, and also facilitate the later viewing and management of historical experiments at a glance. |
|**Experimental label** |You can select an existing experimental label in the drop\-down box, or you can directly enter a new label.<br><br>Generally, keywords such as business line and optimization direction are used as tags to screen and classify experiments. After the subsequent experiments are created, relevant experiments can be quickly searched through the experiment tags in the experiment list. |
|**Type of experiment** |Depending on the experiment plan, choose whether the created experiment is a client side experiment or a server side experiment. |
|**Experiment duration** |Refers to the duration of the experiment, generally in order to avoid differences in user behavior in different time periods (weekdays and weekends), it is recommended to observe at least 2 complete test schedules.<br><br>For example, when considering the impact of weekdays and weekends, the test schedule takes at least one week, and the recommended duration of the experiment is 14 days. |
|**Experiment leader** |Default is the experiment creator. |


<span id="b367e1a0"></span>
## Step2 Set the effective policy

**Effective strategy** related parameters are mainly used to set the subsequent opening AB test, which users will enter the A experiment, which users will enter the B experiment, through scientific experimental traffic allocation, to achieve a sufficient number of users participating in the experiment, and the experiment between each other do not interfere with the effect of credibility.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting up experimental traffic, you need to understand some basic concepts of experimental traffic:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Traffic</strong> & <strong>Audience Users</strong> & <strong>Experiment Traffic</strong>:</div>


   * <div data-tips="true" data-tips-type="warning">Traffic refers to the total number of users a product has.</div>


   * <div data-tips="true" data-tips-type="warning">Audience Users: In the overall user, all users selected by some filter conditions to participate in the AB test.</div>


   * <div data-tips="true" data-tips-type="warning">Experimental traffic: among audience users, the proportion of users participating in a AB test.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Flow layer</strong> / <strong>experimental layer</strong> / <strong>mutual exclusion group</strong> / <strong>mutual exclusion layer & mutual exclusion experiment</strong>:</div>


   * <div data-tips="true" data-tips-type="warning">Flow layer, also known as mutual exclusion group, also known as mutual exclusion layer, experimental layer.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Mutual exclusion experiments</strong>, that is, experiments in <strong>the same flow layer</strong>. The traffic between mutual exclusion experiments is mutual exclusion, that is, all experiments in the mutual exclusion group do not share users: if a user hits Experiment 1 in the mutual exclusion group, it will not hit other experiments in that mutual exclusion group.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5990267731a248fc898746505498a094~tplv-goo7wpa0wc-image.image) </span>


* **Traffic settings**

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Whether mutual exclusion** |When you need to conduct multiple AB test, you need to configure whether the currently created experiment needs mutual exclusion with other experiments according to the experimental situation, so as to avoid the same user being assigned to two experiments that will affect each other, thus affecting AB test results.<br><br>For example, if you want to do an experiment on button color and button shape at the same time, and the two experiments affect each other, you need to add the two experiments to a mutual exclusion group.<br><br>Learn more about traffic tiers and how to create one at: [Traffic Layer and Mutual Exclusion Domain](https://docs.byteplus.com/docs/DataTester/Traffic-Layer-and-Mutual-Exclusion-Domain). |
   |**Experimental traffic** |The proportion of users who satisfied the user audience in the effective experiment. The system defaults to 100% traffic. You can estimate the traffic through the suggestion tool (click Traffic Calculator) to see how much traffic is appropriate.<br><br>After enabling audience rules, the system will **first filter users who meet the rules**, and then take effect according to the configured **experimental traffic ratio**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When estimating the experimental traffic, it is usually necessary to combine the experimental business metrics with the <strong>MDE</strong> (test sensitivity) for estimation. Usually, the experimental metrics are to improve/decrease xx (a certain business metric value). The MDE recommends estimating less than this metric value. Try to avoid the MDE value being large and unable to detect the real experimental results.</div><br> |
   |**Enhanced shunt uniformity** |Configure whether to turn on the enhanced shunt uniformity switch. After turning on the switch:<br><br><br>* You can set the experimental metrics for which uniform shunting is performed, and set the time range for uniform shunting and the conditions for restochastic stopping.<br><br>* After the configuration is completed, after the follow\-up experiment is started, the experimental traffic allocated by each version of the experiment will meet the following preconditions according to the configuration results:<br><br>   * The experimental metrics configured here did not differ significantly across experimental versions before the experiment began.<br><br>   * The populations configured here were evenly distributed across the experimental versions.<br><br>      By meeting the flow uniformity conditions before the experiment, differences can be avoided before the experiment starts, thus making the experimental results more reliable.<br><br><br>For more introduction and configuration details on enhanced shunt uniformity, see [Enhanced Shunt Uniformity](https://docs.byteplus.com/docs/DataTester/Enhanced-Shunt-Uniformity). |
   

* **User audience rules**

   You can create multiple filter groups, filtering the logical relationships between the groups as "or"; you can set multiple filter conditions within each filter group, and the logical relationships between the filter conditions as "and".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b3f4dfb55c54853902fb918c4db77fb~tplv-goo7wpa0wc-image.image) </span>

   For client side experiments and server side experiments, the ability to filter is inconsistent.

   
   |**Filter condition** |**Client side experiment** |**Server side experiment** |
   |---|---|---|
   |**Add filter criteria** |For client side experiments, after clicking **Add Filter Criteria**, you can use **user properties** as filters for user audiences, support using system\-provided **preset properties**, or create **custom properties** for filtering.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a357abcb35249deb7e783261c8fd440~tplv-goo7wpa0wc-image.image) </span><br><br>You can view existing preset and custom properties on the **Metrics Management** \> **Metadata Management** \> **User Properties** page, or you can create new custom properties.<br><br>**Scenario Example: New User Experiment**<br><br>In the "Select Target Audience" filter, you can add a "User First Installation Time" filter for new users, and use the first installation time to identify new users, that is, all users whose first installation time is later than the opening time of the experiment are classified as "New Users". During the start of the experiment, only new users enter the experimental group, and other existing users do not enter the group.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d0e1e462d6c4fafb17023f0fb4b0961~tplv-goo7wpa0wc-image.image) </span> |For server side experiments, after clicking **Add Filter Criteria**, you can use the created **server side request parameters** as filters for your user audience.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60b5571f8cb244fa8f2881f0bd322396~tplv-goo7wpa0wc-image.image) </span><br><br>See activity details for creating server side request parameters [Server Side Filtering Parameters](https://docs.byteplus.com/docs/DataTester/Server-Side-Filtering-Parameters). |
   |**Add cohort** |For client\-side experiments, after clicking **add cohort**, you can filter users using the user cohort you created. See activity details for creating user groups [User Cohorts](https://docs.byteplus.com/docs/DataTester/User-Cohorts). |Not supported |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Since the privatization 4.9.0 version, if you also purchased CDP at the same time, you can also use <strong>customer group comparison</strong> to configure user audience rules, open customer group experiment, please see the details of customer group experiment <a href="https://docs.byteplus.com/docs/DataTester/Programming-Experiment-Customer-Group-Experiment">Programming Experiment \- Customer Group Experiment</a>.   </div>
   

* **Experience consistency**

   After opening, the effective version of the user during the experiment does not change with the adjustment of traffic and audience conditions, which can ensure that the same user can only enter one experimental version during the experiment. After opening, as long as the user has entered the current experimental version (unless the experiment is suspended or closed), the experiment will no longer be released.


<span id="02fd9d72"></span>
## Step3 Configuration experimental version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring the experimental version, you need to understand some basic concepts of the experimental version:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Experimental version</strong> & <strong>experimental group</strong> & <strong>control group</strong></div>


   <div data-tips="true" data-tips-type="warning">AB test is usually a set of controlled experiments: <strong>experimental version</strong>, <strong>control version</strong>. By setting different logical strategies for the experimental version and the control version, it is verified which strategy is better while keeping other conditions stable. <strong>The control version</strong> is generally the current strategy, and the <strong>experimental version</strong> is generally the new strategy we want to try.   </div>
   

* <div data-tips="true" data-tips-type="warning"><strong>Test User</strong> & <strong>User ID: SSID</strong> and <strong>UUID</strong></div>


   * <div data-tips="true" data-tips-type="warning"><strong>Test users:</strong> Before the experiment is officially opened, it is usually necessary to select several users to test, observe whether the experiment can normally obtain the data you want to collect, and test whether there are bugs in the business functions after adding the experimental logic. Test users who participate in the test are also called "whitelisted users". When configuring the experimental version, you need to add test users for the experimental group and the control group.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>SSID:</strong> that is, Standardized Service ID (Standardized Service Id), is the user ID provided by BytePlus Growth Marketing Suite series products to mark and identify users. The SSID is automatically generated and maintained by the system, and you can use it as needed. When adding test users to the experimental version, the users participating in the test are identified by the SSID generated by the system.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>UUID:</strong> that is, User Unique Id, which is usually the user ID used in the product business, generally corresponds to the user's login ID (such as mobile phone number, email, etc.) one\-to\-one, UUID is maintained by you.</div>


* <div data-tips="true" data-tips-type="warning">Feature：</div>


   <div data-tips="true" data-tips-type="warning">Feature can be understood as a functional feature. For example, if you want to do an experiment to see if the new shape of the button can improve the click through rate of the button, and after the experiment is completed, it is found that it is indeed possible. Then the new shape can be regarded as the Feature online/solidified.   </div>
   


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/084bd32b9ea54f8e8156dbeb000085f1~tplv-goo7wpa0wc-image.image) </span>


* **Test user hit condition**

   When selecting the experimental version corresponding to the test user hit, whether the audience rule set in the previous step needs to be satisfied. Since the test user is mainly used for debugging and verification before the experiment is officially launched, the choice of the test user can be inconsistent with the final experimental hit user, and you can configure it according to your actual needs.

* **Whether to Link Features**

   If you have previously created a feature, you can associate the experiment with the feature. After selecting the association, you can bind the experiment to the Feature version. After the association, when the follow\-up experiment is running normally, it can be more convenient to manage and troubleshoot problems, such as online crashes, users entering the group do not meet expectations (user feedback does not experience the function), etc. You can troubleshoot where the configuration is released, which is convenient for subsequent full management.

   See more Feature introduction and creation operations [Experiment Quick Full Release](https://docs.byteplus.com/docs/DataTester/Experiment-Quick-Full-Release).

* **Experimental version**

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Version Type & Version Description** |AB test is usually a set of controlled experiments: **experimental version, control version.**  By setting different logical strategies for the experimental version and the control version, it is verified which strategy is better while keeping other conditions stable. **The control version** is generally the current strategy, and the **experimental version** is generally the new strategy we want to try.<br><br><br>* You can choose the corresponding **version type** , state what the current version policy is in the **version description** , and click **version 1** / **version 2** in the upper left corner to modify the version name, so that you can quickly understand which experimental version is currently available.<br><br>* If you have multiple new policies to experiment with, click **Add Experimental Version** below to continue adding new experimental group versions. |
   |**Test user** |Add test users to the corresponding experimental version. After the subsequent experiment is created, the added test users will enter the corresponding experimental version, which can test whether the experimental logic takes effect and whether the function has bugs.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If a user is a whitelisted user for a certain version, then experimental offloading has no impact on that user and is fixed to that version. For users on the whitelist, the data after the experiment is started will also be calculated into the experiment report.</div><br><br><br><div data-tips="true" data-tips-type="warning">For more information on the whitelist, please refer to <a href="https://docs.byteplus.com/docs/DataTester/Whitelist-Test">Whitelist Test</a>.</div><br><br><br><br>* You can manually enter the user's SSID to add the user as a test user for the current experimental version, with multiple users separated by a carriage return.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can enter the UUID in "Global Settings \- User Review" to query the SSID of the corresponding user.   </div><br>   <br><br>* If your experiment is a mobile end APP experiment, you can also click the QR code logo after the text box to efficiently add the SSID of the test user by scanning the code. Please refer to the introduction of scanning the code to enter the SSID [Scan the Code to Enter the Device ID](https://docs.byteplus.com/docs/DataTester/Scan-the-Code-to-Enter-the-Device-ID).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When scanning the code to add the test user SSID, make sure that the mobile phone that scans the code has installed the APP to be tested.   </div><br>   <br><br>* If you have added test whitelisted users to the **user test whitelist** page in **Global Settings** \> **Audience Management**, you can also select the test user group in the drop\-down box.<br><br>   See activity details for adding whitelisted users [Whitelist Test](https://docs.byteplus.com/docs/DataTester/Whitelist-Test). |
   |**Parameter Configuration** & **SDK Code Sample** |* **Experimental parameter configuration:**  is a supplement to the experimental version, generally a functional control configuration item, used to distinguish the control group and the experimental group. You can configure the experimental parameter name, format, and parameter value on the interface of the corresponding experimental version.<br><br>   For example, to verify the impact of the display timing of a product card on the user's consumption time of a video, an experiment could be designed as follows:<br><br>   * Control group: Product cards are displayed as soon as the video starts playing.<br><br>   * Experimental Group 1: Display the product card after 5 seconds of video playback.<br><br>   * Experimental Group 2: Display the product card after 10 seconds of video playback.<br><br>      With the help of experimental parameter configuration function, first parse the goods_card_show_time parameters in the code and display the product card after video playback {goods_card_show_time} seconds, and then when creating the experiment, the control group/experimental group 1/experimental group 2 configure the experimental parameters goods_card_show_time = 0/5/10, which can complete the flexible and efficient online of the experiment.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When creating an experiment, by configuring the experimental parameters, not only can the experimental flow be achieved, but also a good experimental parameter design can help the experimental creator to conduct more flexible experiments without increasing the development workload. For more information on experimental parameters, see<a href="https://docs.byteplus.com/docs/DataTester/How-to-Configure-Experimental-Parameters">How to configure experimental parameters</a>   </div><br>   <br><br>* **SDK code example**:<br><br>   After creating the experimental parameters, the developer needs to obtain the SDK code containing the experimental parameters and incorporate it into the client side or server side code. After parsing, the experimental parameters can take effect.<br><br>   You can click the SDK sample code button in the upper right corner of the page to get the SDK sample code automatically generated by the system according to the current experimental parameter configuration results, which is convenient for subsequent research and development to embed business code and implement AB test logic through programming.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d283926599e24732baa753d9d42a60f8~tplv-goo7wpa0wc-image.image) </span> |
   |**Traffic allocation** |After the subsequent experiment is started, the proportion of experimental traffic allocated between different experimental versions in all the experimental traffic participating in the AB test.<br><br><br>* **Uniform distribution of traffic\-on:**  The default is on state, and the open state is to force the uniform distribution of traffic in each experimental version.<br><br>* **Traffic evenly distributed\-off:**  After closing, the relative proportion of traffic in the control version and the experimental version can be deployed. You can control the proportion of users hit by each experimental version by entering a value.<br><br>   For example, when the uniform distribution is turned off, the three experimental versions can be configured to account for 20% of the control version, 50% of the experimental version 1, 30% of the experimental version 2, and 100% of the overall sum. The experimental version 3 is automatically divided into 20% traffic.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After the traffic weights of each experimental version are changed, users who have entered the group historically will not be affected, but only users who have been assigned but not entered the group, as well as users who have not been assigned.</div><br> |
   


<span id="5db1321f"></span>
## Step4 Experimental metrics

Experimental metrics are used to evaluate the policy effect of each experimental version, and whether the functions of assisting decision\-making AB test can meet business expectations. By configuring the experimental core metrics and experimental attention metrics, after the follow\-up experiment is completed, the experimental report related to the metrics will be automatically output for you according to the metrics you configured to assist you in analyzing the experimental results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bf3852a49524e189cdafd6865471414~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental core metric configuration** |* **Core metric configuration**:<br><br>   To determine whether the experimental function meets the expected "direct effect metrics" or "success metrics", you can select the metrics as the core metrics of the experiment in the existing metric group in the drop\-down box. It is recommended to conduct the experimental design reasonably and choose carefully. For more experience guidance on the setting of experimental metrics, please refer to [How to Interpret the Experiment Report](https://docs.byteplus.com/docs/DataTester/How-to-Interpret-the-Experiment-Report)the **Determine evaluation metrics** section.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the experimental metrics are configured, after the subsequent experiments are created, if there are special circumstances that need to modify the experimental metrics, please enter the experimental details page to modify them.   </div><br>   <br><br>* **Monitoring alarm:**  You can select the target metric and click "Monitoring alarm", fill in the specific required alarm strategy, choose whether to tick "Significant effect", and choose the effective way of the alarm strategy.<br><br>* **Edit metrics:**  Click on the 3 position in the legend to enter the metric editing page, and edit the name, metric type, and whether it is set as a must\-see metric for metrics. |
|**Experimental attention metric configuration** |Configure the metrics that need attention. You can select the metrics you need to pay attention to in the drop\-down list of the page, or you can click the **New metric** or **Remove metric** button on the page to quickly adjust the metrics you need to pay attention to. |
|**Confidence level** |Confidence level (also known as confidence level, confidence coefficient, statistical significance) refers to the probability that there is a real difference in performance between the experimental group and the control group.<br><br>For example, when the confidence level is 95%, if the confidence level p value of an experimental metric is < 0.05, it means that the metric is significantly different from the control group. To set the confidence level parameter value, you need to contact the group administrator or app administrator and go to " System Administration \- Confidence Level Settings " to set it. |


<span id="989feb5f"></span>
# Debug, start, stop experiments

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list and check the experiment status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>


* **Debugging:**  The newly created experiment is **debugging**. At this stage, you can invite users who have been added as test users to conduct experimental tests to confirm that the experiment meets expectations.

* **In progress:**  After the experiment is debugged, you can click "Start" on the experiment list page to start the experiment. After the start of the experiment, the state of the experiment becomes "**In Progress"** . At this time, the user can view the group in real time, and the metric confidence level will be produced on the second day.

* **Closed:**  After the experiment starts, the experiment will automatically stop when the experiment duration reaches the **experiment duration** configured when the experiment was created; if the experiment duration is not reached, you want to stop the experiment immediately, or you can manually stop the experiment in the experiment list. After stopping the experiment, the experimental state changes to **has been closed**.


<span id="c48dd43d"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, please refer to the details [Experimental Report Overview](https://docs.byteplus.com/docs/DataTester/Experimental-Report-Overview).

<span id="b4d9807a"></span>
# Next steps


* Experiment sharing and permission management:

   After the experiment is created, you can also manage permissions on the experiment, setting the experiment to be public or private, see details [Experimental Permission Management](https://docs.byteplus.com/docs/DataTester/Experimental-Permission-Management).

* Experimental diagnosis:

   After the experiment is created, if you find that the experiment does not meet expectations, you can go to the experiment details page to diagnose the experiment, see the details [Experimental Diagnosis Tool](https://docs.byteplus.com/docs/DataTester/Experimental-Diagnosis-Tool).
