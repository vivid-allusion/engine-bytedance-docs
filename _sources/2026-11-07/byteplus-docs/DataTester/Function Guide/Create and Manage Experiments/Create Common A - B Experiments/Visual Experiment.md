---
title: "Visual Experiment"
product: "BytePlus DataTester"
product_code: "DataTester"
source: "https://docs.byteplus.com/en/docs/DataTester/Visual-Experiment"
---

DataTester provides you with visual experiments that support interface\-based operations through a visual editor, allowing you to create different experimental versions without coding, and explore the best results of different versions of the page through streaming and user feedback to confirm which version of the page is more attractive, improving conversion rates and retention. This article introduces you to the key points of visualization experiments operation.

<span id="7759eb10"></span>
# Feature Overview


* The biggest advantage of visual experiments is that there is **no need for coding, quick experiments**, reducing the cost of using products and operations, and supporting visual operations through the WYSIWYG(What You See Is What You Get) visual editor, such as editing elements and properties, adding widgets components, deleting elements, etc., to form different experimental versions.

* Multi\-page visualization experiment: multiple pages can be included in one version, suitable for multiple pages that are related before and after optimization.


An example of how to create a visual experiment is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b53eef9ba875447fbe9480af94125970~tplv-goo7wpa0wc-image.image) </span>

<span id="ef29dc5b"></span>
# **Preconditions and limitations**


|Limitations/Prerequisites |Description |
|---|---|
|Page transport protocol restrictions |The page transfer protocol requires HTTPS (Hypertext Transfer Protocol Secure: HyperText Transfer Protocol Secure). |
|Page browser suggestion |We recommend using the latest version Chrome browser. |
|Types of supported experiments |* The visual experiment type is **client side** experiment.<br><br>* Currently supports **web and H5 pages**, including H5 pages in the app. |
|Prerequisite |* Before using the visualization experiment, you need to integrate DataTester's data access SDK, see details [Web/JavaScript SDK Integration](https://docs.byteplus.com/docs/DataTester/Web-JavaScript-SDK-Integration).<br><br>* If you want to see the heat map related data at the same time when creating a visual experiment, you need to ensure that the full event tracking switch is turned on when accessing the data. |


<span id="52b920f7"></span>
# Application scenario

Visualization experiments are suitable for single\-page + multi\-page scenarios such as landing pages and homepages. The usage scenarios of AB visualization experiments include:


* **Interface design optimization:**  By comparing different versions of interface design, determine which version is more attractive to users, improve user retention and conversion rate.

* **Content optimization:**  By comparing different versions of content, determine which version is more attractive to users, improve user retention and conversion rate.

* **Function optimization:**  By comparing the functions of different versions, determine which version can better meet user requests, improve user retention and conversion rate.

* **Marketing strategy optimization:**  By comparing different versions of marketing strategy, determine which version is more attractive to users, improve user retention and conversion rate.


<span id="cef37697"></span>
# Create an experiment

Click " **+ Create Experiment**" on the experiment list page, select Visual experiment, enter the experiment creation process, and refer to the following steps to configure the details of the experiment.

<span id="6a43b187"></span>
## Step1 Enter basic information

**Experimental basic information** related parameters are mainly used to identify experiments, clarify experimental types, etc. The configuration details are as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f97b29966bef47b49d03e6c75d10d9ec~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experiment Name & Experiment Description** |* **Experiment name:**  It is recommended to set it to the name related to the experimental content. If there is an experimental version iteration, you can add the version number suffix, so that your partners can quickly understand what the experiment is doing and which iteration version is in.<br><br>* **Experiment description:**  The content of the experiment is briefly described, which can make the project related personnel more clearly know how the experiment is done and what problems to solve, and also facilitate the later viewing and management of historical experiments at a glance. |
|**Experimental label** |You can select an existing experimental label in the drop\-down box, or you can directly enter a new label.<br><br>Generally, keywords such as business line and optimization direction are used as tags to screen and classify experiments. After the subsequent experiments are created, relevant experiments can be quickly searched through the experiment tags in the experiment list. |
|**Type of experiment** |Currently only client side experiments are supported. |
|**Experiment duration** |Refers to the duration of the experiment, generally in order to avoid differences in user behavior in different time periods (weekdays and weekends), it is recommended to observe at least 2 complete test schedules.<br><br>For example, when considering the impact of weekdays and weekends, the test schedule takes at least one week, and the recommended duration of the experiment is 14 days. |
|**Experiment leader** |Default is the experiment creator. |


<span id="2b62e4f3"></span>
## Step2 Configure the effective policy

**Effective strategy** related parameters are mainly used to set the subsequent opening AB testing, which users will enter the A experiment, which users will enter the B experiment, through scientific experimental traffic allocation, to achieve a sufficient number of users participating in the experiment, and the experiment between each other does not interfere with the effect of credibility.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before setting up experimental traffic, you need to understand some basic concepts of experimental traffic:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Traffic</strong> & <strong>Audience Users</strong> & <strong>Experiment Traffic</strong>:</div>


   * <div data-tips="true" data-tips-type="warning">Traffic refers to the total number of users a product has.</div>


   * <div data-tips="true" data-tips-type="warning">Audience Users: In the overall user, all users selected by some filter conditions to participate in the AB testing.</div>


   * <div data-tips="true" data-tips-type="warning">Experimental traffic: among audience users, the proportion of users participating in an AB testing. After enabling audience rules, the system will <strong>first filter users who meet the rules</strong>, and then take effect according to the configured <strong>experimental traffic ratio</strong>.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Flow layer</strong> / <strong>experimental layer</strong> / <strong>mutual exclusion group</strong> / <strong>mutual exclusion layer & mutual exclusion experiment</strong>:</div>


   * <div data-tips="true" data-tips-type="warning">Flow layer, also known as mutual exclusion group, also known as mutual exclusion layer, experimental layer.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Mutual exclusion experiments</strong>, that is, experiments in <strong>the same flow layer</strong>. The traffic between mutual exclusion experiments is mutual exclusion, that is, all experiments in the mutual exclusion group do not share users: if a user hits Experiment 1 in the mutual exclusion group, it will not hit other experiments in that mutual exclusion group.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4d8ccb1cd9047d19b18383d633a1677~tplv-goo7wpa0wc-image.image) </span>


* **Traffic settings**

   
   |**Parameter** |**Configuration instructions** |
   |---|---|
   |**Whether mutual exclusion** |When you need to conduct multiple AB testing, you need to configure whether the currently created experiment needs mutual exclusion with other experiments according to the experimental situation, so as to avoid the same user being assigned to two experiments that will affect each other, thus affecting AB testing results.<br><br>For example, if you want to do an experiment on button color and button shape at the same time, and the two experiments affect each other, you need to add the two experiments to a mutual exclusion group.<br><br>Learn more about traffic tiers and how to create one at: [Traffic Layer and Mutual Exclusion Domain](https://docs.byteplus.com/docs/DataTester/Traffic-Layer-and-Mutual-Exclusion-Domain). |
   |**Experimental traffic** |The proportion of users who satisfied the audience in the effective experiment. The system defaults to 100% traffic, you can estimate the traffic through the suggestion tool (click the traffic calculator), and see how much traffic is set appropriately, see [Traffic Calculator](https://docs.byteplus.com/docs/DataTester/Traffic-Calculator).<br><br>After enabling audience rules, the system will **first filter users who meet the rules** , and then take effect according to the configured **experimental traffic ratio**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When estimating the experimental traffic, it is usually necessary to combine the experimental business indicators with the <strong>MDE</strong> (test sensitivity) for estimation. Usually, the experimental indicators are to improve/decrease xx (a certain business indicator value). The MDE recommends estimating less than this indicator value. Try to avoid the MDE value being large and unable to detect the real experimental results.</div><br> |
   

* **User audience rules**

   You can create multiple filter groups, filtering the logical relationships between the groups as "or"; you can set multiple filter conditions within each filter group, and the logical relationships between the filter conditions as "and".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f1e96e0372e42d3b5dc68ccd8fb5a4b~tplv-goo7wpa0wc-image.image) </span>

   Detailed instructions for configuring each filter group are as follows.

   
   |**Filter condition** |**Configuration instructions** |
   |---|---|
   |**Add and condition** |For client side experiments, after clicking **Add Filter Criteria**, you can use **user properties** as filters for user audiences, support using system\-provided **preset properties**, or create **custom properties** for filtering.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a357abcb35249deb7e783261c8fd440~tplv-goo7wpa0wc-image.image) </span><br><br>You can view existing preset and custom properties on the **Data Management** \> **Metadata Management** \> **User Properties** page, or you can create new custom properties.<br><br>**Scenario Example: New User Experiment**<br><br>In the "Select Target Audience" filter, you can add a "User First Installation Time" filter for new users, and use the first installation time to identify new users, that is, all users whose first installation time is later than the opening time of the experiment are classified as "New Users". During the start of the experiment, only new users enter the experimental group, and other existing users do not enter the group.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d0e1e462d6c4fafb17023f0fb4b0961~tplv-goo7wpa0wc-image.image) </span> |
   |**Add cohort** |For client\-side experiments, after clicking **add cohort**, you can filter users using the user cohort you created. See activity details for creating user groups [User Cohorts](https://docs.byteplus.com/docs/DataTester/User-Cohorts). |
   

* **Experience consistency**

   After opening, the effective version of the user during the experiment does not change with the adjustment of traffic and audience conditions, which can ensure that the same user can only enter one experimental version during the experiment. After opening, as long as the user has entered the current experimental version (unless the experiment is suspended or closed), the experiment will no longer be released.


<span id="166fae96"></span>
## **Step3 C**onfiguration experimental version

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Before configuring the experimental version, you need to understand some basic concepts of the experimental version:</div>



* <div data-tips="true" data-tips-type="warning"><strong>Experimental version</strong> & <strong>experimental group</strong> & <strong>control group</strong></div>


   <div data-tips="true" data-tips-type="warning">AB testing is usually a set of controlled experiments: <strong>experimental version</strong>, <strong>control version</strong>. By setting different logical strategies for the experimental version and the control version, it is verified which strategy is better while keeping other conditions stable. <strong>The control version</strong> is generally the current strategy, and the <strong>experimental version</strong> is generally the new strategy we want to try.   </div>
   

* <div data-tips="true" data-tips-type="warning"><strong>Test User</strong> & <strong>User ID: SSID</strong> and <strong>UUID</strong></div>


   * <div data-tips="true" data-tips-type="warning"><strong>Test users:</strong> Before the experiment is officially opened, it is usually necessary to select several users to test, observe whether the experiment can normally obtain the data you want to collect, and test whether there are bugs in the business functions after adding the experimental logic. Test users who participate in the test are also called "whitelisted users". When configuring the experimental version, you need to add test users for the experimental group and the control group.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>SSID:</strong> that is, Standardized Service ID (Standardized Service Id), is the user ID provided by BytePlus Growth Marketing Suite series products to mark and identify users. The SSID is automatically generated and maintained by the system, and you can use it as needed. When adding test users to the experimental version, the users participating in the test are identified by the SSID generated by the system.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>UUID:</strong> that is, User Unique Id, which is usually the user ID used in the product business, generally corresponds to the user's login ID (such as mobile phone number, email, etc.) one\-to\-one, UUID is maintained by you.</div>



<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7d47498c973448f9c4ccc16b64dfece~tplv-goo7wpa0wc-image.image) </span>


* **Test user hit condition**

   When selecting the experimental version corresponding to the test user hit, whether the audience rule set in the previous step needs to be satisfied. Since the test user is mainly used for debugging and verification before the experiment is officially launched, the choice of the test user can be inconsistent with the final experimental hit user, and you can configure it according to your actual needs.

* **Heat map**

   Support turning on the page heat map. If you want to see the heat map data on the page to be tested later, you can turn on the heat map switch here, and turn on the full event tracking function switch when integrating the data access SDK in advance. Heat map analysis function introduction see [Heat Map Analysis](https://www.volcengine.com/docs/6285/65951).

* **Configure URL rules**

   Configure the rule logic of the URL hit experiment accessed by the user. A URL that can match the rule means that the experiment can be hit, and a mismatch means that the experiment cannot be hit.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The URL rules configured here focus on whether the visited URL can successfully match the experiment; after the subsequent experiment is started, the specific version of the experiment that the user hits is determined by DataTester's streaming service.   </div>
   

   
   |**Matching rule** |**Rule description** |
   |---|---|
   |Simple match |When matching URLs, simple matching ignores query parameters and anchors in URLs, and **experiments can be hit if URL domain names and paths match** on a user's access page.<br><br>For example, if the target URL of the experiment is `https://app.test.com/path?param=a#frag1`, then when the user visits the following URL, the match is shown in the table:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f92b4fcd284469fb64338bb6f33ca21~tplv-goo7wpa0wc-image.image) </span> |
   |Exact match |That is, it is an exact match. Only when the URL of the user visiting the page exactly matches the URL of the experimental page will the experiment be hit. For example, the target URL of the experiment is `https://app.test.com/path?param=a#frag1 ,`then under the accurate matching, only when the user accesses the `https://app.test.com/path?param=a#frag1`, will hit the experiment. It is suitable for scenarios where users need to exclude pages with parameters and clearly know the page URL. |
   

* **Visual editing**

   When using it for the first time, you need to download and install the visual editor according to the interface prompts. See below for activity details [Reference: Installing the Visual Editor](https://docs.byteplus.com/docs/DataTester/Visual-Experiment#157d2e2b).

   After the installation is complete, you can click on an experimental version of "**Enter Visual Editor**" to enter the visual editing page. You can edit the page through the visual editor in the page. After completion, save the page as an experimental version. The main editing operations are shown in the following table. For more visual editor introductions, please refer to [Visual Editor](https://docs.byteplus.com/docs/DataTester/Visual-Editor).

   
   |Module |Child |Product example diagram |Operating instructions |
   |---|---|---|---|
   |Top navigation bar |/ |<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_654253490f21fc9a7ff560edad1d73cc.png) </span> |* Support viewing operation records: the mouse hover the elements of the operation record, you can view the modifier, modification date, and modification details.<br><br>* Support switching width, such as full screen width, tablet, mobile end, custom width.<br><br>* Support switching "Preview Mode, Edit Mode", support switching "Experimental Version", "Experimental Page".<br><br>* Support for "undo, redo, save" operations.<br><br>* Support viewing circled event details. |
   |Content |font layout |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ea80e683de4295ba1fee876ce71258~tplv-goo7wpa0wc-image.image) </span> |1. Supports editing of font size, color, text content, bold/tilt, alignment, and other properties |
   |Style |Size, layout, background |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d764fd3911994a35908c615ed5fb5969~tplv-goo7wpa0wc-image.image) </span> |Size support element size related CSS style editing |
   |Event |Circle event | |Provides the ability to circle events for elements of type "button", "link", "image", and "text".<br><br><br>1. Under **Edit**, click **Events** to add an event name.<br><br>2. **New indicator after saving:**  Click on **New indicator**, the indicator new page will pop up. |
   |HTML new elements |/ | |Support for adding elements through HTML code.<br><br>(1) Formatting (2) Line wrapping and unwrapping (3) HTML code format verification (4) Manual input of tags, automatic closing of tags (5) Optimization of default initialization example code |
   

* **Adding pages (multi\-page visualization experiment)** 

   * Click [Add Page] to add multiple pages to a version, and each page can be edited individually.

      Note: Page order does not affect the user's browsing experience. For example, if a user first sees page 2 and then page 1, they will still see the same experimental version of page 1.

   * Multi\-page editing: You can switch to different pages in the upper left corner for visual editing. The specific actionable items are the same as the visual editing operation instructions.

   * Delete: Click the Delete logo to delete the page, and it cannot be restored after deleting the page.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/430a59c738ac48c9b7a243f4a298bc0a~tplv-goo7wpa0wc-image.image) </span>

* **Traffic allocation**

   After the subsequent experiment is started, the proportion of experimental traffic allocated between different experimental versions in all the experimental traffic participating in the AB testing.

   * **Uniform distribution of traffic\-on:**  The default is on state, and the open state is to force the uniform distribution of traffic in each experimental version.

   * **Traffic evenly distributed\-off:**  After closing, the relative proportion of traffic in the control version and the experimental version can be deployed. You can control the proportion of users hit by each experimental version by entering a value.

      For example, when the uniform distribution is turned off, the three experimental versions can be configured to account for 20% of the control version, 50% of the experimental version 1, 30% of the experimental version 2, and 100% of the overall sum. The experimental version 3 is automatically divided into 20% traffic.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the traffic weights of each experimental version are changed, users who have entered the group historically will not be affected, but only users who have been assigned but not entered the group, as well as users who have not been assigned.   </div>
   

<span id="9f717219"></span>
## Step4 Experimental indicators

Experimental indicators are used to evaluate the policy effect of each experimental version, and whether the functions of assisting decision\-making AB testing can meet business expectations. By configuring the experimental core indicators and experimental attention indicators, after the follow\-up experiment is completed, the experimental report related to the indicators will be automatically output for you according to the indicators you configured to assist you in analyzing the experimental results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6bf3852a49524e189cdafd6865471414~tplv-goo7wpa0wc-image.image) </span>


|**Parameter** |**Configuration instructions** |
|---|---|
|**Experimental core indicator configuration** |* **Core indicator configuration**:<br><br>   To determine whether the experimental function meets the expected "direct effect indicators" or "success indicators", you can select the indicators as the core indicators of the experiment in the existing indicator group in the drop\-down box. It is recommended to conduct the experimental design reasonably and choose carefully. For more experience guidance on experimental indicator setting, please check it [1. Identify evaluation metrics](https://docs.byteplus.com/docs/DataTester/How-to-Interpret-the-Experiment-Report#_1-%E7%A1%AE%E5%AE%9A%E8%AF%84%E4%BC%B0%E6%8C%87%E6%A0%87).<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the experimental indicators are configured, after the subsequent experiments are created, if there are special circumstances that need to modify the experimental indicators, please enter the experimental details page to modify them.   </div><br>   <br><br>* **Monitoring alarm:**  You can select the target indicator and click "Monitoring alarm", fill in the specific required alarm strategy, choose whether to tick "Significant effect", and choose the effective way of the alarm strategy.<br><br>* **Edit indicators:**  Click on the 3 position in the legend to enter the indicator editing page, and edit the name, indicator type, and whether it is set as a must\-see indicator for indicators. |
|**Experimental attention indicator configuration** |Configure the metrics that need attention. You can select the indicators you need to pay attention to in the drop\-down list of the page, or you can click the **New Indicator** or **Remove Indicator** button on the page to quickly adjust the indicators you need to pay attention to. |
|**Confidence level** |Confidence level (also known as confidence level, confidence coefficient, statistical significance) refers to the probability that there is a real difference in performance between the experimental group and the control group.<br><br>For example, when the confidence level is 95%, if the confidence level p value of an experimental indicator is < 0.05, it means that the indicator is significantly different from the control group. To set the confidence level parameter value, you need to contact the group administrator or app administrator and go to " [1.2 Confidence level](https://docs.byteplus.com/docs/DataTester/System-Settings#_1-2-%E7%BD%AE%E4%BF%A1%E6%B0%B4%E5%B9%B3)" to set it up. |


<span id="a40e87d1"></span>
# Debug, start, stop experiments

After the experiment is created, you can view the created experiments in the A/B Testing \> Experiments list and check the experiment status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4731e7999a4d490f9bd1ce7673f65efb~tplv-goo7wpa0wc-image.image) </span>


* **Debugging:**  The newly created experiment is **debugging**. At this stage, you can invite users who have been added as test users to conduct experimental tests to confirm that the experiment meets expectations.

* **In progress:**  After the experiment is debugged, you can click "Start" on the experiment list page to start the experiment. After the start of the experiment, the state of the experiment becomes "I**n Progress"** . At this time, the user can view the group in real time, and the indicator confidence level will be produced on the second day.

* **Closed:**  After the experiment starts, the experiment will automatically stop when the experiment duration reaches the **experiment duration** configured when the experiment was created; if the experiment duration is not reached, you want to stop the experiment immediately, or you can manually stop the experiment in the experiment list. After stopping the experiment, the experimental state changes to **has ended**.


<span id="d885dd6c"></span>
# View the experimental report

After the experiment is opened, you can also click to enter the experimental report page through the experimental operation entrance in the experimental list to view the experimental report, please refer to the details [Experimental Report Overview](https://docs.byteplus.com/docs/DataTester/Experimental-Report-Overview).

<span id="157d2e2b"></span>
# Reference: Installing the Visual Editor

For a detailed introduction to the visual editor, please refer to [Visual Editor](https://docs.byteplus.com/docs/DataTester/Visual-Editor), when creating a visual experiment, **when the chrome extension is not installed** , click to enter the editor, a pop\-up window will prompt the user to install the extension, click the link of "Add Extension", and jump to the details page of the corresponding extension of chrome.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/652ff7d9573747adb0cd38e74fc6612e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f53c1d8d8e04e2ba08cb96af2ce43e1~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c9e520a893e4b28a8260934d7d3d399~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/409a4c0611e344d28e7a29bd8847942b~tplv-goo7wpa0wc-image.image) </span>

**When the chrome extension is installed**, clicking into the editor will open the target page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/169d26f532514e0c88b4e34a94d64510~tplv-goo7wpa0wc-image.image) </span>
